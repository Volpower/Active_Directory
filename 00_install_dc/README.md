# 01- Installing the Domain Controller

1- Use `Sconfig` to:

    - Change the hostname
    - Change the IP @ to static
    - Change the DNS Server to our own IP @

2- Install the Active Directory Windows Features

    ```Shell
    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    ```