# ERDDAP

An overview of **NOAA**'s **_ERDDAP_** data server including a sample setup and configuration.

 
 ---
![alt text][logo]

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

## Setup

Creator Bob Simons (https://github.com/BobSimons) has compiled comprehensive instructions to follow for an ***ERDDAP*** install: http://coastwatch.pfeg.noaa.gov/erddap/download/setup.html

   + **ERDDAP** connects using the *jtds JDBC connector* and the *EDDTableFromDatabase*.
   
   + Each dataset is presented in a single flat view per dataset to **ERDDAP**, e.g. [Marine Institute Weather Buoy Network](https://erddap.marine.ie/erddap/tabledap/IWBNetwork.html).

