# Apptainer scripts

## Container
```bash
apptainer build /path/to/container.sif /path/to/ContainerDefinitionFile.def
```


## Instances: List, log, start
### List all running instances
```bash
apptainer instance list 
```
### List all instances with log files
```bash
apptainer instance list --logs
```

### Start/Stop an instance 
```bash 
apptainer instance start /path/to/container.sif instance_name
```


```bash
apptainer instance stop instance_name
```


## Some apps

### n8n

- Config
```singularity
Bootstrap: docker
From: docker.n8n.io/n8nio/n8n
%environment
    export N8N_HOST="<host-ip-or-domain>"
    export N8N_PORT="5678"
    export N8N_PROTOCOL="http"
    export N8N_SECURE_COOKIE="false"
    export N8N_PAYLOAD_SIZE_MAX="32767"
%files
    /path/to/n8n/n8n_data /home/node/.n8n
    /path/to/n8n/local_files /files
%runscript
    exec echo "$@"
%startscript
    n8n start
```

- Script
```bash
apptainer instance start n8n.sif n8n
```

### MinIO
- Config
```singularity
Bootstrap: docker
From: minio/minio
%environment
  export MINIO_ROOT_USER="username"
  export MINIO_ROOT_PASSWORD="password"
%runscript
  exec echo "$@"
%startscript
  minio server ./data --console-address ":9001"
```

- Script
```bash
apptainer instance start minio.sif minio
```

### MongoDB
- Config
```singularity
Bootstrap: docker
From: mongodb/mongodb-community-server:latest

# Metadata about the container
%labels
    Maintainer bu1th4nh
    Version 1.0

%post
    # Create a default predefined path for MongoDB data
    mkdir -p /data/db
    mkdir -p /etc/mongo-config

    # Add a default MongoDB configuration pointing to /data/db
    echo "dbPath: /data/db" > /etc/mongo-config/mongod.conf
    chmod -R 777 /data/db /etc/mongo-config

%environment
    # Set environment variables
    export MONGO_PORT=27017
    export MONGO_BIND_IP=0.0.0.0
    export MONGODB_INITDB_ROOT_USERNAME="username"
    export MONGODB_INITDB_ROOT_PASSWORD="password"

%startscript
    echo "Starting MongoDB with the following configuration:"
    echo " - Data Directory: /data/db"
    echo " - Port: $MONGO_PORT"
    echo " - Bind IP: $MONGO_BIND_IP"

    # Start MongoDB using the predefined data directory
    exec mongod --dbpath /data/db --bind_ip $MONGO_BIND_IP --port $MONGO_PORT
```


- Script
```bash
apptainer instance start mongo.sif mongo
```


### PostgreSQL
- Config
```singularity
Bootstrap: docker
From: postgres:17

%environment
    export POSTGRES_USER="username"
    export POSTGRES_PASSWORD="password"
    export PGDATA=/var/lib/postgresql/data/db
    export PGPORT=5432
    export LANG="C.UTF-8"
    export LC_ALL="C.UTF-8"


%files
    /home/ti514716/Tools/PostgreSQL/db/data /var/lib/postgresql/data
    /home/ti514716/Tools/PostgreSQL/db/run /var/run/postgresql


%runscript
    # If args were passed to `apptainer run`, forward them to the Docker entrypoint.
    if [ "$#" -gt 0 ]; then
        exec /usr/local/bin/docker-entrypoint.sh "$@"
    else
        # Default is to start the server in foreground
        exec /usr/local/bin/docker-entrypoint.sh postgres
    fi

%startscript
    # For `apptainer instance start ... postgres16.sif <name>`
    exec /usr/local/bin/docker-entrypoint.sh postgres
```

- Script
```bash
apptainer instance start \
  --bind "/path/to/postgres/data:/var/lib/postgresql/data" \
  --bind "/path/to/postgres/run:/var/run/postgresql" \
  --env POSTGRES_PASSWORD="password" \
  --env POSTGRES_USER="username" \
  --env POSTGRES_DB="mlflowdb" \ 
  postgres17.sif postgres_server
```


### MLflow
- Config
```singularity
Bootstrap: docker
From: ghcr.io/mlflow/mlflow:latest

%environment
    export AWS_ACCESS_KEY_ID=<your-access-key>
    export AWS_SECRET_ACCESS_KEY=<your-secret-access-key>
    export MLFLOW_S3_ENDPOINT_URL=http://<your-minio-host>:<your-minio-port>
    export MLFLOW_S3_IGNORE_TLS=true
    export POSTGRES_USER=<your-postgres-username-for-mlflow>
    export POSTGRES_PASSWORD=<your-postgres-password-for-mlflow>
    export POSTGRES_DB=<your-postgres-database-for-mlflow>


%post
    pip install psycopg2-binary boto3 gevent

    
%startscript
    mlflow server \
     --backend-store-uri postgresql://$POSTGRES_USER:$POSTGRES_PASSWORD@localhost:5432/$POSTGRES_DB \
     --host 0.0.0.0 \
     --port 6969 \
     --serve-artifacts \
     --artifacts-destination s3://mlflow \
     --workers 8 \
     --gunicorn-opts "--worker-class gevent --timeout 300 --keep-alive 300 --log-level INFO"
```

- Script
```bash
apptainer instance start \
  --env AWS_ACCESS_KEY_ID=<your-access-key> \
  --env AWS_SECRET_ACCESS_KEY=<your-secret-access-key> \
  --env MLFLOW_S3_ENDPOINT_URL=http://<your-minio-host>:<your-minio-port> \
  --env MLFLOW_S3_IGNORE_TLS=false \
  mlflow.sif mlflow
```