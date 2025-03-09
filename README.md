# Graphazon: CoPurchase Cosmos

**Uncover the hidden patterns of Amazon shopping with AI-powered graph analysis.**

*Graphazon: CoPurchase Cosmos* transforms Amazon co-purchase datasets into interactive graph networks. Powered by NetworkX, LangChain, and ArangoDB, it offers natural language querying, dynamic visualizations, and deep analytical insights through a visually stunning Gradio interface. Whether you're a data scientist, retailer, or curious explorer, *Graphazon* makes sense of complex buying relationships.

---

## Inspiration
The spark for *Graphazon* came from a fascination with how everyday purchases—like what people buy together on Amazon—reveal intricate networks. With graph theory and AI, I aimed to build a tool that not only analyzes these connections but also makes them interactive and intuitive, turning raw data into actionable insights for optimizing recommendations, understanding customer behavior, or exploring market trends.

---

## Features
- **Natural Language Queries**: Ask complex questions like "What products are frequently co-purchased with node 10 in amazon0302?" or "What's the shortest path between two nodes?" and get precise, AI-generated answers in seconds.
- **Interactive Visualizations**: Choose from:
  - **Network Graphs**: Sampled views of product relationships.
  - **Degree Distributions**: Histograms showing node connectivity.
  - **Community Distributions**: Bar charts of cluster sizes.
- **Graph Analysis**: Detailed metrics including:
  - Number of nodes and edges.
  - Average degree and network density.
  - Largest connected component size.
  - Top nodes by degree and community structures (via Louvain algorithm).
- **Scalable Storage**: Persists graphs with hundreds of thousands of nodes in ArangoDB for efficient querying and retrieval.
- **Stunning UI**: A Gradio interface with indigo-purple theming, smooth tab navigation (Query, Visuals, Analysis), and custom CSS for a modern look.

---

## Installation
Clone the repository and set up your environment:

```bash
git clone https://github.com/ArnavKukreja/Graphazon-CoPurchase-Cosmos.git
cd Graphazon-CoPurchase-Cosmos
```

Install dependencies using Conda or pip:

```bash
# Using Conda (recommended for RAPIDS compatibility)
conda env create -f environment.yml
conda activate graphazon-env

# OR using pip
pip install -r requirements.txt
```

### Prerequisites
- **Python**: 3.11+
- **ArangoDB**: Local instance or cloud setup (e.g., ArangoDB Oasis). Configure credentials in your notebook.
- **Cohere API Key**: For LangChain's LLM. Get it from Cohere.
- **Git**: For cloning and version control.
- **Jupyter Notebook**: For running Graphazon.ipynb.

---

## Usage

### Prepare the Data:
Ensure the Amazon SNAP datasets (e.g., amazon0302.txt.gz) are downloaded or placed in an `amazon_data/` directory.

### Run the Notebook:
Launch Jupyter and open the notebook:

```bash
jupyter notebook Graphazon.ipynb
```

Execute cells 1-19 in order:
- Cells 1-4: Install dependencies and set up imports.
- Cell 5: Download and parse co-purchase data into NetworkX graphs.
- Cells 7-8: Define analysis and visualization functions.
- Cell 11: Persist graphs to ArangoDB.
- Cell 12: Set up the LangChain agent.
- Cell 13: Run analysis on all graphs.
- Cells 15-17: Define visualization functions.
- Cell 19: Launch the Gradio interface.

### Interact with the App:
- **Query Explorer Tab**: Type queries like "How many communities in amazon0601?" or "Neighbors of node 5 in amazon0302?" and click "Explore."
- **Visual Insights Tab**: Select a graph (e.g., amazon0302), choose "Graph," "Degree Distribution," or "Community Distribution," and click "Reveal" to see plots.
- **Deep Analysis Tab**: Pick a graph and click "Analyze" for detailed metrics.

### Sample Queries:
- "What's the shortest path from node 0 to node 5 in amazon0312?"
- "Show the degree distribution of amazon0505."
- "What are the top 5 nodes by degree in amazon0601?"

---

## Built With
- **Python**: Core language (v3.11).
- **NetworkX**: Graph creation, manipulation, and analysis.
- **LangChain**: Natural language processing with Cohere's LLM via a ReAct agent.
- **Gradio**: Interactive web interface with custom theming and dynamic port handling.
- **ArangoDB**: Multi-model database for graph persistence and AQL querying.
- **Matplotlib**: Visualization of network graphs, degree histograms, and community bar charts.
- **Pandas**: Parsing and preprocessing co-purchase edge lists.
- **tqdm**: Progress bars for data loading and processing.
- **nx_arangodb**: Bridging NetworkX graphs to ArangoDB.
- **Python-louvain**: Louvain algorithm for community detection.
- **Socket**: Dynamic port selection for Gradio.

---

## How It Works
- **Data Ingestion (Cell 5)**: Downloads gzipped SNAP datasets (e.g., amazon0302.txt.gz) and parses edge lists into Pandas DataFrames.
- **Graph Building (Cell 5)**: Converts edge lists to NetworkX directed graphs, with nodes as products and edges as co-purchases.
- **Persistence (Cell 11)**: Batches nodes and edges into ArangoDB collections (products_<graph_name>, copurchases_<graph_name>), creating scalable graph structures.
- **Analysis (Cells 7, 13)**: Computes metrics (node/edge counts, density) and detects communities using Louvain, storing results in graph_analyses and community_analyses.
- **Visualization (Cells 8, 15, 17)**: Samples large graphs (e.g., 100 nodes) for network plots, and generates degree/community distributions with Matplotlib.
- **Agentic App (Cell 12)**: A LangChain ReAct agent uses two tools:
  - **networkx_query**: Executes Python code for graph operations (e.g., finding neighbors).
  - **arango_query**: Runs AQL queries on persisted graphs.
  - Processes queries like "What's co-bought with node 0?" by reasoning through intent and tool selection.
- **Interface (Cell 19)**: Gradio UI with tabs for querying, visualizing, and analyzing, styled with custom CSS and a Soft theme.

---

## Challenges
- **Scale**: Graphs with 300k+ nodes overwhelmed memory; implemented sampling (e.g., 5000 nodes) in detect_communities (Cell 7).
- **Agent Integration**: Tuned LangChain prompts (Cell 12) to align with NetworkX and ArangoDB, resolving errors like agent_scratchpad type mismatches.
- **Port Conflicts**: Gradio's default port (7860) clashed often; added find_free_port in Cell 19 for dynamic resolution.
- **UI Limitations**: Worked around Gradio's API quirks (e.g., no elem_classes for Examples, fixed with Group wrapper).

---

## Future Plans
- **Metadata Enrichment**: Integrate Amazon product metadata (e.g., titles, categories) from metadata.json.gz (Cell 16) for richer queries.
- **Real-Time Updates**: Stream live co-purchase data via APIs for dynamic graph evolution.
- **Advanced Analytics**: Add centrality measures (PageRank, betweenness) and predictive models for recommendation.
- **Scalability**: Optimize with cuGraph for GPU acceleration and deploy on AWS/GCP for multi-user access.
- **Mobile App**: Port the Gradio interface to a React Native mobile app for broader reach.

---

## Contributing
We'd love your help! To contribute:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit changes (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request with a description of your changes.

Please ensure code follows PEP 8 and include comments for clarity.

---

## License
This project is licensed under the MIT License - see the LICENSE file for details.

---

## Contact
- **Email**: Reach out via GitHub Issues for questions, feedback, or collaboration!
