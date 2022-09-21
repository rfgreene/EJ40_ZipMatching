# Justice40_ZipMatching

This repository contains several programs for determining the percentage of tracts within a given list of zip codes that fit certain environmental justice criteria according to the [Justice40 dataset](https://screeningtool.geoplatform.gov/en/methodology).

It is recommended that you read the (brief!) descriptions below to familiarize yourself with the organization of this repository. However, if you would like to jump straight to a description of how to use this repository to match sheets that include a zip code column, go [here](#workflow).

## Key Data

A <i>crosswalk</i> is a file with two columns which describes a relationship between two different sets of data. As census tracts and zip codes are distinct geographies, a crosswalk is necessary to match census tracts to zip codes. Raw data for the crosswalk was taken from the [U.S. Census Bureau](https://www2.census.gov/geo/docs/maps-data/data/rel/zcta_tract_rel_10.txt).

The <i>Justice40 dataset</i> evaluates U.S. communities according to several socioeconomic and environmental risk criteria, which can be found [here](https://screeningtool.geoplatform.gov/en/methodology). The GitHub project to generate this file is [here](https://github.com/usds/justice40-tool). The Justice40 data is saved in the <code>data/inputs</code> folder as <code>communities-2022-05-31-1915GMT.csv</code>.

## Programs

The full data pipeline runs:

<code>txt2csv.ipynb --> zcta_ej.ipynb --> Zip_EJ_Matching.ipynb --> statistics.ipynb</code>

However, for most use cases, only the latter two programs will be run, as the first two programs are used to generate lookup tables, which do not need to be re-generated for projects that use zip codes as the input geography.

<i>txt2csv</i> converts a .txt file to a .csv file, and is used to convert the zip code/tract crosswalk into a more flexible format.

<i>zcta_ej</i> merges the crosswalk with the Justice40 data to create a <i>lookup</i> that contains key environmental justice data points for each zip code.

<i>Zip_EJ_Matching</i> performs a "match" operation on all .csv files within a specified subfolder of <code>data/to_match</code>. Each .csv must contain a column "Zip" of zip codes. The operation will append environmental justice data for each zip code in the .csv based on the corresponding data in the lookup. This matched file will then be added to the <code>data/matched</code> folder.

<i>statistics</i> generates histograms and can run t-tests on matched .csv's to display the distribution of environmental justice communities within a dataset.

<i>zcta_ej_special</i> and <i>Zip_EJ_Matching_Special</i> are identical to the corresponding base programs, but include code to display additional variables of interest.

## Typical Use Case

The traditional use case of this project is to match petitioner zip codes taken from public comments on [regulations.gov](https://www.regulations.gov/) to Census tracts in order to compare how different campaigns mobilize environmental justice communities. This project could also be used to match other datasets with the Justice40 data based on zip codes, or, with minor modifications and the appropriate crosswalk, other geographies.

## Workflow

To append key environmental justice indicators to one or multiple spreadsheets containing a zip code column (which must be titled "Zip"), simply place those spreadsheets within a folder inside the <code>data/to_match</code> folder. Then, input the name of that subfolder (just the name, not the full path) as a string argument to the <code>match()</code> function call in the second code block of Zip_EJ_Matching.ipynb. Run that program (make sure you run the first code block first!) and a copy of the input spreadsheet(s) with environmental justice data appended will be in a corresponding subfolder under <code>data/matched</code>.
