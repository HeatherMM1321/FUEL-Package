
# FUEL 

During an improved cookstove project if a FUEL sensor is used this tool may be used to vizualize and analyze the data produced by a households cookstove temperature sensor and the weight change information produced by the FUEL sensor. 


## Contained in this Package 

**example datafiles** : These are example files that should be used to test the functionality of the tool as well as examples of what data might look like. 

**example_file_convert.py** : This file was created specificly to convert the example datafiles into the appropriate format for analysis. If your datafiles do not match those of the provided datafiles a new file should be created to prodcue the same outputs. 

**household.py** : This file contains the actual vizualization and analysis tools which are contained within the Household class. 

**tests** : This folder contains a **test_household.py** file as well as an __init__.py file which will be used to test the functionality of the Household class inside **household.py** 

## Getting Started

It is important that before one inputs data into the main file that it is in the correct format. This package contains a eight example data files and a sample data cleaning file (**example_file_convert.py**) which produces data in the correct format for the **household.py** file. If your data does not match the format of the example file you must first reformat your data before using this tool. 

### Packages Needed to Run Files 

For **example_file_convert.py** 
* pandas 
* numpy 

For **household.py** 
* pandas 
* plotly
* scipy 

### Installing
To install the package you can either 
* Clone a local copy of this package directly from the github page 
```
https://github.com/HeatherMM1321/FUEL-package
```
* Use pip install with the following command 
```
pip install -i https://test.pypi.org/simple/ FUEL-millerh
```
Once the package is installed along with all dependencies files, you can obtain stove and fuel usage metrics as well as view interactive plots by using the Household class in household. See example below for more detail. 

### Inputs/Outputs

**example_file_convert.reformat_example_file(datafile_path)** 
* Outputs: 
  * Properly formatted dataframe with sensor data 
  * List of all stoves in data set 
  * List of all fuels in dataset 
  * Household ID 

**household.Household(dataframe, stoves, fuels, hh_id, temp_threshold=15, time_between_events=60, weight_threshold=0.2)** 
* Inputs: 
  * Dataframe : Should be formated in the same manner as the output dataframe above (see example) 
  * stoves(list of strs) : Names of all stoves in the dataframe (shoud match the names of column headers exactly) 
  * fuels(list of strs) : Names of all fuels in the dataframe (shoud match the names of column headers exactly) 
  * hh_id(str) : Unique houehsold ID 
  * temp_threshold(int) : Minimum temperature in degrees from ambient for cooking event identification, **default=15**(i.e. no cooking events will be identified at a temp below this value) 
  * time_between_events(int) : Minimum time in mins between identified cooking events, **default=60**
  * weight_threshold(float) : Minimum significant weight change in kg, **default=0.2** (i.e. no weight change below this value will be recorded) 
* Outputs: 
  * Dataframe contianing all stove and fuel usage recorded in datafile 
  * Interactive plot containing all stove data 
  * Interactive plot containg all fuel data 

### Example 
To run this example using the example data files provided you will first need to input the datafile in to the **example_file_convert.reformat_example_file()** function as shown below. For this example I will be using the data file labeld as **HH_319_2018-08-25_19-27-32_processed_v2.csv** (it should be noted that the example_file_convert will only work with data that is formated like the example files. If you wish to use other datafiles you will need to reformat your data to match the outputs that this file produces). 

```
from FUEL.example_file_convert import reformat_example_file as reformat 

df, stoves, fuels, hh_id = reformat('HH_319_2018-08-25_19-27-32_processed_v2.csv') 
```
This will produce a dataframe,  ![alt text](https://github.com/HeatherMM1321/FUEL-package/blob/master/example_outputs/df_output.PNG)
a list of all of the stoves in the dataset, 
```
['om30', '3stone', 'telia']
```
a list of all of the fuels in the dataset, 
```
['lpg', 'charcoal', 'firewood'] 
```
and finally the household identification. 

```
319
```
This is the data you will need as inputs for the **Household** tool. 

Next you will need to import the **household.Household()** class. 

```
from FUEL.household import Household 

Household(df, stove, fuels, hh_id) 
```
This will produce a dataframe containing usage information for each stove and fuel in the household. Where total is the total usage during the entire study and each row corresponds to a single 24 hour period in the study.

![alt text](https://github.com/HeatherMM1321/FUEL-package/blob/master/example_outputs/dataframe.PNG) 

An interactive html based plot for both fuel and stove usage will also be produced. 
![alt text](https://github.com/HeatherMM1321/FUEL-package/blob/master/example_outputs/fuel.PNG) 
![alt text](https://github.com/HeatherMM1321/FUEL-package/blob/master/example_outputs/stove_full.PNG) 



## Authors

* **Heather Miller** 


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
