Dataset
-------
The data is captured from 9 subjects named as s1 to s9. The data is present in 9 directories, one for each subject. Each directory contains 8 files, which are explained below.

Experiment
----------
Each subjects (S*) were asked to read texts / passage on the screen. There were two types of text namely, easy and difficult. Each type had three passages where each passage were shown at a time on the full screen. The sequence of the information shown on the screen is given below - 
1. A fixation "+" was shown on the screen for approximately 15 seconds. This is termed as baseline. The start and end of the baseline is logged as metadata in file s*_t*_EEG_raw.csv, which is described below
2. After that the first passage is shown and the subjects were asked to silently read. Once the reading is over then a next button is pressed by the subject.
3. Upon the next button the second passage was shown. Once the reading is done then again the next button is pressed.
4. Upon the next button the third passage was shown. Once the reading is done then again the next button is pressed.
5. The session ends here.

The above session is done twice for each subject (S*) - once for easy text and other for the difficult text. The task in a session is termed as t1 or t2. This is indicated as t* in this document. The type of text is logged in s*_t*_sequence.txt file. The eyegaze and the Muse EEG are logged during the experiment along with the time stamp. The eyegaze data is logged in s*_t*_eyeTracker.xls. The MUSE EEG data is logged in s*_t*.mat file

Thus for each subject, there are 4 files for easy text and 4 files for difficult text.

File - s*_t*_EEG_raw.csv
------------------------
This file does not contain the raw EEG data. It contains two columns - 
Column A - Marker metadata
Column B - Time stamp in seconds in UTC

Details of Marker Metadata
11100 - Experiment start
11111 - Baseline start
11112 - Baseline end
11121 - Stimulus start
11130 - Stimulus End

File - s*_t*_sequence.txt
-------------------------
Contains whether the text was easy or difficult.

File - s*_t*_eyeTracker.xls
---------------------------
Column A - StatusCode - 200 means OK
Column B - Fix - 1 means fixation is present
Column C - Avg_x - X coordinate of the screen for the eye gaze (left most point of the screen means x == 0)
Column D - Avg_y - Y coordinate of the screen for the eye gaze top most point of the screen means y == 0)
Column V - Time - Time stamp in seconds in UTC

File - s*_t*.mat
----------------
This contains the MUSE EEG and accelerometer data.
In matlab execute "load s*_t*.mat" by giving appropriate subject and task number.

e.g. "load s1_t1.mat" loads the following data.
  IXDATA        1x1             1900968  struct              
  ans           1x95                190  char                
  config        1x1               13700  struct              
  device        1x2                 362  cell                
  elements      1x1             8431392  struct  
In order to extract the EEG, accelerometer and the corresponding time stamps, perform the following in Matlab.
    accl_data = raw_data.IXDATA.raw.acc.data;
    accl_times = raw_data.IXDATA.raw.acc.times;
    eeg_data = raw_data.IXDATA.raw.eeg.data;
    eeg_times = raw_data.IXDATA.raw.eeg.times;

There are three axis data for accelerometer and four channel data for EEG. 
The times correspond to seconds in UTC.

Thus one needs to aling the EEG, eyetracker and the stimulus using the time information and then do the processing.

Stimulus
--------
The content of the easy and difficult stimulus are given in directories - 
stimulus->easy
stimulus->difficult
Each directories has 3 slides which are shown in the sequence as numbered.
