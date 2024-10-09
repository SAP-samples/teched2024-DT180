# Exercise 1 - Configure, deploy and analyse Run Integrate Business Partners...

In this exercise, we will modify, execute and analyse iFlow Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your P S I D C user-

## Exercise 1.1 Configure and deploy the Run Business Partner iFlow

After completing these steps you will have modified and deployed the above mentioned iFlow.

1. Log on to the Cloud Integration instance

2. Navigate to `Design -> Integrations and APIs` on the left. 
3. If there are too many entries for scrolling you can search by your user ID to shrink the list
4. Click on your self-created package `Session DT180 -your own user-`
     The details of that package should be shown
5. Click on tab `Artifacts`
6. Click on `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-`

Please note that the integration process has a main integration process with several transforms. The first one is for defining modified headers and the second one is a processDirect call of the standard iFlow for Integration of Business Partners from S/4 to IBP. It is possible to schedule the standard iFlows standalone, but they only can have one configuration. So if there is a need to run the iFlows with different configurations it is better to define wrapper iFlows, like the one you uploaded, which modify the header parameters before they call the standard iFlows. This way every user can have his own set of configuration parameters without interfering with others. Please do not change the configuration of the main iFlows in package `SAP IBP - Integration with SAP S/4HANA Cloud`, but only the configuration of you own wrapper iFlows. Otherwise you risk to make the main iFlows unusable for other users.
<br>![](/exercises/ex1/images/SessionDT180BuPaDefineHeaders.gif)
The rounded boxes around the source values of the headers indicate that the source values are not defined statically, but by externalized parameters, which can be configured. 

8. Click `Configure`. A popup will be opened that shows the configurable parameters of the iFlow.
9. In `Batch Name` the value should be `-your P S I D C user- Run Business Partner: ${header.SAP_MplCorrelationId}`, replace `-your P S I D C user-` by your own user ID
10. Change the value of `Dummy Customer ID` from `-keep default-` to `DUMMY`
11. Set the `Customer Filter` to an empty string
12. The rest of the configuration parameters should be left unchanged.
13. Click `Deploy` on the lower right corner of the screen
16. On the upcoming popup leave the Runtime Profile Cloud Integration as is an click `Yes`
17. A popup is shown with the Deployment information 'Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP ...' is triggered for deployment.
18. After some time there should be another temporary popup saying 'Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP ...' successfully deployed.

## Exercise 1.2 Check the logs of the first iFlow run

After completing these steps you will have a rough idea how to analyse what the actual run of the iFlow did. 
Note: The iFlow is set up in a way that it is triggered once after every new deployment. This is very useful for testing the iFlow. So to start the iFlow again you just need to repeat the deployment step. In a productive environment it is better to schedule the iFlow with a certain frequency or to call it from outside, but this is not part of this exercise. The standard iFlows have a few more configuration parameters, where you can schedule the runs in a periodic manner. There are also some parameters to influence the technical settings for the remote connections. This is also skipped for this exercise setup.

1. To check the results of the run of the iFlow triggered during deployment you should duplicate the tab in the browser
2. In the duplicate tab navigate to `Monitor -> Integrations and APIs` on the left and then `Monitor Message Processing -> All Artifacts` on the right
3. You should be able to find an entry with the Artifact Name `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` quite high in the shown list
4. You can click on that entry and scroll though the content on the right
5. Under `Properties` you can find the `Correlation ID`. Please copy the correlation ID to the clipboard by marking it and typing ctrl-C
6. Then click on field `ID` on the top right corner of the screen and type ctrl-V to set a filter for the correlation ID
7. Then click on the search button on the right of the `ID` field. The result is that only your iFlow and the iFlows that have been called by your iFlow are shown on the screen. All Artifacts shown should have status `Completed`.
8. Click on Artifact Name `SAP IBP Write - Process Posted Data`
The screen should look similar to this one:
<br>![](/exercises/ex1/images/SessionDT180IBPWriteProcessPostedData.gif)
[!NOTE]
As you can see from the screenshot above there should be one entry sent to IBP and processed successfully there. The reason for that is that we have defined a `Dummy Customer ID`, but we set `Customer Filter` to an empty string. This way we only creaded a dummy customer in IBP, but we did not replicate customers from S/4 to IBP, which is only triggered if a filter is defined in `Customer Fliter`. This is why the delivered default value of that field is `0-ZZZ`, which means all customers with an ID that is alphabetically between `0` and `ZZZ` are replicated from S/4 to IBP.
10. Click on artifact `Integrate Business Partners from SAP S4HANA Cloud to SAP IBP`
You should be able to see some `Custom Headers`, at least if you scroll down, and attachment `Parameters` even further down in the list. Please click on the link of attachment `Parameters`. You should be able to see the content of that attachment. If the content is not readable, because all rows are written into the same row you can download the attachment and open it with an editor to read the content. The attachment contains the most important information about which parameters were used when processing the business iFlow `Integrate Business Partners from SAP S4HANA Cloud to SAP IBP`.
The content of the attachment could look like this:
```Customer Filter: 
Dummy Customer ID: DUMMY
Field Extensions: 
Attributes in SAP IBP: CUSTID,CUSTCHANNEL,CUSTCOUNTRY,CUSTDESCR,CUSTREGION
Further Filters: 
Host for SAP S4/HANA Cloud: ...-api.s4hana.ondemand.com
Master Data Prefix: T24
OData Package Size: 50000
```
## Exercise 1.3 Produce and analyse an escalation

1. Switch back to the first tab and navigate to the configuration of iFlow `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` as described in exercise 1.1 above
2. Change the Value of configuration parameter `Field Extensions` to `<CUSTDESCR value="'DUMMY''s description'"/>`. This will overwrite the mapping of field `CUSTDESCR` and set is to `DUMMY's description`
3. Deploy the iFlow again
4. Switch back to the second tab and navigate to `Monitor Message Processing` again
5. Find the latest entry of `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-`
6. Filter by the correlation ID of this new run as described in exercise 1.2

Note that your iFlow and iFlow `SAP IBP Write - Process Posted Data` have status `Escalated`. You also can see from the `Custom Headers` of that Artifact that there was again one entry, but it failed the validation. 
<br>![](/exercises/ex1/images/SessionDT180IBPWriteProcessPostedDataValidationError.gif)
Now let's analyse more in detail what is the issue here.

7. Duplicate the second tab again to create a third one
8. On the new tab navigate to `Monitor -> Integrations and APIs` on the left and `Manage Integration Content -> All` on the right
9. Find iFlow `Integrate Business Partners from SAP S4HANA Cloud to SAP IBP`, evtl. by using a search string (this is the standard one, not your wrapper iFlow)
10. Click on it and check the Log Configuration
11. If the `Log Level` is not `Trace` then change it to `Trace`

[!NOTE]
The log level trace is activated for all users and is deactivated after 15 minutes already. So it might be that someone else already activated the trace level for the iFlow and it also might happen quite often that it is deactivated automatically

12. Switch back to the first tab and deploy iFlow `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` again
13. Switch to the third tab. As long as the status of iFlow `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` is `Starting` click the refresh button
14. Afterwards go to the second tab and refresh the list there until the latest run of `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` is `Completed`
15. Find the corresponding run of iFlow `Integrate Business Partners from SAP S4HANA Cloud to SAP IBP`. If there are several ones within a short timeframe filter by the correlation ID of your iFlow.
16. Double-click it
17. Scroll down to `Logs`
18. The entry `Log Level` should be a link with text `Trace`. Click on it. (If it's not Trace try again to set log level trace for this iFlow on the third tab and make sure it's the right one and redeploy your iFlow.)
19. Click on entry `Delete body from property` in the list of `Run Steps`. This is the last step before `IBP Write - Post Data` is called via ProcessDirect. Please note that the list of `Run Steps` is in descending chronological order (newest on top)
20. Then click on tab `Message Content` on top
21. Click on tab `Payload`

The result should look similar to this:
<br>![](/exercises/ex1/images/SessionDT180IBPWritePostDataPayload.gif)

Note that field `CUSTDESCR` contains string `DUMMY's description`, which contains a single quote. This is not supported in IBP. IBP cannot handle the special characters single and double quote, less than, greater than, carriage return and line feed. But there is a convenient solution to that.

22. Just repeat the steps before, but use Source Value `<CUSTDESCR value="ibp:escape('DUMMY''s description')"/>` for configuration parameter `Field Extensions`
There won't be any validation error any more and if you have a look at the trace again you will find that `CUSTDESCR` has now the value `DUMMY⨩s description`, where the `'` is replaced by a look-alike unicode character `⨩`. The replacement characters for the non-supported characters in IBP are defined in iFlow `Define Default Values for Data Integration Between SAP IBP and SAP S4HANA Cloud` in configuration parameter `Escaped Quotes` and can be adapted if needed.

## Exercise 1.4 Replicate customers from S/4

Till now we only created one dummy customer. Now we also want to replicate business partners of type customer from S/4 to IBP. To do so we need to set a filter
1. Switch back to the first tab and navigate to the configuration of iFlow `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` 
2. Change the Value of configuration parameter `Customer Filter` from the empty string to `1035161-1035164`
3. Change the value of configuration parameter `Field Extensions` from `<CUSTDESCR value="ibp:escape('DUMMY''s description')"/>` to `<CUSTDESCR value="ibp:escape(if (./to_Customer/A_CustomerType/BPCustomerFullName) then ./to_Customer/A_CustomerType/BPCustomerFullName else 'DUMMY''s description')"/>`
4. Deploy the iFlow again
5. Switch back to the second tab and navigate to `Monitor Message Processing` again
6. Find the latest entry of `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-`
7. Filter by the correlation ID of this new run as described in exercise 1.2. All iFlows should have status Completed
8. Switch back to the first tab and deploy iFlow `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` again
9. Switch to the third tab. As long as the status of iFlow `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` is `Starting` click the refresh button
10. On the second tab refresh the `Messages` list until the latest run of `Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-` is Completed
11. Find the corresponding run of iFlow `Integrate Business Partners from SAP S4HANA Cloud to SAP IBP` and navigate to the trace log. If the `Log Level` is not `Trace` activate the trace again on the third tab and repeat steps 8 to 11.
12. Click on entry `Delete body from property` in the list of `Run Steps`. This is the last step before `IBP Write - Post Data` is called via `ProcessDirect`
13. Then click on tab `Message Content` on top
14. Click on tab `Payload`

You should see five items with `CUSTID` equal to `1035161`, `1035162`, `1035163`, `1035164` and `DUMMY` and different values in `CUSTDESCR`

## Summary

You've now learned the basics on how you can analyse the run of an iFlow

Continue to - [Exercise 2 - Configure, deploy and analyse Run Integrate Plants...](../ex2/README.md)

