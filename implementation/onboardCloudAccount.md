  - [Onboard accounts to Dome9](#onboard-accounts-to-dome9)
  - [What it does](#what-it-does)
  - [Setup](#setup)
      - [Prerequisites](#prerequisites)
      - [Parameters](#parameters)
  - [Usage examples](#usage-examples)

# Onboard accounts to Dome9

# What it does

This script does the following:
- Onboard an AWS or Azure account to
Dome9
- Attach the onboarded account to an OU
- Attach the view role to
the account
- Attach the admin role to the account

# Setup

## Prerequisites

  - Dome9 API Key ID and secret (see [here](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk144514&partition=General&product=CloudGuard) for details how to generate these using the Dome9 Web app)
  - Python 2.7 or later
  - Python modules:
      - dome9ApiV2Py
      - requests

## Parameters

  - **dome9ApiKeyID** (String): Dome9 API key ID
  - **dome9ApiKeySecret** (String): Dome9 API Key secret
  - **cloudVendorType** (String): type of cloud account vendor: *aws*, or *azure*
    AWS account
  - **dome9OuID** (String, optional): Organization Unit ID to which the
    cloud account will be attached (to obtain this ID, use the
    [Organization Unit
    method](https://api-v2-docs.dome9.com/#Dome9-API-OrganizationalUnit)
    in the Dome9 REST API)
  - **dome9CloudAccountName** (String, optional): account name as it will appear on the Dome9 console, default is *account-randomString*
  - **dome9AdminRoleID** (String, optional): Dome9 admin role ID to
    attach to the account (to obtain this ID, use the [Role
    method](https://api-v2-docs.dome9.com/#Dome9-API-Role) in the Dome9
    REST API)
  - **dome9ViewRoleID** (String, optional): Dome9 view (read) role ID to
    attach to the account (to obtain this ID, use the [Role
    method](https://api-v2-docs.dome9.com/#Dome9-API-Role) in the Dome9
    REST API)
	
	For AWS accounts use these parameters:
	
  - **awsRoleArn** (String): the ARN of the *Dome9-Connect* role in your
  - **awsRoleExternalID** (String): the external ID value used to create
    the role in your AWS account
  - **awsAllowReadOnly** (String, optional): set to True to onboard the account to 
    *Read-Only* mode, and False to onboard it to  *Full Protection* mode; default is True (*Read-Only*)
  - **awsFullProtection** (String, optional): set to True to set the
    Security Groups in the account to *Full-Protection* in the course of
    onboarding, or False to leave the Security Groups in *Read-Only*
    mode; default is False (*Read-Only*)
	
	For Azure accounts, use these:
	
  - **azureSubscriptionID** (String): Azure subscription ID
  - **azureActiveDirectoryID** (String): Azure
    Active Directory ID\\tenant ID
  - **azureApplicationID** (String): Azure Application ID
  - **azureSecretKey** (String): Azure Secret Key
  - **azureOperationMode** (String): Azure operation mode,
    *Read* or *Manage*; default is Read
	

# Usage examples

**Onboard an AWS account to Read-Only mode, with Admin role and OU:**

`onboardCloudAccount.py --dome9ApiKeyID sdfsdfssdf --dome9ApiKeySecret
sdfsdfssdf --cloudVendorType aws --awsRoleArn
arn:aws:iam::111111111:role/Dome9-Connect --awsRoleExternalID sdfsdfsdff
--dome9OuID e21b3e8b-e02f-46df-bd70-8ce65ca8a3a5 --dome9CloudAccountName
production --dome9AdminRoleID 118187 --dome9ViewRoleID 118203`

**Onboard an Azure account to Managed mode, with Admin role and OU:**

`onboardCloudAcoount.py --dome9ApiKeyID ddsfsdfsdf --dome9ApiKeySecret
sdfsdfssdf --cloudVendorType azure --azureSubscriptionID sdfsdfsdfsdfsd
--azureActiveDirectoryID sdfsdsdfsdsdfsd --azureApplicationID
sfsdfsdfsfdsdf --azureSecretKey sdfsfsfsfd
--dome9OuID 92f9a334-bf29-48a5-9cf8-66a10efe51e6 --dome9CloudAccountName
production --dome9AdminRoleID 118881 --dome9ViewRoleID 118901
--azureOperationMode Manage`
