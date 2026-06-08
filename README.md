# 🗺️ Bandung Road Network Analysis
 
Structural, dynamic, and graph-learning analysis of the Bandung urban road network, built from open geospatial data sources.
 
The project is organized as a self-contained notebook covering three distinct perspectives on what makes urban road networks interesting as complex systems.
 
## 📓 Notebook
 
| Notebook | Focus | Key Methods |
|---|---------|-------------|
| `bandung_road_network_analysis.ipynb` | Structural analysis, congestion dynamics, and intersection classification on Bandung's road network | Network construction via city2graph + Overture Maps, degree/centrality/power-law analysis, ER/WS/BA model comparisons, articulation points, FCRF congestion simulation, GCN node classification |
 
The notebook is organized into four major sections:
 
| Section | Description |
|---|---------|
| **1. Network Construction & Visualization** | Downloads Bandung road data from Overture Maps, reprojects to local UTM, builds a NetworkX graph, and visualizes at full-city, city-centre, and neighbourhood scales |
| **2. Structural Network Analysis** | Computes basic stats, fits degree distributions, compares against ER/WS/BA reference models, runs centrality analysis (degree, closeness, betweenness, PageRank), and identifies articulation points and bridges |
| **3. Network Dynamics** | Runs a discrete-time FCRF (Flow Congestion Reaction-Flow) simulation comparing seed strategies, parameter sensitivity, and multi-origin spatial spreading |
| **4. Graph Neural Network (GNN)** | Applies a GCN to classify road intersections by importance using node features derived from structural position |
 
---
 
## 💾 Data
 
Two datasets are required, produced by running Section 1 of the notebook (downloaded automatically via city2graph):
 
| File | Source | Contents |
|---|---------|-------------|
| `datasets/bandung_segment.geojson` | [Overture Maps](https://overturemaps.org/) via city2graph | Road segments — geometry, class, subtype |
| `datasets/bandung_connector.geojson` | [Overture Maps](https://overturemaps.org/) via city2graph | Connector points for segment splitting |
| `datasets/bandung_drive.pkl` | Generated | Processed NetworkX graph (LCC, UTM-projected) |
 
Road types retained: `motorway`, `trunk`, `primary`, `secondary`, `tertiary`, `residential`, `service`, `living_street`, `unclassified`.
 
---
 
## 🔍 Key Findings
 
### Structure
 
- Bandung's road network degree distribution does not follow a clean power law — unlike scale-free social networks, road connectivity is bounded by geography and urban grid constraints
- Compared against ER, WS, and BA reference models: clustering is higher than ER but lower than WS; degree heterogeneity is lower than BA
- Betweenness centrality reveals a small set of arterial intersections (Braga / Asia Afrika corridor) serving as major bottlenecks
### Dynamics
 
- High-betweenness seeds produce faster and more spatially concentrated congestion compared to high-degree or random seeds
- FCRF parameter sensitivity shows β (spread rate) has the dominant effect on peak congestion; δ (decay) controls recovery time
### GNN Node Classification
 
- GCN classifies intersections by structural importance using node features derived from degree, centrality, and spatial position
- Only the largest connected component is used; node and edge attributes are stripped before conversion to PyTorch Geometric format
---
 
## 🛠️ Tech Stack
 
| Library | Purpose |
|---|---|
| `city2graph` | Overture Maps data download, segment processing, graph construction, and plotting |
| `geopandas` | Geospatial data loading and CRS reprojection |
| `networkx` | Graph construction, centrality, articulation points, and path metrics |
| `pandas` / `numpy` | Data loading and preprocessing |
| `matplotlib` / `seaborn` | Visualization |
| `powerlaw` | Degree distribution fitting |
| `scipy` | Statistical tests |
| `torch` | GNN training |
| `torch-geometric` | `GCNConv` and graph conversion utilities |
| `scikit-learn` | Evaluation metrics and feature scaling |
 
---
 
## ⚙️ Setup
 
**Prerequisites**
- Python 3.10+
**Installation**
```bash
git clone https://github.com/JasonYehezkiel/bandung-road-network-analysis.git
cd bandung-road-network-analysis
 
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
 
pip install -r requirements.txt
```
 
Run all four sections in order — the graph pickle produced in Section 1 is loaded by all subsequent sections.
 
## 👤 Authored by
 
Name: Jason Yehezkiel Wijaya
