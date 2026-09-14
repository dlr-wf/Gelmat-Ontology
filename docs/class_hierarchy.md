# Gelmat Class Hierarchy

**Ontology:** Gelmat (`https://w3id.org/gelmat/`, prefix `gmat:`) · Version 1.1.0
**Base:** [PolyMat](https://w3id.org/polymat/) (`pmat:`)

This document covers the **299 sol-gel/aerogel terms authored by Gelmat** (`gmat:`). The full ontology also reuses classes from PolyMat (`pmat:`; polymer synthesis, membrane fabrication, data management, laboratory infrastructure, etc.): see the [PolyMat documentation](https://w3id.org/polymat/) for those.

> `[o]` PolyMat (`pmat:`) base class (shown as parent context) · `[e]` external (BFO / OM-2 / ChEBI) · `[n]` Gelmat (`gmat:`) class · `*` multiple parents

---

## 1 · Material Entities

### 1.1 Gel-Based Materials and Aerogel Types

- `BFO:0000040` `[e]`
    - `Substance` `[o]`
        - `AlkoxideSolution` `[n]`
        - `CatalystSolution` `[n]`
        - `Gel` `[n]`
            - `Aerogel` `[n]`
                - `CarbonAerogel` `[n]`: not under OrganicAerogel, since pyrolysis leaves no organic bonds; the two are disjoint
                - `CompositeAerogel` `[n]`: matrix and filler linked via `hasMatrix` / `hasReinforcement`
                - `HybridAerogel` `[n]`
                    - `OrganosilicaAerogel` `[n]`
                - `InorganicAerogel` `[n]`
                    - `MetalAerogel` `[n]`
                    - `MetalOxideAerogel` `[n]`
                        - `AluminaAerogel` `[n]`
                        - `IronOxideAerogel` `[n]`
                        - `TitaniaAerogel` `[n]`
                        - `ZirconiaAerogel` `[n]`
                    - `SilicaAerogel` `[n]`
                - `OrganicAerogel` `[n]`
                    - `PhenolicAerogel` `[n]`
                - `PolymerAerogel` `[n]`
                    - `BioAerogel` `[n]`
                    - `PolyimideAerogel` `[n]`
                    - `PolyurethaneAerogel` `[n]`
            - `Ambigel` `[n]`: ambient-dried with structure largely preserved
            - `Cryogel` `[n]`: freeze-dried
            - `WetGel` `[n]`
                - `Alcogel` `[n]`
                - `Hydrogel` `[n]`
            - `Xerogel` `[n]`
        - `Reinforcement` `[n]`: filler phases for composites
            - `CarbonFibre` `[n]` · `CarbonNanotube` `[n]` · `CelluloseFibre` `[n]` · `Clay` `[n]` · `GlassFibre` `[n]` · `GrapheneOxide` `[n]`
        - `Sol` `[n]`
        - `StockSolution` `[n]`
        - `SupercriticalFluid` `[n]`
            - `SupercriticalCO2` `[n]`
            - `SupercriticalEthanol` `[n]`

### 1.2 Chemical Substances

Substances are typed by chemical identity; the function in a specific step is stated with a role (§4.5). Common precursors, solvents, and catalysts carry CAS numbers (`pmat:hasCASNr`), acronyms (`pmat:hasAcronym`), and ChEBI mappings (`skos:exactMatch` / `skos:closeMatch`).

- `CHEBI:24431` `[e]`
    - `Acetone` `[n]`
    - `Acid` `[n]`
        - `AcidCatalyst` `[n]`
            - `AceticAcid` `[n]` · `CitricAcid` `[n]` · `HydrofluoricAcid` `[n]` · `NitricAcid` `[n]` · `OxalicAcid` `[n]`
    - `Alcohol` `[n]`
        - `Ethanol` `[n]` · `Isopropanol` `[n]` · `Methanol` `[n]`
    - `AmmoniumCompound` `[n]`
        - `AmmoniumHydroxide` `[n]`
    - `Base` `[n]`
        - `BaseCatalyst` `[n]`
            - `SodiumCarbonate` `[n]` · `SodiumHydroxide` `[n]`
    - `Crosslinker` `[n]`
    - `Dimethylformamide` `[n]`
    - `DryingControlChemicalAdditive` `[n]`
        - `Formamide` `[n]` · `Glycerol` `[n]`
    - `FluorideAdditive` `[n]`
    - `FluorideSalt` `[n]`
        - `AmmoniumFluoride` `[n]`
    - `Gas` `[n]`
        - `Air` `[n]` · `Argon` `[n]` · `CarbonDioxide` `[n]` · `Nitrogen` `[n]`
    - `Heptane` `[n]` · `Hexane` `[n]`
    - `OrganosiliconCompound` `[n]`
        - `SiliconAlkoxidePrecursor` `[n]` \* also subClassOf `SilicaPrecursor`
            - `APTES` `[n]` · `BTMSE` `[n]` · `GPTMS` `[n]` · `MTES` `[n]` · `MTMS` `[n]` · `PEDS` `[n]` · `TMOS` `[n]` · `Tetraethoxysilane` `[n]` \* · `VTMS` `[n]`
    - `PHAdjuster` `[n]`
    - `Precursor` `[n]`: network formers grouped by material family
        - `BiopolymerPrecursor` `[n]`
            - `Alginate` `[n]` · `Cellulose` `[n]` (→ `Nanocellulose` `[n]`) · `Chitosan` `[n]` · `Gelatin` `[n]` · `Pectin` `[n]` · `Starch` `[n]`
        - `MetalOxidePrecursor` `[n]`
            - `MetalAlkoxide` `[n]`
                - `AluminiumSecButoxide` `[n]` · `TitaniumIsopropoxide` `[n]` · `ZirconiumPropoxide` `[n]`
        - `OrganicPrecursor` `[n]`
            - `Formaldehyde` `[n]` · `Furfural` `[n]` · `Lignin` `[n]` · `Melamine` `[n]` · `Phenol` `[n]` · `Resorcinol` `[n]` · `Tannin` `[n]`
        - `PolymerPrecursor` `[n]`
            - `Diamine` `[n]` · `Dianhydride` `[n]` · `Isocyanate` `[n]` · `Polyol` `[n]`
        - `SilicaPrecursor` `[n]`
            - `SilicatePrecursor` `[n]` (→ `SodiumSilicate` `[n]`, the water-glass route)
    - `Silanol` `[n]`
    - `SilylationAgent` `[n]`
        - `Hexamethyldisilazane` `[n]` · `Trimethylchlorosilane` `[n]`
    - `Surfactant` `[n]`
    - `Urea` `[n]`
    - `Water` `[n]`
        - `DeionizedWater` `[n]`

---

## 2 · Processes and Methods

### 2.1 Synthesis and Creation

`Procedure` and everything below it denote **executed processes** (BFO occurrents), not recipes: the recipe/plan is `SynthesisProtocol` (§4.4), linked from a run via `realizesProtocol`. `AerogelSynthesis` requires sol formation, gelation, and drying as parts; aging, solvent exchange, and surface modification are optional.

- `Procedure` `[o]` *(⊑ BFO occurrent)*
    - `Method` `[o]`
        - `CreationProcess` `[n]`
            - `AerogelSynthesis` `[n]`
                - `APDAerogelSynthesis` `[n]`
            - `Aging` `[n]`
            - `Condensation` `[n]`
            - `Gelation` `[n]`
                - `AcidCatalysis` `[n]` · `BaseCatalysis` `[n]` · `TwoStepCatalysis` `[n]`
            - `SolFormation` `[n]`
                - `Hydrolysis` `[n]`
            - `SolGelTransition` `[n]`: the gel-point event; `Gelation` has it as part
            - `ThermalTreatment` `[n]`
                - `Activation` `[n]` · `Calcination` `[n]` · `Curing` `[n]` · `Pyrolysis` `[n]` · `Sintering` `[n]` · `TemperatureRamping` `[n]`

### 2.2 Sample Preparation and Drying

- `Method` `[o]`
    - `SamplePreparation` `[o]`
        - `Casting` `[n]` · `Cooling` `[n]` · `Depressurization` `[n]` · `FreezeCasting` `[n]` · `Impregnation` `[n]` · `IonExchange` `[n]` · `Pressurization` `[n]` · `Sonication` `[n]` · `WashingCycle` `[n]`
        - `Mixing` `[n]`
            - `Stirring` `[n]`
        - `SolventExchange` `[n]`
        - `SurfaceModification` `[n]`
            - `SurfaceSilylation` `[n]`
        - `Drying` `[o]`
            - `AmbientPressureDrying` `[n]`
            - `FreezeDrying` `[n]`
            - `MicrowaveDrying` `[n]`
            - `SupercriticalDrying` `[n]`
                - `HighTemperatureSupercriticalDrying` `[n]`: direct ethanol/methanol route
            - `VacuumDrying` `[n]`

### 2.3 Characterisation and Analysis

- `Method` `[o]`
    - `Analysis` `[o]`
        - `BulkDensityMeasurement` `[n]`
        - `CompressionTesting` `[n]`
        - `DifferentialScanningCalorimetry` `[n]` · `ThermogravimetricAnalysis` `[n]`
        - `EDXAnalysis` `[n]` · `XPSAnalysis` `[n]` · `XRayDiffraction` `[n]`
        - `FTIRSpectroscopy` `[n]` · `RamanSpectroscopy` `[n]` · `SolidStateNMR` `[n]`
        - `HydrophobicityTesting` `[n]`
        - `OpticalTransmittanceMeasurement` `[n]`
        - `PorosityMeasurement` `[n]`
            - `BETAnalysis` `[n]` · `BJHAnalysis` `[n]` · `MercuryIntrusionPorosimetry` `[n]`
        - `SANS` `[n]` · `SAXS` `[n]`
        - `SkeletalDensityMeasurement` `[n]`
            - `HeliumPycnometry` `[n]`
        - `SpecificSurfaceAreaMeasurement` `[n]`
        - `TEMImaging` `[n]`
        - `ThermalConductivityTesting` `[n]`
            - `GuardedHotPlate` `[n]` · `HeatFlowMeterMethod` `[n]` · `LaserFlash` `[n]` · `TransientHotWire` `[n]`

> A measured quantity links to the method that produced it via `gmat:measuredBy` (domain `om:Quantity`, range `pmat:Analysis`).

---

## 3 · Laboratory Equipment

### 3.1 Equipment

- `Device` `[o]`
    - `Equipment` `[o]`
        - `CO2SupplySystem` `[n]`
        - `CoolingSystem` `[n]`
        - `Dryer` `[n]`
            - `FreezeDryer` `[n]` · `Oven` `[n]` · `SupercriticalDryer` `[n]`
        - `PressureVessel` `[n]`

### 3.2 Instruments

- `Device` `[o]`
    - `Instrument` `[o]`
        - `Accupyc` `[n]` · `ForceCell` `[n]` · `Geopyc` `[n]` · `HeatFlowMeter` `[n]` · `HeatingBath` `[n]` · `MagneticStirrer` `[n]` · `OverheadStirrer` `[n]` · `PressurePlate` `[n]` · `Pycnometer` `[n]` · `TensileClamps` `[n]` · `Triflex` `[n]`
    - `Pump` `[o]`
        - `SyringePump` `[n]` · `VacuumPump` `[n]`

### 3.3 Apparatus

- `Device` `[o]`
    - `Apparatus` `[o]`
        - `Mold` `[n]`

---

## 4 · Features, Defects, Parameters, Roles

### 4.1 Aerogel Defects

A defect class describes the lasting defect in the material (linked via `hasDefect`), not the event that caused it. The labels therefore name the state ("Crack", "Residual solvent"), with the process forms kept as `skos:altLabel`. The defect kinds are mutually disjoint.

- `Feature` `[o]`
    - `AerogelDefect` `[n]`
        - `Cracking` `[n]`: label "Crack" (alt: "Cracking")
        - `IncompleteDrying` `[n]`: label "Residual solvent" (alt: "Incomplete drying")
        - `Macroporosity` `[n]`
        - `NonuniformStructure` `[n]`
        - `Opacity` `[n]`
        - `SpringbackFailure` `[n]`
        - `StructuralCollapse` `[n]`: label "Collapsed structure" (alt: "Structural collapse")

### 4.2 Gelation Pathways and Geometry

- `Feature` `[o]`
    - `GelationPathway` `[n]`: the mechanism of a gelation, not the process itself; linked to the realising `Gelation` via `realisedAs`
        - `AcidCatalysisPathway` `[n]` · `BaseCatalysisPathway` `[n]` · `DissolutionParticipation` `[n]` · `PhaseSeparation` `[n]` · `SolGelPolymerisation` `[n]` · `TwoStepCatalysisPathway` `[n]`
    - `Geometry` `[n]`
        - `Beads` `[n]` · `DogBone` `[n]` · `Monolith` `[n]` · `Slabs` `[n]`
    - `NetworkConnectivity` `[n]`

### 4.3 Process Parameters

`ProcessParameter` is both a **BFO quality** (`BFO:0000019`) and an **`om:Quantity`**: a parameter is a quality inhering in an independent continuant (typically the reacting sol), carries its magnitude via `om:hasValue → om:Measure`, and attaches to the process it characterises via `pmat:isParameterOf`. Parameters record the *achieved, per-run* value.

- `BFO:0000019` `[e]` *(quality)* ∩ `om:Quantity` `[e]`
    - `ProcessParameter` `[n]` \*
        - `ExchangeRatio` `[n]`
        - `MolarRatio` `[n]`
            - `WaterToSilicaRatio` `[n]`
        - `PHCondition` `[n]`
        - `PressureProfile` `[n]`
        - `StirringRate` `[n]`
        - `TemperatureProfile` `[n]`: for ramps/programmes; single temperature values use `om:Temperature`
        - `VolumeRatio` `[n]`

### 4.4 Plans and Protocols

The reusable recipe is separated from the executed run: `Procedure` and its subtree are occurrents (executed processes), while the plan is a generically dependent continuant.

- `BFO:0000031` `[e]` *(generically dependent continuant)*
    - `SynthesisProtocol` `[n]`: the recipe/plan specification; linked from a concrete run via `realizesProtocol`

### 4.5 Substance Roles

The function of a substance in a step is stated with the pattern `step usesSubstance substance ; substance prov:hadRole [a Role]`. `pmat:Catalyst` and `pmat:Solvent` are reused.

- `Role` `[o]` *(⊑ BFO role)*
    - `CrosslinkerRole` `[n]` · `DryingControlAdditiveRole` `[n]` · `GellingAgentRole` `[n]` · `PrecursorRole` `[n]` · `ReinforcementRole` `[n]` · `SilylationAgentRole` `[n]` · `SupercriticalFluidRole` `[n]` · `SurfactantRole` `[n]`

### 4.6 Applications

- `BFO:0000017` `[e]` *(realizable entity)*
    - `Application` `[n]`: linked from a material via `hasApplication`
        - `AcousticInsulation` `[n]` · `Adsorption` `[n]` · `CatalystSupport` `[n]` · `DrugDelivery` `[n]` · `Electrode` `[n]` · `ThermalInsulation` `[n]`

---

## 5 · Quantitative Measures

Every quantity class declares its canonical unit via `gmat:hasCanonicalUnit` (SI units).

- `om:Quantity` `[e]`
    - `ActivationEnergy` `[n]` · `ArrheniusConstant` `[n]` · `CoefficientOfDetermination` `[n]`: Arrhenius/kinetics quantities
    - `ContactAngle` `[n]`
    - `Density` `[n]`
        - `BulkDensity` `[n]` · `SkeletalDensity` `[n]` · `TapDensity` `[n]`: mutually disjoint
    - `HeatingRate` `[n]`
    - `MassFraction` `[n]`: wt% loadings, solid content
    - `PHValue` `[n]`
    - `PoissonRatio` `[n]`
    - `PoreSizeDistribution` `[n]`
    - `PoreVolume` `[n]`: specific pore volume, canonical unit m³/kg (cm³/g convention)
    - `Porosity` `[n]`
    - `Shrinkage` `[n]`
    - `SurfaceArea` `[n]`
    - `ThermalExpansionCoefficient` `[n]`: no dedicated OM-2 class; unit `om:reciprocalKelvin`
    - `Transmittance` `[n]`
    - `VolumetricFlowRate` `[n]`
- `om:AmountOfSubstanceConcentration` `[e]`
    - `SolConcentration` `[n]`
- `om:Length` `[e]`
    - `CorrelationLength` `[n]` · `MeanPoreSize` `[n]` (≡ `pmat:MeanPoreDiameter`) · `ParticleSize` `[n]`
- `om:Time` `[e]`
    - `Duration` `[n]` · `GelationTime` `[n]`
- `om:Measure` `[e]`
    - `RatioValue` `[n]`: value node for dimensionless ratios; numerically queryable via `om:hasNumericalValue` (unit `om:one`, *a:b* = *a/b*) with display form in `hasRatioString`; multi-component ratios (e.g. `'1:10:4:4'`) string-only

### 5.1 Mechanical Properties (subclassing OM-2 mechanics quantities)

- `om:ModulusOfElasticity` `[e]`
    - `CompressiveModulus` `[n]` · `FlexuralModulus` `[n]` · `YoungsModulus` `[n]`
- `om:Stress` `[e]` (≡ `pmat:Stress`)
    - `FlexuralStrength` `[n]`
    - `om:CompressiveStress` `[e]`
        - `CompressiveStrength` `[n]`
- `pmat:UltimateTensileStrength` `[o]`: reused as the range of `gmat:hasTensileStrength`

### 5.2 Thermal Properties (subclassing OM-2 thermal quantities)

- `om:ThermalConductivity` `[e]` → `ThermalConductivity` `[n]`
- `om:ThermalDiffusivity` `[e]` → `ThermalDiffusivity` `[n]`
- `om:SpecificHeatCapacity` `[e]` → `SpecificHeatCapacity` `[n]`

### 5.3 Fractal, Scattering and Structural Descriptors

- `om:Quantity` `[e]`
    - `FractalDimension` `[n]`: general dimensionless fractal-scaling exponent
        - `MassFractalDimension` `[n]`: Dm (1-3), from the fractal region, `I(q) ∝ q⁻ᴰᵐ`
        - `SurfaceFractalDimension` `[n]`: Ds (2-3), from the Porod region, `I(q) ∝ q⁻⁽⁶⁻ᴰˢ⁾`
    - `PorodExponent` `[n]`: P, scattering power-law exponent (P = Dm or 6−Ds)
- `om:Length` `[e]`
    - `CorrelationLength` `[n]`: ξ, fractal upper cutoff / cluster size

> Linking properties (all `⊑ obo:RO_0000053`, typically domain `pmat:Substance`): `hasBulkDensity`, `hasSkeletalDensity` (⊑ `hasDensity`), `hasSurfaceArea`, `hasPoreVolume`, `hasMeanPoreSize`, `hasPoreSizeDistribution`, `hasParticleSize`, `hasPorosity`, `hasContactAngle`, `hasLinearShrinkage`, `hasTransmittance`, `hasMassFraction`, `hasPressure`, `hasHeatingRate`, `hasActivationEnergy`, `hasSolConcentration`, `hasCompressiveStrength`, `hasCompressiveModulus`, `hasYoungsModulus`, `hasTensileStrength`, `hasPoissonRatio`, `hasFlexuralStrength`, `hasFlexuralModulus`, `hasThermalConductivity`, `hasThermalDiffusivity`, `hasSpecificHeatCapacity`, `hasThermalExpansionCoefficient`, `hasFractalDimension` (with `hasMassFractalDimension`, `hasSurfaceFractalDimension`), `hasPorodExponent`, `hasCorrelationLength`.
