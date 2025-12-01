---
title:  "eDNA"
layout: single
sidebar:
  nav: "in-situ_methods"
excerpt: "environmental DNA (eDNA) analysis of soil biological properties is becoming more and more beneficial for understaning soil health. The combined decrease of analysis costs and increase of reference data rapidy advance the information that can be retrieved from soil eDNA analysis."
permalink: /in-situ_methods/edna/
author_profile: false
date:   2025-11-27 06:13:03 +0200
last_modified_at:   2025-11-27 06:13:03 +0200
---

environmental DNA (eDNA) analysis is a complex laboratory bound chain of processes called metabarcoding. Also the sampling in the field requires special equipment and the sample has to be preserved with a shielding liquid preserving the DNA during storage and transport. The raw eDNA result is a dataset of nucleotid sequences, that is then compared to database libraries (bioinformatic treatment) for determining both the organisms (or orgamism groups) and the processes that occur in the soil.

With growing DNA sequence libraries and reduced costs for the metabarcoding, progressively more and more information can be obtained from eDNA analysis. eDNA metabarcoding is thus increasingly becoming an important method for soil health characterisation.

## Short method description

The field sampling requires care to avoid DNA contamination from e.g. human DNA. Once extracted only a very samll sample (milligram) is required. The sample must be preserved to prevent any deterioration or metabolic changes in the DNA nuceoltides and that requires a DNA sheild to be added to the sample. Once the DNA shield is added, the sample can be stored and transported.

The pipeline of processes that compose eDNA metabarcoding in the laboratry include:
- extraction,
- amplification,
- purification,
- sequencing, and
- bioinformatic treatment (database library mining).

The eDNA analysed as part of AI4SH focused on three taxonomic domains:
- Bacteria,
- Archaea, and
- Eukarya.

For the Eukarya the analyses were restricted to fungi.

For each group the richness (total number of species - recorded as _alpha_ and _chao1_ indexes), diversity (recorded as alpha _Shannon_ and alpha _Simpson_ indexes) and evenness (_pielo_ index) are recorded. Group related soil functions included for example chemoheterotrophy, human pathogens, plant pathogens and nitrogen fixation. Table 1 is a complete list of eDNA derived eDNA derived organism groups and functions.

Table 1. eDNA derived organism groups and functions recorded with each observation with the applied metabarcoding pipelines.

| Property | Indicator | AI4SH extended naming | Unit |
| :------- | :----- | :----- | :---- |
| Prokaryotes alpha observed richness | Prokaryotes alpha richness | metabarcoding_Prokaryotes-alpha-observed-richness | unitless |
| Prokaryotes alpha chao1 estimated richness | Prokaryotes chao1 richness | metabarcoding_Prokaryotes-alpha-chao1-estimated-richness | unitless |
| Prokaryotes alpha dominance | Prokaryotes alpha dominance | metabarcoding_Prokaryotes-alpha-dominance | unitless |
| Prokaryotes alpha pielou e | Prokaryotes Pielou evenness | metabarcoding_Prokaryotes-alpha-pielou-e | unitless |
| Prokaryotes alpha shannon | Prokaryotes alpha Shannon diversity | metabarcoding_Prokaryotes-alpha-shannon | unitless |
| Prokaryotes alpha shannon | Prokaryotes alpha Simpson diversity | metabarcoding_Prokaryotes-alpha-simpson | unitless |
| Prokaryotes functional prediction chemoheterotrophy | Prokaryotes chemoheterotrophy | metabarcoding_Prokaryotes-functional-prediction-chemoheterotrophy | unitless |
| Prokaryotes functional prediction human pathogens all | Prokaryotes human pathogens | metabarcoding_Prokaryotes-functional-prediction-human-pathogens-all | unitless |
| Prokaryotes functional prediction nitrogen fixation | Nitrogen fixation | metabarcoding_Prokaryotes-functional-prediction-nitrogen-fixation | unitless |
| Fungi alpha observed richness | Fungi alpha richness | metabarcoding_Fungi-alpha-observed-richness | unitless |
| Fungi alpha chao1 estimated richness | Fungi chao1 richness | metabarcoding_Fungi-alpha-chao1-estimated-richness | unitless |
| Fungi alpha dominance | Fungi alpha dominance | metabarcoding_Fungi-alpha-dominance | uitless |
| Fungi alpha pielou e | Fungi Pielou evenness | metabarcoding_Fungi-alpha-pielou-e | unitless |
| Fungi alpha shannon | Fungi alpha shannon diversity | metabarcoding_Fungi-alpha-shannon | unitless |
| Fungi alpha simpson | Fungi alpha simpson diversity | metabarcoding_Fungi-alpha-simpson | unitless |
| Fungi funtional prediction Ectomycorrhizal fungi | Ectomycorrhizal fungi function | metabarcoding_Fungi-funtional-prediction-Ectomycorrhizal-fungi | unitless |
| Fungi funtional prediction Arbuscular mycorrhizal fungi | Arbuscular mycorrhizal fungi function | metabarcoding_Fungi-funtional-prediction-Arbuscular-mycorrhizal-fungi | unitless |
| Fungi funtional prediction fungal saprotrophs | Saprotrophic fungi function | metabarcoding_Fungi-funtional-prediction-fungal-saprotrophs | unitless |
| Fungi funtional prediction fungal plant pathogens | Plant pathogenic fungi function  | metabarcoding_Fungi-funtional-prediction-fungal-plant-pathogens | unitless |

## Data format

The AI4SH observed eDNA derived organism groups and functions data are available in 2 differently formatted json objects, a flat version more suitable for direct accessibility and a nested version intended for users who wants to convert the data to a relational sql database. The flat version does not include any arrays whereas the nested version is structured with nested arrays.

### Flat json object

Below is an example of a flat json object for eDNA derived organism groups and functions observations. Object keys with a double underscore denote a link to other entries in the database. For example _"person__email"_ is a key for the person responsible, with more detailed contact information in a separate json document. The hashtag comments are not allowed when operating a json file, they are added here for explaining each json object.

```
{
  "data_source": "ai4sh_se-loennstorp", # 'project'+'_'+'country'+'-'+'pilot site'
  "sampling_log": { # Assembly of samples collected in the same day at a particular pilot site  
    "name": "se-loennstorp-20240815", # 'country'+'-'+'pilot site'+'-'+'sampling date'
    "date_stamp": "20240815", # Date when the sample was collected in the field
    "person__email": "sampling@gmail.com" # Email of person responsible for the sampling
  },
  "sample": "se-loennstorp-20240815_55-c_0-20", # 'country'+'-'+'pilot site'+'-'+'sampling date'+'_'+'sample point id'+'_'+'min depth''+'-'+'max depth'
  "locus": { # Assembly of the point location, setting and depth
    "position__name": "se-loennstorp_55-c", # 'country'+'-'+'pilot site'+'-'+'sample point id' used for checking internal consistency
    "point": "55-c", # sample point id
    "setting": "uniform", # The spatial setting in the landscape (uniform, alley, plantline, edge)
    "latitude": 55.6671111111111, # Latitude in WGS84
    "longitude": 13.1156944444444, # Longitude in WGS84
    "min_depth": 0, # Sample upper limit in cm in soil profile
    "max_depth": 20 # Sample lower limit in cm in soil profile
  },
  "observation": { # Assembly of metadata and data related to the obeservation
    sample_preparation__name": "mixed-untreated-soil-in-lab", # Explanatory name of soil treatment before observation
    "person__email": "analysis@gmail.com", # Email of person responsible for the obeservation
    "subsample": "a", # For registering if physically different soil subsamples were analysed separately, default for a single analysis = a
    "replicate": 0, # If the analysis was replicated on the same subsample more than once, the first test is always set to 0
    "n_repeats": 1, # The number of repetitions done by any instrument on a single subsample and as part of a single replicate, with results reported as mean or mean and standard deviation
    "date_stamp": "20241110", # Date when the analysis was done
    "logistic": { # Assembly of logistical metadata on the handling of the sample
      "sample_preservation__name": "dna shield", # Explanatory name of soil preservation
      "sample_transport__name": "cold", # Explanatory name of soil transportation if sensitive for analysis results
      "transport_duration_h": 14, # duration of any sensitive transportation in hours
      "sample_storage__name": "cold",  # Explanatory name of soil storage if sensitive for analysis results
      "storage_duration_h": 2088, # Storage duration in hours
      "person__email": "logistic@gmail.com" # Email of person responsible for the logistics
    },
    "analysis": { # Assembly of analysis results, procedures and instruments
      "metabarcoding_Prokaryotes-alpha-observed-richness": { # Soil property reported as AI4SH extended naming (part after underscore = core indicator)
        "value": 1219.0, # Recorded value (single value or mean of repeated observations)
        "unit__name": "unitless", # Recorded unit
        "indicator__name": "metabarcoding_Prokaryotes-alpha-observed-richness", # AI4SH extended name of the soil indicator (part after underscore = core indicator)
        "procedure": "metabarcoding", # Procedure for the analysis
        "analysis_method__name": "edna-prokaryotes-alpha-observed-richness", # Name of the method
        "instrument_brand__name": "edna-prokaryotes-alpha-observed-richness", # Instrument type or brand
        "instrument_model__name": "metabarcoding-chain",  # Model or version of the instrument
        "instrument_id": "0" # Any individual instrument id, the default for unknown id is
      },
      "metabarcoding_Prokaryotes-alpha-chao1-estimated-richness": {
        "value": 1247.879,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-alpha-chao1-estimated-richness",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-alpha-chao1-estimated-richness",
        "instrument_brand__name": "edna-prokaryotes-alpha-chao1-estimated-richness",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Prokaryotes-alpha-dominance": {
        "value": 0.004,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-alpha-dominance",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-alpha-dominance",
        "instrument_brand__name": "edna-prokaryotes-alpha-dominance",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Prokaryotes-alpha-pielou-e": {
        "value": 0.887,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-alpha-pielou-e",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-alpha-pielou-e",
        "instrument_brand__name": "edna-prokaryotes-alpha-pielou-e",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Prokaryotes-alpha-shannon": {
        "value": 9.094,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-alpha-shannon",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-alpha-shannon",
        "instrument_brand__name": "edna-prokaryotes-alpha-shannon",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Prokaryotes-alpha-simpson": {
        "value": 0.996,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-alpha-simpson",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-alpha-simpson",
        "instrument_brand__name": "edna-prokaryotes-alpha-simpson",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Prokaryotes-functional-prediction-chemoheterotrophy": {
        "value": 0.110063849194,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-functional-prediction-chemoheterotrophy",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-functional-prediction-chemoheterotrophy",
        "instrument_brand__name": "edna-prokaryotes-functional-prediction-chemoheterotrophy",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Prokaryotes-functional-prediction-human-pathogens-all": {
        "value": 0.000337826424783,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-functional-prediction-human-pathogens-all",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-functional-prediction-human-pathogens-all",
        "instrument_brand__name": "edna-prokaryotes-functional-prediction-human-pathogens-all",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Prokaryotes-functional-prediction-nitrogen-fixation": {
        "value": 0.0,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Prokaryotes-functional-prediction-nitrogen-fixation",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-prokaryotes-functional-prediction-nitrogen-fixation",
        "instrument_brand__name": "edna-prokaryotes-functional-prediction-nitrogen-fixation",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-alpha-observed-richness": {
        "value": 537.0,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-alpha-observed-richness",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-alpha-observed-richness",
        "instrument_brand__name": "edna-fungi-alpha-observed-richness",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-alpha-chao1-estimated-richness": {
        "value": 543.6,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-alpha-chao1-estimated-richness",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-alpha-chao1-estimated-richness",
        "instrument_brand__name": "edna-fungi-alpha-chao1-estimated-richness",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-alpha-dominance": {
        "value": 0.044,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-alpha-dominance",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-alpha-dominance",
        "instrument_brand__name": "edna-fungi-alpha-dominance",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-alpha-pielou-e": {
        "value": 0.671,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-alpha-pielou-e",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-alpha-pielou-e",
        "instrument_brand__name": "edna-fungi-alpha-pielou-e",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-alpha-shannon": {
        "value": 6.082,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-alpha-shannon",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-alpha-shannon",
        "instrument_brand__name": "edna-fungi-alpha-shannon",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-alpha-simpson": {
        "value": 0.956,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-alpha-simpson",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-alpha-simpson",
        "instrument_brand__name": "edna-fungi-alpha-simpson",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-funtional-prediction-Ectomycorrhizal-fungi": {
        "value": 0.00284074439098,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-funtional-prediction-Ectomycorrhizal-fungi",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-funtional-prediction-ectomycorrhizal-fungi",
        "instrument_brand__name": "edna-fungi-funtional-prediction-ectomycorrhizal-fungi",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-funtional-prediction-Arbuscular-mycorrhizal-fungi": {
        "value": 0.000135273542428,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-funtional-prediction-Arbuscular-mycorrhizal-fungi",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-funtional-prediction-arbuscular-mycorrhizal-fungi",
        "instrument_brand__name": "edna-fungi-funtional-prediction-arbuscular-mycorrhizal-fungi",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-funtional-prediction-fungal-saprotrophs": {
        "value": 0.381471389645888,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-funtional-prediction-fungal-saprotrophs",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-funtional-prediction-fungal-saprotrophs",
        "instrument_brand__name": "edna-fungi-funtional-prediction-fungal-saprotrophs",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      },
      "metabarcoding_Fungi-funtional-prediction-fungal-plant-pathogens": {
        "value": 0.395404564515375,
        "unit__name": "unitless",
        "indicator__name": "metabarcoding_Fungi-funtional-prediction-fungal-plant-pathogens",
        "procedure": "metabarcoding",
        "analysis_method__name": "edna-fungi-funtional-prediction-fungal-plant-pathogens",
        "instrument_brand__name": "edna-fungi-funtional-prediction-fungal-plant-pathogens",
        "instrument_model__name": "metabarcoding-chain",
        "instrument_id": "0"
      }
    }
  }
}
```

### Nested json object

The nested json object for the eDNA derived organism groups and functions observations contains the same object keys and values as the flat version, but hierarcically organised with nested arrays. For explanations of the object keys please see the flat json object above.

```
{
  "data_source": [
    {
      "name": "ai4sh_se-loennstorp",
      "site": [
        {
          "name": "se-loennstorp",
          "point": [
            {
              "name": "55-c",
              "latitude": 55.6671111111111,
              "longitude": 13.1156944444444,
              "setting": "uniform",
              "sampling_log": [
                {
                  "name": "se-loennstorp-20240815",
                  "date_stamp": "20240815",
                  "person__email": "sampling@gmail.com",
                  "sample": [
                    {
                      "name": "se-loennstorp-20240815_55-c_0-20",
                      "min_depth": 0,
                      "max_depth": 20,
                      "observation": [
                        {
                          "sample_preparation__name": "mixed-untreated-soil-in-lab",
                          "person__email": "analysis@gmail.com",
                          "subsample": "a",
                          "replicate": 0,
                          "n_repeats": 1,
                          "date_stamp": "20241110",
                          "logistic": {
                            "sample_preservation__name": "dna shield",
                            "sample_transport__name": "cold",
                            "transport_duration_h": 14,
                            "sample_storage__name": "cold",
                            "storage_duration_h": 2088,
                            "person__email": "logistic@gmail.com"
                          },
                          "analysis_method": {
                            "metabarcoding": [
                              {
                                "edna": [
                                  {
                                    "value": 1219.0,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-alpha-observed-richness",
                                    "analysis_method__name": "edna-prokaryotes-alpha-observed-richness",
                                    "instrument_brand__name": "edna-prokaryotes-alpha-observed-richness",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 1247.879,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-alpha-chao1-estimated-richness",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-alpha-chao1-estimated-richness",
                                    "instrument_brand__name": "edna-prokaryotes-alpha-chao1-estimated-richness",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.004,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-alpha-dominance",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-alpha-dominance",
                                    "instrument_brand__name": "edna-prokaryotes-alpha-dominance",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.887,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-alpha-pielou-e",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-alpha-pielou-e",
                                    "instrument_brand__name": "edna-prokaryotes-alpha-pielou-e",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 9.094,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-alpha-shannon",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-alpha-shannon",
                                    "instrument_brand__name": "edna-prokaryotes-alpha-shannon",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.996,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-alpha-simpson",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-alpha-simpson",
                                    "instrument_brand__name": "edna-prokaryotes-alpha-simpson",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.110063849194,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-functional-prediction-chemoheterotrophy",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-functional-prediction-chemoheterotrophy",
                                    "instrument_brand__name": "edna-prokaryotes-functional-prediction-chemoheterotrophy",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.000337826424783,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-functional-prediction-human-pathogens-all",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-functional-prediction-human-pathogens-all",
                                    "instrument_brand__name": "edna-prokaryotes-functional-prediction-human-pathogens-all",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.0,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Prokaryotes-functional-prediction-nitrogen-fixation",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-prokaryotes-functional-prediction-nitrogen-fixation",
                                    "instrument_brand__name": "edna-prokaryotes-functional-prediction-nitrogen-fixation",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 537.0,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-alpha-observed-richness",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-alpha-observed-richness",
                                    "instrument_brand__name": "edna-fungi-alpha-observed-richness",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 543.6,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-alpha-chao1-estimated-richness",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-alpha-chao1-estimated-richness",
                                    "instrument_brand__name": "edna-fungi-alpha-chao1-estimated-richness",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.044,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-alpha-dominance",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-alpha-dominance",
                                    "instrument_brand__name": "edna-fungi-alpha-dominance",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.671,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-alpha-pielou-e",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-alpha-pielou-e",
                                    "instrument_brand__name": "edna-fungi-alpha-pielou-e",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 6.082,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-alpha-shannon",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-alpha-shannon",
                                    "instrument_brand__name": "edna-fungi-alpha-shannon",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.956,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-alpha-simpson",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-alpha-simpson",
                                    "instrument_brand__name": "edna-fungi-alpha-simpson",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.00284074439098,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-funtional-prediction-Ectomycorrhizal-fungi",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-funtional-prediction-ectomycorrhizal-fungi",
                                    "instrument_brand__name": "edna-fungi-funtional-prediction-ectomycorrhizal-fungi",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.000135273542428,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-funtional-prediction-Arbuscular-mycorrhizal-fungi",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-funtional-prediction-arbuscular-mycorrhizal-fungi",
                                    "instrument_brand__name": "edna-fungi-funtional-prediction-arbuscular-mycorrhizal-fungi",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.381471389645888,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-funtional-prediction-fungal-saprotrophs",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-funtional-prediction-fungal-saprotrophs",
                                    "instrument_brand__name": "edna-fungi-funtional-prediction-fungal-saprotrophs",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.395404564515375,
                                    "unit__name": "unitless",
                                    "indicator__name": "metabarcoding_Fungi-funtional-prediction-fungal-plant-pathogens",
                                    "procedure": "metabarcoding",
                                    "analysis_method__name": "edna-fungi-funtional-prediction-fungal-plant-pathogens",
                                    "instrument_brand__name": "edna-fungi-funtional-prediction-fungal-plant-pathogens",
                                    "instrument_model__name": "metabarcoding-chain",
                                    "instrument_id": "0"
                                  }
                                ]
                              }
                            ]
                          }
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

## Data access and file naming

Recorded data from the eDNA metabarcoding analysis are available at:

 - Flat json format [https://github.com/AI4SH/in-situ_data/tree/main/flat/edna][github_edna_flat]
 - Nested json format: [https://github.com/AI4SH/in-situ_data/tree/main/nested/edna][github_edna_nested]

The file naming is defined to separate alll eventual renewed sampling or analysis efforts and is built up from the following metadata:
- country
- pilot site
- sampling date
- point id
- min depth
- max depth
- subsample
- replicate
- setting
- sample_preservation
- procedure
- instrument
- analysis date

For the examples above, the file name thus have the following component values:

- se
- loennstorp
- 20240815
- 55-c
- 0
- 20
- a
- 0
- uniform
- mix-wet
- metabarcoding-chain
- 0
- 20241110

And the final file name becomes:

```
se-loennstorp-20240815_55-c_0-20_a_0_uniform_mix-wet_metabarcoding-chain_0_20241110.json
```

[github_edna_flat]: https://github.com/AI4SH/in-situ_data/tree/main/flat/edna

[github_edna_nested]: https://github.com/AI4SH/in-situ_data/tree/main/nested/edna
