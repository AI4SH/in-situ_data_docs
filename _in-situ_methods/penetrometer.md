---
title:  "Penetrometer"
layout: single
sidebar:
  nav: "in-situ_methods"
excerpt: "Penetrometers can be used for determining a range of soil both physical and chemical properties. Soil compaction ..."
permalink: /in-situ_methods/penetrometer/
author_profile: false
date:   2025-11-27 06:13:03 +0200
last_modified_at:   2025-11-27 06:13:03 +0200
---

Physically robust and microchip controlled pentrometers for analysing physicochemical soil properties directly in-situ has become available over the past few years. Using multiple steel pins, developments in microelectronics and signal interpretation these simple instrumetns can now separate water and salt content and also detect specific ions, like hydrogen (pH) and those derived from nitrogen, phosphorus and potassium (NPK) – the key soil macronutrients. Soil penetrometers that can operate at the power levels of mobile phones have emerged only recently and are as yet scientifically unproven. The AI4SH project tested the 5-pin penetrometer model NPKPHCTH-S from [ComWinTop store on AliExpress][comwintop] operating at 5 volt and mounted with a microcontroller and usb/bluetooth connection, developed by the startup [Xsepctre][xspectre].

Note the following issues related to the penetrometer data when applying it for further analysis:
- the penetrometer data is only available for a subset of pilot sites,
- in most cases each sample was anaysed using more than 1 subsample (thus there are more than one record per sample), and
- for the Finnish site (Jokionen, used as examples below), 3 different copies of the same penetrometer model where used to allow evaluating bias and consistency.

## Difference between subsample, replicate and repetition

The difference between a subsample and a replicate is that if the same physical volume of soil is used for the analysis it is a replicate, but if the analysis is used on a separate physical volume it is a subsample. Thus all destructive analysis methods can per definition not be replicates. For the soil penetrometers to apply a replicate would mean letting it stay in the exact same postion for two sequantial observaion. As each penetrometer observation is already based on 6 repetion and the recorded data is stated as mean value and standard deviation (see example below), one more observation in the exact same position renders no new information. Thus, for the penetrometer analysis done as part of AI4SH, the position was typically shifted to different sides in the dug central pit, and each observation recorded as a subsample.

## Short method description

The penetrometer is simply pushed into the soil, either from the top or vertically in a pit. The observation is started from the device (computer or smartphone) connected to the microcontroller unit. In the setup used in AI4SH, each observation is repeated 6 times and the user must approve of the results displayed as mean and standard deviation before the observation is recorded. The penetrometer used in the AI4SH project simultaneously records 9 soil parameters with each observation, table 1.

Table 1. Soil properties recorded with each observation with the ComWinTop NPKPHCTH-S 5 steel pin penetrometer.

| Property | Abbreviation | AI4SH Indicator | Unit |
| :------- | :----- | :----- | :---- |
| temperature | temp | temp | C |
| Soil moisture | sm  | sm | vol*vol^-1 |
| pH | pH | pH | ph |
| Nitrogen | N | n | mg*l-1 |
| Phosphorus | P | p | mg*l-1 |
| Potassium | K | k | mg*l-1 |
| Electric conductivity | ec | ec | us*cm-1 |
| Salinity | Sal | sal | mg*l-1 |
| Total Dissolved Solid | TDS | tds | mg*l-1 |

## Data format

Each measurement with the NPKPHCTH-S penetrometer is based on 6 repetions and the recorded data contains the mean value and the standard deviation of these 6 repetitions. The observed penetrometer data are available in 2 differently formatted json objects, a flat version more suitable for direct accessibility and a nested version intended for users who wants to convert the data to a relational sql database. The flat version does not include any arrays whereas the nested version is structured with nested arrays.

### Flat json object

Below is an example of a flat json object for penetrometer observations. Object keys with a double underscore denote a link to other entries in the database. For example _"person__email"_ is a key for the person responsible, with more detailed contact information in a separate json document. The hashtag comments are not allowed when operating a json file, they are added here for explaining each json object.

```
{
  "campaign": "ai4sh_fi-jokioinen", # 'project'+'_'+'country'+'-'+'pilot site'
  "sampling_log": { # Assembly of samples collected in the same day at a particular pilot site
    "name": "fi-jokioinen-20241008", # 'country'+'-'+'pilot site'+'-'+'sampling date'
    "date_stamp": "20241008", # Date when the sample was collected in the field
    "person__email": "thomasg@xspectre.com" # Email of person responsible for the sampling
  },
  "sample": "fi-jokioinen-20241008_22-r_0-20", # 'country'+'-'+'pilot site'+'-'+'sampling date'+'_'+'sample
  "locus": { # Assembly of the point location, setting and depth
    "position__name": "fi-jokioinen_22-r",  # 'country'+'-'+'pilot site'+'-'+'sample point id' used for checking internal consistency
    "point": "22-r", # sample point id
    "setting": "uniform", # The spatial setting in the landscape (uniform, alley, plantline, edge)
    "latitude": 60.817773051, # Latitude in WGS84
    "longitude": 23.479190111, # Longitude in WGS84
    "min_depth": 0, # Sample upper limit in cm in soil profile
    "max_depth": 20 # Sample lower limit in cm in soil profile
  },
  "observation": { # Assembly of metadata and data related to the obeservation
    "sample_preparation__name": "mixed-untreated-soil-in-lab", # Explanatory name of soil treatment before observation
    "person__email": "thomasg@xspectre.com", # Email of person responsible for the obeservation
    "subsample": "b", # For registering if physically different soil subsamples were analysed separately, default for a single analysis = a
    "replicate": 0, # If the analysis was replicated on the same subsample more than once, the first test is always set to 0
    "n_repeats": 6, # The number of repetitions done by any instrument on a single subsample and as part of a single replicate, with results reported as mean or mean and standard deviation
    "date_stamp": "20241008", # Date when the analysis was done
    "logistic": { # Assembly of logistical metadata on the handling of the sample
      "sample_preservation__name": null, # Explanatory name of soil preservation
      "sample_transport__name": null, # Explanatory name of soil transportation if sensitive for analysis results
      "transport_duration_h": 0, # duration of any sensitive transportation in hours
      "sample_storage__name": null, # Explanatory name of soil storage if sensitive for analysis results
      "storage_duration_h": 0, # Storage duration in hours
      "person__email": "thomasg@gxspectre.com" # Email of person responsible for the logistics
    },
    "analysis": { # Assembly of analysis results, procedures and instruments
      "temperature": { # Soil property reported from the analysis
        "value": 16.45, # The recorded value (single value or mean or repeated observations)
        "standard_deviation": 0.05000000000000071, # The recorded satandard deviation, if applicable
        "unit__name": "C", # the recorded unit
        "indicator__name": "temperature", # The name of the soil indicator
        "procedure": "xspectre-penetrometer", # The procedure used for the analysis
        "analysis_method__name": "penetrometer", # The instrument type or brand used for the analysis
        "instrument-brand__name": "comwintop", # # Name of the method used for the analysis
        "instrument-model__name": "npkphcth-s", # The instrument type or brand used for the analysis
        "instrument_id": "0003" # Any individual instrument id, the default for unknown id is "0"
      },
      "sm": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 22.183333333333334,
        "standard_deviation": 0.24094720491334964,
        "unit__name": "vol*vol-1",
        "indicator__name": "sm",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      },
      "ec": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 28.0,
        "standard_deviation": 0.0,
        "unit__name": "us*cm-1",
        "indicator__name": "ec",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      },
      "ph": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 6.366666666666667,
        "standard_deviation": 0.18856180831641262,
        "unit__name": "pH",
        "indicator__name": "ph",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      },
      "nitrogen": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 88.0,
        "standard_deviation": 0.0,
        "unit__name": "mg*l-1",
        "indicator__name": "nitrogen",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      },
      "phosphorus": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 21.0,
        "standard_deviation": 0.0,
        "unit__name": "mg*l-1",
        "indicator__name": "phosphorus",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      },
      "potassium": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 96.0,
        "standard_deviation": 0.0,
        "unit__name": "mg*l-1",
        "indicator__name": "potassium",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      },
      "salinity": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 158.0,
        "standard_deviation": 0.0,
        "unit__name": "mg*l-1",
        "indicator__name": "salinity",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      },
      "tds": { # Each soil property reported with the same instrument are reported as individual objects
        "value": 144.0,
        "standard_deviation": 0.0,
        "unit__name": "mg*l-1",
        "indicator__name": "tds",
        "procedure": "xspectre-penetrometer",
        "analysis_method__name": "penetrometer",
        "instrument-brand__name": "comwintop",
        "instrument-model__name": "npkphcth-s",
        "instrument_id": "0003"
      }
    }
  }
}
```

### Nested json object

The nested json object for penetrometer observations contains the same object keys and values as the flat version, but hierarcically organised with nested arrays. For explanations of the object keys please see the flat json object above.

```
{
  "data_source": [
    {
      "name": "ai4sh_fi-jokioinen",
      "site": [
        {
          "name": "fi-jokioinen",
          "point": [
            {
              "name": "22-r",
              "latitude": 60.817773051,
              "longitude": 23.479190111,
              "setting": "uniform",
              "sampling_log": [
                {
                  "name": "fi-jokioinen-20241008",
                  "date_stamp": "20241008",
                  "person__email": "thomasg@xspectre.com",
                  "sample": [
                    {
                      "name": "fi-jokioinen-20241008_22-r_0-20",
                      "min_depth": 0,
                      "max_depth": 20,
                      "observation": [
                        {
                          "sample_preparation__name": "mixed-untreated-soil-in-lab",
                          "person__email": "thomasg@xspectre.com",
                          "subsample": "b",
                          "replicate": 0,
                          "n_repeats": 6,
                          "date_stamp": "20241008",
                          "logistic": {
                            "sample_preservation__name": null,
                            "sample_transport__name": null,
                            "transport_duration_h": 0,
                            "sample_storage__name": null,
                            "storage_duration_h": 0,
                            "person__email": "thomasg@xspectre.com"
                          },
                          "analysis_method": {
                            "xspectre-penetrometer": [
                              {
                                "value": 16.45,
                                "standard_deviation": 0.05000000000000071,
                                "unit__name": "C",
                                "indicator__name": "temperature",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 22.183333333333334,
                                "standard_deviation": 0.24094720491334964,
                                "unit__name": "vol*vol-1",
                                "indicator__name": "sm",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 28.0,
                                "standard_deviation": 0.0,
                                "unit__name": "us*cm-1",
                                "indicator__name": "ec",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 6.366666666666667,
                                "standard_deviation": 0.18856180831641262,
                                "unit__name": "pH",
                                "indicator__name": "ph",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 88.0,
                                "standard_deviation": 0.0,
                                "unit__name": "mg*l-1",
                                "indicator__name": "nitrogen",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 21.0,
                                "standard_deviation": 0.0,
                                "unit__name": "mg*l-1",
                                "indicator__name": "phosphorus",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 96.0,
                                "standard_deviation": 0.0,
                                "unit__name": "mg*l-1",
                                "indicator__name": "potassium",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 158.0,
                                "standard_deviation": 0.0,
                                "unit__name": "mg*l-1",
                                "indicator__name": "salinity",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
                              },
                              {
                                "value": 144.0,
                                "standard_deviation": 0.0,
                                "unit__name": "mg*l-1",
                                "indicator__name": "tds",
                                "analysis_method__name": "penetrometer",
                                "instrument-brand__name": "comwintop",
                                "instrument-model__name": "npkphcth-s",
                                "instrument_id": "0003"
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

recorded data from the Microbiometer analysis are available at

 - Flat json format [https://github.com/AI4SH/in-situ_data/tree/main/flat/penetrometer][github_penetrometer_flat]
 - Nested json format: [https://github.com/AI4SH/in-situ_data/tree/main/flat/penetrometer][github_penetrometer_nested]

The file naming is defined to separate all eventual renewed sampling or analysis efforts and is built up from the following metadata:
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

- fi
- jokioinen
- 20241008
- 22-r
- 0
- 20
- b
- 0
- uniform
- mix-wet
- npkphcth-s
- 0003
- 20241008

And the final file name becomes:

```
fi-jokioinen-20241008_22-r_0-20_b_0_uniform_mix-wet_npkphcth-s_0003_20241008
```

As noted above, the the peneteromer observations in Jokioinen, Finlad, three copies of the penterometer model (with id's 0001, 0002 and 0003) where used and each penetroemter where tested on several subsampels (denoted a, b, c, etc).

[github_penetrometer_flat]: https://github.com/AI4SH/in-situ_data/tree/main/flat/npkphcth-s

[github_penetrometer_nested]: https://github.com/AI4SH/in-situ_data/tree/main/nested/npkphcth-s

[comwintop]: https://www.aliexpress.com/store/1101541124

[xspectre]: https://www.xspectre.com
