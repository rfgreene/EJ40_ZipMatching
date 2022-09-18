# Justice40_ZipMatching

This repository contains several programs for determining the percentage of tracts within a given list of zip codes that fit certain environmental justice criteria according to the [Justice40 dataset](https://screeningtool.geoplatform.gov/en/methodology).

It is recommended that you read the (brief!) descriptions below to familiarize yourself with the organization of this repository. However, if you would like to jump straight to a description of how to use this repository to match sheets that include a zip code column, go [here](#workflow).

## Key Data

A <i>crosswalk</i> is a file with two columns which describes a relationship between two different sets of data. As census tracts and zip codes are distinct geographies, a crosswalk is necessary to match census tracts to zip codes. Raw data for the crosswalk was taken from the [U.S. Census Bureau](https://www2.census.gov/geo/docs/maps-data/data/rel/zcta_tract_rel_10.txt).

The <i>Justice40 dataset</i> evaluates U.S. communities according to several socioeconomic and environmental risk criteria, which can be found [here](https://screeningtool.geoplatform.gov/en/methodology). The GitHub project to generate this file is [here](https://github.com/usds/justice40-tool). The Justice40 data is saved in the <code>data/inputs</code> folder as <code>communities-2022-05-31-1915GMT.csv</code>.

## Programs

The full data pipeline runs:
<pre><code>
txt2csv.ipynb --> zcta_ej.ipynb --> Zip_EJ_Matching.ipynb --> statistics.ipynb
</pre></code>

However, for most use cases, only the latter two programs will be run, as the first two programs are used to generate lookup tables, which do not need to be re-generated in most cases.

<i>txt2csv</i> converts a .txt file to a .csv file, and is used to convert the zip code/tract crosswalk into a more flexible format.

<i>zcta_ej</i> merges the crosswalk with the Justice40 data to create a <i>lookup</i> that contains key environmental justice data points for each zip code.

<i>Zip_EJ_Matching</i> performs a "match" operation on all .csv files within a specified subfolder of <code>data/to_match</code>. Each .csv must contain a column "Zip" of zip codes. The operation will append environmental justice data for each zip code in the .csv based on the corresponding data in the lookup. This matched file will then be added to the <code>data/matched</code> folder.

<i>statistics</i> generates histograms and can run t-tests on matched .csv's to display the distribution of environmental justice communities within a dataset.

<i>zcta_ej_special</i> and <i>Zip_EJ_Matching_Special</i> are identical to the corresponding base programs, but include code to display additional variables of interest.

## Typical Use Case

What is this used for?

## Workflow

Describe workflow
