# Gelmat: An Ontology for Sol-Gel Materials

**Version:** 1.1.0
**Namespace:** `https://w3id.org/gelmat/` (prefix `gmat:`)
**License:** [CC-BY-NC-4.0](https://creativecommons.org/licenses/by-nc/4.0/)

## Overview

Gelmat is a domain ontology for sol-gel materials. It covers synthesis routes, gel types (aerogel, xerogel, cryogel, ambigel, hydrogel, alcogel), precursor chemistry, surface modification, drying methods, thermal treatments, characterisation methods, laboratory equipment, defects, applications, and quantitative material properties. The major sol-gel derived material families are included: silica, organosilica, metal oxide, organic, carbon, polymer, bio-based, and composite aerogels.

The ontology defines 299 classes, 57 object properties, and 9 datatype properties. Quantity classes declare canonical SI units, common substances are mapped to ChEBI and carry CAS numbers and acronyms, and every class has a label, a comment, and a definition. Design decisions are documented in [`docs/modelling_notes.md`](docs/modelling_notes.md).

## Reused ontologies

| Prefix | Ontology | Used for |
|--------|----------|----------|
| `pmat:` | [PolyMat](https://w3id.org/polymat/) | Base ontology, extended by Gelmat (imported) |
| `om:` | [OM-2](http://www.ontology-of-units-of-measure.org/) (Rijgersberg, Willems) | Units of measure and quantities (imported) |
| `obo:` | [BFO](https://basic-formal-ontology.org/), [RO](https://obofoundry.org/ontology/ro.html), [ChEBI](https://www.ebi.ac.uk/chebi/) | Upper-level structure, relations, chemical entities |
| `prov:` | [PROV-O](https://www.w3.org/TR/prov-o/) | Provenance and roles |

## Files

| File | Description |
|------|-------------|
| `gelmat.ttl` | The Gelmat ontology (TBox) in Turtle format |
| `aerogel_data.ttl` | Example MTMS aerogel synthesis data (ABox) with 8 samples, process parameters, and kinetic data in SI units |
| `docs/index.html` | Browsable HTML documentation, served at https://dlr-wf.github.io/Gelmat-Ontology/ |
| `docs/modelling_notes.md` | Modelling patterns and design decisions |
| `docs/class_hierarchy.md` | Class hierarchy overview |
| `docs/class_hierarchy_diagram.md` | Mermaid diagrams of the core hierarchy |
| `docs/general_competency_questions.md` | Competency questions with SPARQL queries |
| `docs/prefixes.md` | SPARQL prefix declarations |

## Quick start

Open `gelmat.ttl` in [Protégé](https://protege.stanford.edu/), or load it with [rdflib](https://rdflib.readthedocs.io/):

```python
from rdflib import Graph

g = Graph()
g.parse("gelmat.ttl", format="turtle")
g.parse("aerogel_data.ttl", format="turtle")
```

```sparql
PREFIX gmat: <https://w3id.org/gelmat/>
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?aerogel ?label
WHERE {
  ?aerogel rdf:type/rdfs:subClassOf* gmat:Aerogel .
  ?aerogel rdfs:label ?label .
}
```

More example queries are in [`docs/general_competency_questions.md`](docs/general_competency_questions.md).

## Contributors

- **Prakul Pandit**, Institute for Frontier Materials on Earth and in Space, German Aerospace Center (DLR), Cologne. [ORCID 0000-0002-1343-3046](https://orcid.org/0000-0002-1343-3046)
- **Antoni Dudij**, Institute for Frontier Materials on Earth and in Space, German Aerospace Center (DLR), Cologne [ORCID 0009-0001-2543-8610](https://orcid.org/0009-0001-2543-8610)
- **Barbara Milow**, Institute for Frontier Materials on Earth and in Space, German Aerospace Center (DLR), Cologne. [ORCID 0000-0002-6350-7728](https://orcid.org/0000-0002-6350-7728)

## Citation

> Pandit, P., Dudij, A., & Milow, B. (2026). *Gelmat: An Ontology for Sol-Gel Materials* (Version 1.1.0). German Aerospace Center (DLR). https://w3id.org/gelmat/


## License

Copyright (c) 2026 Prakul Pandit, Antoni Dudij, Barbara Milow. Institute for Frontier Materials on Earth and in Space, German Aerospace Center (DLR), Cologne, Germany.

This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/); see the [LICENSE](LICENSE) file for the full text.

Gelmat is an adaptation of the [PolyMat ontology](https://w3id.org/polymat/) by Marta Dembska, Martin Held, and Sirko Schindler, used under CC BY-NC 4.0; changes have been made. Units of measure are provided by the [Ontology of units of Measure (OM-2)](http://www.ontology-of-units-of-measure.org/) by Hajo Rijgersberg and Don Willems, used under CC BY 4.0.

