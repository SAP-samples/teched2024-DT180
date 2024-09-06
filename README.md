# teched2024-DT180 - Integrating SAP S/4HANA Cloud with SAP IBP using SAP Integration Suite

## Description

This repository contains the material for the SAP TechEd 2024 session called DT180 - Integrating SAP S/4HANA Cloud with SAP IBP using SAP Integration Suite.  

## Overview

This session introduces attendees to the SAP Integration Suite part of the demand planning integration between SAP S/4HANA Cloud Public Edition and SAP Integrated Business Planning for Supply Chain (SAP IBP).
The SAP IBP solution holds a breadth of ERP information that is critical for many supply chain planning scenarios. SAP S/4HANA Cloud Public Edition stands as a system of record and is important for planning data in SAP IBP. As a result, the need for integrating SAP IBP with SAP S/4HANA is critical for customers. Learn how to setup, configure and run this integration in SAP Integration Suite using interfaces in SAP IBP to exchange volumes of data with SAP S/4HANA Cloud Public Edition.

## Requirements

The requirements to follow the exercises in this repository are:
- Set up an Integration Suite Trial as described here: https://developers.sap.com/tutorials/cp-starter-isuite-onboard-subscribe..html
- In the BTP Cockpit navigate to your trial subaccount and then to Security -> Users
- Click on your user
- If on the right the role collection PI_Integration_Developer is not assigned do the following:
  - On the right click on Assign Role Collection
  - Mark entry PI_Integration_Developer
  - Click on Assign Role Collection
 
Note: Please be aware that these settings will only allow you to discover, configure, deploy and run the Integration Suite iFlows. As long as you don't connect a fitting S/4 and IBP system the iFlows will throw exceptions due to connection errors.
So if you want to run the integration end to end you need test systems of type S/4HANA Cloud Public Edition and SAP IBP. For S/4HANA the trial version is not allowing integration scenarios and for SAP IBP there is no trial version. But if you have such test systems available and the needed authorizations in both systems to setup the communication you can follow the description in Best Practices ConConfigure tent 
IBP for demand – demand forecast for SAP S/4HANA Cloud, public edition (78P) (https://me.sap.com/processnavigator/SolS/EARL_SolS-034/2408/SolP/78P)
This will allow you to run the whole process end to end.

## Exercises

Provide the exercise content here directly in README.md using [markdown](https://guides.github.com/features/mastering-markdown/) and linking to the specific exercise pages, below is an example.

- [Getting Started](exercises/ex0/)
- [Exercise 1 - Discover and copy the needed integration packages](exercises/ex1/)
    - [Exercise 1.1 - Exercise 1 Sub Exercise 1 Description](exercises/ex1#exercise-11-sub-exercise-1-description)
    - [Exercise 1.2 - Exercise 1 Sub Exercise 2 Description](exercises/ex1#exercise-12-sub-exercise-2-description)
- [Exercise 2 - Second Exercise Description](exercises/ex2/)
    - [Exercise 2.1 - Exercise 2 Sub Exercise 1 Description](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Exercise 2.2 - Exercise 2 Sub Exercise 2 Description](exercises/ex2#exercise-22-sub-exercise-2-description)
- Get an overview on the available reusable iFlows
- Configure the iFlow for defining default settings
- Configure, deploy and schedule the iFlow for plant replication
- Analyse the error log
- Change the configuration concerning filtering by plant
- Create and deploy a wrapper iFlow calling the plant iFlow with deviating settings
  
**OR** Link to the Tutorial Navigator for example...

Start the exercises [here](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).

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
