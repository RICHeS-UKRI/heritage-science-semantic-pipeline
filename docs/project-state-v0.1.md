# Heritage Science Semantic Pipeline -- Overarching State Document

**Version:** 0.1  
**Date:** 2026-03-31  
**Author:** Joe Padfield, National Gallery, London  
**Status:** Draft for review  

---

## 1. Overall Goal

The long-term goal of this programme of work is to build a reusable,
modular pipeline that can take simple standardised metadata exports from
any heritage science system and automatically convert them into
semantically rich CIDOC CRM-based RDF, ready for use in ResearchSpace
or equivalent linked data platforms.

The pipeline is deliberately system-agnostic. The principle is: if a
collections management system, digital asset management system,
laboratory information system, or any other tool can produce an agreed
simple export in a defined format for a given documentation module, the
pipeline should be able to consume that export and produce correct,
consistent semantic output without manual intervention or
system-specific customisation.

The long-term output is a documented, reusable, and publishable
framework comprising:

- A set of clearly defined heritage science documentation modules, each
  with a canonical list of key metadata fields
- A set of CIDOC CRM-based semantic models, one per module, defining
  how those metadata fields map to ontology classes and properties
- A set of conversion functions implementing those mappings and
  producing ResearchSpace-compatible RDF
- A set of input adapters, one per data source type, that normalise
  source data into the canonical metadata field format for each module
- Evidence of the framework operating across multiple real data sources
  and systems

---

## 2. Design Principles

**Modularity.** Each heritage science activity or data type is
represented as a discrete, well-defined module. Modules are
independently implementable and testable, and connect to each other
through clearly defined linking points.

**Separation of concerns.** The pipeline has three distinct layers that
should not be conflated:

1. Source data normalisation (input adapters)
2. Metadata field definition (module specifications)
3. Semantic conversion (RDF output functions)

Keeping these layers separate is what makes the pipeline reusable
across data sources.

**System-agnostic metadata fields.** The canonical metadata fields for
each module are defined independently of any source system.
Source-specific adapters are responsible for mapping system outputs to
these canonical fields. The semantic conversion layer operates only on
canonical fields.

**CIDOC CRM alignment.** All semantic models use CIDOC CRM 7.1.3 as
the primary ontology, with CRMsci, CRMdig, and ResearchSpace-specific
extensions used where appropriate and documented explicitly. No new
classes or properties are invented; uncertainty about the correct term
is flagged rather than resolved by assumption.

**ResearchSpace compatibility.** All RDF output follows ResearchSpace
conventions, including the primary appellation pattern, PC102/PC14
reification, vocab list links, and EX_Digital_Image/EX_File patterns.
These conventions are documented in the individual project state
documents.

**Incremental development.** The framework is built and validated
incrementally against real data sources, starting with the Reynolds
wiki. Each new data source exercises additional modules and may reveal
gaps in module definitions or conversion functions.

**Open by default.** All framework code, models, and documentation are
developed openly under the RICHeS-UKRI GitHub organisation. Development
work may be carried out in personal forks with pull requests back to
the organisation repositories.

---

## 3. Project Inventory

> **[REVIEW NEEDED]** Please confirm repository names, state document
> locations, and any details about HSR repositories that should be
> listed here. Add or remove projects as needed.

### 3.1 HPSWG-Models

**Repository:** [RICHeS-UKRI/HPSWG-Models](https://github.com/RICHeS-UKRI/HPSWG-Models)  
**Role in pipeline:** Defines the semantic models layer. Contains
CIDOC CRM-based TSV models for heritage science documentation modules,
automated README generation, consistency checking, and Dynamic Modeller
integration for visual representation.  
**Current state document:** To be confirmed  
**Current status:** Active. Models exist for Heritage Object and
sample-related activities. The `annotation_image` model is planned but
not yet built.  
**Role as module specification:** The TSV models in this repository are
the authoritative module specifications. The `//field` and
`//field-via` directives define the canonical metadata fields for each
module.

### 3.2 riches-crm-easyrdf

**Repository:** To be confirmed -- proposed move to
`RICHeS-UKRI/riches-crm-easyrdf`  
**Role in pipeline:** Implements the semantic conversion layer. Contains
PHP functions that accept metadata and produce ResearchSpace-compatible
RDF using EasyRDF. Also currently contains the Reynolds wiki input
adapter (embedded in `index.php` -- planned for separation).  
**Current state document:** `riches-crm-easyrdf-state-v2.md` (v3
update in progress)  
**Current status:** Active. Basic object, tombstone, entry text,
technical, X-ray, and infra-red sections confirmed against Reynolds
wiki data. `easyRDFAddImage()` corrected March 2026.  
**Relationship to HPSWG-Models:** Each function or function group
should map explicitly to one or more HPSWG module models. This mapping
is currently implicit and is being made explicit as the framework
matures.

### 3.3 Heritage Samples Registry (HSR)

**Repository:** To be confirmed  
**Role in pipeline:** Provides PID authority infrastructure for sample
entities. Sample PIDs issued by the HSR are the persistent identifiers
used when sample-related modules are instantiated in the pipeline.  
**Current status:** Active. Website content at
[heritagesamples.org](https://heritagesamples.org) refined, SKOS
ConceptSchemes extracted from JSON Schema. Registry positioned as PID
authority rather than documentation publisher.  
**Relationship to pipeline:** Sample-related modules will reference HSR
PIDs as the identity anchor for sample entities.

### 3.4 This Repository

**Repository:** Proposed `RICHeS-UKRI/heritage-science-semantic-pipeline`  
**Role in pipeline:** Overarching coordination and documentation.
Contains this state document, the module framework definition, the
connection map between projects, and input adapter specifications and
mappings.  
**Current status:** Being established.

---

## 4. Module Framework

> **[REVIEW NEEDED]** Please check the HPSWG Model column against the
> actual repository contents. Add rows for any modules that exist in
> HPSWG but are not listed here, and correct any module names that do
> not match the repository conventions.

| Module | HPSWG Model | Conversion Functions | Test Data Source |
|---|---|---|---|
| Heritage Object (basic identity) | Yes | `easyRDFAddThingV2`, `easyRDFAddIdentifier`, `easyRDFAddTitle` | Reynolds wiki |
| Text document (wiki page) | Partial | `easyRDFaddSimpleWikiTextPage` | Reynolds wiki |
| Technical examination (imaging) | Not yet | Not yet -- placeholder planned | Reynolds wiki |
| Digital image | Partial | `easyRDFAddImage` | Reynolds wiki |
| Physical description | Not yet | Not yet | Reynolds wiki (support section) |
| Sample taking | Yes | Not yet | Planned |
| Sample (entity) | Yes | Not yet | Planned |
| Sample observation | Yes | Not yet | Planned |
| Sample splitting | Yes | Not yet | Planned |
| Sample modification | Yes | Not yet | Planned |
| Sample site | Yes | Not yet | Planned |
| Annotation (image region) | Planned | Not yet | Planned |

---

## 5. Data Source Inventory

> **[REVIEW NEEDED]** Please add or correct data source details,
> particularly for the CMS and DAM. Remove or rename any sources that
> are not currently planned.

### 5.1 Reynolds Wiki

**Type:** MediaWiki instance, data extracted to JSON  
**Owner:** National Gallery, London  
**Modules exercised:** Heritage Object, text document, digital image,
technical examination (partial)  
**Adapter status:** Partially implemented within `index.php` in
riches-crm-easyrdf. Separation into a discrete input adapter is a
planned refactor.  
**Notes:** Data is real but incomplete. Examination dates and actors
are not available in the wiki data; examination events are modelled as
placeholders. Wiki contribution metadata (authors, edit counts, dates)
maps to document creation provenance, not examination provenance.

### 5.2 Collections Management System

**Type:** To be confirmed  
**Modules anticipated:** Heritage Object (richer), physical
description, provenance, exhibition history  
**Adapter status:** Not yet started  

### 5.3 Digital Asset Management System (DAM)

**Type:** To be confirmed  
**Modules anticipated:** Digital image, file metadata, technical
capture parameters  
**Adapter status:** Not yet started  

### 5.4 External Sources

**Type:** To be confirmed  
**Notes:** E-RIHS, ECHOES, and other external initiatives may provide
sample and examination data exercising sample-related modules.

---

## 6. Connection Map

> **[REVIEW NEEDED]** Please check that this diagram correctly
> represents the intended connections between modules. The sample chain
> in particular may need adjustment based on the HPSWG model
> definitions.
```
Heritage Object (HPSWG)
    |
    |-- identified by ---------> Identifier, Title
    |
    |-- documented in ----------> Text Document (wiki page)
    |                                 |
    |                                 |-- incorporates --> Digital Image
    |                                 |-- documents -----> Examination Event
    |
    |-- examined in ------------> Technical Examination Event
    |                                 |
    |                                 |-- produced ------> Digital Image
    |                                                          |
    |                                                          |-- depicts --> Heritage Object
    |
    |-- has sample taken -------> Sample Taking Event (HPSWG S20)
                                      |
                                      |-- produced -------> Sample (HPSWG S13)
                                                                |
                                                                |-- observed in -> Observation (S27)
```

---

## 7. Reynolds Wiki to Canonical Metadata Fields

This section documents how the Reynolds wiki JSON structure maps to
canonical metadata fields for each module. This is the specification
for the Reynolds wiki input adapter.

> **[REVIEW NEEDED]** Please check field names and wiki source
> references. The canonical field names in particular should align with
> the `//field` directive names used in HPSWG-Models where those models
> exist.

### 7.1 Heritage Object Fields

| Canonical Field | Wiki Source | Notes |
|---|---|---|
| Object label | `$inv[5] . ': ' . $ptitle` | Inventory number plus title |
| Object type | Hardcoded: `painting`, `paintings_visual_works` | AAT and local vocab |
| Preferred identifier value | `$inv[5]` | Wallace Collection number |
| Preferred identifier assigner | Wallace Collection | Hardcoded |
| Secondary identifier value | `$page['wInvNo']` | NG research number |
| Secondary identifier assigner | National Gallery | Hardcoded |
| Title text | `$page['title']` | Full title |
| Title type | `full titles` | AAT term |
| Current keeper | Wallace Collection | Hardcoded |

### 7.2 Text Document Fields

| Canonical Field | Wiki Source | Notes |
|---|---|---|
| Document label | Section name plus painting name | Constructed |
| Document text | `$page['pages'][section]['text']` | Full wiki text |
| Document types | `$eTypes` array per section | Mapped per `$do` value |
| Earliest date | `$page['pages'][section]['earliest']` | Wiki edit date |
| Latest date | `$page['pages'][section]['latest']` | Wiki edit date |
| Contributors | `$page['pages'][section]['contributions']` | Wiki usernames |

### 7.3 Digital Image Fields

| Canonical Field | Wiki Source | Notes |
|---|---|---|
| Image file name | `figure['file']` | From wiki figure array |
| Image label | `figure['figure']` | Caption text |
| Image type | `illustrations`, `digital_image` | Hardcoded |
| Parent document | Containing document URI | Via `P165_incorporates` |
| Depicts | Painting URI | `P62_depicts` -- to be implemented |

### 7.4 Technical Examination Fields (Placeholder)

> **[REVIEW NEEDED]** These fields are proposed based on the available
> wiki data. They will need to be validated against the HPSWG model
> once that model is developed, and against DAM/CMS data once those
> sources are in scope.

| Canonical Field | Wiki Source | Notes |
|---|---|---|
| Examination type | Section key (`x-ray`, `infra-red`) | Maps to AAT term |
| Examined object | Painting URI | Linked from event |
| Image produced | Image URI | Via `P108_has_produced` |
| Document produced | Document URI | Via `P70_documents` |
| Examination date | Not available in wiki | Placeholder -- to come from DAM/CMS |
| Examiner | Not available in wiki | Placeholder -- to come from DAM/CMS |

---

## 8. Known Gaps and Open Questions

> **[REVIEW NEEDED]** Please add any gaps or open questions not listed
> here.

- **Examination event implementation:** CRMsci `S4_Observation` pattern
  agreed in principle, PHP implementation not yet started.
- **`P62_depicts` connection:** Required for RS image display, not yet
  implemented in `easyRDFAddImage()`.
- **Input adapter separation:** Wiki data normalisation currently
  embedded in `index.php`. Should be refactored into a discrete adapter
  layer with a clean function signature.
- **HPSWG model coverage:** Physical description and technical
  examination modules have no HPSWG model yet.
- **DAM and CMS adapters:** Data source details to be confirmed.
- **`annotation_image` model:** Planned in HPSWG-Models but not yet
  built.
- **ECHOES/HSDS integration:** Relationship to external project data
  not yet formally mapped to the pipeline.

---

## 9. Next Steps

> **[REVIEW NEEDED]** Please reorder or add steps as appropriate.

1. Review and correct this document
2. Create `RICHeS-UKRI/heritage-science-semantic-pipeline` repository
   and commit this document
3. Confirm repository moves or forks to `RICHeS-UKRI` organisation
4. Update riches-crm-easyrdf state document to v3
5. Implement examination event placeholder in X-ray and IR functions
6. Add `P62_depicts` to `easyRDFAddImage()`
7. Begin explicit mapping between riches-crm-easyrdf functions and
   HPSWG module models
8. Identify priority HPSWG modules for development based on next data
   source
