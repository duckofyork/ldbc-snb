## LDBCouncil Social Network Benchmark data generator for MindmapsDB

This generator generates a gql file containg SNB data that can be loaded to MindmapsDB using Mindmaps Engine. You can find more information on SNB data here:  https://github.com/ldbc/ldbc_snb_datagen.

## Loading included sample dataset

A small sample dataset is included:

``` ldbc-snb-data-person-100.gql ```

To load this file into MindmapsDB, you need to do the following:

1 . Make sure you have MindmapsDB running : https://github.com/mindmapsdb/mindmapsdb

2 . Open a terminal, use the following command to load the ontology file:

``` curl -H "Content-Type: application/json" -X POST -d '{"path":"FILE_PATH/ldbc-snb-ontology.gql"}' http://localhost:4567/import/ontology ```

where FILE_PATH is the root folder of this project, which contains the ontology graql file.

3 . load the data using the following command:

``` curl -H "Content-Type: application/json" -X POST -d '{"path":"FILE_PATH/ldbc-snb-data-person-100.gql"}' http://localhost:4567/import/batch/data ```

again, FILE_PATH is the project root path. Loading this dataset can take up to 30 seconds.

4 . Start graql shell, check if the data has been loaded by using the following graql query

``` >>> compute count in person ```

``` 100 ```

## Generating your own dataset

If you want to generate your own dataset,
you can customize it by modifying params.ini in project root folder.

You can set the number of person in your dataset by setting the following
``` ldbc.snb.datagen.generator.numPersons ```

Or you can simply set the scale factor
``` ldbc.snb.datagen.generator.scaleFactor ```

For more information on how to customize the dataset, please check LDBC github
https://github.com/ldbc/ldbc_snb_datagen.

To generate the dataset, simply run the following command in the terminal:
``` FILE_PATH/run.sh ```

where FILE_PATH is the path of this project, containing the shell script.

Generating the data can take from several minutes to several hours,
depending on the size of the dataset.

When it's done, you can find the generated graql file in the project folder:

``` ldbc-snb-data.gql ```

Load the customized data to MindmapsDB using the following command:

``` curl -H "Content-Type: application/json" -X POST -d '{"path":"FILE_PATH/ldbc-snb-data-person.gql"}' http://localhost:4567/import/batch/data ```

Note that you still need to load the ontology file before loading your customized data!

MindmapsDB Discussion: https://discuss.mindmaps.io/
