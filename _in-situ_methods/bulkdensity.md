---
title:  "Bulk density and volumetric soil moisture content"
layout: single
sidebar:
  nav: "in-situ_methods"
excerpt: "The bulk density of the soil upper layers is influenced by the soil mother material, soil natural processes and human soil management. To record the bulk density the classical method of sinking and withdrawing a soil cylinder into and out of underdisturbed soil is the superior method."
permalink: /in-situ_methods/bulkdensity/
author_profile: false
date:   2025-11-27 06:13:03 +0200
last_modified_at:   2025-11-27 06:13:03 +0200
---

Soil compaction is recognised as one of the major threats to soil health. Compaction affects the infiltration, soil water holding capacity and other hydraulic properties. It also affects the macrofauna and indirectly also the microbiological community.

The bulk density of the soil upper layers is influenced by the soil mother material, soil natural processes and human soil management. To record the bulk density the classical method of sinking and withdrawing a soil cylinder into and out of underdisturbed soil is the superior method.

## Short method description

A sturdy soil cylinder, usually with one end sharpened and with a precisely determined volumes is sunk (i.e. hammered) into the soil and taken out with soil extending out from both sides. A knife or similar tool is used to cut off any soil sticking out from the cylinder and the ends are sealed, e.g. with a plastic cap. The cylinder with its wet soil is then weighed, dried at 105<sup>o</sup> C and weighed again. Together with the weight of the cylinder (and caps if needed), the weight and volume of the wet and dry cylinder content are calculated. From this data the soil bulk density and volumetric soil moisture content are calculated.

## Data format

The AI4SH observed bulk density and volumetric soil moisture content data are available in 2 differently formatted json objects, a flat version more suitable for direct accessibility and a nested version intended for users who wants to convert the data to a relational sql database. The flat version does not include any arrays whereas the nested version is structured with nested arrays.

### Flat json object

Below is an example of a flat json object for bulk density and volumetric soil moisture content observations. Object keys with a double underscore denote a link to other entries in the database. For example _"person__email"_ is a key for the person responsible, with more detailed contact information in a separate json document. The hashtag comments are not allowed when operating a json file, they are added here for explaining each json object.

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
      "soil-cylinder-drying@105c_soil-moisture-volumetric-content": { # Soil property reported as AI4SH extended naming (part after underscore = core indicator)
        "value": 0.162717138949006, # Recorded value (single value or mean of repeated observations)
        "unit__name": "vol*vol^-1", # Recorded unit
        "indicator__name": "soil-cylinder-drying@105c_soil-moisture-volumetric-content", # AI4SH extended name of the soil indicator (part after underscore = core indicator)
        "procedure": "soil-cylinder-drying@105c", # Procedure for the analysis (not always similar to method)
        "analysis_method__name": "soil-cylinder-drying@105c", # Name of the method
        "instrument_brand__name": "general-soil-cylinder", # Instrument type or brand
        "instrument_model__name": "0", # Model or version of the instrument
        "instrument_id": "0" # Any individual instrument id, the default for unknown id is "0"    
      }
      "soil-cylinder-drying@105c_bulk-density": {
        "value": 1.28338286105099,
        "unit__name": "g*cm^-3",
        "indicator__name": "soil-cylinder-drying@105c_bulk-density",
        "procedure": "soil-cylinder-drying@105c",
        "analysis_method__name": "soil-cylinder-drying@105c",
        "instrument_brand__name": "general-soil-cylinder",
        "instrument_model__name": "0",
        "instrument_id": "0"
      }
    }
  }
}
```

### Nested json object

The nested json object for soil bulk density and volumetric soil moisture content observations contains the same object keys and values as the flat version, but hierarcically organised with nested arrays. For explanations of the object keys please see the flat json object above.

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
                            "soil-cylinder-drying@105c": [
                              {
                                "soil-cylinder": [
                                  {
                                    "value": 0.162717138949006,
                                    "unit__name": "vol*vol^-1",
                                    "indicator__name": "soil-cylinder-drying@105c_soil-moisture-volumetric-content",
                                    "analysis_method__name": "soil-cylinder-drying@105c",
                                    "instrument_brand__name": "general-soil-cylinder",
                                    "instrument_model__name": "0",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 1.28338286105099,
                                    "unit__name": "g*cm^-3",
                                    "indicator__name": "soil-cylinder-drying@105c_bulk-density",
                                    "procedure": "soil-cylinder-drying@105c",
                                    "analysis_method__name": "soil-cylinder-drying@105c",
                                    "instrument_brand__name": "general-soil-cylinder",
                                    "instrument_model__name": "0",
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

Recorded data from the bulk density and volumetric soil moisture content analysis are available at:

 - Flat json format [https://github.com/AI4SH/in-situ_data/tree/main/flat/bulk_density][github_bulk_density_flat]
 - Nested json format: [https://github.com/AI4SH/in-situ_data/tree/main/nested/bulk_density][github_bulk_density_nested]

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
- soil-cylinder-drying@105c
- 0
- 20240815

And the final file name becomes:

```
se-loennstorp-20240815_55-c_0-20_a_0_uniform_no-prep_soil-cylinder-drying@105c_0_20240815.json
```

[github_bulk_density_flat]: https://github.com/AI4SH/in-situ_data/tree/main/flat/bulkdensity

[github_bulk_density_nested]: https://github.com/AI4SH/in-situ_data/tree/main/nested/bulkdensity
