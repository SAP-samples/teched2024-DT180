# Exercise 4 - Configure, deploy and analyse Run Integrate Sales History Data...

In this exercise, we will modify, execute and analyse iFlow Run Integrate Sales Order History from SAP S4HANA Cloud to SAP IBP -your own user-

## Exercise 4.1 Configure and deploy the Run Sales Order History iFlow

After completing these steps you will have configured and deployed the above mentioned iFlow.

1. On the first tab open iFlow Run Integrate Sales Order History from SAP S4HANA Cloud to SAP IBP -your own user-
2. Click Configure. A popup will be opened that shows the configurable parameters of the iFlow.
3. In Batch Name the value should be -your P S I D C user- Sales Order History Run ID: ${header.SAP_MplCorrelationId}, replace -your P S I D C user- by your own user ID
4. Change the value of Plant Filter from -keep default- to 05AA-09ZZ,1000-1999,2060,4060. This will select all plants between 05AA and 09ZZ, between 1000 and 1999, 2060 and 4060 similar to what we configured in the Plants iFlow.
4. Change the value of Product Filter from -keep default- to FG126-FG426,HT2000,FG426-FG626. This will select all products between FG126 and FG426, HT200 and between FG426 and FG626 similar to what we selected in the Products, etc. iFlow.
5. In Datastore ID for Product Plant Filter replace -keep default- by the empty string
6. In Date From set the following value for selecting the last two years: xsd:yearMonthDuration('-P24M') + xsd:date(substring($IFlowStartTimestamp,1,10))
7. The rest of the configuration parameters should be left unchanged.
8. Click Deploy on the lower right corner of the screen
9. On the upcoming popup click Yes
10. You can switch to the third tab and check when your Flow is started
11. Switch to the second tab and navigate to Monitor -> Integrations and APIs, Monitor Message Processing -> All Artifacts
12. Update the display if needed until the run of your iFlow is finished
13. Filter by the correlation ID of the new run of your iFlow Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-
The following three iFlows all should have status Escalated: Run Integrate Sales Order History from SAP S4HANA Cloud to SAP IBP -your own user-, Integrate Sales Order History Data from SAP S4HANA Cloud to SAP IBP, SAP IBP Write - Process Posted Data
15. CLick on iFlow SAP IBP Write - Process Posted Data
16. Custom Header IBP Write Batch File should have the following entry:
    
batch:..., name:Sales Order History, count:421, status:PROCESSED_WITH_ERRORS, errorCount:1

## Exercise 4.2 Add the product plant filter

After completing these steps you will be able to run the integration of key figures only for products replicated to IBP

1. On the first tab configure iFlow Run Integrate Sales Order History from SAP S4HANA Cloud to SAP IBP -your own user-
2. Change configuration parameter Datastore ID for Product Plant Filter from empty string to -your own user- Product Plant FIlter
3. Deploy the iFlow again
4. Switch to the second tab and navigate to Monitor -> Integrations and APIs, Monitor Message Processing -> All Artifacts
5. Update the display if needed
6. Filter by the correlation ID of the latest run of your iFlow if needed. All iFlows of this run should have status Completed
7. CLick on iFlow SAP IBP Write - Process Posted Data
8. Custom Header IBP Write Batch File should have the following content: batch:..., name:Sales Order History, count:420, status:PROCESSED, errorCount:0

So one entry less is integrated now. If you would activate the trace for SAP IBP Write - Post Data and compare the input to IBP for the two runs above you would see that without the filter there was one entry for product HT200 in the sales history, which is filtered out by the Product Plant Filter, as for product HT200 no planned independent requirements can be created and thus there is no need to do any forecasting for this product.

## Exercise 4.3 Change the aggregation criteria

After completing these steps you will be able to influence how data are replicated to IBP

1. On the first tab configure iFlow Run Integrate Sales Order History from SAP S4HANA Cloud to SAP IBP -your own user-
2. Change configuration parameter Key Figure Name from ACUTUALSQTY to SENSEDDEMANDQTY
3. Change configuration parameter Time Period Type in SAP S/4HANA Cloud from Technical Week to Date
4. Change configuration parameter Time Profile Level in SAP IBP from 2 (technical week) to 1 (day)
5. Deploy the iFlow again
6. Check that the iFlow was started and finished successfully
7. Filter by the correlation ID of the latest run of your iFlow if needed. All iFlows of this run should have status Completed
8. CLick on iFlow SAP IBP Write - Process Posted Data
9. Custom Header IBP Write Batch File should have the following content: batch:..., name:Sales Order History, count:2296, status:PROCESSED, errorCount:0, so more entries have been integrated to IBP, as we only aggregated by date, not by month and week.
10. Repeat steps 1 to 9, but with the following changes to configuration parameters and the following expected result:
- Change configuration parameter Key Figure Name from SENSEDDEMANDQTY back to ACUTUALSQTY
- Change configuration parameter Time Period Type in SAP S/4HANA Cloud from Date back to Technical Week
- Change configuration parameter Time Profile Level in SAP IBP from 1 (day) back to 2 (technical week)
- Change configuration parameter Customer Source for SAP IBP from DummyCustomerID to ShipToParty
- Custom Header IBP Write Batch File should have the following content: batch:..., name:Sales Order History, count:2296, status:PROCESSED, errorCount:0, so more entries have been integrated to IBP, as we only aggregated by date, not by month and week.

This datastore can be used later when integrating the sales order history data, so that no sales history is loaded for products that have not been created in IBP or for product plant combinations for which no planned independent requirements can be created in S/4 after the forcast has been calculated in IBP.

## Summary

You've now learned to configure and deploy the iFlow for repilcating products etc and some of it's configuration parameters

Continue to - [Exercise 5 - Configure, deploy and analyse Run Integrate KFs from SAP IBP to SAP S4HANA Cloud...](../ex5/README.md)


