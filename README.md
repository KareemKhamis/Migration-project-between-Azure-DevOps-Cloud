# Migration-project-between-Azure-DevOps-Cloud


  

# Services/Tools used in the project:

- PowerShell

- Azure DevOps Services

- [Azure DevOps Migration Tools](https://nkdagility.com/learn/azure-devops-migration-tools/) developed by (Martin Hinshelwood)

  
  
# Steps:


* [Introduction](#introduction)

* [Getting Environment Ready](#getting-environment-ready)

* [Preparing The Destination Project](#preparing-the-destination-project)

* [Preparing JSON File](#preparing-json-file)

* [Migrate Test Cases](#migrate-test-cases)

* [Migrate Test Suits and Test Plans](#migrate-test-suits-andtestplans) 

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




### 2. Create a default configuration file

1.  Open a command prompt or PowerShell window at  `C:\tools\MigrationTools\`
2.  Run  `./migration.exe init`  to create a default configuration
3.  Open  `configuration.json`  from the current directory

Reference: https://nkdagility.com/learn/azure-devops-migration-tools/getting-started/

#  Preparing The Destination Project

#### 1. Migration State:

In order to store the state for the migration you need to use a custom field, the  `ReflectedWorkItemId` field, which needs to be added to the Target only. 

1. Open your **Azure organization setting**
2. Open **Process Settings**

![Process](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/c49931d5-a8c3-435e-83ee-0c4c70b4358e)
3. Open Your **Inherited Process Settings**

![InheritedProcess](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/a2b6d8d8-66e0-4008-a7a6-d2ed7ade562d)
4. For Each Work Item Type, Open it and repeat the following steps

![WorkItem](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/2628e2f4-9a75-41f1-a9dd-8687ad0f8913)

5. Click **New Field**

6. In the Create Field Dialog, Set the New Field name to **ReflectedWorkItemId**

7. Make sure it’s of Type **Text Single Line**
8. Click **Add Field**

![ReflectedWorkItemId](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/0a4d910f-47a4-4b77-a6d5-0a5266e33b42)

Make sure you have added the field to all Work Item Types, You can check the Work Items (to make sure you have added the field) by Going to Your Inherited Process and checking every work Item.


![CheckReflectedWoekItemID](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/bbfb0da0-4b7e-4757-97c0-7b1c81561afe)


Reference: https://docs.microsoft.com/en-us/azure/devops/organizations/settings/work/add-custom-field?view=azure-devops

##### 2.Process Customization:
In this step, I customized the Inherited Agile process template as required : 
1.  **Building a field customization layout**:

1.1. Open your **Azure organization setting**

1.2. Open **Process Settings**

![Process](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/c49931d5-a8c3-435e-83ee-0c4c70b4358e)
1.3. Open Your **Inherited Process Settings**

![InheritedProcess](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/a2b6d8d8-66e0-4008-a7a6-d2ed7ade562d)
1.4 For Each Work Item Type, Open it and repeat the following steps

![WorkItem](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/2628e2f4-9a75-41f1-a9dd-8687ad0f8913)
1.5 Click on the dots at the inherited group 

1.6 Click **New Field**

![DoCustomField1](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/f2bc1d05-42f2-4e5c-9ee5-b64b25692712)

1.7 In the Create Field Dialog, Set the New Field name to **Business Team**

1.8 Make sure it’s of Type **Text Single Line**

1.9 Click **Add Field**

![DoCustomField2](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/e256a355-9183-4a31-b813-12e145e3b4ea)

You can check the Work Items (to make sure you have customized the layout) by Going to Your Inherited Process and checking every work Item layout.


![AfterFieldCustom](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/58362d4d-852c-4119-be6a-fef1f7f6acaa)

Note: Repeat the field customization layout process for each work item in the inherited process template in the destination project as required..

2.  **Build & Customize the States**:

2.1 Open your **Azure organization setting**

2.2 Open **Process Settings**

![Process](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/c49931d5-a8c3-435e-83ee-0c4c70b4358e)
2.3 Open Your **Inherited Process Settings**

![InheritedProcess](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/a2b6d8d8-66e0-4008-a7a6-d2ed7ade562d)
2.4 For Each Work Item Type, Open it and repeat the following steps

![WorkItem](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/2628e2f4-9a75-41f1-a9dd-8687ad0f8913)

2.5 Click on **States**

2.6 Click on **New state**

2.7 In the Name Dialog, Set the New State name to **Development**

2.8 In the Name State category, Set the New State name to **In Progress**

2.9 In the Color category, Set the desired **Color**

2.10 Click **Create**

![StateCustom](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/91498587-527e-427c-a0e7-8324e9db3987)

I can check the Work Items (to make sure you have customized the States) by Going to Your Inherited Process and checking every work Item States.

![AftterStateCustom](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/1a478950-a257-420d-a363-53ac56d7706d)

Note: Repeat the State customization layout process for each work item in the inherited process template in the destination project as required.

#  Preparing JSON File

Navigate to `C:\tools\MigrationTools` then Open `configuration.json` from the current directory
1. In `Endpoints`, I set the values for the **Source Project**:

`Organization`: **Organization URL**

`Project`: **Source Project Name** 

`AuthenticationMode`: **Access type name**

`AccessToken`:  **XXXXXXX**

2. In `Endpoints`, I set the values for the **Target Project**

`Organization`: **Organization URL**

`Project`: **Target Project Name** 

`AuthenticationMode`: **Access type name**

`AccessToken`:  **XXXXXXX**


3. In `ChangeSetMappingFile`, I set the values for the **Source Project**

`Collection`: **Organization URL**

`Project`: **Source Project Name** 

`AuthenticationMode`: **Access type name**

`AccessToken`:  **XXXXXXX**

4. In `ChangeSetMappingFile`, I set the values for the **Target Project**

`Collection`: **Organization URL**

`Project`: **Target Project Name** 

`AuthenticationMode`: **Access type name**

`AccessToken`:  **XXXXXXX*

![json1](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/f6c2ecff-6d86-4ecf-b2d7-096b8beaf222)

5. In `FieldMaps`, I used the `FieldMergeMapConfig` method for each work item to store the Archived data from the source project into a specific layout page into the source project

`"$type": "FieldMergeMapConfig"` (In case of migration of multiple fields, use this mapping method)

`WorkItemTypeName`: **Work item name** 
  
`sourceFields`: **Field Reference Name** I got the Field Reference Name from the inherited process of the source project.

`targetField`: **Field Reference Name** In this dialogue, I have created a **New page** with a **New field** with the name: **Data Archived from Old project** to store the archived data from the source project. 

formatExpression: I have listed the names of the unused fields which will be reflected in the Data Archived layout page of the target project.

6. In `FieldMaps`, I used the `FieldValueMapConfig` method for each work item to configure & value mapping the states for each work item*

![Fieldmapping](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/15b5f359-fe7d-49f7-b4e7-488d405b8d6d)

7. `Processors` are the control units for migration, each processor controls the migration of a specific part of Azure DevOps Project.
**Remember:** If you want a processor to run, its `Enabled` attribute must be set to `true`

8. Each processor has an `Enabled` attribute, which is either  `true` or `false`, if it’s enabled (`true`) then this processor will be executed during migration.
   
9. Modify the  `WIQLQueryBit`  to migrate only the work items you want. The default WIQL will migrate all open work items and revisions excluding test suites and plans

10. For Attachments migration configuration:
`"LinkMigration"`: `true`,
`"AttachmentMigration"`: `true`,
"AttachmentWorkingPath":`"c:\\temp\\WorkItemAttachmentWorkingFolder\\"` 

![Processors](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/c96364b9-5d7e-4e46-add4-6f8b74873c3a)


# Migrate Test Cases

I started the migration with **Test Cases** along with their attachments to the Target Project, This is its configuration at the Processors in the JSON file: `"WIQLQueryBit": "AND [System.WorkItemType] = 'Test Case'` "

![TestCaseBeforeMigration](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/dc61090e-96ea-4b41-9f2b-57786165a74f)

2. Now To Migrate **Test Cases**, Let’s get back to the JSON File:
* Enable the  `WorkItemMigrationConfig`  processor by setting  `Enabled`  to  `true`
* Set `"WIQLQueryBit"`: `"AND [System.WorkItemType]` = `'Test Case'` "`
  
![TestcaeJson](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/549ed61b-9069-4d86-91b3-b7af28be3e70)

3. From the `C:\tools\MigrationTools\` path, run `.\migration.exe execute --config .\configuration.json`

![TestCasePowrershell](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/0651d6f6-6787-4b5c-812e-939f10168454)

4. Once finished you’ll see something like this:

![TestCasesJSONdone (2)](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/64f74b4b-c72e-4995-b26b-1e72e40a54a7)

Here is how the Target Project Looks like after Migration

![TestCasesAfterMigration](https://github.com/KareemKhamis/Migration-project-between-Azure-DevOps-Cloud/assets/96993017/2cfdfc03-968e-4d93-83a3-89affd8720e0)


 # Migrate Test Suits and Test Plans  
