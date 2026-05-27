# ✈️ Flight Network Analysis

Structural, dynamic, and graph-learning analysis of the global commercial aviation network, built from open data sources.

The project is organized as three self-contained notebooks that share the same underlying graph — each tackles a distinct perspective on what makes flight networks interesting as complex systems.

## 📓 Notebooks

| Notebook | Focus | Key Methods |
|---|---------|-------------|
| `Network_Structure.ipynb` | How the real network compares to ideal random graph models | Degree distribution, power-law fitting, clustering, path length, modularity —  benchmarked against ER, WS, BA, XBS, and LFR models  |
| `Network_Dynamics.ipynb` | How a pathogen spreads through the aviation backbone | Discrete-time stochastic SIR simulation, heterogeneous mean-field epidemic threshold, four experiments across seed strategy, β, γ, and immunization |
| `Network_GNN.ipynb` | Whether GNN can recover hidden flight routes | Link prediction with GCN, GraphSAGE, and GAT; node features: log-degree, clustering coefficient, normalized lat/lon; evaluated on AUC, AP, F1, and accuracy |

---

## 💾 Data

Two open datasets are required, place them in a `datasets/` folder at the repo root:

| File | Source | Contents |
|---|---------|-------------|
| `airports.csv` | [OurAirports](https://ourairports.com/data/) | Airport metadata — IATA code, type, country, lat/lon |
| `routes.dat` | [OpenFlights](https://openflights.org/data.php) | Flight routes — airline, source IATA, destination IATA |
---

All three notebooks filter to airports with valid IATA codes, build an undirected graph, extract the Giant Connected Component (GCC), and remove self-loops before any analysis begins. The GCC construction is identical across notebooks so results are directly comparable.

## 🔍 Key Findings

### Structure

- Degree distribution follows a heavy tail (scale-free-like); log-log CCDF is approximately linear
- Real network has high clustering and short average path length — classic small-world signature
- Compared with ER, WS, BA, XBS, and LFR models at matched N and ⟨k⟩, the flight network most closely resembles BA in degree heterogeneity but exceeds it in clustering

### Dynamics

- Epidemic threshold β_c ≈ ⟨k⟩ / ⟨k²⟩ is extremely small due to the heavy tail — even a weakly transmissible pathogen can sustain global spread if it reaches a major hub
- Hub seeding (high-degree and high-betweenness airports) produces significantly faster and broader outbreaks than random or peripheral seeding.
- Targeted immunization of top-degree airports is substantially more effective than random vaccination.

### GNN Link Prediction
- Task: hide 10 real routes, train on the remaining graph, evaluate recovery against 10 negative samples
- Node features encode both structural position (log-degree, clustering) and geography (normalized lat/lon)
- GCN, GraphSAGE, and GAT are compared: high variance is expected given the small 20-pair test set

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `networkx` | Graph construction, centrality, and path metrics |
| `pandas` / `numpy` | Data loading and preprocessing |
| `matplotlib` / `seaborn` | Visualization |
| `powerlaw` | Degree distribution fitting |
| `scipy` | Statistical tests |
| `torch` | GNN training |
| `torch-geometric` | `GCNConv`, `SAGEConv`, `GATConv`, and `negative_sampling` |
| `scikit-learn` | AUC, AP, F1, and accuracy evaluation |

---

## ⚙️ Setup

**Prerequisites**
- Python 3.10+

**Installation**
```
git clone https://github.com/JasonYehezkiel/flight-network-analysis.git
cd flight-network-analysis

# place airports.csv and routes.dat inside datasets/
mkdir datasets

python -m venv .venv
.venv\Scripts\activate # MacOS/Linux: source .venv/bin/activate

pip install -r requirements.txt
```

Run the notebooks in order — Structure → Dynamics → GNN — since they share the same graph construction logic and the EDA in Structure provides context for interpreting the later two.

## 👤  Authored by:

Name: Jason Yehezkiel Wijaya