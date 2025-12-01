---
title:  "Enzymatic activity"
layout: single
sidebar:
  nav: "in-situ_methods"
excerpt: "Soil enzymatic activity reveals the dominating soil biological processes. "
permalink: /in-situ_methods/digitsoil/
author_profile: false
date:   2025-11-27 06:13:03 +0200
last_modified_at:   2025-11-27 06:13:03 +0200
---

All biolgical processes and functions are related to enzymes and their activities. Assessing enzymatic metabolic activities and their rates have traditionally been a specialist bound and expensive analysis. The Swiss start-up [Digit Soil][digitsoil], a partner of the AI4SH project, has developed a rapid method for observing five key enzymatic activities. The instrument developed by Digit Soil is a stand alone unit that can be used in an ordinary home or office and is applicable for use by for instance citizen scientists.

## Short method description

The Soil Enzymatic Activity Reader (SEAR) developed by Digit Soil uses a combination of reaction plates and fluorescence spectroscopy. The method requires fresh samples, either directly from the field or kept at a few degrees C when stored and transported and then analysed. Soil samples are placed on a reaction plate with 5*5 cells (i.e. 5 replicates for each enzyme) and inserted into a spectrometer that uses UV light to excite the enzymes and a digital camera that registers the enzmatic activity and its change over a 40 minute period. The enzymatic activity rates of five key enzymes are then reported. The enzymatic activities observed are summarised in table 1.

Table 1. Enzymatic activities recorded with each observation with the Soil Enzymatic Activity Reader (SEAR).

| Property | Indicator | AI4SH extended naming | Unit |
| :------- | :----- | :----- | :---- |
| Chitinase/β-glucosaminidase | GLA | digit-soil-sear_GLA | pmol*min^-1 |
| β-Glucosidase | GLU  | digit-soil-sear_GLU | pmol*min^-1 |
| phosphatases (Phosphomonesterases) | PHO | digit-soil-sear_PHO | pmol*min^-1 |
| β-Xylosidase | XYL | digit-soil-sear_XYL | pmol*min^-1 |
| Leucine-aminopeptidase | LEU | digit-soil-sear_LEU | pmol*min^-1 |


## Data format

Each SEAR measurement is based on 5 replications of each enzymatic activity and the recorded data reports the mean value. The observed enzymatic activity data are available in 2 differently formatted json objects, a flat version more suitable for direct accessibility and a nested version intended for users who wants to convert the data to a relational sql database. The flat version does not include any arrays whereas the nested version is structured with nested arrays.

### Flat json object

Below is an example of a flat json object for enzymatic observations. Object keys with a double underscore denote a link to other entries in the database. For example _"person__email"_ is a key for the person responsible, with more detailed contact information in a separate json document. The hashtag comments are not allowed when operating a json file, they are added here for explaining each json object.

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
    "n_repeats": 5, # The number of repetitions done by any instrument on a single subsample and as part of a single replicate, with results reported as mean or mean and standard deviation
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
      "digit-soil-sear_LEU": { # Soil property reported as AI4SH extended naming (part after underscore = core indicator)
        "value": 3.5, # Recorded value (single value or mean of repeated observations)
        "unit__name": "pmol*min^-1", # Recorded unit
        "indicator__name": "digit-soil-sear_LEU", # AI4SH extended name of the soil indicator (part after underscore = core indicator)
        "procedure": "digit-soil-sear", # Procedure for the analysis (not always similar to method)
        "analysis_method__name": "digit-soil-sear", # Name of the method
        "instrument_brand__name": "digit-soil", # Instrument type or brand
        "instrument_model__name": "bob", # Model or version of the instrument
        "instrument_id": "0" # Any individual instrument id, the default for unknown id is "0"
      },
      "digit-soil-sear_GLA": {
        "value": 8.2905,
        "unit__name": "pmol*min^-1",
        "indicator__name": "digit-soil-sear_GLA",
        "procedure": "digit-soil-sear",
        "analysis_method__name": "digit-soil-sear",
        "instrument_brand__name": "digit-soil",
        "instrument_model__name": "bob",
        "instrument_id": "0"
      },
      "digit-soil-sear_GLU": {
        "value": 25.273,
        "unit__name": "pmol*min^-1",
        "indicator__name": "digit-soil-sear_GLU",
        "procedure": "digit-soil-sear",
        "analysis_method__name": "digit-soil-sear",
        "instrument_brand__name": "digit-soil",
        "instrument_model__name": "bob",
        "instrument_id": "0"
      },
      "digit-soil-sear_PHO": {
        "value": 60.2077,
        "unit__name": "pmol*min^-1",
        "indicator__name": "digit-soil-sear_PHO",
        "procedure": "digit-soil-sear",
        "analysis_method__name": "digit-soil-sear",
        "instrument_brand__name": "digit-soil",
        "instrument_model__name": "bob",
        "instrument_id": "0"
      },
      "digit-soil-sear_XYL": {
        "value": 8.1644,
        "unit__name": "pmol*min^-1",
        "indicator__name": "digit-soil-sear_XYL",
        "procedure": "digit-soil-sear",
        "analysis_method__name": "digit-soil-sear",
        "instrument_brand__name": "digit-soil",
        "instrument_model__name": "bob",
        "instrument_id": "0"
      }
    }
  }
}
```

### Nested json object

The nested json object for soil enzymatic activity observations contains the same object keys and values as the flat version, but hierarcically organised with nested arrays. For explanations of the object keys please see the flat json object above.

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
                            "digit-soil-sear": [
                              {
                                "digitsoil": [
                                  {
                                    "value": 3.5,
                                    "unit__name": "pmol*min^-1",
                                    "indicator__name": "digit-soil-sear_LEU",
                                    "analysis_method__name": "digit-soil-sear",
                                    "instrument_brand__name": "digit-soil",
                                    "instrument_model__name": "bob",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 3.8288,
                                    "unit__name": "pmol*min^-1",
                                    "indicator__name": "digit-soil-sear_GLA",
                                    "procedure": "digit-soil-sear",
                                    "analysis_method__name": "digit-soil-sear",
                                    "instrument_brand__name": "digit-soil",
                                    "instrument_model__name": "bob",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 6.5383,
                                    "unit__name": "pmol*min^-1",
                                    "indicator__name": "digit-soil-sear_GLU",
                                    "procedure": "digit-soil-sear",
                                    "analysis_method__name": "digit-soil-sear",
                                    "instrument_brand__name": "digit-soil",
                                    "instrument_model__name": "bob",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 7.9978,
                                    "unit__name": "pmol*min^-1",
                                    "indicator__name": "digit-soil-sear_PHO",
                                    "procedure": "digit-soil-sear",
                                    "analysis_method__name": "digit-soil-sear",
                                    "instrument_brand__name": "digit-soil",
                                    "instrument_model__name": "bob",
                                    "instrument_id": "0"
                                  },
                                  {
                                    "value": 0.5,
                                    "unit__name": "pmol*min^-1",
                                    "indicator__name": "digit-soil-sear_XYL",
                                    "procedure": "digit-soil-sear",
                                    "analysis_method__name": "digit-soil-sear",
                                    "instrument_brand__name": "digit-soil",
                                    "instrument_model__name": "bob",
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

Recorded data from the enzymatic activity analysis are available at:

 - Flat json format [https://github.com/AI4SH/in-situ_data/tree/main/flat/digit-soil_sear][github_sear_flat]
 - Nested json format: [https://github.com/AI4SH/in-situ_data/tree/main/nested/digit-soil_sear][github_sear_nested]

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
- bob
- 0
- 20240815

And the final file name becomes:

```
se-loennstorp-20240815_55-c_0-20_a_0_uniform_mix-wet_bob_0_20240815.json
```


[github_sear_flat]: https://github.com/AI4SH/in-situ_data/tree/main/flat/digit-soil_sear

[github_sear_nested]: https://github.com/AI4SH/in-situ_data/tree/main/nested/digit-soil_sear

[digitsoil]: https://www.digit-soil.com
