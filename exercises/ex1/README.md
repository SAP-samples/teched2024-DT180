# Exercise 1 - Modify, execute and analyse Basic Run Integrate Business Partners...

In this exercise, we will modify, execute and analyse iFlow Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your P S I D C user-

## Exercise 1.1 Modify and deploy the basic iFlow

After completing these steps you will have modified and deployed the above mentioned iFlow.

1. Log on to the Cloud Integration instance

2. Navigate to Design -> Integrations and APIs on the left. 
3. If there are too many entries for scrolling you can search by your user ID to shrink the list
4. Click on your self-created package Session DT180 -your own user-
     The details of that package should be shown
5. Click on tab Artifacts
6. Click on Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-
7. Click Edit

Please note that the integration process has two transforms. One is for defining modified headers and the other one is a processDirect call of the standard iFlow for Integration of Business Partners from S/4 to IBP. It is possible to schedule the standard iFlows standalone, but they only can have one configuration. So if there is a need to run the iFlows with different configurations it is better to define wrapper iFlows, like the one you uploaded, which modify the header parameters before they call the standard iFlows. This way every user can have his own set of configuration parameters without interfering with others.
8. Double-click on transform Define Modified Headers
9. On the bottom part of the screen a subscreen called Content Modifier is shown. Click on tab Message Header there
10. Find a row with Name DummyCustomerID and overwrite SourceValue with DUMMY
11. Find a row with Name CustomerFilter and overwrite SourceValue with an empty string (you might need to scroll for that)
12. Find a row with Name BatchName. The Source Value is -your P S I D C user- Basic Run Business Partner: ${header.SAP_MplCorrelationId}. Please replace -your P S I D C user- with your own user ID
13. The rest of the headers can be left unchanged.
14. Click Deploy on the top right corner of the screen
15. On the upcoming popup leave the Runtime Profile Cloud Integration as is an click Yes
16. A popup is shown with the Deployment information 'Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP ...' is triggered for deployment.
17. After some time there should be another temporary popup saying 'Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP ...' successfully deployed.

## Exercise 1.2 Check the logs of the first iFlow run

After completing these steps you will have a rough idea how to analyse what the actual run of the iFlow did. 
Note: The iFlow is set up in a way that it is triggered once after every new deployment. This is very useful for testing the iFlow. So to start the iFlow again you just need to repeat the deployment step. In a productive environment it is better to schedule the iFlow with a certain frequency or to call it from outside, but this is not part of this exercise.

1. To check the results of the run of the iFlow triggered during deployment you should duplicate the tab in the browser
2. In the duplicate tab navigate to Monitor -> Integrations and APIs on the left and then Monitor Message Processing -> All Artifacts on the right
3. You should be able to find an entry with the Artifact Name 'Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-' quite high in the shown list
4. You can click on that entry and scroll though the content on the right
5. Under Properties you can find the Correlation ID. Please copy the correlation ID to the clipboard by marking it and typing ctrl-C
6. Then click on field ID on the top right corner of the screen and type ctrl-V to set a filter for the correlation ID
7. Then click on the search button on the right of the ID field. The result is that only your iFlow and the iFlows that have been called by you iFlow are shown on the screen. All Artifacts shown should have status Completed.
8. Click on Artifact Name SAP IBP Write - Process Posted Data
The screen should look similar to this one:
<br>![](/exercises/ex1/images/SessionDT180IBPWriteProcessPostedData.gif)
Note 1: As you can see from the screenshot above there should be one entry sent to IBP and processed successfully there. The reason for that is that we have defined a DummyCustomerID, but we set CustomerFilter to an empty string. This way we only creaded a dummy customer in IBP, but we did not replicate customers from S/4 to IBP, which is only triggered if a filter is defined in CustomerFliter. This is why the delivered default value of that field is 0-ZZZ, which means all customers with an ID that is alphabetically between 0 and ZZZ are replicated from S/4 to IBP.
9. Click on artifact Integrate Business Partners from SAP S4HANA Cloud to SAP IBP
You should be able to see some Custom Headers, at least if you scroll down and and attachment Parameters even further down in the list. Please click on the link of attachment Parameters. You should be able to see the content of the attachment Parameters. If the content is not readable, because all rows are written into the same row you can download the atatchment and open it with an editor to read the content. The attachment contains the most important information about which parameters were used when processing the business iFlow Integrate Business Partners from SAP S4HANA Cloud to SAP IBP.
The content of the attachment could look like this:
Customer Filter: 
Dummy Customer ID: DUMMY
Field Extensions: 
Attributes in SAP IBP: CUSTID,CUSTCHANNEL,CUSTCOUNTRY,CUSTDESCR,CUSTREGION
Further Filters: 
Host for SAP S4/HANA Cloud: ...-api.s4hana.ondemand.com
Master Data Prefix: T24
OData Package Size: 50000

## Summary

You've now learned the basics on how you can analyse the run of an iFlow

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)

