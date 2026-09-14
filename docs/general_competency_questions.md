# MTMS Aerogel Data Queries

Competency questions for the MTMS organosilica aerogel data in `aerogel_data.ttl`. The dataset covers samples A to H, prepared with different MTMS/MeOH ratios; samples E to H include kinetic studies.

The diagrams use the following color coding:

🔵 Processes (light blue)
🟡 Chemicals/Substances (yellow)
🟢 Results/Values (green)
🟠 Equipment (orange)
🔴 Temperature/Energy parameters (red/orange)
🟣 Ratios (purple)

## Prefixes for MTMS Queries

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX prov: <http://www.w3.org/ns/prov#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>
PREFIX : <https://w3id.org/gelmat/data/>
```

---

## MQ1: How many aerogel syntheses are in the database?

**Natural Language Question**: What is the total count of aerogel synthesis processes recorded in the database?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT (COUNT(?synthesis) AS ?totalSyntheses)
WHERE {
  ?synthesis rdf:type gmat:AerogelSynthesis .
}
```

**Expected Results**: 8 (Samples A through H)

**Mermaid Diagram**:
```mermaid
graph LR
    A[AerogelSynthesis] -->|count| B[Total: 8]
    style A fill:#e1f5ff
    style B fill:#c8e6c9
```

---

## MQ2: What are all the aerogel samples and their precursors?

**Natural Language Question**: List all aerogel samples (organosilica, from MTMS) in the database along with their silicon precursor.

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT ?aerogel ?aerogelLabel ?precursor ?precursorLabel
WHERE {
  ?aerogel rdf:type/rdfs:subClassOf* gmat:Aerogel ;
           rdfs:label ?aerogelLabel ;
           gmat:hasPrecursor ?precursor .
  ?precursor rdfs:label ?precursorLabel .
}
ORDER BY ?aerogelLabel
```

**Expected Results**: 8 aerogels (A-H), all using MTMS (Trimethoxymethylsilane) as precursor

**Mermaid Diagram**:
```mermaid
graph TD
    A[SilicaAerogel A] -->|hasPrecursor| P[MTMS]
    B[SilicaAerogel B] -->|hasPrecursor| P
    C[SilicaAerogel C] -->|hasPrecursor| P
    D[SilicaAerogel D] -->|hasPrecursor| P
    E[SilicaAerogel E] -->|hasPrecursor| P
    F[SilicaAerogel F] -->|hasPrecursor| P
    G[SilicaAerogel G] -->|hasPrecursor| P
    H[SilicaAerogel H] -->|hasPrecursor| P
    P[MTMS<br/>Trimethoxymethylsilane]
    style P fill:#ffeb3b
    style A fill:#e1f5ff
    style B fill:#e1f5ff
    style C fill:#e1f5ff
    style D fill:#e1f5ff
    style E fill:#e1f5ff
    style F fill:#e1f5ff
    style G fill:#e1f5ff
    style H fill:#e1f5ff
```

---

## MQ3: What are the complete process steps for a specific synthesis?

**Natural Language Question**: What process steps are part of MTMS Synthesis Sample A?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX : <https://w3id.org/gelmat/data/>

SELECT ?process ?processLabel ?processType
WHERE {
  :MTMS_Synthesis_Sample_A obo:BFO_0000051 ?process .
  ?process rdfs:label ?processLabel ;
           rdf:type ?processType .
  FILTER(?processType != owl:NamedIndividual)
}
ORDER BY ?processLabel
```

**Expected Results**: Sol Formation, Gelation, Aging, Solvent Exchange, Drying

**Mermaid Diagram**:
```mermaid
graph LR
    S[MTMS Synthesis<br/>Sample A] --> SF[Sol Formation]
    S --> G[Gelation]
    S --> A[Aging]
    S --> SE[Solvent Exchange]
    S --> D[Drying]
    style S fill:#ffeb3b
    style SF fill:#e1f5ff
    style G fill:#e1f5ff
    style A fill:#e1f5ff
    style SE fill:#e1f5ff
    style D fill:#e1f5ff
```

---

## MQ4: What is the aging time (duration) for each sample?

**Natural Language Question**: What is the aging duration used for each MTMS aerogel sample?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?duration ?durationLabel ?agingProcess ?value ?unit
WHERE {
  ?duration rdf:type gmat:Duration ;
            rdfs:label ?durationLabel ;
            obo:RO_0000052 ?agingProcess ;
            om:hasValue ?measure .
  ?agingProcess rdf:type gmat:Aging .
  ?measure om:hasNumericalValue ?value ;
           om:hasUnit ?unitIRI .
  OPTIONAL { ?unitIRI rdfs:label ?unit }  # label resolves when OM-2 is loaded
}
ORDER BY ?durationLabel
```

**Expected Results**: 172800 s (= 48 h) for all samples (A-D); values in SI seconds

**Mermaid Diagram**:
```mermaid
graph TD
    D[Duration] -->|hasValue| M["172800 s (48 h)"]
    D -->|RO_0000052| A[Aging Process]
    A --> SA[Sample A]
    A --> SB[Sample B]
    A --> SC[Sample C]
    A --> SD[Sample D]
    style D fill:#ffeb3b
    style M fill:#c8e6c9
    style A fill:#e1f5ff
```

---

## MQ5: What is the aging temperature for each sample?

**Natural Language Question**: At what temperature is the aging process performed for each sample?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT ?tempLabel ?agingProcess ?value ?unit
WHERE {
  ?temp rdf:type om:Temperature ;
        rdfs:label ?tempLabel ;
        obo:RO_0000052 ?agingProcess ;
        om:hasValue ?measure .
  ?agingProcess rdf:type gmat:Aging .
  ?measure om:hasNumericalValue ?value ;
           om:hasUnit ?unitIRI .
  OPTIONAL { ?unitIRI rdfs:label ?unit }  # label resolves when OM-2 is loaded
}
ORDER BY ?tempLabel
```

**Expected Results**: 323.15 K (= 50 °C) for all samples with aging temperature data; values in SI kelvin

**Mermaid Diagram**:
```mermaid
graph TD
    T[Temperature] -->|hasValue| V["323.15 K (50 °C)"]
    T -->|RO_0000052| A[Aging Process]
    A --> SA[Sample A/B/C/D]
    style T fill:#ff9800
    style V fill:#c8e6c9
    style A fill:#e1f5ff
```

---

## MQ6: What is the drying temperature used in the synthesis?

**Natural Language Question**: What temperature is used during the drying process for each sample?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>
PREFIX pmat: <https://w3id.org/polymat/>

SELECT ?tempLabel ?dryingProcess ?value ?unit
WHERE {
  ?temp rdf:type om:Temperature ;
        rdfs:label ?tempLabel ;
        obo:RO_0000052 ?dryingProcess ;
        om:hasValue ?measure .
  ?dryingProcess rdf:type pmat:Drying .
  ?measure om:hasNumericalValue ?value ;
           om:hasUnit ?unitIRI .
  OPTIONAL { ?unitIRI rdfs:label ?unit }  # label resolves when OM-2 is loaded
}
ORDER BY ?tempLabel
```

**Expected Results**: 373.15 K (= 100 °C) for all samples with drying temperature data; values in SI kelvin

**Mermaid Diagram**:
```mermaid
graph TD
    T[Temperature] -->|hasValue| V["373.15 K (100 °C)"]
    T -->|RO_0000052| D[Drying Process]
    D --> SA[Sample A/B/C/D]
    style T fill:#ff5722
    style V fill:#c8e6c9
    style D fill:#e1f5ff
```

---

## MQ7: What are the MTMS to Methanol volume ratios for each sample?

**Natural Language Question**: What are the different MTMS/MeOH volume ratios used across all samples?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?ratioLabel ?ratioValue
WHERE {
  ?ratio rdf:type gmat:VolumeRatio ;
         rdfs:label ?ratioLabel ;
         om:hasValue ?valueIRI .
  ?valueIRI gmat:hasRatioString ?ratioValue .
  FILTER(CONTAINS(?ratioLabel, "MTMS to Methanol"))
}
ORDER BY ?ratioLabel
```

**Expected Results**: 1:10 (A), 1:15 (B), 1:20 (C), 1:25 (D)

**Mermaid Diagram**:
```mermaid
graph LR
    VR[VolumeRatio] --> A["1:10 (A)"]
    VR --> B["1:15 (B)"]
    VR --> C["1:20 (C)"]
    VR --> D["1:25 (D)"]
    VR -.-> M[MTMS]
    VR -.-> ME[Methanol]
    style VR fill:#9c27b0
    style M fill:#ffeb3b
    style ME fill:#ffeb3b
```

---

## MQ8: What is the H₂O to MTMS molar ratio (r value) for each sample?

**Natural Language Question**: What are the water to MTMS molar ratios used in the different synthesis experiments?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?ratioLabel ?ratioValue ?sol
WHERE {
  # The molar ratio is a quality inhering in the sol (the reacting mixture)
  ?ratio rdf:type gmat:MolarRatio ;
         rdfs:label ?ratioLabel ;
         om:hasValue ?valueIRI ;
         <http://purl.obolibrary.org/obo/RO_0000052> ?sol .
  ?valueIRI gmat:hasRatioString ?ratioValue .
}
ORDER BY ?ratioLabel
```

**Expected Results**: Various r values: 8.09 (E), 9.71 (F), 11.33 (G), 12.94 (H), 59.75 (A-D)

**Mermaid Diagram**:
```mermaid
graph TD
    MR[MolarRatio H₂O/MTMS] --> E[8.09 - Sample E]
    MR --> F[9.71 - Sample F]
    MR --> G[11.33 - Sample G]
    MR --> H[12.94 - Sample H]
    MR --> AD[59.75 - Samples A-D]
    MR -.-> W[H₂O]
    MR -.-> M[MTMS]
    style MR fill:#3f51b5
    style W fill:#2196f3
    style M fill:#ffeb3b
```

---

## MQ9: What equipment is used in the sol formation process?

**Natural Language Question**: What laboratory equipment is required for the sol formation step?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT DISTINCT ?equipment ?equipmentLabel ?equipmentType
WHERE {
  ?solFormation rdf:type gmat:SolFormation ;
                gmat:requiresEquipment ?equipment .
  ?equipment rdfs:label ?equipmentLabel ;
             rdf:type ?equipmentType .
  FILTER(?equipmentType != owl:NamedIndividual)
}
```

**Expected Results**: Syringe Pump (1.667e-8 m³/s = 60 mL/h)

**Mermaid Diagram**:
```mermaid
graph LR
    SF[Sol Formation] -->|requiresEquipment| SP[Syringe Pump]
    SP -->|flow rate| FR["1.667e-8 m³/s (60 mL/h)"]
    style SF fill:#e1f5ff
    style SP fill:#ff9800
    style FR fill:#c8e6c9
```

---

## MQ10: What substances are used in the sol formation process?

**Natural Language Question**: What chemical substances are combined during sol formation?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT DISTINCT ?substance ?substanceLabel ?substanceType
WHERE {
  ?solFormation rdf:type gmat:SolFormation ;
                gmat:usesSubstance ?substance .
  ?substance rdfs:label ?substanceLabel ;
             rdf:type ?substanceType .
  FILTER(?substanceType != owl:NamedIndividual)
}
ORDER BY ?substanceLabel
```

**Expected Results**: MTMS, Methanol, Oxalic Acid, Water

**Mermaid Diagram**:
```mermaid
graph TD
    SF[Sol Formation] --> M[MTMS]
    SF --> ME[Methanol]
    SF --> OA[Oxalic Acid]
    SF --> W[Water]
    style SF fill:#e1f5ff
    style M fill:#ffeb3b
    style ME fill:#ffeb3b
    style OA fill:#ffeb3b
    style W fill:#2196f3
```

---

## MQ11: What intermediate products are generated during synthesis?

**Natural Language Question**: What are all the intermediate gel products formed throughout the synthesis process?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT ?intermediate ?label ?type ?generatingProcess
WHERE {
  ?process gmat:generatesIntermediate ?intermediate .
  ?intermediate rdfs:label ?label ;
                rdf:type ?type .
  ?process rdfs:label ?generatingProcess .
  FILTER(?type != owl:NamedIndividual)
}
ORDER BY ?label
```

**Expected Results**: Sols, Wet Gels, Hydrogels, Alcogels for each sample

**Mermaid Diagram**:
```mermaid
graph LR
    P1[Sol Formation] -->|generates| S[Sol]
    P2[Gelation] -->|generates| WG[Wet Gel]
    P3[Aging] -->|generates| HG[Hydrogel]
    P4[Solvent Exchange] -->|generates| AG[Alcogel]
    P5[Drying] -->|produces| AE[Aerogel]
    S --> WG
    WG --> HG
    HG --> AG
    AG --> AE
    style S fill:#fff9c4
    style WG fill:#f0f4c3
    style HG fill:#dcedc8
    style AG fill:#c5e1a5
    style AE fill:#aed581
```

---

## MQ12: What is the flow rate of the syringe pump?

**Natural Language Question**: What volumetric flow rate is configured for the syringe pump equipment?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?flowRate ?value ?unit
WHERE {
  ?flowRate rdf:type gmat:VolumetricFlowRate ;
            obo:RO_0000052 ?equipment ;
            om:hasValue ?measure .
  ?equipment rdf:type gmat:SyringePump .
  ?measure om:hasNumericalValue ?value ;
           om:hasUnit ?unitIRI .
  OPTIONAL { ?unitIRI rdfs:label ?unit }  # label resolves when OM-2 is loaded
}
```

**Expected Results**: 1.667e-8 m³/s (= 60 mL/h); value in SI

**Mermaid Diagram**:
```mermaid
graph LR
    VFR[VolumetricFlowRate] -->|hasValue| V["1.667e-8 m³/s (60 mL/h)"]
    VFR -->|RO_0000052| SP[Syringe Pump]
    SP -->|used in| SF[Sol Formation]
    style VFR fill:#9c27b0
    style V fill:#c8e6c9
    style SP fill:#ff9800
    style SF fill:#e1f5ff
```

---

## MQ13: What is the complete reagent volume ratio for sol formation?

**Natural Language Question**: What is the overall volume ratio of all reagents (MTMS:MeOH:NH₄OH:C₂H₂O₄) used in sol formation?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?ratioLabel ?ratioValue ?comment
WHERE {
  ?ratio rdf:type gmat:VolumeRatio ;
         rdfs:label ?ratioLabel ;
         om:hasValue ?valueIRI .
  ?valueIRI gmat:hasRatioString ?ratioValue .
  OPTIONAL { ?ratio rdfs:comment ?comment }
  FILTER(CONTAINS(?ratioLabel, "Sol Formation Overall"))
}
ORDER BY ?ratioLabel
```

**Expected Results**: 1:10:4:4 (A), 1:15:4:4 (B), 1:20:4:4 (C), 1:25:4:4 (D)

**Mermaid Diagram**:
```mermaid
graph TD
    SF[Sol Formation] --> R[Overall Ratio]
    R --> A["1:10:4:4 (A)"]
    R --> B["1:15:4:4 (B)"]
    R --> C["1:20:4:4 (C)"]
    R --> D["1:25:4:4 (D)"]
    R -.-> M[MTMS]
    R -.-> ME[MeOH]
    R -.-> NH[NH₄OH]
    R -.-> OX[C₂H₂O₄]
    style SF fill:#e1f5ff
    style R fill:#9c27b0
    style M fill:#ffeb3b
    style ME fill:#ffeb3b
    style NH fill:#ffeb3b
    style OX fill:#ffeb3b
```

---

## MQ14: Which samples have kinetic study data (activation energy)?

**Natural Language Question**: Which samples have activation energy measurements from kinetic studies?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>
PREFIX : <https://w3id.org/gelmat/data/>

SELECT ?activationEnergy ?label ?gelationProcess ?value ?unit
WHERE {
  ?activationEnergy rdfs:label ?label ;
                    obo:RO_0000052 ?gelationProcess ;
                    om:hasValue ?measure .
  ?measure om:hasNumericalValue ?value ;
           om:hasUnit ?unitIRI .
  OPTIONAL { ?unitIRI rdfs:label ?unit }  # label resolves when OM-2 is loaded
  FILTER(CONTAINS(?label, "Activation Energy"))
}
ORDER BY ?label
```

**Expected Results**: Samples E (35450 J/mol), F (29900 J/mol), G (33290 J/mol), H (28890 J/mol); SI J/mol (= 35.45, 29.90, 33.29, 28.89 kJ/mol)

**Mermaid Diagram**:
```mermaid
graph TD
    AE[Activation Energy] --> E["Sample E: 35450 J/mol"]
    AE --> F["Sample F: 29900 J/mol"]
    AE --> G["Sample G: 33290 J/mol"]
    AE --> H["Sample H: 28890 J/mol"]
    AE -->|RO_0000052| GEL[Gelation Process]
    style AE fill:#f44336
    style GEL fill:#e1f5ff
    style E fill:#ffcdd2
    style F fill:#ffcdd2
    style G fill:#ffcdd2
    style H fill:#ffcdd2
```

---

## MQ15: What are the Arrhenius constants for the gelation kinetics?

**Natural Language Question**: What are the Arrhenius pre-exponential constants for each sample's gelation kinetics?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?arrheniusLabel ?gelation ?value
WHERE {
  ?arrhenius rdfs:label ?arrheniusLabel ;
             obo:RO_0000052 ?gelation ;
             om:hasValue ?measure .
  ?measure om:hasNumericalValue ?value .
  FILTER(CONTAINS(?arrheniusLabel, "Arrhenius"))
}
ORDER BY ?arrheniusLabel
```

**Expected Results**: E (244.86), F (51.15), G (272.73), H (72.39)

**Mermaid Diagram**:
```mermaid
graph TD
    AC[Arrhenius Constant] --> E["Sample E: 244.86"]
    AC --> F["Sample F: 51.15"]
    AC --> G["Sample G: 272.73"]
    AC --> H["Sample H: 72.39"]
    AC -->|RO_0000052| GEL[Gelation Process]
    style AC fill:#673ab7
    style GEL fill:#e1f5ff
    style E fill:#d1c4e9
    style F fill:#d1c4e9
    style G fill:#d1c4e9
    style H fill:#d1c4e9
```

---

## MQ16: Which experiment contains which synthesis samples?

**Natural Language Question**: What synthesis samples are part of each experiment in the database?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX pmat: <https://w3id.org/polymat/>

SELECT ?experiment ?expLabel ?synthesis ?synthLabel
WHERE {
  ?experiment rdf:type pmat:Experiment ;
              rdfs:label ?expLabel ;
              obo:BFO_0000051 ?synthesis .
  ?synthesis rdfs:label ?synthLabel .
}
ORDER BY ?expLabel ?synthLabel
```

**Expected Results**: Experiment_01 contains Samples A, B, C, D

**Mermaid Diagram**:
```mermaid
graph TD
    EXP[Experiment_01] --> SA[MTMS Synthesis A]
    EXP --> SB[MTMS Synthesis B]
    EXP --> SC[MTMS Synthesis C]
    EXP --> SD[MTMS Synthesis D]
    style EXP fill:#4caf50
    style SA fill:#e1f5ff
    style SB fill:#e1f5ff
    style SC fill:#e1f5ff
    style SD fill:#e1f5ff
```

---

## MQ17: What aerogels are generated by each experiment?

**Natural Language Question**: Which aerogel products are generated by each experiment?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX prov: <http://www.w3.org/ns/prov#>
PREFIX pmat: <https://w3id.org/polymat/>

SELECT ?experiment ?expLabel ?aerogel ?aerogelLabel
WHERE {
  ?experiment rdf:type pmat:Experiment ;
              rdfs:label ?expLabel ;
              prov:generated ?aerogel .
  ?aerogel rdfs:label ?aerogelLabel .
}
ORDER BY ?expLabel ?aerogelLabel
```

**Expected Results**: Experiment_01 generates Aerogels A, B, C, D

**Mermaid Diagram**:
```mermaid
graph TD
    EXP[Experiment_01] -->|generated| AA[MTMS Aerogel A]
    EXP -->|generated| AB[MTMS Aerogel B]
    EXP -->|generated| AC[MTMS Aerogel C]
    EXP -->|generated| AD[MTMS Aerogel D]
    style EXP fill:#4caf50
    style AA fill:#aed581
    style AB fill:#aed581
    style AC fill:#aed581
    style AD fill:#aed581
```

---

## MQ18: What is the transformation chain from alcogel to aerogel?

**Natural Language Question**: Which drying processes transform alcogels into aerogels?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX pmat: <https://w3id.org/polymat/>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT ?drying ?dryingLabel ?alcogel ?alcogelLabel ?aerogel ?aerogelLabel
WHERE {
  ?drying rdf:type pmat:Drying ;
          rdfs:label ?dryingLabel ;
          gmat:usesSubstance ?alcogel ;
          gmat:producesAerogel ?aerogel .
  ?alcogel rdfs:label ?alcogelLabel .
  ?aerogel rdfs:label ?aerogelLabel .
}
ORDER BY ?dryingLabel
```

**Expected Results**: Each sample's drying process with corresponding alcogel input and aerogel output

**Mermaid Diagram**:
```mermaid
graph LR
    AG[Alcogel] -->|usesSubstance| DRY[Drying Process]
    DRY -->|producesAerogel| AER[Aerogel]
    DRY -->|requiresEquipment| DRYER[Dryer]
    DRY -->|hasTemperature| TEMP["373.15 K (100 °C)"]
    style AG fill:#c5e1a5
    style DRY fill:#e1f5ff
    style AER fill:#aed581
    style DRYER fill:#ff9800
    style TEMP fill:#ff5722
```

---

## MQ19: What gelation time equations are available in the database?

**Natural Language Question**: What gelation time approximation equations are documented in the data?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>

SELECT ?gelation ?gelationLabel ?comment
WHERE {
  ?gelation rdf:type gmat:Gelation ;
            rdfs:label ?gelationLabel ;
            rdfs:comment ?comment .
  FILTER(CONTAINS(?comment, "Gelation time"))
}
ORDER BY ?gelationLabel
```

**Expected Results**: Gelation time equations for samples E, F, G, H (e.g., tg = 17211e^-0.041Tg for Sample E)

**Mermaid Diagram**:
```mermaid
graph TD
    GEL[Gelation Process] -->|has equation| EQ[Gelation Time Formula]
    EQ --> E["E: tg = 17211e^-0.041Tg<br/>R² = 0.95"]
    EQ --> F["F: tg = 7611.1e^-0.034Tg<br/>R² = 0.94"]
    EQ --> G["G: tg = 6149.5e^-0.038Tg<br/>R² = 0.98"]
    EQ --> H["H: tg = 3453.2e^-0.0330Tg<br/>R² = 0.94"]
    style GEL fill:#e1f5ff
    style EQ fill:#9c27b0
    style E fill:#e1bee7
    style F fill:#e1bee7
    style G fill:#e1bee7
    style H fill:#e1bee7
```

---

## MQ20: Compare all samples by their H₂O/MTMS molar ratio and activation energy

**Natural Language Question**: What is the relationship between H₂O/MTMS molar ratio and activation energy across samples?

**SPARQL Query**:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX gmat: <https://w3id.org/gelmat/>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?sample ?molarRatioValue ?activationEnergyValue
WHERE {
  # Get molar ratio: a quality inhering in the sol (the reacting mixture)
  ?molarRatio rdf:type gmat:MolarRatio ;
              obo:RO_0000052 ?sol ;
              om:hasValue ?mrValue .
  ?mrValue gmat:hasRatioString ?molarRatioValue .

  # The sol formation step that produced this sol
  ?solFormation gmat:generatesIntermediate ?sol .

  # Get synthesis containing this sol formation
  ?synthesis obo:BFO_0000051 ?solFormation ;
             obo:BFO_0000051 ?gelation ;
             rdfs:label ?sample .
  ?gelation rdf:type gmat:Gelation .
  
  # Get activation energy for gelation
  ?actEnergy obo:RO_0000052 ?gelation ;
             om:hasValue ?aeValue .
  ?aeValue om:hasNumericalValue ?activationEnergyValue ;
           om:hasUnit om:joulePerMole .   # SI: values in J/mol
}
ORDER BY ?molarRatioValue
```

**Expected Results**: Correlation between r values (8.09-12.94) and Ea (28890-35450 J/mol) for kinetic study samples

**Mermaid Diagram**:
```mermaid
graph TD
    COMP[Comparison Analysis] --> MR[Molar Ratio r]
    COMP --> AE[Activation Energy Ea]
    MR --> E["E: r=8.09"]
    MR --> F["F: r=9.71"]
    MR --> G["G: r=11.33"]
    MR --> H["H: r=12.94"]
    AE --> E2["E: 35450 J/mol"]
    AE --> F2["F: 29900 J/mol"]
    AE --> G2["G: 33290 J/mol"]
    AE --> H2["H: 28890 J/mol"]
    E -.correlation.- E2
    F -.correlation.- F2
    G -.correlation.- G2
    H -.correlation.- H2
    style COMP fill:#00bcd4
    style MR fill:#3f51b5
    style AE fill:#f44336
```

---

## Summary of Queries

| Query ID | Topic | Key Data Explored |
|----------|-------|-------------------|
| MQ1 | Synthesis Count | Total number of aerogel syntheses |
| MQ2 | Aerogels & Precursors | All aerogel samples with MTMS precursor |
| MQ3 | Process Steps | Complete synthesis workflow |
| MQ4 | Aging Duration | 48-hour aging time |
| MQ5 | Aging Temperature | 323.15 K (50 °C) aging temperature |
| MQ6 | Drying Temperature | 373.15 K (100 °C) drying temperature |
| MQ7 | MTMS/MeOH Ratios | Volume ratios 1:10 to 1:25 |
| MQ8 | H₂O/MTMS Ratios | Molar ratios (r values) |
| MQ9 | Equipment | Syringe pump usage |
| MQ10 | Substances | Chemical reagents |
| MQ11 | Intermediates | Sol, Wet Gel, Hydrogel, Alcogel |
| MQ12 | Flow Rate | 1.667e-8 m³/s (60 mL/h) pump setting |
| MQ13 | Overall Ratios | Complete reagent ratios |
| MQ14 | Activation Energy | Kinetic study data |
| MQ15 | Arrhenius Constants | Pre-exponential factors |
| MQ16 | Experiment Structure | Experiment-synthesis relationships |
| MQ17 | Generated Products | Experiment outputs |
| MQ18 | Drying Transformation | Alcogel to aerogel conversion |
| MQ19 | Gelation Equations | Time-temperature correlations |
| MQ20 | Ratio-Energy Comparison | Cross-parameter analysis |

The questions cover the chemical inputs and their ratios, the sequence of synthesis steps, the intermediate products from sol to aerogel, the process parameters and equipment settings, and the gelation kinetics of samples E to H. All queries run as shown against `gelmat.ttl` and `aerogel_data.ttl`.
