# ERDDAP

An overview of **NOAA**'s **_ERDDAP_** data server including a sample setup and configuration.

---
![ERDDAP in Action][logo]

[logo]: http://www.digital-geography.com/wp-content/uploads/2016/03/MakeGraph.png "Example ERDDAP Interface"


---
**ERDDAP** is a data server that gives you a simple, consistent way to download subsets of scientific datasets in common file formats & then make graphs/maps.

---
Free and open source with a basic interface which overlays the data. It breaks data into **2** forms:

1. **Grid Dap** - Data best explored in a grid like manner.

   For example, a digital camera photograph is a who load of grids containing RGB values for that particular cell.
For marine data, each cell corresponds to a particular time value or locational value which has a value apportioned to it - which all combines to make up the full dataset.

2. **Tab Dap** - More traditional point driven data - normally maintained in regular tables.

   Data with a time series and locational value and a single return value - e.g. Ships course taken on a cruise.
Look at the graph of data to understand them better.
Focus is on making it easier to get scientific data.

**ERDDAP** unifies the different types of data servers so you have a consistent way to get the data you want, in the format you want.

1. Acts as a middleman between you & various remote data servers.

   + When you request data from **ERDDAP**, it reformats the request into the format required by the remote server, sends the request, gets the data, reformats the data into the format that you requested & sends it to you.

   + No need to go to different data servers to get data from different datasets.

2. Offers an easy-to-use, consistent way to request data (via the *OPENDAP* standard).

   + Via the *Web Map Service* (**WMS**).

3. Returns data in the common file format of your choice:
  
   + Offers all data as *.html table, ESRI .asc and .csv, Google Earth .kml, OPeNDAP binary, .mat, .nc, ODV .txt, .csv, .tsv, .json, and .xhtml*.

   + Can return an image with a customized graph/map.

   + No need to reformat.
  
4. Standardizes date/time formats:

   + Always uses *ISO 8601:2004(E)* standard format.

   + Uses Zulu (*UTC, GMT*).
  
5. Has *RESTful* web services for searching for datasets, downloading data and making maps.

---
## Advantages

Acting as a middleman between the user and the data source allows **ERDDAP** to have several useful features, including:

   1. The ability to modify and add to each dataset's existing metadata:
   
      - _Metadata_ is the who, what, when, where, why and how inform about each dataset that helps users understand it.
      
      - As functionality has been improved, **ERDDAP** can generate ***ISO 19115 metadata files***, the format required for US Government's data catalogs, while others such as ***MEDIN*** can be configured also.
      
   2. Standardized time data formats:
   
      - Makes it easier to compare data from different datasets.
      
      - Avoids the horrendous ordeal of dealing with a multitude of existing varying date time formats.
      
   3. Provides a unified way for users to search for datasets:
   
       - Via Google-like,  full-text search, via category browsing (aka faceted search) and via advanced search, which combines all search options.
       
   4. Offers a standard way to request a subset of the data from any dataset:
   
        - via **web applications** -- web pages with forms for humans.
        
        - via **web services** -- where one *RESTful* URL specifies the entire request.
        
   5. Allows users to specify the **response file format**, which ERDDAP generates **on-the-fly**:
   
        - No time wasted converting data from one format to another.
        
        - **20** different data file types.
        
        - Some image file types, so users can request customized maps and graphs.
       
      
 All of the features are designed to make life easier for data providers and for users.     

---
## Install

Creator [Bob Simons](https://github.com/BobSimons) has compiled comprehensive [instructions](http://coastwatch.pfeg.noaa.gov/erddap/download/setup.html) to follow for an **ERDDAP** install.

   + **ERDDAP** will run on any server which supports both Java and Tomcat, so AWS, Linux, Mac, Windows and even Docker. 

   + For best results, you're best to work on a **Linux** server with both Java and Tomcat web server installed. 
   
   + Download [ERDDAP](https://coastwatch.pfeg.noaa.gov/erddap/download/erddapContent.zip), extract and deploy it to the WebApps folder in the Tomcat directory.

     + **ERDDAP** connects using the *jtds JDBC connector* and the *EDDTableFromDatabase*.
   
     + Each dataset is presented in a single flat view per dataset to **ERDDAP**, e.g. [Marine Institute Weather Buoy Network](https://erddap.marine.ie/erddap/tabledap/IWBNetwork.html).

---
## Setup.xml

Configure your ERDDAP instance using the [setup.xml]() file (included in the content folder in ERDDAP after install):

   - You must set basic information like where you will save your parent directory (filled with logs and the like).

   - Set the access point for your server (i.e. its URL).
   
   - Email and ERDDAP admin information in case of error or the need to be contacted.
   
   - Details of the organisation that has ownership of the ERDDAP as well as its data.
   
   - Email details (including log-ins) for **ERDDAP** if you want the server itself to send out emails when needed (errors, etc).
 
[Here]() is an example of a functioning **setup.xml** file to follow to get you going.

---
## Datasets.xml

For **ERDDAP** to be able to serve any data, it must first understand the structure of the data. 
This understanding comes from configuring the **Datasets.xml** with database details, including connection strings as well as metadata.

Use Bob's included ***generatedatasets.xml*** script to automate the basic outline creation of the xml required for a particular dataset, otherwise it will take a while and you **will** make mistakes.
 
      This will ask you questions such as the location of the *dataset, its username, password, the associated schema, the primary key* and various other general pieces of connection specific information required to connect and understand the source data.
 
Following the successful completion of the dataset questionnaire (if it's unsuccessful, an error trace will be produced and you can use that along with the *log.txt* file in the **ERDDAP** folder to debug your code), copy in the produced xml data to the bottom of the existing *datasets.xml* file.
 
All going well, the next time the **ERDDAP** instance is updated (either according to the timer set up by minutes in *setup.xml* or by you manually rebooting the service on **Tomcat**), the dataset should appear in the ERDDAP index.
 
Ensure that the data can be viewed in-browser, so that you receive no numbered errors and can fully interrogate the data in GEOJSON.

      - If GEOJSON is inaccessible, you may need to introduce a small script to generate longitude/latitude based on a geometric data type or add a tummy time field to each row of data you want displayed in the database.

      - Depending on your source DBMS, this can be achieved using scripts to create and add data to views.

      - Once a view is created, you can add that to the datasets.xml file in the same way as you followed above and it should pass testing this time.

      - You may need to add the SRID to the dataset.

      - The dataset should then support **WMS** features.
 
To support metadata vocabularies, you can manually enter in what **IOOS** category each parameter equates.
 
[Here]() is a sample **datasets.xml** file to use when setting up an instance.

---
