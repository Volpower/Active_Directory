# 01- Installing the Domain Controller

1- Use `Sconfig` to:

    - Change the hostname
    - Change the IP @ to static
    - Change the DNS Server to our own IP @

2- Install the Active Directory Windows Features

    ```Shell
    * To check windows features on the Domain Controller use:
        Get-WindowsFeature | ? {$_.Name -LIKE "AD*"}

    * To install the Domain Controller use:
        Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

    * To configure the Domain Controller use:
        Import-Module ADDSDeployement
        Install-ADDSForest
  
    *To Check and reconfigure the DNS back to the proper server-ip use:
        Get-DNSClientServeAddress
        Set-DNSClientServerAddress -InterfaceIndex "index_number" -ServerAddress "IP-address"
    ```


3- Other ways of setting up interface ip and routes

    ```Shell
    * To find the index and set the ip to static of an interface:
        Get-NetIPAddress -IPAddress "ip address"  
        Get-NetIPInterface -InterfaceIndex 12 | Set-NetIPInterface -Dhcp Disabled (This command insures that dhcp is disable)
        Remove-NetIPAddress -IPAddress 'ip address' (This removes the ip from the persistence store)
        New-NetIPAddress -InterfaceIndex 'index' -AddressFamily IPv4 -IPAddress 'ip @' -PrefixLength 24 (This set the new ip)
        Remove-NetRoute -InterfaceIndex 'index' -NextHop 'nexthop-ip@'
        New-NetRoute -InterfaceIndex 'index' -DestinationPrefix '0.0.0.0/0' -AddressFamily 'add_family' -NextHop 'nexthop-ip@' -RouteMetric 0
