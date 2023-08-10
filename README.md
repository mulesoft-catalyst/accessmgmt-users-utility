Table of Contents
=================

   * [Table of Contents](#table-of-contents)
   * [Access Management Utility - Users](#access-management-utility---users)
      * [Utility Details](#utility-details)
      * [Requirements](#requirements)
      * [Steps to configure and test the utility](#steps-to-configure-the-utility)


# Access Management Utility - Users

This utility is a MuleSoft application intended to manage those users who have not logged in to the Anypoint Platform for the past configurable number of days. Following are the operations included in this utility.
* Disable the users
* Delete the users

## Utility Details
This utility is a MuleSoft application with 2 scheduler flows - one to disable the users, and the other to delete the users.
For both the operations, disabled/deleted user details are captured in the logs. Sample below.

```json
{
    "message": "The following users have been DISABLED.",
    "disabledUserCount": 1,
    "disabledUsers": [
        {
            "userEmail": "max.mule@mulesoft.com",
            "userName": "max_mule",
            "lastLogin": "2019-04-23T16:01:59.387Z",
            "userId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        }
    ]
}
```

## Requirements
* Mule Runtime 4.2.2 or above
* Anypoint Platform credentials - A Connected App (client credentials) with below scopes for the appropriate business groups
    * View Users in a particular organization
    * Edit users in an organization

## Steps to configure the utility
* Clone or download the project from GitHub ``` git clone git@github.com:mulesoft-catalyst/accessmgmt-users-utility.git ```
* Adjust below properties
    ```yaml
    platform:
      orgid: "<orgId>"
    connectedapp:
      client_id: "<client_id>"
      client_secret: "<client_secret>"
    userlastlogin:
      deletedays: "<number_of_days>"
      disabledays: "<number_of_days>"
    schedule:
      disableusers: <cron-expression>
      deleteusers: <cron-expression>
    ```
    * ```userlastlogin.deletedays``` and ```userlastlogin.disabledays``` represent the number of days since the user has not logged in.
    * ```schedule.disableusers``` and ```schedule.deleteusers``` represent the cron expression to execute the schedules for both the operations. We recommend to have the schedule execute in such a way that users are first disabled, and then deleted.
* Default configurations are defined in ``` /src/main/resources/properties.yaml ```
* Make sure to encrypt all sensitive data using the Secure Properties Module: https://docs.mulesoft.com/mule-runtime/4.4/secure-configuration-properties.



*This is an UNLICENSED software. If you need assistance on extending this application, contact your MuleSoft Customer Success representative or MuleSoft Professional Services. Alternatively, you can customize this application as per your requirements.*
