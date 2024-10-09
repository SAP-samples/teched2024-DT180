# Exercise 5 - Configure, deploy and analyse Run Integrate KFs from SAP IBP to SAP S4HANA Cloud...

In this exercise, we will configure, deploy and analyse iFlow `Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your own user-`

## Exercise 5.1 Configure and deploy the Run KFs iFlow

After completing these steps you will have modified and deployed the above mentioned iFlow.

1. On the first tab open iFlow `Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your own user-`
2. Click `Configure`. A popup will be opened that shows the configurable parameters of the iFlow.
3. Change the value of `Key Figure Name` from `-keep default-` to `ACTUALSQTY`
4. The rest of the configuration parameters should be left unchanged.
5. Click `Deploy` on the lower right corner of the screen
6. On the upcoming popup click `Yes`
7. Switch to the second tab opened in exercise 1 and navigate to `Monitor -> Integrations and APIs, Monitor Message Processing -> All Artifacts`
8. Update the display if needed
9. Filter by the correlation ID of the run of your iFlow `Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your own user-`
10. All iFlows belonging to the correlation ID shall have status `Completed`
11. Click on iFlow `SAP IBP Read - Initialize`
12. Find and open attachment `4IBPReadRequestsResults`
13. If the content is not readable click `Download` on the right and open the downloaded file in an editor
14. Under node `Messages.Message0.IBPRead` you should find an atribute `Rows` with value `915`
15. Open Message `SAP IBP Read - Close`
16. Under `Properties` have a look at the `Custom Headers`, especially `IBP Read Close Message 1.1` to `IBP Read Close Message 1.3`, which contain some run time statistics

## Exercise 5.2 Change the time aggregation to Month

After completing these steps you will be able to run the integration of key figures as PIRs on monthly level

1. On the first tab configure iFlow `Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your own user-`
2. Change configuration parameter `Period Type` from `Week` to `Month`
3. Change configuration parameter `Period Type - Time Profile Level` from `3` to `4`
4. Deploy the iFlow again
5. Switch to the second tab and navigate to `Monitor -> Integrations and APIs, Monitor Message Processing -> All Artifacts`
6. Update the display if needed
7. Filter by the correlation ID of the latest run of your iFlow `Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your own user-`
8. All iFlows belonging to the correlation ID shall have status `Completed`
9. CLick on iFlow `SAP IBP Read - Initialize`
10. Find and open attachment `4IBPReadRequestsResults`
11. If the content is not readable click `Download` on the right and open the downloaded file in an editor
12. Under node `Messages.Message0.IBPRead` you should find an atribute `Rows` with the lower value `256`. This is due to the fact that we only replicate one entry per month, not per week. Feel free to check the output of the IBP system and the input to the S/4 system in the trace log of iFlow `Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements`

## Exercise 5.3 Lower the package size, so that several fetches are needed

After completing these steps you will be able to lower the package size and analyse how several package are handled

1. On the first tab configure iFlow `Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your own user-`
2. Change configuration parameter `Package Size in Rows` from `100000` to `50`
3. Deploy the iFlow again
4. Switch to the second tab and navigate to `Monitor -> Integrations and APIs, Monitor Message Processing -> All Artifacts`
5. Update the display if needed
6. Filter by the correlation ID of the latest run of your iFlow `Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your own user-`
7. All iFlows belonging to the correlation ID shall have status `Completed`
8. There should be 6 messages of type `SAP IBP Read - Fetch Data`. The reason is that there were more data selected than are fitting in one package, so the fetch had to be executed six times.
9. If you want to you can double check that the number of selected rows is still the same as before

## Summary

You've now learned to configure and deploy the iFlow for repilcating key figures as PIRs to S/4 and some of it's configuration parameters.

This will end the exercises of this session.


