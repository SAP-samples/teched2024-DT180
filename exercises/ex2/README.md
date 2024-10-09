# Exercise 2 - Configure, deploy and analyse Run Integrate Plants...

In this exercise, we will modify, execute and analyse iFlow Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your P S I D C user-

## Exercise 2.1 Configure and deploy the Run Plants iFlow

After completing these steps you will have modified and deployed the above mentioned iFlow.

1. On the first tab open iFlow `Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-` of your package `Session DT180 -your own user-`
2. Click `Configure`. A popup will be opened that shows the configurable parameters of the iFlow.
3. In `Batch Name` the value should be `-your P S I D C user- Run Plant: ${header.SAP_MplCorrelationId}`, replace `-your P S I D C user-` by your own user ID
4. Change the value of `Plant Filter` from `-keep default-` to `1000-1999`. This will select all plants between 1000 and 1999.
5. The rest of the configuration parameters should be left unchanged.
6. Click Deploy on the lower right corner of the screen
7. On the upcoming popup click `Yes`
8. Switch to the second tab opened in exercise 1 and navigate to `Monitor -> Integrations and APIs`, `Monitor Message Processing -> All Artifacts`
9. Update the display if needed
10. Filter by the correlation ID of the run of your iFlow `Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-`
11. CLick on iFlow `SAP IBP Write - Process Posted Data`
12. Custom Header `IBP Write Batch File` should have the following content: `batch:..., name:Plants, count:13, status:PROCESSED, errorCount:0`, so 13 plants shoud have been replicated

> [!NOTE]
>  If you want to analyse more in detail how the data have been processed in IBP and which errors occured there you can logon to the IBP system (not possible in this exercise) and open app `Data Integration Job`s. You can find the write batch with the `Batch ID` you can see in this parameter, but it is also possible to search the fitting batch by the `Correlation ID` in that app. In the app you will be able to download the first around 50000 rows of every batch file and the first 50000 rows with errors for analysing the data and the error messages in detail. It also can be helpful to use app 'Application Logs' for a more detailed analysis. Please use the `Batch ID` there for seraching the relevant entries.

## Exercise 2.2 Use a more complex plant filter

After completing these steps you will be able to define filters for the plant ID with several intervals and single values

1. Switch back to the first tab and open iFlow `Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-` if not done yet
2. Click `Configure`. A popup will be opened that shows the configurable parameters of the iFlow.
4. Change the value of `Plant Filter` from `1000-1999` to `05AA-09ZZ,1000-1999,2060,4060`. This will select all plants between 05AA and 09ZZ, between 1000 and 1999, 2060  and 4060.
5. The rest of the configuration parameters should be left unchanged.
6. Click `Deploy` on the lower right corner of the screen
7. On the upcoming popup click `Yes`
8. Switch to the second tab opened above and navigate to `Monitor -> Integrations and APIs`, `Monitor Message Processing -> All Artifacts`
9. Update the display if needed
10. Filter by the correlation ID of the second run of your iFlow `Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-`
11. Click on iFlow `SAP IBP Write - Process Posted Data`
12. Custom Header `IBP Write Batch File` should have the following content: `batch:..., name:Plants, count:18, status:PROCESSED, errorCount:0`, so 5 more plants should have been selected and processed

> [!NOTE]
> Configuration Parameter `Plant Filter` is also available in your iFlows `Run Integrate Products etc from SAP S4HANA Cloud to SAP IBP -your own user-` and `Run Integrate Sales Order History from SAP S4HANA Cloud to SAP IBP -your own user-`. Whatever filter you are setting in this iFlow you also should set there to make sure that you are not integrating any products that are not assigned to at least one of the plants or sales history data for non-integrated plants. In the standard settings of the underlying configuration-only iFlows these configuration parameters have the default value `-keep default-`, which means they are taking over the value from iFlow `Define Default Values for Data Integration Between SAP IBP and SAP S4HANA Cloud`. So the filter can be defined centrally there. For this exercise you shall not change the configuration of the configuration-only iFlows, so you have to do double or tripple maintenance of some configuration parameters in different iFlows. If you forget to keep the filters in sync it is still possible that you are not running into any issues, as the needed data probably have been replicated already by other users.

## Exercise 2.3 Define a field extension for plants

After completing these steps you will be able to define a field extension for plants

1. On the third tab activate log level trace for iFlow `Integrate Plants from SAP S4HANA Cloud to SAP IBP`
2. On the first tab open iFlow `Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-` if not done yet
3. Click `Configure`. A popup will be opened that shows the configurable parameters of the iFlow.
4. Change the value of `Field Extensions` from empty string to `<LOCREGION value="if(FactoryCalendar eq 'US') then 'Americas' else if (FactoryCalendar eq'01') then 'EMEA' else 'ASIA' "/>`
5. The rest of the configuration parameters should be left unchanged.
6. Click `Deploy` on the lower right corner of the screen
7. On the upcoming popup click `Yes`
8. Switch to the second tab and navigate to` Monitor -> Integrations and APIs`, `Monitor Message Processing -> All Artifacts`
9. Update the display if needed
10. Filter by the correlation ID of the latest run of your iFlow `Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your own user-`
11. CLick on iFlow `Integrate Plants from SAP S4HANA Cloud to SAP IBP`
12. Click on the `Trace` link under `Logs` -> `Log Level`
13. Click on `ProcessDirect` between the run steps `Set Log Custom Headers End` and `Delete body from property` (or the other way round, as the list is sorted chronologically in descending order)
14. Click on Tab `Message Content` and sub tab `Payload`
15. If you have the needed authorization you should be able to see the content of the data that are sent to IBP and you should see that some entries have value `EMEA` in variable `LOCREGION`, while others have value `Americas`. There should also be a comment before the items: `<!--custom fields: LOCREGION-->` It is indicating that field `LOCREGION` has been modified by custom logic

> [!NOTE]
> The content of attribute `value` cannot consist of a field path only: `value ="./AddressID"` is not allowed, give a function instead like `value ="string(./AddressID)"`, `value ="ibp:escape(./AddressID)"` or `value ="concat('',./AddressID)"` 

## Summary

You've now learned to configure and deploy the iFlow for repilcating plants and it's most important configuration parameters

Continue to - [Exercise 3 - Configure, deploy and analyse Run Integrate Products etc...](../ex3/README.md)

