# Getting started

For getting started we will upload the needed integration flows.

## Level 2 Heading

After completing these steps you will have uploaded all integration flows needed for the exercises into the integration content package you already created in the prerequisites step

1. Download all the zip files from directory [IntegrationFLows](/IntegrationFLows)
2.	Navigate to Design -> Integrations and APIs
<br>![](/exercises/ex0/images/00_00_0010.png)

3.	Click on package Session DT180 -your identifier-
4.	Click button Edit
5.	Click tab Artifacts
6.	On drop-down-box Add choose sub entry Integration Flow
7.	Choose radio button Upload
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

Now that you have created all the needed integration flows
Continue to - [Exercise 1 - Exercise 1 Description](../ex1/README.md)
