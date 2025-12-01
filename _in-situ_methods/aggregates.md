---
title:  "Aggregates"
layout: single
sidebar:
  nav: "in-situ_methods"
excerpt: "The free smartphone apps Moulder and Slakes determine soil aggregate stability by soaking dried pea-sized soil clumps for 20 minutes and record the disintegration using the smartphone camera."
permalink: /in-situ_methods/aggregates/
author_profile: false
date:   2025-11-27 06:13:03 +0200
last_modified_at:   2025-11-27 06:13:03 +0200
---

Aggregates, clumps of smaller soil particles glued together by biological processes, are key components for e.g. soil hydraulic properties, nutrient recycling and pool sizes. Stable soil aggregates also contribute to resistance towards wind and water erosion, and are linked to improved water capture, infiltration, and storage.

The smartphone apps [Slakes][slakes] and Moulder (a renamed version of Slakes) uses image analysis of dried, pea sized soil aggregates before and after soaking. Aggregates that resist dispersion after rewetting and _slake_ (or _mould_, i.e. disintegrate) less are more stable compared to those that break apart. A higher resistance indicate a healthier soil.

## Short method description

From a dired soil sample three pea sized aggregates are selected and put in a shallow dish. A smartphone with the app installed is mounted above the dish and an image taken of the dish and the three aggregates. The dish is then gently filled with water, enough to just cover the aggregates. The user can adjust the app's identification of the aggregates, and another images is captured. After 10 minutes a third image is taken and the app calculates an aggregate stability index.

## Data format

The AI4SH observed aggregate stability data are available in 2 differently formatted json objects, a flat version more suitable for direct accessibility and a nested version intended for users who wants to convert the data to a relational sql database. The flat version does not include any arrays whereas the nested version is structured with nested arrays.

### Flat json object

Below is an example of a flat json object for aggregates stability observations. Object keys with a double underscore denote a link to other entries in the database. For example _"person__email"_ is a key for the person responsible, with more detailed contact information in a separate json document. The hashtag comments are not allowed when operating a json file, they are added here for explaining each json object.

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
    "sample_preparation__name": "dried-aggregate-select+soaked", # Explanatory name of soil treatment before observation
    "person__email": "analysis@gmail.com", # Email of person responsible for the obeservation
    "subsample": "a", # For registering if physically different soil subsamples were analysed separately, default for a single analysis = a
    "replicate": 0, # If the analysis was replicated on the same subsample more than once, the first test is always set to 0
    "n_repeats": 1, # The number of repetitions done by any instrument on a single subsample and as part of a single replicate, with results reported as mean or mean and standard deviation
    "date_stamp": "20241110", # Date when the analysis was done
    "logistic": { # Assembly of logistical metadata on the handling of the sample
      "sample_preservation__name": null, # Explanatory name of soil preservation
      "sample_transport__name": null, # Explanatory name of soil transportation if sensitive for analysis results
      "transport_duration_h": 0, # duration of any sensitive transportation in hours
      "sample_storage__name": null, # Explanatory name of soil storage if sensitive for analysis results
      "storage_duration_h": 2008, # Storage duration in hours
      "person__email": "logistic@gmail.com" # Email of person responsible for the logistics
    },
    "analysis": { # Assembly of analysis results, procedures and instruments
      "slakes_aggregate-stability-index": { # Soil property reported as AI4SH extended naming (part after underscore = core indicator)
        "value": 0.69, # Recorded value (single value or mean of repeated observations)
        "unit__name": "index", # Recorded unit
        "indicator__name": "slakes_aggregate-stability-index", # AI4SH extended name of the soil indicator (part after underscore = core indicator)
        "procedure": "slakes", # Procedure for the analysis (not always similar to method)
        "analysis_method__name": "slakes", # Name of the method
        "instrument_brand__name": "smartphone", # Instrument type or brand
        "instrument_model__name": "slakes+samsung-a26", # Model or version of the instrument
        "instrument_id": "0" # Any individual instrument id, the default for unknown id is "0"
      }
    }
  }
}
```

### Nested json object

The nested json object for aggregate stability observations contains the same object keys and values as the flat version, but hierarcically organised with nested arrays. For explanations of the object keys please see the flat json object above.

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
                          "sample_preparation__name": "dried-aggregate-select+soaked",
                          "person__email": "analysis@gmail.com",
                          "subsample": "a",
                          "replicate": 0,
                          "n_repeats": 1,
                          "date_stamp": "20241110",
                          "logistic": {
                            "sample_preservation__name": "dried",
                            "sample_transport__name": null,
                            "transport_duration_h": 0,
                            "sample_storage__name": null,
                            "storage_duration_h": 2088,
                            "person__email": "logistic@gmail.com"
                          },
                          "analysis_method": {
                            "slakes": [
                              {
                                "slakes app": [
                                  {
                                    "value": 0.69,
                                    "unit__name": "index",
                                    "indicator__name": "slakes_aggregate-stability-index",
                                    "analysis_method__name": "slakes",
                                    "instrument_brand__name": "smartphone",
                                    "instrument_model__name": "slakes+samsung-a26",
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

Recorded data from the aggregate stability analysis are available at:

 - Flat json format [https://github.com/AI4SH/in-situ_data/tree/main/flat/aggregates][github_aggregates_flat]
 - Nested json format: [https://github.com/AI4SH/in-situ_data/tree/main/nested/aggregates][github_aggregates_nested]

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
- dry-pick-soak
- slakes+samsung-a26
- 0
- 20241110

And the final file name becomes:

```
se-loennstorp-20240815_55-c_0-20_a_0_uniform_dry-pick-soak_slakes+samsung-a26_0_20241110.json
```

[github_aggregates_flat]: https://github.com/AI4SH/in-situ_data/tree/main/flat/aggregates

[github_aggregates_nested]: https://github.com/AI4SH/in-situ_data/tree/main/nested/aggregates

[slakes]: https://soilhealthinstitute.org/our-work/initiatives/slakes/
