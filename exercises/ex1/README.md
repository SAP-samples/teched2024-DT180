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
8. Double-click on transform Define Modified Headers
9. On the bottom part of the screen a subscreen called Content Modifier is shown. Click on tab Message Header there
10. Scroll down until you find a row with Name BatchName
11. The Source Value is -your P S I D C user- Basic Run Business Partner: ${header.SAP_MplCorrelationId}. Please replace -your P S I D C user- with your own user ID
12. The rest of the headers can be left unchanged.
13. Click Deploy on the top right corner of the screen
14. On the upcoming popup leave the Runtime Profile Cloud Integration as is an click Yes
15. A popup is shown with the Deployment information 'Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP ...' is triggered for deployment.
16. After some time there should be another temporary popup saying 'Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP ...' successfully deployed.

## Exercise 1.2 Check the logs of the first iFlow run

After completing these steps you will have a rough idea how to analyse what the actual run of the iFlow did. 
Note: The iFlow is set up in a way that it is triggered once after every new deployment. This is very useful for testing the iFlow. So to start the iFlow again you just need to repeat the deployment step. In a productive environment it is better to schedule the iFlow with a certain frequency or to call it from outside, but this is not part of this exercise.

1. To check the results of the run of the iFlow triggered during deployment you should duplicate the tab in the browser
2. In the duplicate tab navigate to Monitor -> Integrations and APIs on the left and then Monitor Message Processing -> All Artifacts on the right
3. You should be able to find an entry with the Artifact Name 'Basic Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your own user-' quite high in the shown list
4. You can click on that entry and scroll though the content on the right
5. Under Properties you can find the Correlation ID. Please copy the correlation ID to the clipboard by marking it and typing ctrl-C
6. Then click on field ID on the top right corner of the screen and type ctrl-V to set a filter for the correlation ID
7. Then click on the search button on the right of the ID field. The result is that only your iFlow and the iFlows that have been called by you iFlow are shown on the screen
7. Click on Artifact Name SAP IBP Write - Process Posted Data
The screen should look similar to this one:
<br>![](/exercises/ex1/images/SessionDT180IBPWriteProcessPostedData.gif)

## Summary

You've now ...

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)

