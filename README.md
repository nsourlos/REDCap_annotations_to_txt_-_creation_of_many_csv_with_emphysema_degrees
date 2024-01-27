# Save nodule information to txt files & Extract subcases for a given participant characteristic 

![Alt text](./nodule-information-to-txt-file.svg)
![Alt text](./participant-characteristic-subdivide-to-cases.svg)


[![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](https://www.python.org/)
[![forthebadge](https://forthebadge.com/images/badges/uses-badges.svg)](https://forthebadge.com)

[![Maintenance](https://img.shields.io/badge/Maintained%3F-no-red.svg)]( https://github.com/nsourlos/REDCap_annotations_to_txt_-_creation_of_many_csv_with_emphysema_degrees)


> This tool consists of two tools: 

1. This [tool](./nodule_information_to_txt.ipynb) can be used to extract nodule information of all participants of a given characteristic (eg. a given emphysema degree, as saved in REDCap). Nodule information is considered the nodule id, the slice number, and the volumes of its components (solid, subsolid etc.).

For each of the above characteristics one txt file is created. 

The above txt files are convenient to be used for manual comparison of the AI results with those of radiologists 
(instead of opening the REDCap page of each participant each time).

2. This [tool](./characteristic_all_to_many_subcases.ipynb) can be used for cases in which information was extracted from REDCap having all subcases of a given participant characteristic in a given csv file (eg. all emphysema degrees in one csv file).
The code here creates one csv file for each subcase by extracting the required information from the above file.  

The actual csv file is not included due to privacy issues.

## Documentation (by *Chat GPT*)

The documentation below was created by using the prompt 
> Write documentation for the following code

### 1. [nodule_information_to_txt.ipynb](./nodule_information_to_txt.ipynb)

**Introduction**

This code is used to extract and analyze annotations from a set of CSV files that contain information about the degree of emphysema in medical scans. The code reads the information from the CSV files and writes the extracted data to a text file.

**Library Imports**

The following libraries are used in the code:

`pandas` is used to read the information from the CSV files.
`numpy` is used to perform mathematical operations on the data.
`os` is used to interact with the file system.

**Variables**

The following variables are defined in the code:

`paths` is a list of strings that contains the paths to the directories where the CSV files are located.

`ground_truth_path` is a string that defines the main directory where the CSV files are located.

`path_to_save` is a string that defines the path where the text file will be saved.

**Main Functionality**

The code uses a for loop to iterate over the paths list. For each path, the code opens a text file and writes the extracted information to the text file.

The following information is extracted for each CSV file:

- The participant ID, which is the name of the file.
- The slices that contain the annotations.
- The nodule IDs of the annotations.
- The volume of the annotations, separated into solid and subsolid.

The extracted information is written to the text file in a readable format, including the file name, the slices, the nodule IDs, and the volume of the annotations. The code also adds newline characters to separate the information for different files.

### 2. [characteristic_all_to_many_subcases.ipynb](./characteristic_all_to_many_subcases.ipynb)

This code is written in Python and it uses the modules os, numpy, and pandas. The purpose of the code is to process the data from a csv file named `Emphysema_DATA_12-9.csv` and categorize individuals based on the severity of their emphysema.

The first step is to read the emphysema data using the pd.read_csv function. The path to the csv file is constructed using `os.getcwd()` which returns the current working directory and the string `/Emphysema_DATA_12-9.csv`.

The next step is to filter the data to only include cases where the emphysema classification was verified, using the following line:

`emph_all=emph_all[emph_all['emphysema_specific_complete']==2]`

The code then categorizes individuals based on the severity of their emphysema. The categories are: `advanced`, `confluent`, `moderate`, `noemph`, `mild`, and `trace`. The severity of emphysema is determined based on the values in the columns `centr_emph_wl_ef` and `centr_emph_wl_f`. The values can range from 1 to 6. The code uses `np.where` function to find the indices of individuals with specific severity and then filters the data using the `.iloc` method of the pandas dataframe.

After categorizing the individuals, the code saves each category to a separate csv file using the `.to_csv` method of the pandas dataframe. The file names are generated with a pattern: `ImaLife20-[CategoryName]CentrEmphyNo_DATA_2022-04-07_nikos.csv`.

The code also checks if there are any individuals who are in more than one category by comparing the `participant_id` column. If any duplicates are found, they are printed to the console with a message indicating the categories they belong to.

Finally, the code prints the unique values of the columns `centr_emph_wl_ef` and `centr_emph_wl_f` which should be 1-6. These lines are commented out and serve as a reference for the possible values of the columns. 



## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.