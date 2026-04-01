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
[docs/project-state-v0.2.md](docs/project-state-v0.2.md).

This document describes the overall goals, design principles, module
framework, data source inventory, and known gaps. It is a living
document and will be versioned as the project develops.

## Pipeline Architecture

The pipeline has three distinct layers, each maintained in its own
repository:

1. **Source data normalisation** -- input adapters transform raw source
   data into canonical metadata JSON documents conforming to the HPSWG
   module field specifications.
2. **Metadata field definition** -- CIDOC CRM-based TSV models define
   the canonical fields for each heritage science documentation module.
3. **Semantic conversion** -- conversion functions accept canonical
   metadata and produce ResearchSpace-compatible RDF.

A shared UUID generation utility supports the conversion layer.

## Related Repositories

| Repository | Role |
|---|---|
| [RICHeS-UKRI/HPSWG-Models](https://github.com/RICHeS-UKRI/HPSWG-Models) | Semantic models layer -- CIDOC CRM TSV models defining the canonical module specifications |
| [RICHeS-UKRI/HPSWG-source-adaptors](https://github.com/RICHeS-UKRI/HPSWG-source-adaptors) | Source data normalisation layer -- input adapters transforming raw source data into canonical metadata JSON |
| [RICHeS-UKRI/HPSWG-crm-converter-php](https://github.com/RICHeS-UKRI/HPSWG-crm-converter-php) | Semantic conversion layer -- PHP functions producing ResearchSpace-compatible RDF using EasyRDF |
| [RICHeS-UKRI/simple-uuid-server](https://github.com/RICHeS-UKRI/simple-uuid-server) | Utility -- UUID generation service used by the conversion layer |
| [HeritageSamples/heritagesamples.org](https://github.com/HeritageSamples/heritagesamples.org) | Heritage Samples Registry -- PID authority infrastructure for sample entities (ECHOES project) |

## Funding and Context

This work is carried out within the
[RICHeS](https://github.com/RICHeS-UKRI) programme and is supported
by two UKRI-funded projects:

<table>
  <tr>
    <td width="200">
      <a href="https://hsds.ac.uk/">
        <img src="https://hsds.ac.uk/wp-content/uploads/2024/09/HSDS_Blue-and-black_1920px.png"
             alt="HSDS Logo" height="64">
      </a>
    </td>
    <td>
      This work was developed within the
      <a href="https://hsds.ac.uk/">Heritage Science Data Service (HSDS)</a>
      project, funded by
      <a href="https://www.ukri.org/">UK Research and Innovation (UKRI)</a>
      as part of the <a href="https://www.riches.ukri.org/">RICHeS Programme</a>.
    </td>
  </tr>
  <tr>
    <td width="200">
      <a href="https://www.riches.ukri.org/funding/riches-investments/tranche-1-collections/reynolds-digital-research-resource/">
        <img src="https://reynolds.nationalgallery.org.uk/project/assets/rdrr%2064.png"
             alt="RDRR Logo" height="64">
      </a>
    </td>
    <td>
      This work was developed within the
      <a href="https://www.riches.ukri.org/funding/riches-investments/tranche-1-collections/reynolds-digital-research-resource/">Reynolds Digital Research Resource (RDRR)</a>
      project, funded by
      <a href="https://www.ukri.org/">UK Research and Innovation (UKRI)</a>
      as part of the <a href="https://www.riches.ukri.org/">RICHeS Programme</a>.
    </td>
  </tr>

  <tr>
    <td width="200">
      <a href="https://www.echoes-eccch.eu/">
        <img src="https://www.echoes-eccch.eu/wp-content/uploads/2024/07/ECHOES_Logo.png"
             alt="ECHOES Logo" height="64">
      </a>
    </td>
    <td>
      The Heritage Samples Registry component of this pipeline is
      funded separately by the
      <a href="https://www.echoes-eccch.eu/">ECHOES</a>
      (European Collaborative Cloud for Cultural Heritage) project and is
      developed under the
      <a href="https://github.com/HeritageSamples">HeritageSamples</a>
      GitHub organisation.
    </td>
  </tr>
</table>

## Status

Early development. The framework is being built and validated
incrementally against real heritage science data, starting with
Reynolds painting documentation from a MediaWiki source. See the
project state document for current status and next steps.

## Contributing

Development is carried out openly. Work may be done in personal forks
with pull requests back to this organisation. Issues and discussion
are welcome.
