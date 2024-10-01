# Getting started

For getting started we will upload the needed integration flows.

## Level 2 Heading

After completing these steps you will have uploaded all integration flows needed for the exercises into the integration content package you already created in the prerequisites step

1. Download all the zip files from directory IntegrationFlows:
 - [Basic Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your P S I D C user-.zip](/IntegrationFlows/BasicRunIntegrateBusinessPartnersFromSAPS4HANACloudToSAPIBP-yourPSIDCuser-.zip)
 - [Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your P S I D C user-.zip](/IntegrationFlows/RunIntegrateBusinessPartnersFromSAPS4HANACloudToSAPIBP-yourPSIDCuser-.zip)
3.	Navigate to Design -> Integrations and APIs
<br>![](/exercises/ex0/images/00_00_0010.png)

4.	Click on package Session DT180 -your pseudonym-
5.	Click button Edit
6.	Click tab Artifacts
7.	On drop-down-box Add choose sub entry Integration Flow
8.	Choose radio button Upload
9.	Click on Browse...
10.	Choose file Basic Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your P S I D C user-.zip
11.	Replace -your P S I D C user- by your user ID in field Name of the to be created integration flow (iFlow)
12.	Click Add
13.	Repeat steps 7 to 12 for the following files:
- Run Integrate Plants from SAP S4HANA Cloud to SAP IBP -your P S I D C user-.zip
- Run Integrate Products etc from SAP S4HANA Cloud to SAP IBP -your P S I D C user-.zip
- Run Integrate Business Partners from SAP S4HANA Cloud to SAP IBP -your P S I D C user-.zip
- Run Integrate Sales Order History from SAP S4HANA Cloud to SAP IBP -your P S I D C user-.zip
- Run Integrate KFs from SAP IBP to SAP S4HANA Cloud as Planned Independent Requirements -your P S I D C user-.zip
    
``` abap
 DATA(params) = request->get_form_fields(  ).
 READ TABLE params REFERENCE INTO DATA(param) WITH KEY name = 'cmd'.
  IF sy-subrc <> 0.
    response->set_status( i_code = 400
                     i_reason = 'Bad request').
    RETURN.
  ENDIF.
```

## Summary
The result of the steps above should look similar to this, except that -your P S I D C user- should be replaced by your own user ID everywhere:
<br>![](/exercises/ex0/images/00_00_0010.png)
Now that you have created all the needed integration flows
Continue to - [Exercise 1 - Exercise 1 Description](../ex1/README.md)
