# FLARe trauma exposed feasibility trial
## PI: Dr Kaitlin Bountress
## Org: VCU


Code respository for processing data from the FLARe app V3 (VCU) from raw to summary data files.

Raw data should be stored in a datafiles folder outside of the git repository. All new datasets will likewise be stored in a datafiles folder outside of the git repository. Data QC figures, including an elephant plot and affective rating plot, will be stored in a folder outside the main script directory.


## Description of each analysis step as found in the scripts folder 

### stage zero
the stage zero script is the primary data processing script.

It will start by asking you to select the raw datfile which contains trial data. This should be saved in .csv format, and called **ratings.csv**. It should be saved in the same folder on your computer as the aw data containing information about the app user. This should also be saved in .csv format and should be called **users.csv**. It will ask you to select this file from your file browser when you run the script.

it will use this to locate the files on your computer and create some new folders in the same directory to store data and figures. 

It will then run through the following steps:

1. Identify possible reasons for post hoc exclusion and save this is a new data set called **possible_exclusion_dataset.csv**. By the end of steps 1 and two, this file will include variables that provide: participants minmum, maximum and average volume during acquistion, whether the participant left then restarted the app during any of the key experimental phases, whether the participant dropped out (i.e. ceased seeing trials) and how many trials they missed due to this drop out for each phase, how many trials participants failed to respond to.

This file will allow you to make decisions about who to exclude from your analyses due to participant task engagement and behaviour.

2. Create a wide (participant per row) dataframe with participant response values (either expectancy ratings or affective ratings) for every trial of the task labelled according to phase, stimulus type, and trial.

3. Normalise output acording to CSplus allocation. This means that data will reflect which shape was allocated to each participant as their CS Plus. 

4.  identify trials which were never seen by the participant (due to drop out, restart, etc) as NA, and trials which were seen by the participant, but which the participant failed to respond to as 999. 

You may wish to recode these when creating aggregate scores

5. Save a final dataset containing subject ID, CS plus ID (which shape was the CS plus), volume during acquisition, and all responses for all trialsper person.

### stage one

This script takes the processed raw data and derives some siple summary dataframe to use for elephant plotting, and affective rating plots. The script takes as input the stage zero cleaned data outputted from stage zero. It will ask you to select this file from your file browser when you run the script.


This script will calculate the number of trials missed per person per phase due either to drop out, or due to missed responses and incorporate this information in the exclusions data file (see poin 1 in section above).

Currently, this script doesnt do anything more. Once you have amde decisions about how to deal with missing data, you may want to incorporate these analytic steps in this script.

### elephtant plots

This script takes the processed raw data and derives some siple summary dataframe to use for elephant plotting, and affective rating plots. The script takes as input the stage zero cleaned data outputted from stage zero. It will ask you to select this file from your file browser when you run the script.

It will seperate this raw data into expectancy and affective rating datasets, drop truly missing trials, recode missed values (999) to NA, and create summaries of data across all particpants for each trial, for each phase and stimulus type. This will result in an average and 95% confidence intervals for each stimulus for each trial of the experiment.

This will be used to produce an elephant plot (acquisition, extinction, return of fear) and affective ratings plot (familiarity, arousal, fear, valence) that will be saved in a figure folder in the same directory that your raw data is kept.

For affective ratings, phase 1 is baseline (before the experiment), 2 is post acquisition, 3 is post extinction, and 4 is post renewal.

The figures will be labelled with your maximum (those with any data) and minimum (those with complete data for all phases) sample sizes based on the input data.

These figures can be used diagnostically to ensure that there are no unexpected data deviations that need addressing either at the code or experiment level. 


