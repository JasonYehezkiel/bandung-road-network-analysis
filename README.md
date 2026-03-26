# 🌍 Global Arms Trade Network Analysis

This project analyzes global arms transfers (2000–2023) using network science techniques to uncover structural patterns, central actors, and geopolitical blocs.

---

## 🔍 Key Findings

- The network exhibits **heavy-tailed structure** with dominant exporter hubs
- Trade is **economically concentrated but structurally distributed**
- Strong **hub-and-spoke dynamics** with moderate community structure
- Influence is **multi-dimensional** (volume, position, connectivity)

---

## 🧠 Methods

- Network construction (weighted & unweighted)
- Degree & strength distribution (CCDF, heavy-tail analysis)
- Clustering coefficients
- Path length & diameter (LSCC)
- Centrality measures (PageRank, Betweenness, Eigenvector, etc.)
- Community detection (modularity-based)

---

## 📊 Visualizations

- Degree & strength distributions
- Centrality rankings
- Network layouts (4 types)
- Community structure & inter-bloc trade

---

## 📁 Files

- `arms_trade_network_analysis.ipynb` → full analysis notebook

---

## ⚙️ How to Run

```bash
pip install -r requirements.txt
jupyter notebook  # Launch Jupyter Notebook (skip if running in VS Code)