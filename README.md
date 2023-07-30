# Migration-project-between-Azure-DevOps-Cloud


  

# Services/Tools used in the project:

- Git

- Azure DevOps Services

- [Azure DevOps Migration Tools](https://nkdagility.com/learn/azure-devops-migration-tools/) developed by (Martin Hinshelwood)

  
  
# Steps:


* [Introduction](#introduction)

 

* [Getting Environment Ready](#getting-environment-ready)

* [Preparing The Destination Project](#preparing-the-destination-project)

*  [Preparing The Destination Project](#preparing-the-destination-project)

*  Preparing JSON File

*  Migrate Work Iterations

* Migrating Work Items

* Migrating Links between Work Items

* Migrating Attachments

* Conclusion

  

# Introduction

Using the Azure DevOps Migration Tools to migrate a project from the source organization to the destination organization, which includes Work Items, Test Plans & Suits, Teams, and Shared Queries.

  

#  Getting Environment Ready

Before starting the migration, make sure to have

  

### 1. Download & Install [Azure DevOps Migration Tools](https://marketplace.visualstudio.com/items?itemName=nkdagility.vsts-sync-migration)

 

1.1 Install

In order to run the migration you will need to install the tools first.

  

1. Install Chocolatey from https://chocolatey.org/install

2. Run `choco install vsts-sync-migrator` to install the tools [source](https://community.chocolatey.org/packages/vsts-sync-migrator)

The tools are now installed. To run them, you must switch to `c:\tools\MigrationTools\` and `run migration.exe`.

  

1.2 Upgrade

Run `choco upgrade vsts-sync-migrator` to upgrade the tools [source](https://community.chocolatey.org/packages/vsts-sync-migrator)

1.3 Server configuration and setup


### 2. Create a default configuration file

1.  Open a command prompt or PowerShell window at  `C:\tools\MigrationTools\`
2.  Run  `./migration.exe init`  to create a default configuration
3.  Open  `configuration.json`  from the current directory

Reference: https://nkdagility.com/learn/azure-devops-migration-tools/getting-started/

#  Preparing The Destination Project

#### Migration State:

In order to store the state for the migration you need to use a custom field, the  `ReflectedWorkItemId`  field which needs added to the Target only. 

1. Open your **Azure organization setting**
2. Open **Process Settings**

![Process](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/c49931d5-a8c3-435e-83ee-0c4c70b4358e)
3. Open Your **Inherited Process Settings**

![InheritedProcess](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/a2b6d8d8-66e0-4008-a7a6-d2ed7ade562d)
4. For Each Work Item Type, Open it and repeat the following steps

![WorkItem](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/2628e2f4-9a75-41f1-a9dd-8687ad0f8913)

5. Click **Add New**

6. In the New Field Dialog, Set the New Field name to be **ReflectedWorkItemId**

7. Make sure it’s of Type **Text Single Line**
8. Click **Add Field**

![ReflectedWorkItemId](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/0a4d910f-47a4-4b77-a6d5-0a5266e33b42)

Make sure you have added the field to all Work Item Types, You can check the Work Items (to make sure you have added the field) by Going to Your Inherited Process and check every work Item.


![CheckReflectedWoekItemID](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/bbfb0da0-4b7e-4757-97c0-7b1c81561afe)


Refernce: https://docs.microsoft.com/en-us/azure/devops/organizations/settings/work/add-custom-field?view=azure-devops
