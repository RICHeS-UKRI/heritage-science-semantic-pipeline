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
| riches-crm-easyrdf (to be confirmed under RICHeS-UKRI) | Semantic conversion layer -- PHP functions producing ResearchSpace-compatible RDF |
| [HeritageSamples/heritagesamples.org](https://github.com/HeritageSamples/heritagesamples.org) | Heritage Samples Registry -- PID authority infrastructure for sample entities (ECHOES project) |

## Funding and Context

This work is carried out within the
[RICHeS](https://github.com/RICHeS-UKRI) programme and is supported
by two UKRI-funded projects:

- The [Heritage Science Data Service (HSDS)](https://hsds.ac.uk),
  which is developing shared data infrastructure for heritage science
  in the UK. See the
  [HSDS RICHeS investment page](https://www.riches.ukri.org/funding/riches-investments/heritage-science-data-service-hsds/)
  for further details.
- The [Reynolds Digital Research Resource](https://www.riches.ukri.org/funding/riches-investments/tranche-1-collections/reynolds-digital-research-resource/),
  which is developing a semantically rich digital research resource
  for the Reynolds paintings at the Wallace Collection, drawing on
  technical documentation held at the National Gallery, London.

The Heritage Samples Registry component of the broader pipeline is
funded separately by the
[ECHOES project](https://www.echoes-eccch.eu/) and is developed
under the [HeritageSamples](https://github.com/HeritageSamples)
GitHub organisation.

## Status

Early development. The framework is being built and validated
incrementally against real heritage science data, starting with
Reynolds painting documentation from a MediaWiki source. See the
project state document for current status and next steps.

## Contributing

Development is carried out openly. Work may be done in personal forks
with pull requests back to this organisation. Issues and discussion
are welcome.
