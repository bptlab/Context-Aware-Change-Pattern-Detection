# Context-Aware-Change-Detection

## Introduction
This repository provides the implementation and further evaluation details of the paper entitled <b>Context-Aware Change Pattern Detection in Event Attributes of Recurring Activities</b>. The implementation includes four jupyter notebooks and a modified [pm4py implementation](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/pm4py.zip). The jupyter notebooks enumerated from 1 to 3 represent the approach of the paper, starting with the [detection and transformation of recurring events](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/1_Repetitive_Activity_Detection_Context_Identification.ipynb). Then, the [change pattern detection](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/2_Applying_Change_Detection.ipynb) is applied in the second jupyter notebook. The third jupyter notebook includes the [UI](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/3_UI.ipynb) to interact with the identified change patterns and to illustrate them in a process model. The modified pm4py package is only required, if one wants to visualize change patterns in the process model.

## Reproducing Sepsis and MIMIC results
To reproduce the results of the Sepsis event log, the scripts are ready to be executed, as the Sepsis event log is already available in the [Logs](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/tree/main/Logs) folder. The [outputs](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/tree/main/Outputs) of the preprocessing steps, including the transformed event log and the detected change patterns, are also already available for Sepsis, so one can immediately execute the [UI](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/3_UI.ipynb) jupyter notebook if desired. 

To reproduce the MIMIC results, one needs access to the [MIMIC-IV](https://mimic.mit.edu/iv/) database, which requires CITI training. Usually, that does not take much more than a day and access is granted within a week. If access is granted, the event log can be retrieved. We implemented an [event log generation tool](https://github.com/bptlab/mimic-log-extraction/tree/main) for MIMIC-IV, which allows to provide a config file as an input, which results in an ready-to-use event log. Use the [config file](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/MIMIC_LOG_CONFIG.yml) in this repository to retrieve an event log by executing the following command: ```python extract_log.py --config MIMIC_Config.yml```. Some post-processing is required, which is conducted in [this jupyter notebook](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/0_MIMIC-IV_Generation.ipynb). After that, the other jupyter notebooks can be executed with the MIMIC event log.

## Detailed Evaluation

As mentioned in the paper, the following presents detailed results regarding the detection of recurring activities and change pattern results for the MIMIC event log. First, the results of the vectors dfr/dpr representing the directly follows and directly preceding ratios for all activities in MIMIC and Sepsis are shown. The repetition score is then the sum of one row, which are also illustrated below. The matrices are supposed to be read row-wise. For example, the "Measurement" activity in Tab. 1 is followed by "START Invasive Ventilation" in 84.5% of the occurences of "START Invasive Ventilation". Tab. 1 and Tab. 2 show, that the "Measurement" is mostly conducted before the START and after the END of a treatment activity. Tab. 3 and Tab. 4 show the respective results for Sepsis. In Sepsis, "CRP" and "Leucocytes" are almost never following "Release A", but precede it relatively often.


|![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/dfr_MIMIC.PNG?raw=true)|
|:--:| 
| *Tab. 1 Directly-Follows ratios for activities in MIMIC* |

|![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/dpr_MIMIC.PNG?raw=true)|
|:--:| 
| *Tab. 2 Directly-Precedes ratios for activities in MIMIC* |

![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/dfr_Sepsis.PNG?raw=true)
|:--:| 
| *Tab. 3 Directly-Follows ratios for activities in MIMIC* |

![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/dpr_Sepsis.PNG?raw=true)
|:--:| 
| *Tab. 4 Directly-Precedes ratios for activities in MIMIC* |

Tab. 5 and Tab. 6 show the repetition scores, which are the average scores of the rows in the matrices.

![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/rep_score_MIMIC.PNG?raw=true)|![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/rep_score_Sepsis.PNG?raw=true)
:-------------------------:|:-------------------------:
 *Tab. 5 Repetition scores for all activities in MIMIC* | *Tab. 6 Repetition scores for all activities in Sepsis* 

The following figures show detailed results of the change pattern detection in MIMIC. 


![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/MIMIC_PM_RAW.png?raw=true)
|:--:| 
| *Fig. 1 Enhanced process model with change patterns detected on the raw MIMIC event log* |


![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/MIMIC_PM.png?raw=true)
|:--:| 
| *Fig. 2 Enhanced process model with change patterns detected on the raw Sepsis event log* |

![alt text](https://github.com/bptlab/Context-Aware-Change-Pattern-Detection/blob/main/Evaluation/matrix_MIMIC.PNG?raw=true)
|:--:| 
| *Fig. 3 Change Pattern Matrix of selected event attributes and relations independent of a trace variant* |

