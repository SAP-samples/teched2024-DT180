# Exercise 1 - Discover and copy the needed integration packages

In this exercise, we will discover the needed integration packages and copy them to the design area

## Exercise 1.1 Sub Exercise 1 Description

After completing these steps you will have created copies of the needed integration packages in your design area.

1. Log on to the Cloud Integration instance
To do so is to start in the BTP Cockpit and navigate from your Global Account to Subaccount trial.
Then go to Instances and Subscriptions and click on Integration Suite.
It could be a good idea to create a bookmark for the Integration Suite page.

2. Navigate to Discover -> Integrations on the left. 
     If the category Discover is not available please check if you have assigned role collection PI_Integration_Developer as described in the prerequisites
3. In the search field enter IBP and click the search button on the right of the search field or press enter
     About half a dozen of integration packages should show up
4. Click on SAP IBP - Reusable Integration Flows  
     The details of that package should be shown
5. Click on Copy
     For a short moment a popup message Package copied should be shown 
     If the package was already copied before an error will be shown, as configuration only integration packages only can be copied once
6. Navigate back to Discover (Integrations)
7. Repeat steps 4 to 6 for integration package SAP IBP - Integration with SAP S/4HANA Cloud
8. Navigate to Design -> Integrations and APIs
     The two integration packages copied in the steps above should be visible here
     
10.   Click here.
<br>![](/exercises/ex1/images/01_01_0010.png)

11.	Insert this line of code.
```abap
response->set_text( |Hello World! | ). 
```



## Exercise 1.2 Sub Exercise 2 Description

After completing these steps you will have...

1.	Enter this code.
```abap
DATA(lt_params) = request->get_form_fields(  ).
READ TABLE lt_params REFERENCE INTO DATA(lr_params) WITH KEY name = 'cmd'.
  IF sy-subrc <> 0.
    response->set_status( i_code = 400
                     i_reason = 'Bad request').
    RETURN.
  ENDIF.

```

2.	Click here.
<br>![](/exercises/ex1/images/01_02_0010.png)


## Summary

You've now ...

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)

