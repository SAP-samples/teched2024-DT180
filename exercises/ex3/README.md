# Exercise 3 - Configure, deploy and analyse Run Integrate Products etc...

In this exercise, we will modify, execute and analyse iFlow Run Integrate Products etc from SAP S4HANA Cloud to SAP IBP -your P S I D C user-

## Exercise 3.1 Configure and deploy the Run Products etc iFlow

After completing these steps you will have modified and deployed the above mentioned iFlow.

The Product, etc. iFlow is the most complex one of the provided iFlows. It is selecting not only products, but also other related data. Using the default settings not only products (master data type PRODUCT) are created in IBP, but also units of measure (UOMTO) and product specific unit of measure conversion factors (UOMCONVERSIONFACTOR)

1. On the first tab open iFlow Run Integrate Products etc from SAP S4HANA Cloud to SAP IBP -your own user- of your package Session DT180 -your own user-
2. Click Configure. A popup will be opened that shows the configurable parameters of the iFlow.
3. In Batch Name the value should be -your P S I D C user- Run Product, etc.: ${header.SAP_MplCorrelationId}, replace -your P S I D C user- by your own user ID
4. Change the value of Plant Filter from -keep default- to 05AA-09ZZ,1000-1999,2060,4060. This will select all plants between 05AA and 09ZZ, between 1000 and 1999, 2060 and 4060.
4. Change the value of Product Filter from -keep default- to FG126-FG426,HT2000. This will select all products between FG126 and FG426 and HT2000
5. In Datastore ID for Product Plant Filter replace -keep default- by the empty string
7. The rest of the configuration parameters should be left unchanged.
8. Click Deploy on the lower right corner of the screen
9. On the upcoming popup click Yes
10. Switch to the second tab opened in exercise 1 and navigate to Monitor -> Integrations and APIs, Monitor Message Processing -> All Artifacts
11. Update the display if needed
12. Filter by the correlation ID of the run of your iFlow Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-
13. CLick on iFlow SAP IBP Write - Process Posted Data
14. Custom Header IBP Write Batch File should have the following three entires:
    
batch:..., name:UomTo, count:4, status:PROCESSED, errorCount:0
batch:..., name:UomConversionFactor, count:31, status:PROCESSED, errorCount:0
batch:..., name:Product, count:11, status:PROCESSED, errorCount:0

## Exercise 3.2 Create only some data types in IBP

After completing these steps you will be able to run the integration of products, etc. for only some master data types

1. On the first tab configure iFlow Run Integrate Products etc from SAP S4HANA Cloud to SAP IBP -your own user-
2. Change configuration parameter Master Data Types from PRODUCT,UOMTO,UOMCONVERSIONFACTOR to PRODUCT,UOMTO
3. Deploy the iFlow again
4. Switch to the second tab and navigate to Monitor -> Integrations and APIs, Monitor Message Processing -> All Artifacts
5. Update the display if needed
6. Filter by the correlation ID of the latest run of your iFlow Run Integrate Products etc from SAP S4HANA Cloud to SAP IBP -your own user-
7. CLick on iFlow SAP IBP Write - Process Posted Data
8. Custom Header IBP Write Batch File should have the following content: batch:..., name:Plants, count:18, status:PROCESSED, errorCount:0, so 5 more plants should have been selected and processed
9. Custom Header IBP Write Batch File should have the following two entires:
    
batch:..., name:UomTo, count:4, status:PROCESSED, errorCount:0
batch:..., name:Product, count:11, status:PROCESSED, errorCount:0

10. Repeat steps 1 t 9 above, but Change configuration parameter Master Data Types to UOMCONVERSIONFACTOR
11. Custom Header IBP Write Batch File of iFlow iFlow SAP IBP Write - Process Posted Data should have the following  entry now:
    
batch:..., name:UomConversionFactor, count:31, status:PROCESSED, errorCount:0

## Exercise 3.3 Create a datastore with selected product plant combinations

After completing these steps you will be able to save the selected product plant combinations in a datastore for later filtering

1. Create a fourth tab by duplicating the thrird one
2. Navigate to Monitor -> Integrations and APIs and then Manage Stores -> Data Stores
3. Check that there is a data store with name ProductPlantFilter
4. Click on that data store
5. Check that there is no entry with ID -your own user- Product Plant Filter
6. On the first tab configure iFlow Run Integrate Products etc from SAP S4HANA Cloud to SAP IBP -your own user-
7. Change configuration parameter Datastore ID for Product Plant Filter from empty string to -your own user- Product Plant Filter
8. Deploy the iFlow again
9. Check that the iFlow was started and finished successfully
10. Go to the fourth tab again and refresh the list of Data Stores
11. Click on data store ProducPlantFilters again
12. Check that there is an entry with ID -your own user- Product Plant Filter now
13. Mark the new entry and download it
14. Open the zip file and the file body within it
15. It should look as follows:
    
&lt;?xml version="1.0" encoding="utf-8"?>&lt;S4ProductPlantFilter>FG126:1010,1710;FG129:1010,1710;FG130:1010,1710;FG2_CP:1010,1710;FG226:1010,1710;FG228:1010,1710;FG233:1010,1710;FG29:1010,1710;FG326:1010,1710;FG328:1010,1710;FG426:1010,1710&lt;/S4ProductPlantFilter>

16. Repeat steps 6 to 14, but set configuration parameter Product Filter to FG426-FG626 instead of FG126-FG426
17. The file body of the downloaded zip file now should look like this:

&lt;?xml version="1.0" encoding="utf-8"?>&lt;S4ProductPlantFilter>FG126:1010,1710;FG129:1010,1710;FG130:1010,1710;FG2_CP:1010,1710;FG226:1010,1710;FG228:1010,1710;FG233:1010,1710;FG29:1010,1710;FG326:1010,1710;FG328:1010,1710;FG426:1010,1710;FG626:1010,1710&lt;/S4ProductPlantFilter>

So basically the entity in the datastore is updated with the new product FG626 and the old entries are still kept. If needed the entity in the data store can be deleted to reset it.

The entity in the data store can be used later when integrating the sales order history data, so that no sales history is loaded for products that have not been created in IBP or for product plant combinations for which no planned independent requirements can be created in S/4 after the forcast has been calculated in IBP.

## Summary

You've now learned to configure and deploy the iFlow for repilcating products etc and some of it's configuration parameters

Continue to - [Exercise 4 - Configure, deploy and analyse Run Integrate Sales History Data...](../ex4/README.md)

