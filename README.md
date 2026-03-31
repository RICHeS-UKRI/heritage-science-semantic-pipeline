# Heritage Science Semantic Pipeline

This repository provides overarching documentation and coordination
for the Heritage Science Semantic Pipeline -- a modular framework for
converting standardised heritage science metadata exports into
CIDOC CRM-based RDF, ready for use in
[ResearchSpace](https://researchspace.org) or equivalent linked data
platforms.

The pipeline is system-agnostic. The goal is that any collections
management system, digital asset management system, or laboratory
information system that can produce an agreed simple metadata export
for a given documentation module can have that export automatically
mapped to CIDOC CRM and ingested into a ResearchSpace knowledge graph.

## Documentation

The primary project state document is at
[docs/project-state-v0.1.md](docs/project-state-v0.1.md).
This document describes the overall goals, design principles, module
framework, data source inventory, and known gaps. It is a living
document and will be versioned as the project develops.

## Related Repositories

| Repository | Role |
|---|---|
| [RICHeS-UKRI/HPSWG-Models](https://github.com/RICHeS-UKRI/HPSWG-Models) | Semantic models layer -- CIDOC CRM TSV models defining the canonical module specifications |
| riches-crm-easyrdf (to be moved to RICHeS-UKRI) | Semantic conversion layer -- PHP functions producing ResearchSpace-compatible RDF |
| heritagesamples.org (HSR) | PID authority infrastructure for sample entities |

## Funding and Context

This work is supported by UKRI and carried out within the
[RICHeS](https://github.com/RICHeS-UKRI) programme. It builds on
heritage science data infrastructure work at the
[National Gallery, London](https://www.nationalgallery.org.uk),
including the Reynolds technical documentation project, the Heritage
Samples Registry, and the E-RIHS and ECHOES initiatives.

## Status

Early development. The framework is being built and validated
incrementally against real heritage science data, starting with
Reynolds painting documentation from a MediaWiki source. See the
project state document for current status and next steps.

## Contributing

Development is carried out openly. Work may be done in personal forks
with pull requests back to this organisation. Issues and discussion
are welcome.
