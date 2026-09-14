# Gelmat Modelling Notes

**Ontology:** Gelmat (`https://w3id.org/gelmat/`, prefix `gmat:`) · Version 1.1.0

Design decisions behind the main modelling patterns in `gelmat.ttl`.

## Quantities and units

All quantitative properties follow the OM-2 measurement pattern: a quantity individual links via `om:hasValue` to an `om:Measure` carrying `om:hasNumericalValue` and `om:hasUnit`. Each quantity class declares its canonical unit via `gmat:hasCanonicalUnit`, in SI units (for example `gmat:Density` uses `om:kilogramPerCubicmetre` and `gmat:ThermalConductivity` uses `om:wattPerMetreKelvin`). Density is split into bulk, skeletal, and tap density. Fractal and small-angle scattering descriptors (mass and surface fractal dimension, Porod exponent, correlation length) describe the self-similar network structure that is typical for aerogels. `gmat:measuredBy` links a quantity to the analysis method that produced it.

## Substances and roles

Substances are typed by chemical identity (under `obo:CHEBI_24431`), with a precursor hierarchy organised by material family (silica, metal oxide, organic, polymer, biopolymer) and a reinforcement branch for composite fillers. The function of a substance in a specific step is stated through roles:

```turtle
:step gmat:usesSubstance :substance .
:substance prov:hadRole [ a pmat:Catalyst ] .
```

Gelmat reuses `pmat:Catalyst` and `pmat:Solvent` and adds its own roles (precursor, crosslinker, surfactant, silylation agent, reinforcement, drying control additive, supercritical fluid, gelling agent). This way the same ethanol can be a solvent in one step and a reactant in another.

## Plan vs. execution

`pmat:Procedure` and its subtree (`Method`, `CreationProcess`, `Gelation`, `Drying`, ...) denote executed processes (BFO occurrents). The reusable recipe is modelled separately as `gmat:SynthesisProtocol` (a BFO generically dependent continuant). A concrete run links to its recipe via `gmat:realizesProtocol`.

## Process parameters

`gmat:ProcessParameter` (molar and volume ratios, pH condition, stirring rate, temperature and pressure profiles, ...) is a BFO quality and an `om:Quantity` at the same time. Parameters carry their magnitude via `om:hasValue` and attach to the process they characterise via `pmat:isParameterOf`. They record achieved, per-run values, not plan prescriptions.

## Required vs. optional synthesis steps

`gmat:AerogelSynthesis` requires sol formation, gelation, and drying as parts. Aging, solvent exchange, and surface modification are common but optional steps, so syntheses that skip them remain valid.

## Sibling disjointness

Sibling classes that exclude each other (gel forms, drying methods, geometries, parameter kinds, density kinds, equipment, solvents, synthesis steps, characterisation methods, quantity kinds, defect kinds) are declared disjoint, so mistyped individuals show up during validation. Where one individual can belong to several siblings at once (substance roles, co-occurring gelation pathways, coinciding moduli, composite and hybrid families) no disjointness is asserted. See the General-axioms section of `gelmat.ttl`.
