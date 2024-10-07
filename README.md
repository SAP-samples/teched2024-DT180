# DT180 - Integrating SAP S/4HANA Cloud with SAP IBP using SAP Integration Suite

## Description

This repository contains the material for the SAP TechEd 2024 session called DT180 - Integrating SAP S/4HANA Cloud with SAP IBP using SAP Integration Suite.  

## Overview

This session introduces attendees to the SAP Integration Suite part of the demand planning integration between SAP S/4HANA Cloud Public Edition and SAP Integrated Business Planning for Supply Chain (SAP IBP).
The SAP IBP solution holds a breadth of ERP information that is critical for many supply chain planning scenarios. SAP S/4HANA Cloud Public Edition stands as a system of record and is important for planning data in SAP IBP. As a result, the need for integrating SAP IBP with SAP S/4HANA is critical for customers. Learn how to setup, configure and run this integration in SAP Integration Suite using interfaces in SAP IBP to exchange volumes of data with SAP S/4HANA Cloud Public Edition.

## Requirements

The requirements to follow the exercises in this repository are:
- You need an SAP user (type P,S,I or D)
- You need to register yourself in the booker app with an email that was not used for another user already: [TechEd Tenant Booker Application](https://techedtenantbookerapplication-ad5b9d48b.dispatcher.hana.ondemand.com/index.html)

- Navigate from the booker tool to the Integration Suite instance you are assigned to by clicking the corresponding link
- Optionally you can bookmark the opened Integration Suite url for later direct access
- Create your own integration content package the following way:
  - Navigate to Design -> Integrations and APIs
  - Click button Create
  - Fill field Name with the following content: Session DT180 -your P/S/I/D/C user-
      - -your P/S/I/D/C user- should be the SAP user you used in the booker app
      - We will reuse -your P/S/I/D/C user- later on for other objects as well
  - Fill field Short Description with 'Wrapper iFlows for Session DT180', for example
  - Click Save  
 
Note 1: Please be aware that you are only allowed to access the SAP Integration Suite in the setup for these exercises. There are an S/4 and an IBP system connected and data can be transfered from S/4 to IBP, but you won't be able to access the S/4 and IBP systems. The back integration from IBP to S/4 is not supported in this test setup.
If you have test systems of type Integration Suite, S/4HANA Cloud Public Edition and SAP Integrated Buisiness Planning for Supply Chain available and the needed authorizations in both systems to setup the communication you can follow the description in Best Practices Content 
IBP for demand – demand forecast for SAP S/4HANA Cloud, public edition (78P) (https://me.sap.com/processnavigator/SolS/EARL_SolS-034/2408/SolP/78P)
This will allow you to go through all the setup steps and run the whole process end to end including the steps needed in S/4 and IBP. You also will be able to check the results of the integration in the corresponding target system.

Note 2: The iFlows of package SAP IBP - Integration with SAP S/4HANA Cloud have a lot of configuration parameters that influence their behavior and we will learn about some of those parameters in the exercises below. Most of the parameters also can be set as headers before calling the iFlows. This is what we mainly do in the exercises below. You own iFlows have similar configuration parameters as the main iFlows and overwrite the default values if needed. If you are uncertain about the behavior or possible values of some parameters the package SAP IBP - Integration with SAP S/4HANA Cloud contains documents describing the configuration parameters of all the contained iFlows.

## Exercises

- [Getting Started](exercises/ex0/)
- [Exercise 1 - Configure, deploy and analyse Run Integrate Business Partners...](exercises/ex1/)
    - [Exercise 1.1 - Configure and deploy the Run Business Partner iFlow](exercises/ex1#exercise-11-configure-and-deploy-the-run-business-partner-iflow)
    - [Exercise 1.2 - Check the logs of the first iFlow run](exercises/ex1#exercise-12-check-the-logs-of-the-first-iflow-run)
    - [Exercise 1.3 - Produce and analyse an escalation](exercises/ex1#exercise-13-produce-and-analyse-an-escalation)
- [Exercise 2 - Second Exercise Description](exercises/ex2/)
    - [Exercise 2.1 - Exercise 2 Sub Exercise 1 Description](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Exercise 2.2 - Exercise 2 Sub Exercise 2 Description](exercises/ex2#exercise-22-sub-exercise-2-description)
- Get an overview on the available reusable iFlows
- Configure the iFlow for defining default settings
- Configure, deploy and schedule the iFlow for plant replication
- Analyse the error log
- Change the configuration concerning filtering by plant
- Create and deploy a wrapper iFlow calling the plant iFlow with deviating settings
  

**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 

## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct
Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2024 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
