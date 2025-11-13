# Semantic Bridge Analysis - TACC Computational Cookbook

[![TACC](https://img.shields.io/badge/TACC-UT%20Austin-BF5700?style=flat-square)](https://www.tacc.utexas.edu)
[![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square)](https://www.python.org)
[![License](https://img.shields.io/badge/License-BSD--3--Clause-blue?style=flat-square)](LICENSE)
[![Citation Required](https://img.shields.io/badge/Citation-Required-orange?style=flat-square)](#citation)

## Overview

A computational workflow that **bridges the semantic gap** between human narratives and scientific analysis. This cookbook enables researchers, planners, and decision-makers to systematically translate stakeholder experiences—expressed in everyday language—into actionable scientific data, models, and decision frameworks.

### The Challenge

When communities face complex environmental or infrastructure challenges, they describe their experiences using natural language: *"flooding is getting worse,"* *"our wells taste salty,"* *"we need better drainage."* Scientists and decision-makers need structured methods to connect these narratives to:

- Relevant scientific disciplines and expertise
- Measurable variables and data sources  
- Computational models and analytical tools
- Formal decision support frameworks

### The Solution

This workflow uses **Natural Language Processing (NLP)** and **Machine Learning** to automatically:

1. **Analyze text corpora** (interviews, reports, meeting notes, narratives)
2. **Discover key themes and topics** using Latent Dirichlet Allocation
3. **Map topics to scientific domains** through a customizable "science backbone" structure
4. **Extract decision components** (goals, objectives, variables, constraints, indicators)  
5. **Create semantic links** between natural language terms and standardized Scientific Variable Objects (SVOs)
6. **Generate visualizations** showing connections between stakeholder perspectives and scientific frameworks

## Key Features

- **Multi-format input:** Process .txt, .json, .docx, and image files (with OCR)
- **Customizable vocabularies:** Adapt science backbone and SVO definitions to any domain
- **Interactive visualizations:** Network diagrams, topic distributions, domain coverage charts
- **Reproducible workflow:** Designed for TACC HPC systems with full provenance tracking
- **Comprehensive outputs:** CSV files, HTML visualizations, and markdown reports
- **Scalable architecture:** Process corpora from dozens to thousands of documents

## Use Cases

### Environmental Planning
- Climate adaptation planning with Arctic communities
- Coastal resilience decision-making
- Groundwater management stakeholder engagement

### Infrastructure Decision Support  
- Urban planning with community input
- Transportation system analysis
- Public health facility placement

### Research Applications
- Participatory modeling projects
- Mixed-methods research synthesis
- Community-based participatory research (CBPR)
- Interdisciplinary problem framing

## Technical Approach

### Analysis Pipeline

```
Raw Text Documents
       ↓
Text Preprocessing & Tokenization
       ↓
Topic Discovery (LDA)
       ↓
Science Backbone Mapping
       ↓
Decision Component Extraction
       ↓
SVO Semantic Linking
       ↓
Visualization & Reporting
```

### Core Technologies

- **NLP:** NLTK, spaCy (Named Entity Recognition, part-of-speech tagging)
- **Machine Learning:** scikit-learn (TF-IDF, LDA topic modeling)
- **Document Processing:** python-docx, pytesseract (OCR), Pillow
- **Network Analysis:** NetworkX (graph structures, layouts)
- **Visualization:** Plotly (interactive charts), Pandas (data manipulation)

### Scientific Variable Objects (SVOs)

The notebook links natural language to **Scientific Variable Objects** - standardized metadata describing:
- Standard variable names (CF conventions, COARDS)
- Units of measurement
- Data sources and APIs
- Scientific domain classification

Example SVO mapping:
```
Natural Language: "flood depth"
    ↓
SVO: water_level
    ├─ standard_name: "surface_water_elevation"
    ├─ units: "meters"
    ├─ data_source: "USGS stream gauges"  
    └─ domain: "Hydrology"
```

## Getting Started

### Prerequisites

**TACC Account:**
- Active account: Academic Users [Register here](https://accounts.tacc.utexas.edu/register)
- System allocation (startup allocations available)
- Access to TACC data portals (optional)

**Skills:**
- Basic Python programming
- Jupyter notebook familiarity
- Domain knowledge for vocabulary customization

### Installation

#### On TACC Systems (Recommended)

```bash
# Clone the repository
git clone https://github.com/helpfultangent/semantic-bridge-demo.git
cd semantic-bridge-demo

# Load required modules
module load python3
module load jupyter

# Start Jupyter notebook
jupyter notebook semantic_bridge_cookbook.ipynb
```

#### Local Installation

```bash
# Clone repository
git clone https://github.com/helpfultangent/semantic-bridge-demo.git
cd semantic-bridge-demo

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
python -m spacy download en_core_web_sm

# Launch notebook
jupyter notebook semantic_bridge_cookbook.ipynb
```

### Quick Start Example

1. **Prepare Data:** Place your text files in `data/transcripts/`

2. **Run Notebook:** Execute cells sequentially (or use "Run All")

3. **Customize Vocabularies:**
   - Edit `science_backbone` dictionary (Step 4) for your domains
   - Expand `svo_vocabulary` (Step 6) with your variables

4. **Review Outputs:** Check `outputs/` folder for:
   - CSV data files
   - Interactive HTML visualizations  
   - Markdown analysis report

## Outputs

### Generated Files

| File | Description |
|------|-------------|
| `*_topic_mappings.csv` | Topics linked to scientific domains |
| `*_components.csv` | Extracted decision components (goals, objectives, etc.) |
| `*_svo_mappings.csv` | Natural language → SVO semantic links |
| `*_network.html` | Interactive science backbone network visualization |
| `*_sunburst.html` | Domain coverage sunburst chart |
| `*_report.md` | Comprehensive analysis summary with statistics |

### Visualizations

- **Topic Distribution:** Stacked bar charts showing topic proportions across documents
- **Science Backbone Network:** Interactive graph connecting domains, subdisciplines, and topics  
- **Domain Coverage:** Sunburst chart showing distribution of scientific variables by domain
- **Decision Components:** Bar charts of extracted goals, objectives, variables, constraints, indicators

## Customization Guide

### For Your Domain

**Step 1: Define Your Science Backbone** (Step 4, Cell 2)

```python
science_backbone = {
    'Your Primary Domain': [
        'Subdiscipline 1',
        'Subdiscipline 2',
        'Subdiscipline 3'
    ],
    'Secondary Domain': [
        'Subdiscipline A',
        'Subdiscipline B'
    ]
}
```

**Step 2: Create Your SVO Vocabulary** (Step 6, Cell 1)

```python
svo_vocabulary = {
    'your_variable': {
        'standard_name': 'cf_standard_name',
        'units': 'SI units',
        'data_source': 'Your data source/API',
        'keywords': ['keyword1', 'keyword2', 'keyword3'],
        'domain': 'Your Domain'
    }
}
```

**Step 3: Adjust Parameters**

- `n_topics`: Number of topics to discover (Step 3, Cell 1)
- `max_vocabulary`: TF-IDF vocabulary size (Step 3, Cell 3)
- Decision component patterns (Step 5, Cell 1)

### For TACC HPC Integration

**Connect to TACC Data:**
```python
# Example: Load from TACC storage
import requests
data_url = "https://dataverse.tdl.org/api/access/datafile/YOUR_ID"
response = requests.get(data_url)
```

**Scale to Large Corpora:**
```python
# Process documents in batches
from concurrent.futures import ProcessPoolExecutor

with ProcessPoolExecutor(max_workers=8) as executor:
    results = executor.map(process_document, document_list)
```

## Example Applications

### Hurricane Harvey Recovery Planning

**Corpus:** 156 stakeholder interviews, 23 community meetings, 8 planning documents

**Discovered Topics:**
- Topic 1: Flood infrastructure needs → Engineering  
- Topic 2: Environmental impacts → Environmental Science
- Topic 3: Economic recovery → Social Science

**Key SVOs Linked:**
- `flood_depth`, `economic_damage`, `population_at_risk`

**Outcome:** Decision pathways framework connecting community priorities to computational models

### Arctic Infrastructure Adaptation

**Corpus:** 45 Alaska Native community interviews, field observations

**Discovered Topics:**
- Traditional knowledge indicators → Social Science
- Permafrost changes → Physical Science  
- Infrastructure vulnerability → Engineering

**Key SVOs Linked:**
- `ground_temperature`, `infrastructure_vulnerability`, `sea_ice_extent`

**Outcome:** Semantic links between traditional ecological knowledge and climate model variables

## Citation

If you use this cookbook in your research, please cite:

Pierce, S.A. (2025). Semantic Bridge Analysis: A Computational Cookbook for Linking Human Narratives to Scientific Data. Texas Advanced Computing Center, The University of Texas at Austin. https://github.com/helpfultangent/semantic-bridge-demo

```bibtex
@software{semantic_bridge_2025,
  title = {Semantic Bridge Analysis: A Computational Cookbook for Linking Human Narratives to Scientific Data},
  author = {Pierce, Suzanne A.}},
  year = {2025},
  institution = {Texas Advanced Computing Center, The University of Texas at Austin},
  url = {https://github.com/helpfultangent/semantic-bridge-demo}
}
```

## Contributing

We welcome contributions! Areas for expansion:

- Additional SVO vocabularies for different domains
- Integration with semantic web standards (RDF, OWL)
- Support for multilingual analysis
- Advanced NLP models (BERT, GPT)
- Integration with specific data APIs

Please submit issues or pull requests on GitHub.

## License

BSD 3-Clause License

Copyright (c) 2025, Suzanne Pierce and Texas Advanced Computing Center
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its
   contributors may be used to endorse or promote products derived from
   this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

--------------------------------------------------------------------------------

CITATION REQUIREMENT

While this software is licensed permissively under BSD-3-Clause, we strongly
request that any use of this software in academic research or publications
include proper citation. Please cite this work as:

Pierce, S.A. (2025). Semantic Bridge Analysis: 
A Computational Cookbook for Linking Human Narratives to Scientific Data. 
Texas Advanced Computing Center, The University of Texas at Austin.
https://github.com/helpfultangent/semantic-bridge-demo

See the CITATION.cff file for structured citation information that can be
imported into reference managers.

## Support

**TACC User Support:**
- Email: dso@tacc.utexas.edu
- Documentation: TBD
- Training: TBD

**Project Issues:**
- GitHub Issues: https://github.com/helpfultangent/semantic-bridge-demo/issues

## Acknowledgments

** Research funding supporting method development provided by:**
- National Science Foundation, Navigating the New Arctic Program (Award No 2127353).
- The Bridging Barriers Program at The University of Texas at Austin through the Planet Texas 2050 initiative.
- We thank our collaborators at the Museum of South Texas History, Dr. Francisco Guajardo, Rene Ballesteros, Patricia Gomez, Leticia Cavazos, and Melissa Peña, for invaluable assistance in documenting the
Hurricane Beulah event as an initial test case. We also thank Dr. Clint Dawson for the coastal surge modeling of the Beulah case study used to initiate semantic variable object linking for the test case.

---

**Developed by the Decision Support Office at the Texas Advanced Computing Center**  
**The University of Texas at Austin**

[TACC](https://www.tacc.utexas.edu) | [UT Austin](https://www.utexas.edu) 

## Authors
Suzanne A. Pierce 
