---
title:  "Infiltration"
layout: single
sidebar:
  nav: "in-situ_methods"
excerpt: "Water infiltration tests with a small, 5 to 10 cm, ring and measuring the sequential time it takes for the soil to swallow a constant volume of water reveal soil hydraulic properties."
permalink: /in-situ_methods/infiltration/
author_profile: false
date:   2025-11-27 06:13:03 +0200
last_modified_at:   2025-11-27 06:13:03 +0200
---

Infiltration, the capacity of soil to swallow water, is a prerequisit for soils and their ecosystems to function. Reduced infiltration capacity, due e.g. to compaction or water repellant conditions arising from drought, makes soils more prone to erosion and less resilient to droughts and storms. Low infiltrations capacity also exacerbate flash floods and downstream flooding. As part of AI4SH a fairly simple singe-ring infiltration method is used.

## Short method description

Single ring infiltration is a published scientific method for estimating soil hydraulic properties. The ring is easily constructed from a food tin can (or other tin can) and inserted a few cm into the soil. Small, fixed volumes of water (typically 50 to 100 ml) are sequentially poured into the ring and the time it takes for the water to infiltrate is recorded. The pouring of water contiuous until the time it takes for it to infiltration is stable. To calculate the hydraulic properties (table 1), data on bulk denisty and soil mositure prior to the infiltration test are needed - e.g. obtained using the [soil cylinder bulk density and volumetric soil moisture content][bulk-density] method.

Table 1. Hydarulic soil properties recorded with each single ring infiltration observation.

| Property | Indicator | AI4SH extended naming | Unit |
| :------- | :----- | :----- | :---- |
| infiltration rate | infiltration | single-ring-infiltration_final-infiltration-rate | m*day^-1 |
| porosity | porosity | single-ring-infiltration_porosity | vol*vol^-1 |
| sorptivity | sorptivity | single-ring-infiltration_sorptivity | m*day^-1/2 |
| saturated hydraulic conductivity | hydraulic conductivity | single-ring-infiltration_saturated-hydraulic-conductivity | m*day^-1 |
| field capacity | field capacity | single-ring-infiltration_field-capacity | vol*vol^-1 |
| plant avaiable water | plant available water | single-ring-infiltration_plant-available-water | vol*vol^-1 |
| saturated water content | saturated water content | single-ring-infiltration_saturated-water-content | vol*vol^-1 |
| hg water pressure head scale parameter | hg water pressure head | single-ring-infiltration_hg-water-pressure-head-scale-parameter | mm |
| n shape parameter of retention curve | retention curve n | single-ring-infiltration_n-shape-parameter-of-retention-curve | unitless |
| m shape parameter of retention curve | retention curve m | single-ring-infiltration_n-shape-parameter-of-retention-curve | unitless |


## Data format

The AI4SH observed infiltration derived data are available in 2 differently formatted json objects, a flat version more suitable for direct accessibility and a nested version intended for users who wants to convert the data to a relational sql database. The flat version does not include any arrays whereas the nested version is structured with nested arrays.

### Flat json object

Below is an example of a flat json object for infiltration derived observations. Object keys with a double underscore denote a link to other entries in the database. For example _"person__email"_ is a key for the person responsible, with more detailed contact information in a separate json document. The hashtag comments are not allowed when operating a json file, they are added here for explaining each json object.

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
    sample_preparation__name": "soil-undisturbed-in-situ", # Explanatory name of soil treatment before observation
    "person__email": "analysis@gmail.com", # Email of person responsible for the obeservation
    "subsample": "a", # For registering if physically different soil subsamples were analysed separately, default for a single analysis = a
    "replicate": 0, # If the analysis was replicated on the same subsample more than once, the first test is always set to 0
    "n_repeats": 1, # The number of repetitions done by any instrument on a single subsample and as part of a single replicate, with results reported as mean or mean and standard deviation
    "date_stamp": "20240815", # Date when the analysis was done
    "logistic": { # Assembly of logistical metadata on the handling of the sample
      "sample_preservation__name": null, # Explanatory name of soil preservation
      "sample_transport__name": null, # Explanatory name of soil transportation if sensitive for analysis results
      "transport_duration_h": 0, # duration of any sensitive transportation in hours
      "sample_storage__name": null, # Explanatory name of soil storage if sensitive for analysis results
      "storage_duration_h": 0, # Storage duration in hours
      "person__email": "logistic@gmail.com" # Email of person responsible for the logistics
    },
    "analysis": { # Assembly of analysis results, procedures and instruments
      "single-ring-infiltration_porosity": { # Soil property reported as AI4SH extended naming (part after underscore = core indicator)
        "value": 0.53,  # Recorded value (single value or mean of repeated observations)
        "unit__name": "vol*vol^-1",  # Recorded unit
        "indicator__name": "single-ring-infiltration_porosity",  # AI4SH extended name of the soil indicator (part after underscore = core indicator)
        "procedure": "single-ring-infiltration", # Procedure for the analysis (not always similar to method)
        "analysis_method__name": "single-ring-infiltration", # Name of the method
        "instrument_brand__name": "single-ring", # Instrument type or brand
        "instrument_model__name": "tin-can", # Model or version of the instrument
        "instrument_id": "0" # Any individual instrument id, the default for unknown id is "0"
      },
      "single-ring-infiltration_final-infiltration-rate": {
        "value": 10.8524,
        "unit__name": "m*day^-1",
        "indicator__name": "single-ring-infiltration_final-infiltration-rate",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_sorptivity": {
        "value": 0.291019,
        "unit__name": "m*day^-1/2",
        "indicator__name": "single-ring-infiltration_sorptivity",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_saturated-hydraulic-conductivity": {
        "value": 7.61166,
        "unit__name": "m*day^-1",
        "indicator__name": "single-ring-infiltration_saturated-hydraulic-conductivity",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_field-capacity": {
        "value": 0.206606,
        "unit__name": "vol*vol^-1",
        "indicator__name": "single-ring-infiltration_field-capacity",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_plant-available-water": {
        "value": 0.0981831,
        "unit__name": "vol*vol^-1",
        "indicator__name": "single-ring-infiltration_plant-available-water",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_saturated-water-content": {
        "value": 0.53,
        "unit__name": "vol*vol^-1",
        "indicator__name": "single-ring-infiltration_saturated-water-content",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_hg-water-pressure-head-scale-parameter": {
        "value": 0.0124932,
        "unit__name": "mm",
        "indicator__name": "single-ring-infiltration_hg-water-pressure-head-scale-parameter",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_n-shape-parameter-of-retention-curve": {
        "value": 2.16893,
        "unit__name": "unitless",
        "indicator__name": "single-ring-infiltration_n-shape-parameter-of-retention-curve",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      },
      "single-ring-infiltration_m-shape-parameter-of-retention-curve": {
        "value": 0.0778884,
        "unit__name": "unitless",
        "indicator__name": "single-ring-infiltration_m-shape-parameter-of-retention-curve",
        "procedure": "single-ring-infiltration",
        "analysis_method__name": "single-ring-infiltration",
        "instrument_brand__name": "single-ring",
        "instrument_model__name": "tin-can",
        "instrument_id": "0"
      }
    }
  }
}
```

### Nested json object

The nested json object for soil infiltration derived observations contains the same object keys and values as the flat version, but hierarcically organised with nested arrays. For explanations of the object keys please see the flat json object above.

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
                          "sample_preparation__name": "soil-undisturbed-in-situ",
                          "person__email": "analysis@gmail.com",
                          "subsample": "a",
                          "replicate": 0,
                          "n_repeats": 1,
                          "date_stamp": "20240815",
                          "logistic": {
                            "sample_preservation__name": null,
                            "sample_transport__name": null,
                            "transport_duration_h": 0,
                            "sample_storage__name": null,
                            "storage_duration_h": 0,
                            "person__email": "logistic@gmail.com"
                          },
                          "analysis_method": {
                            "single-ring-infiltration": [
                              {
                                "single-ring infiltration": [
                                  {
                                    "value": 0.53,
                                    "unit__name": "vol*vol^-1",
                                    "indicator__name": "single-ring-infiltration_porosity",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 10.8524,
                                    "unit__name": "m*day^-1",
                                    "indicator__name": "single-ring-infiltration_final-infiltration-rate",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.291019,
                                    "unit__name": "m*day^-1/2",
                                    "indicator__name": "single-ring-infiltration_sorptivity",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 7.61166,
                                    "unit__name": "m*day^-1",
                                    "indicator__name": "single-ring-infiltration_saturated-hydraulic-conductivity",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.206606,
                                    "unit__name": "vol*vol^-1",
                                    "indicator__name": "single-ring-infiltration_field-capacity",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.0981831,
                                    "unit__name": "vol*vol^-1",
                                    "indicator__name": "single-ring-infiltration_plant-available-water",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.53,
                                    "unit__name": "vol*vol^-1",
                                    "indicator__name": "single-ring-infiltration_saturated-water-content",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.0124932,
                                    "unit__name": "mm",
                                    "indicator__name": "single-ring-infiltration_hg-water-pressure-head-scale-parameter",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 2.16893,
                                    "unit__name": "unitless",
                                    "indicator__name": "single-ring-infiltration_n-shape-parameter-of-retention-curve",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.0778884,
                                    "unit__name": "unitless",
                                    "indicator__name": "single-ring-infiltration_m-shape-parameter-of-retention-curve",
                                    "procedure": "single-ring-infiltration",
                                    "analysis_method__name": "single-ring-infiltration",
                                    "instrument_brand__name": "single-ring",
                                    "instrument_model__name": "tin-can",
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

Recorded data from the infiltration derived analysis are available at:

 - Flat json format [https://github.com/AI4SH/in-situ_data/tree/main/flat/infiltration][github_infiltration_flat]
 - Nested json format: [https://github.com/AI4SH/in-situ_data/tree/main/nested/infiltration][github_infiltration_nested]

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
- no-prep
- tin-can
- 0
- 20240815

And the final file name becomes:

```
se-loennstorp-20240815_55-c_0-20_a_0_uniform_no-prep_tin-can_0_20240815.json
```

[github_infiltration_flat]: https://github.com/AI4SH/in-situ_data/tree/main/flat/infiltration

[github_infiltration_nested]: https://github.com/AI4SH/in-situ_data/tree/main/nested/infiltration

[bulk-density]: ../bulk_density/
