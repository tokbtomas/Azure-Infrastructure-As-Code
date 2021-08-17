* ## Overview

We are going to build a System using ARM Templates. The following Azure Services have been integrated:
```
 - AppInsights
 - Log Analytics 
 - Keyvault
    -Secret Management
    -Access Policies Management
 - Azure Function
 - Cosmos Db Account
```

## Task 1: Update Parameter File

We will update the following file .\ArmDeployers\azuredeploy.parameters.json parameters

    - baseName: 5 first letters of you alias
    - if setAppKeyVaultPermissions = true then update
        - settings.value.secretManager.accountList line 65 and 66

## Task 2: Login and set context

1. __Login__ via PowerShell. You should be prompted to login with your Microsoft credentials. 
    ```
    Login-AzAccount
    ```
1.  __Set__ the subscriptionid. In the code below.
    ```
     Select-AzSubscription -SubscriptionId "<Your Subscription Id>"
    ```
## Task 3: Deploy Resources

1. Navigate to ARM template location
    ```
    cd "YOUR-LOCAL-PATH\Azure-Infrastructure-As-Code\"
    ```

2.  __Deploy__  Resources

    ```
    .\Deploy-AzureResources.ps1
    ```
## Summary

In this exercise you used the Azure ARM templates to create a system end to end that includes.

    ```
        -Creates Common Resource Group
        -Creates Common Storage Account
        -Uploads everything under ArmResources Folder to Common Storage Account
        -Starts Execution of Link Arm Templates.
        -Under Common Resource Group, it creates common resources like:
            -AppInsights
            -Keyvault
            -Storage
            -Log Analytics
        -Creates a New Resource Group for the function.
            -Creates the Function,
            -Puts the Function key into the keyvault.
            -Sets Function Configuration to read secrets from keyvault
            -Provides permissions to keyvault to the identity of the function.
            -Create a Cosmos Db Acccount and pushes its secrets directly to keyvault.
                -by Default it creates a free cosmos db account. If you already have
                 a free instance, please update the parameter file 
                 Azure-Infrastructure-As-Code\ArmDeployers\azuredeploy.parameters.json
    ```
