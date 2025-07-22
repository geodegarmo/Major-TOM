# Major TOM Overview

## 🛰️ What is Major TOM?

Major TOM (Terrestrial Observation Metaset) is an extensible framework designed to standardize and facilitate the creation of large-scale Earth Observation (EO) datasets. Rather than being just another dataset, Major TOM provides a unified approach to organizing, accessing, and combining multiple EO datasets from different sources.

## 🎯 Purpose and Vision

The Earth Observation field faces significant challenges with data interoperability due to diverse formats and data structures. Major TOM addresses this by:

- **Standardizing** EO dataset formats and metadata structures
- **Enabling** seamless combination of multiple datasets
- **Reducing** duplication of effort in dataset creation
- **Providing** a geographical indexing system for global coverage
- **Supporting** Terabyte-scale dataset management

## 🗺️ Core Components

### 1. Geographical Indexing System
Major TOM employs a uniform grid system that divides the Earth's surface into manageable cells, enabling:
- Consistent spatial referencing across datasets
- Efficient data retrieval and processing
- Scalable grid generation at various resolutions (default: 10km)

### 2. Metadata Framework
A standardized metadata structure that allows:
- Integration of diverse data sources
- Consistent dataset documentation
- Enhanced discoverability and usability

### 3. Python API
The `MajorTOM` Python package provides:
- Dataset loading and manipulation tools
- Grid generation utilities
- Embedding generation capabilities
- Integration with popular ML frameworks (PyTorch)

## 📊 Available Datasets

### Image Datasets
- **Core-S2L2A**: Sentinel-2 Level 2A (2.2M patches, ~23TB)
- **Core-S2L1C**: Sentinel-2 Level 1C (2.2M patches, ~23TB)
- **Core-S1RTC**: Sentinel-1 RTC SAR (1.5M patches, ~16TB)
- **Core-DEM**: Copernicus DEM 30 (1.8M patches, ~1TB)

### Embedding Datasets
- **Core-S2L1C-SSL4EO**: 56M embeddings from SSL4EO-ResNet50 (253GB)
- **Core-S1RTC-SSL4EO**: 37M embeddings from SSL4EO-ResNet50 (333GB)
- **Core-S2RGB-DINOv2**: 56M embeddings from DINOv2 (223GB)
- **Core-S2RGB-SigLIP**: 20M embeddings from SigLIP (41GB)

## 🔧 Technical Architecture

### Data Organization
```
Major TOM Dataset Structure:
├── Grid Cell (e.g., "0U_0R")
│   ├── Product ID (timestamp-based)
│   │   ├── Band files (.tif)
│   │   ├── Thumbnail (.png)
│   │   └── Metadata
└── Global metadata.parquet
```

### Key Classes and Modules

1. **MajorTOM Dataset Class**: PyTorch Dataset implementation for efficient data loading
2. **Grid Module**: Generates uniform global grids at configurable resolutions
3. **Embedder Module**: Pre-trained model integration for feature extraction
4. **Helper Modules**: Metadata and sample manipulation utilities

## 🚀 Getting Started

### Installation
```bash
pip install majortom
```

### Basic Usage
```python
from MajorTOM import MajorTOM, Grid
import pandas as pd

# Load metadata
df = pd.read_parquet('metadata.parquet')

# Create dataset
dataset = MajorTOM(
    df=df,
    local_dir='/path/to/data',
    tif_bands=['B04', 'B03', 'B02'],  # RGB
    png_bands=['thumbnail']
)

# Generate custom grid
grid = Grid(dist=50)  # 50km grid
```

## 🌍 Use Cases

- **Machine Learning**: Large-scale model training with standardized EO data
- **Global Monitoring**: Environmental change detection and analysis
- **Research**: Standardized benchmarking and reproducible studies
- **Applications**: Land use classification, disaster monitoring, climate research

## 📈 Impact and Benefits

- **Scale**: Manages Terabyte-scale datasets efficiently
- **Interoperability**: Seamless integration of multiple data sources
- **Community**: Open-source framework encouraging collaboration
- **Accessibility**: Simplified access to complex EO datasets
- **Standardization**: Promotes best practices in EO data management

## 🔗 Resources

- **Datasets**: Available on [Hugging Face](https://huggingface.co/Major-TOM)
- **Demo**: [Interactive Viewer](https://huggingface.co/spaces/Major-TOM/MajorTOM-Core-Viewer)
- **Paper**: [arXiv:2402.12095](https://arxiv.org/abs/2402.12095)
- **Examples**: Jupyter notebooks included in repository

## 🤝 Contributing

Major TOM is designed as a community-driven initiative. Contributions are welcome in the form of:
- New datasets following the Major TOM standard
- Code improvements and bug fixes
- Documentation enhancements
- Use case examples and tutorials

## 📄 Citation

```bibtex
@inproceedings{Major_TOM,
  title={Major TOM: Expandable Datasets for Earth Observation}, 
  author={Alistair Francis and Mikolaj Czerkawski},
  year={2024},
  eprint={2402.12095},
  archivePrefix={arXiv},
  primaryClass={cs.CV}
}
```

---

*Powered by [Φ-lab, European Space Agency (ESA) 🛰️](https://huggingface.co/ESA-philab)*