# Contributing to WAM-ONTO

Thank you for your interest in contributing to the Water Asset Management Ontology (WAM-ONTO)! This document provides guidelines for contributing to the project.

## Code of Conduct

By participating in this project, you agree to abide by our Code of Conduct. Please treat all contributors with respect and maintain professional discourse.

## How to Contribute

### Reporting Issues

Before creating an issue, please:
- Check existing issues to avoid duplicates
- Use the appropriate issue template
- Provide clear, reproducible examples
- Include your environment details (Protégé version, reasoner, OS)

### Suggesting Enhancements

Enhancement suggestions are welcome! Please:
- Use the feature request template
- Explain the use case and expected benefits
- Consider backward compatibility
- Provide mockups or examples where applicable

### Contributing Code/Ontology Changes

1. **Fork the Repository**
   ```bash
   git clone https://github.com/yourusername/WAM-ONTO.git
   cd WAM-ONTO
   git remote add upstream https://github.com/originalowner/WAM-ONTO.git
   ```

2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/issue-number
   ```

3. **Make Your Changes**
   - Follow ontology best practices
   - Maintain consistent naming conventions
   - Add appropriate documentation
   - Include test cases

4. **Validate Your Changes**
   ```bash
   # Run ontology validation
   python tools/validation-scripts/validate-ontology.py
   
   # Test SPARQL queries
   python tools/validation-scripts/test-queries.py
   
   # Check reasoning consistency
   python tools/validation-scripts/check-consistency.py
   ```

5. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "Add: brief description of changes"
   ```

6. **Push and Create Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```

## Ontology Development Guidelines

### Naming Conventions

- **Classes**: PascalCase (e.g., `WaterTreatmentPlant`)
- **Properties**: camelCase (e.g., `hasMaintenanceSchedule`)
- **Individuals**: camelCase (e.g., `pump001`)
- **Use descriptive names** that clearly indicate purpose

### Class Definition Requirements

When adding new classes:

```turtle
:NewAssetClass rdf:type owl:Class ;
               rdfs:subClassOf :ParentClass ;
               rdfs:label "New Asset Class"@en ;
               rdfs:comment "Clear description of what this class represents and when to use it."@en ;
               # Add domain constraints
               rdfs:subClassOf [ rdf:type owl:Restriction ;
                               owl:onProperty :hasRequiredProperty ;
                               owl:someValuesFrom :RequiredType ] .
```

### Property Guidelines

- Define clear domains and ranges
- Add cardinality constraints where appropriate
- Include functional/inverse functional annotations
- Provide comprehensive comments

```turtle
:hasMaintenanceSchedule rdf:type owl:ObjectProperty ;
                       rdfs:domain :Asset ;
                       rdfs:range :MaintenanceSchedule ;
                       rdfs:label "has maintenance schedule"@en ;
                       rdfs:comment "Links an asset to its maintenance schedule."@en .
```

### Data Property Standards

```turtle
:hasAssetID rdf:type owl:DatatypeProperty ;
           rdf:type owl:FunctionalProperty ;
           rdfs:domain :Asset ;
           rdfs:range xsd:string ;
           rdfs:label "has asset ID"@en ;
           rdfs:comment "Unique identifier for the asset."@en .
```

## Testing Requirements

### Competency Questions

All new ontology additions must address at least one competency question. Add tests to `validation/competency-questions.md`:

```markdown
**CQ-XX**: What maintenance activities are overdue for high-criticality assets?

**SPARQL Query**:
```sparql
SELECT ?asset ?activity ?dueDate WHERE {
  ?asset wam:hasCriticality wam:HighCritical ;
         wam:requiresMaintenance ?activity .
  ?activity wam:hasScheduledDate ?dueDate .
  FILTER(?dueDate < NOW())
}
```

**Expected Result**: List of overdue activities for critical assets
```

### Validation Checklist

Before submitting changes:

- [ ] Ontology loads without errors in Protégé
- [ ] HermiT reasoner completes successfully
- [ ] No unsatisfiable classes detected
- [ ] All competency questions pass
- [ ] Documentation updated
- [ ] Example queries provided
- [ ] Backward compatibility maintained

## Documentation Standards

### Code Comments

- Use clear, concise comments
- Explain complex reasoning rules
- Document assumptions and constraints

### File Headers

Include standard headers in all files:

```turtle
# WAM-ONTO: Water Asset Management Ontology
# Module: [Module Name]
# Version: [Version]
# Author: [Your Name]
# Date: [Date]
# Description: [Brief description of module purpose]
```

## Review Process

1. **Automated Checks**: All PRs trigger automated validation
2. **Peer Review**: At least one maintainer review required
3. **Expert Review**: Domain expert approval for significant changes
4. **Integration Testing**: Full test suite execution

## Release Process

### Version Numbering

We follow semantic versioning (MAJOR.MINOR.PATCH):
- **MAJOR**: Incompatible API changes
- **MINOR**: Backward-compatible functionality additions
- **PATCH**: Backward-compatible bug fixes

### Release Checklist

- [ ] All tests pass
- [ ] Documentation updated
- [ ] Changelog updated
- [ ] Version numbers bumped
- [ ] Tagged release created

## Getting Help

If you need assistance:

1. **Check Documentation**: Review existing docs first
2. **Search Issues**: Look for similar questions
3. **Ask Questions**: Open a discussion or issue
4. **Contact Maintainers**: Email for complex questions

## Ontology Modules

When contributing to specific modules:

### Core Asset Module (`ontology/modules/asset-core.owl`)
- Fundamental asset classes and properties
- Requires expert review for all changes

### Maintenance Module (`ontology/modules/maintenance.owl`)
- Maintenance strategies, schedules, activities
- Focus on practical maintenance workflows

### Risk & Performance Module (`ontology/modules/risk-performance.owl`)
- Risk assessment and performance metrics
- Ensure statistical validity of measures

### Compliance Module (`ontology/modules/compliance.owl`)
- Regulatory requirements and standards
- Verify against actual regulations

## Style Guide

### Ontology Organization

```turtle
# 1. Header and imports
@prefix : <http://www.semanticweb.org/azabin/ontologies/2025/4/untitled-ontology-7/> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .

# 2. Object Properties
# 3. Data Properties  
# 4. Classes (alphabetical order)
# 5. Individuals (if any)
```

### Query Style

```sparql
# Use clear prefixes
PREFIX wam: <http://www.semanticweb.org/azabin/ontologies/2025/4/untitled-ontology-7/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

# Format queries for readability
SELECT ?asset ?type ?condition 
WHERE {
  ?asset a wam:Asset ;
         wam:hasAssetType ?type ;
         wam:hasCondition ?condition .
  
  # Add meaningful filters
  FILTER(?condition != wam:Good)
}
ORDER BY ?asset
```

## Community

Join our community:
- **Discussions**: GitHub Discussions for general questions
- **Issues**: Specific bugs and feature requests
- **Email**: [maintainer-email] for private inquiries

Thank you for contributing to WAM-ONTO!
