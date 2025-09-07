# WAM-ONTO: Water Asset Management Ontology

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![OWL](https://img.shields.io/badge/OWL-2-blue.svg)](https://www.w3.org/TR/owl2-overview/)
[![Protégé](https://img.shields.io/badge/Protégé-5.5+-green.svg)](https://protege.stanford.edu/)

A comprehensive semantic framework for water treatment plant asset management that integrates Building Information Modeling (BIM) with formal ontologies to enable automated reasoning and intelligent decision support.

## 🌊 Overview

WAM-ONTO addresses the critical challenge of knowledge fragmentation in water infrastructure management by providing the first domain-specific ontological framework for water treatment facilities. The framework enables seamless integration between design knowledge (BIM/IFC) and operational asset management through automated semantic reasoning.

### Key Features

- **996 specialized ontology classes** across 12 knowledge domains
- **Automated BIM integration** with 91% classification accuracy  
- **Semantic reasoning capabilities** for maintenance, risk assessment, and compliance
- **Expert validated** with 96% consensus among domain specialists
- **Real-world tested** with Clean-in-Place (CIP) system case study

## 🚀 Quick Start

### Prerequisites

- [Protégé](https://protege.stanford.edu/) 5.5.0 or later
- [Apache Jena](https://jena.apache.org/) 4.7.0 for SPARQL processing
- Minimum 8GB RAM for reasoning operations

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/WAM-ONTO.git
   cd WAM-ONTO
   ```

2. **Load in Protégé**
   - Open Protégé
   - File → Open → Select `ontology/wam-onto.owl`
   - Enable HermiT reasoner for full semantic reasoning

3. **Verify Installation**
   ```bash
   # Test SPARQL queries
   sparql --data=ontology/wam-onto.owl --query=examples/sample-queries.rq
   ```

## 📋 Ontology Structure

### Core Classes Hierarchy

```
Asset (Root Class)
├── Buildings
├── ChambersAndManholes
├── Civil
├── ConsumableAsset
├── ContainmentStructure
├── ControlStructures
├── ControlSystem
├── ElectricalLines
├── ElectricalRotating
├── ElectricalStatic
├── InstrumentsAndMonitoring
├── MechanicalRotating
├── MechanicalStatic
├── Nodes
├── PipesAndConduits
└── Valve
```

### Knowledge Domains

| Domain | Classes | Key Concepts |
|--------|---------|--------------|
| **Asset Identification** | 15 | Asset types, classifications, hierarchies |
| **Maintenance Management** | 89 | Strategies, schedules, work orders, history |
| **Risk & Performance** | 67 | Failure modes, risk levels, KPIs |
| **Financial Management** | 34 | Costs, budgets, depreciation, ROI |
| **Compliance & Regulatory** | 45 | Requirements, standards, audits |
| **Location & Geography** | 12 | Functional/geographic positioning |
| **Documentation** | 78 | Manuals, drawings, specifications |
| **Organizational** | 23 | Personnel, departments, stakeholders |
| **Instrumentation** | 234 | Sensors, monitoring, control systems |
| **Mechanical Systems** | 156 | Pumps, valves, rotating equipment |
| **Electrical Systems** | 89 | Motors, transformers, protection |
| **Civil Infrastructure** | 154 | Structures, chambers, containment |

## 💡 Usage Examples

### Basic Asset Query
```sparql
PREFIX wam: <http://www.semanticweb.org/azabin/ontologies/2025/4/untitled-ontology-7/>

SELECT ?asset ?type ?condition WHERE {
  ?asset a wam:Asset ;
         wam:hasAssetType ?type ;
         wam:hasCondition ?condition .
}
```

### Maintenance Due Query
```sparql
SELECT ?asset ?nextMaintenance WHERE {
  ?asset wam:hasNextMaintenanceDate ?nextMaintenance .
  FILTER(?nextMaintenance < NOW())
}
```

### High-Risk Assets
```sparql
SELECT ?asset ?riskScore WHERE {
  ?asset wam:hasRiskScore ?riskScore .
  FILTER(?riskScore >= 0.7)
}
ORDER BY DESC(?riskScore)
```

## 🏗️ Architecture

### Core Components

1. **Asset Model**: Comprehensive asset classification with 996+ classes
2. **Relationship Framework**: 58+ object properties defining asset interactions
3. **Data Properties**: 100+ attributes for asset characteristics
4. **Reasoning Rules**: Automated inference for maintenance, risk, and compliance
5. **SPARQL Endpoints**: Query interfaces for data extraction

### Integration Points

- **BIM/IFC Integration**: Automated mapping from IFC entities to ontology classes
- **CMMS Systems**: Work order and maintenance data synchronization  
- **SCADA/IoT**: Real-time sensor data ingestion
- **ERP Systems**: Financial and procurement data integration

## 📊 Validation Results

| Metric | Score | Method |
|--------|-------|---------|
| Expert Validation | 96% consensus | Domain expert review (n=25) |
| BIM Classification | 91% accuracy | IFC entity mapping validation |
| Query Performance | <50ms | Average response time (10K assets) |
| Reasoning Consistency | 100% | HermiT reasoner validation |

## 📁 Repository Structure

```
WAM-ONTO/
├── ontology/
│   ├── wam-onto.owl              # Main ontology file
│   ├── modules/                  # Modular ontology components
│   │   ├── asset-core.owl
│   │   ├── maintenance.owl
│   │   ├── risk-performance.owl
│   │   └── compliance.owl
│   └── imports/                  # External ontology imports
├── examples/
│   ├── sample-queries.rq         # SPARQL query examples
│   ├── use-cases/                # Real-world scenarios
│   └── datasets/                 # Sample data for testing
├── validation/
│   ├── competency-questions.md   # Validation queries
│   ├── test-cases/               # Unit tests
│   └── expert-evaluation/        # Validation results
├── documentation/
│   ├── user-guide.md             # Comprehensive usage guide
│   ├── api-reference.md          # SPARQL API documentation
│   ├── integration-guide.md      # BIM/CMMS integration
│   └── architecture.md           # Technical architecture
├── tools/
│   ├── ifc-mapping/              # BIM integration utilities
│   ├── data-conversion/          # Format conversion scripts
│   └── validation-scripts/       # Automated testing
└── papers/                       # Academic publications
    ├── wam-onto-2025.pdf
    └── citations.bib
```

## 🔧 Advanced Usage

### Custom Reasoning Rules

Add domain-specific rules for your organization:

```turtle
# Automatic criticality assessment
[CriticalAssetRule: 
  (?asset wam:hasRiskScore ?risk) 
  (?asset wam:hasAcquisitionCost ?cost)
  greaterThan(?risk, 0.8)
  greaterThan(?cost, 100000)
  -> (?asset wam:hasCriticality wam:ExtremeCritical)]
```

### Custom Asset Classes

Extend the ontology for specific equipment:

```turtle
:CustomPumpType rdfs:subClassOf wam:Pump ;
               wam:hasManufacturer "SpecificBrand" ;
               wam:hasModelNumber "Model123" .
```

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Development Setup

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-capability`
3. Validate changes: `python tools/validation-scripts/validate-ontology.py`
4. Submit a pull request

### Reporting Issues

- Use GitHub Issues for bug reports and feature requests
- Include ontology version and reasoning engine details
- Provide minimal reproducible examples

## 📚 Documentation

- **[Sample Queries](examples/sample-queries.rq)**: 30 practical SPARQL examples
- **[Contributing Guide](CONTRIBUTING.md)**: Development and contribution guidelines  
- **[Ontology Structure](#ontology-structure)**: Core classes and domains (see above)

*Additional documentation (User Guide, API Reference, Integration Guide) is under development. Contributions welcome!*

## 🎓 Academic Usage

If you use WAM-ONTO in academic work, please cite:

```bibtex
@article{wam-onto-2025,
  title={WAM-ONTO: A Comprehensive Ontology Framework for Water Asset Management},
  author={[Author Names]},
  journal={[Journal Name]},
  year={2025},
  volume={[Volume]},
  pages={[Pages]},
  doi={[DOI]}
}
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Water industry experts who provided validation feedback
- Open-source ontology development community
- [Protégé](https://protege.stanford.edu/) development team
- [Apache Jena](https://jena.apache.org/) project

## 📞 Support & Contact

- **Issues**: GitHub Issues
- **Discussions**: GitHub Discussions  
- **Email**: [your-email@domain.com]
- **Documentation**: [GitHub Wiki](../../wiki)

---

**Maintained by**: [Your Organization]  
**Last Updated**: September 2025  
**Version**: 1.0.0
