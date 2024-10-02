# Exercise 1 - Modify, execute and analyse Run Integrate Business Partners...

In this exercise, we will modify, execute and analyse iFlow Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your P S I D C user-

## Exercise 1.1 Modify and deploy the Business Partner iFlow

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
13. The rest of the headers should be left unchanged.
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

## Exercise 1.3 Produce and analyse an escalation

1. Switch back to the first tab and navigate to the edit mode of iFlow Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user- as described in exercise 1.1 above
2. Double-click on transform DefineModifiedHeaders and change the Source Value of header FieldExtensions to &lt;CUSTDESCR value="'DUMMY''s description'"/>. This will overwrite the mapping of field CUSTDESCR and set is to DUMMY's description
3. Deploy the iFlow again
4. Switch back to the second tab and navigate to Monitor Message Processing again
5. Find the latest entry of Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-
6. Filter by the correlation ID of this new run as described in exercise 1.2

Note that iFlow SAP IBP Write - Process Posted Data has status Escalated. You also can see from the Custom Headers of that Artifact that there was only one entry, which failed the validation. 
<br>![](/exercises/ex1/images/SessionDT180IBPWriteProcessPostedDataValidationError.gif)
Now let's analyse more in detail what is the issue here.

7. Duplicate the second tab again to create a third one
8. On the new tab navigate to Monitor -> Integrations and APIs on the left and Manage Integration Content -> All on the right
9. Find iFlow Integrate Business Partners from SAP S4HANA Cloud to SAP IBP, evtl. by using a search string (this is the standard one, not your wrapper iFlow)
10. Click on it and check the Log Configuration
11. If the Log Level is not Trace then change it to Trace

Note that the log level trace is activated for all users and is deactivated after 15 minutes already. So it might be that someone else already activated the trace level for the iFlow and it also might happen quite often that it is deactivated automatically

12. Switch back to the first tab and deploy iFlow Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user- again
13. Switch to the third tab. As long as the status of iFlow Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user- is starting click the refresh button
14. Afterwards go to the second tab and refresh the list there until the latest run of Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user- is Completed
15. Find the corresponding run of iFlow Integrate Business Partners from SAP S4HANA Cloud to SAP IBP. If there are several ones in parallel fliter by the correlation ID.
16. Double-click it
17. Scroll down to Logs
18. The entry Log Level should be a link with text Trace. Click on it
19. Click on entry Delete body from property in the list of run steps. THis is the last step before IBP Write - Post Data is called via ProcessDirect
20. Then click on tab Message Content on top
21. Click on tab Payload

The result should look similar to this:
<br>![](/exercises/ex1/images/SessionDT180IBPWritePostDataPayload.gif)

Note that field CUSTDESCR contains string DUMMY's description, which contains a single quote. This is not supported in IBP. IBP cannot handle the special characters single and double quote, less than, greater than, carriage return and line feed. But there is a convenient solution to that.

22. Just repeat the steps before, but use Source Value &lt;CUSTDESCR value="ibp:escape('DUMMY''s description')"/> for header FieldExtensions
There won't be any validation error any more and if you have a look at the trace again you will find that CUSTDESCR has now the value DUMMY⨩s description, where the ' is replaced by a lookalike unicode character ⨩. The replacement characters for the non-supported characters in IBP are defined in iFlow Define Default Values for Data Integration Between SAP IBP and SAP S4HANA Cloud in externalized parameter Escaped Quotes and can be adapted if needed.

## Summary

You've now learned the basics on how you can analyse the run of an iFlow

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)

