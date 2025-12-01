---
title:  "Microbiometer"
layout: single
sidebar:
  nav: "in-situ_methods"
excerpt: "Microbiometer commercial kit for quick estimation soil carbon content and the ratio between bacteria and fungi."
permalink: /in-situ_methods/microbiometer/
author_profile: false
date:   2025-11-27 06:13:03 +0200
last_modified_at:   2025-11-27 06:13:03 +0200
---

[Microbiometer][microbiometer] is a commercial kit for quick estimation of soil microbial carbon biomass and the ratio between bacteria and fungi.  

## Short method description

The commercial Microbiometer test mixes a small (1 ml) soil sample with a reagent solution whereafter the mixture is rested for 20 minutes while the reaction is completed and the solution settles. Three drops of the supernatant are extracetd using a provided pipette and applied to a likewise provided test card. The test card is then scanned with a smartphone using the Microbiometer app. If the color change of the drop area on the test card is too weak, additional three drops are added and the test card re-scanned. From the color intensity of the drop area, the app reports the soil's microbial biomass carbon content and fungal-to-bacterial ratio. The test takes approximately 30 minutes in total. The app and the test card were updated during 2025 and thus the AI4SH reported results relate to both the _classic_ and _pro_ versions of the Microbiometer.

## Data format

The AI4SH observed microbiometer data are available in 2 differently formatted json objects, a flat version more suitable for direct accessibility and a nested version intended for users who wants to convert the data to a relational sql database. The flat version does not include any arrays whereas the nested version is structured with nested arrays.

### Flat json object

Below is an example of a flat json object for Microbiometer observations. Object keys with a double underscore denote a link to other entries in the database. For example _"person__email"_ is a key for the person responsible, with more detailed contact information in a separate json document. The hashtag comments are not allowed when operating a json file, they are added here for explaining each json object.

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
    "sample_preparation__name": "mixed-untreated-soil-in-lab", # Explanatory name of soil treatment before observation
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
      "microbiometer_Microbial-C": { # Soil property reported as AI4SH extended naming (part after underscore = core indicator)
        "value": 385.0, # Recorded value (single value or mean of repeated observations)
        "unit__name": "ug*g^-1", # Recorded unit
        "indicator__name": "microbiometer_Microbial-C", # AI4SH extended name of the soil indicator (part after underscore = core indicator)
        "procedure": "microbiometer", # Procedure for the analysis (not always similar to method)
        "analysis_method__name": "microbiometer", # Name of the method
        "instrument_brand__name": "microbiometer", # Instrument type or brand
        "instrument_model__name": "classic", # Model or version of the instrument
        "instrument_id": "0" # Any individual instrument id, the default for unknown id is "0"
      },
      "microbiometer_fungi-fraction": {
        "value": 42.0,
        "unit__name": "%",
        "indicator__name": "microbiometer_fungi-fraction",
        "procedure": "microbiometer",
        "analysis_method__name": "microbiometer",
        "instrument_brand__name": "microbiometer",
        "instrument_model__name": "classic",
        "instrument_id": "0"
      },
      "microbiometer_bacteria-fraction": {
        "value": 58.0,
        "unit__name": "%",
        "indicator__name": "microbiometer_bacteria-fraction",
        "procedure": "microbiometer",
        "analysis_method__name": "microbiometer",
        "instrument_brand__name": "microbiometer",
        "instrument_model__name": "classic",
        "instrument_id": "0"
      }
    }
  }
}
```

### Nested json object

The nested json object for Microbiometer observations contains the same object keys and values as the flat version, but hierarcically organised with nested arrays. For explanations of the object keys please see the flat json object above.

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
                            "microbiometer": [
                              {
                                "microbiometer": [
                                  {
                                    "value": 385.0,
                                    "unit__name": "ug*g^-1",
                                    "indicator__name": "tot-c",
                                    "analysis_method__name": "microbiometer-tot-c",
                                    "instrument-brand__name": "microbiometer-tot-c",
                                    "instrument-model__name": "classic",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 42.0,
                                    "unit__name": "%",
                                    "indicator__name": "fungi",
                                    "procedure": "microbiometer-fungi",
                                    "analysis_method__name": "microbiometer-fungi",
                                    "instrument-brand__name": "microbiometer-fungi",
                                    "instrument-model__name": "classic",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 58.0,
                                    "unit__name": "%",
                                    "indicator__name": "bacteria",
                                    "procedure": "microbiometer-bacteria",
                                    "analysis_method__name": "microbiometer-bacteria",
                                    "instrument-brand__name": "microbiometer-bacteria",
                                    "instrument-model__name": "classic",
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

Recorded data from the Microbiometer analysis are available at:

 - Flat json format [https://github.com/AI4SH/in-situ_data/tree/main/flat/microbiometer][github_microbiometer_flat]
 - Nested json format: [https://github.com/AI4SH/in-situ_data/tree/main/nested/microbiometer][github_microbiometer_nested]

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
- classic
- 0
- 20240815

And the final file name becomes:

```
se-loennstorp-20240815_55-c_0-20_a_0_uniform_mix-wet_classic_0_20240815.json
```


[github_microbiometer_flat]: https://github.com/AI4SH/in-situ_data/tree/main/flat/microbiometer

[github_microbiometer_nested]: https://github.com/AI4SH/in-situ_data/tree/main/nested/microbiometer

[microbiometer]: https://microbiometer.com
