# Tables


### Example 1
```latex
\begin{table}
    \centering
    % \vspace{-0.5em}
    \footnotesize
    \begin{tabular}{lccc}
        \toprule
        \textbf{Model} & \textbf{GAIA} (Success \%) & \textbf{SWE-Bench Verified} (Resolved \%) & \textbf{WebVoyager} (Success \%) \\
        \midrule
        \multicolumn{4}{l}{\textit{General-Purpose Agents}} \\
        Langfun        & 71.5 & --   & --   \\
        Trase          & 70.3 & --   & --   \\
        OWL            & 69.1 & --   & --   \\
        \midrule
        \multicolumn{4}{l}{\textit{Software Engineering Agents}} \\
        SWE-agent      & --   & 62.4 & --   \\
        OpenHands      & --   & 65.8 & --   \\
        \midrule
        \multicolumn{4}{l}{\textit{Web Navigation Agents}} \\
        Browser use    & --   & --   & 89.1 \\
        Operator       & --   & --   & 87.0 \\
        Skyvern        & --   & --   & 85.6 \\
        \midrule
        \textbf{Aime (Ours)} & \textbf{77.6} & \textbf{66.4} & \textbf{92.3} \\
        \bottomrule
    \end{tabular}
    \caption{\small Performance comparison of Aime against specialized baselines across three benchmarks. Baselines are evaluated only on their target domain, while Aime is evaluated on all three. Best scores in each column are in \textbf{bold}.} \label{tab:main_results}
\end{table}
```


### Example 2
```latex
 \begin{table*}[t]
    \centering
    \small
    \begin{tabular}{llccccccccccc}
        \toprule
        \multicolumn{2}{l}{\textbf{LVLM backbones}} & \multicolumn{6}{c}{\textbf{LLaVa 2}} & \multicolumn{5}{c}{\textbf{InstructBLIP}}  \\
        \cmidrule(r){1-2} \cmidrule(lr){3-8} \cmidrule(l){9-13} 
        \multirow{3}{*}{\textbf{Config}} 
        & Threshold     & N/A  & N/A  & 0.0 & 0.1   & 0.5   & 0.9   & N/A & 0.0   & 0.1 & 0.5 & 0.9 \\
        & Guidance      & 0.0  & 0.7  & 0.7 & 0.7   & 0.7   & 0.7   & 0.0 & 0.7   & 0.7 & 0.7 & 0.7 \\
        & Batch size    & 4    & 4    & 4   & 4     & 4     & 4     & 16  & 16    & 16  & 16  & 16  \\
        \midrule
        \midrule
        \multirow{3}{*}{\textbf{CHAIR}} 
        & CHAIRi        &  4.1    &  5.4 &  5.4 &  8.2 &  8.6 &  7.8 & 33.2 & 4.8  & 4.0  & 4.8  & 4.7 \\
        & CHAIRs        &     7.8 &  2.7 &  2.7 &  4.1 &  4.3 &  3.9 & 13.2 & 4.0  & 3.5  & 4.2  & 3.9 \\
        & Recall        &     40.8 & 47.5 & 47.4 & 42.2 & 41.7 & 41.3 & 52.8 & 23.4 & 21.7 & 22.4 & 23.5 \\
        \midrule
        \multirow{6}{*}{\textbf{POPE}} 
        & Accuracy      & 79.4  & 85   & 85.3 & 83.2 & 80.2 & 81.8 &  72.1  & 77.6   &  81.8    & 79.2    & 78.2 \\
        & Yes Ratio     & 61.6  & 45.7 & 45.6 & 50.5 & 59   & 55.1 &  69.5  & 62.5   &  42.7    & 53      & 59.8 \\
        & Precision     & 73.9  & 88.3 & 88.6 & 82.9 & 75.6 & 78.9 &  65.9  & 72.1   &  87.3    & 77.6    & 73.6 \\
        & Recall        & 91.0  & 80.7 & 80.9 & 83.7 & 89.2 & 86.9 &  91.7  & 90.1   &  74.5    & 82.2    & 88.1 \\
        & Specificity   & 67.9  & 89.3 & 89.6 & 92.7 & 71.2 & 76.7 &  52.6  & 65.1   &  89.2    & 76.2    & 68.4 \\
        & F1            & 81.6  & 84.3 & 84.6 & 83.3 & 81.8 & 82.7 &  76.7  & 80.1   &  80.4    & 79.8    & 80.2 \\
        \bottomrule
    \end{tabular}
    \caption{CHAIR and POPE metrics (\%) with LLaVa and InstructBLIP when adding CLIP with various thresholds to grounding models}
    \label{tab:clip-grounding}
\end{table*}

```