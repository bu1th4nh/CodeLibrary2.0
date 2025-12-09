# MLFlow snippets


## Log Artifact File

```python
with tempfile.TemporaryDirectory() as tmp_dir:
    path = Path(tmp_dir, "config.yaml")
    path.write_text(OmegaConf.to_yaml(final_run_profile, resolve=True))
    mlflow.log_artifact(path)
```