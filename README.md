# SolrMeter

<!-- TOC -->

- [SolrMeter](#solrmeter)
    - [Overview](#overview)
    - [Compile from source](#compile-from-source)
        - [Requirements](#requirements)
        - [HOWTO Compile](#howto-compile)
    - [Run SolrMeter](#run-solrmeter)
        - [GUI](#gui)
        - [Headless](#headless)
    - [Configuration Files](#configuration-files)
        - [Queries File Configuration](#queries-file-configuration)
            - [Example Queries File](#example-queries-file)
        - [Fields File Configuration](#fields-file-configuration)
            - [Example Fields File](#example-fields-file)
        - [Add and Update Configuration](#add-and-update-configuration)
            - [Example Add Update File](#example-add-update-file)
            - [Escaping characters](#escaping-characters)
        - [Filter Queries File Configuration](#filter-queries-file-configuration)
            - [Example Filter Queries File](#example-filter-queries-file)

<!-- /TOC -->

## Overview

This is a standalone Java Tool to test SOLR instances.  This project was maintained [here](https://github.com/tflobbe/solrmeter), however, it is no longer in development.

The main goal of this open source project is bring to the solr user community a generic tool to interact specifically with solr, firing queries and adding documents to make sure that your Solr implementation will support the real use.
With SolrMeter you can simulate your work load over solr index and retrieve statistics graphically.

## Compile from source

### Requirements

* Apache Maven 3.5.3
* Java version: 1.8 - JRE/JDK

### HOWTO Compile

1. Clone this repository to your working directory
2. Run `mvn package`
3. This will create a `.jar` file under `solrmeter/target` directory.  The jar file is named `solr-meter-{version}-jar-with-dependencies.jar`

## Run SolrMeter

The following steps should be followed to get SolrMeter up and running.

### GUI

1. Download latest released version
2. run it from the command line with ```java -jar solrmeter-{version}-jar-with-dependencies.jar```
3. create files with information of [queries](queries.md), [fields](fields.md), [updates](updates.md) and [filter queries](filterqueries.md)
4. specify the URL of Solr for updates and queries.
5. run the executors with the "Start" button.

### Headless

TBD

## Configuration Files

### Queries File Configuration

A simple text file, each line should be the extact text you want to put on the "q" parameter.
This file is used by the [FileQueryExtractor](../../tree/master/solrmeter/src/main/java/com/plugtree/solrmeter/model/extractor/FileQueryExtractor.java) class.

#### Example Queries File

```text
car
pig
red
dog category:animal
"solr roks"
category:(animal OR vegetable)
```

Before creating this file you have to think on the search handler you are going to use.

This file is going to be referenced from the "settings" window of the UI.

Also, you can check de [example file](../../tree/master/solrmeter/src/main/resources/example/queries.txt) from the sorce code, this example works just fine with the [solr example](http://lucene.apache.org/solr/tutorial.html).

### Fields File Configuration

A simple text file, each line should be the a declared field of the schema. This fields are going to be used for faceting. (Only fields that you want to be used for faceting should be added to this file).

This file is going to be used by the [FileQueryExtractor](../../tree/master/solrmeter/src/main/java/com/plugtree/solrmeter/model/extractor/FileFieldExtractor.java) class

#### Example Fields File

```text
content
category
fileExtension
```

Also, you can check de [example file](../../tree/master/solrmeter/src/main/resources/example/fields.txt) from the sorce code, this example works just fine with the [solr example](http://lucene.apache.org/solr/tutorial.html).

### Add and Update Configuration

A simple text file, each line representing a document that is going to be added to solr. The format is:
`fieldName:fieldValue;`
All required fields must be on the file.

#### Example Add Update File

```text
id:1;name:dog;category:animal
id:2;name:cat;category:animal
id:3;name:lettuce;category:vegetable
```

#### Escaping characters

if you want to escape a semicolon, use a slash and then a semicolon "\;". If you want to add a slash, add two slashes "\\".

Also, you can check de [example file](../../tree/master/solrmeter/src/main/resources/example/updates.txt) from the sorce code, this example works just fine with the [solr example](http://lucene.apache.org/solr/tutorial.html).

### Filter Queries File Configuration

A simple text file, each line should be the extact text you want to put on the "fq" parameter. This file is used by the [FileQueryExtractor](../../tree/master/solrmeter/src/main/java/com/plugtree/solrmeter/model/extractor/FileQueryExtractor.java) class.
You can put multiple filter queries on the same line if you want them all to be used as one (on the same query).
You can also use blank lines if you want the query to execute some queries with no filter queries.

#### Example Filter Queries File

```text
category:animal

category:vegetable
categoty:vegetable price:[0 TO 10]
categoty:vegetable price:[10 TO *]
```

Also, you can check de [example file](../../tree/master/solrmeter/src/main/resources/example/filterQueries.txt) from the sorce code, this example works just fine with the [solr example](http://lucene.apache.org/solr/tutorial.html).