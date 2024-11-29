# shu_zi_luo_ji
\documentclass[tikz,border=2mm]{standalone}
\usetikzlibrary{shapes.geometric, arrows, positioning}

\tikzstyle{process} = [rectangle, rounded corners, minimum width=3cm, minimum height=1cm, text centered, draw=black, fill=blue!30]
\tikzstyle{decision} = [diamond, minimum width=3cm, minimum height=1cm, text centered, draw=black, fill=green!30]
\tikzstyle{arrow} = [thick,->,>=stealth]

\begin{document}

\begin{tikzpicture}[node distance=2cm]

% Nodes
\node (start) [process] {启动操作};
\node (loadRx) [process, below of=start] {从寄存器 $R_x$ 输出 (e.g., $R_x \text{out} = 1$)};
\node (alu) [process, below of=loadRx] {ALU 执行操作 (e.g., ADD/SUB)};
\node (writeG) [process, right of=alu, xshift=5cm] {结果写入 $G$ (e.g., $G_{\text{in}} = 1$)};
\node (decision) [decision, below of=alu, yshift=-1cm] {结果需要存储到 $R_x$?};
\node (writeRx) [process, below of=decision, yshift=-1cm] {结果写入 $R_x$ (e.g., $R_x \text{in} = 1$)};
\node (end) [process, below of=writeRx] {操作完成};

\node (storeBackup) [process, right of=decision, xshift=5cm] {备份原数据到 $R_{\text{temp}}$};

% Arrows
\draw [arrow] (start) -- (loadRx);
\draw [arrow] (loadRx) -- (alu);
\draw [arrow] (alu) -- (writeG);
\draw [arrow] (alu) -- (decision);
\draw [arrow] (decision) -- node[anchor=east] {是} (writeRx);
\draw [arrow] (writeRx) -- (end);
\draw [arrow] (decision.east) -- ++(2,0) |- node[anchor=south] {否} (storeBackup);
\draw [arrow] (storeBackup) |- (writeG);

\end{tikzpicture}

\end{document}
