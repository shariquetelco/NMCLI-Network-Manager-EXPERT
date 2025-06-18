
# Table of Contents

1.  [1) connection](#orga5369cc)
    1.  [Show details of connection profiles](#org7290036)
    2.  [Up, activate a connection on a device](#orgcfcafd4)
    3.  [Down, deactivate a connection from a device](#org8c534f3)
    4.  [Add a new connection profile](#org6a088a1)
    5.  [Modify one or more properties of a connection profile](#org1d36e57)
    6.  [Clone an existing connection profile](#org18cac42)
    7.  [Delete a connection profile](#orgf383cd9)
    8.  [Reload all connection files from disk](#org9aa0180)
    9.  [Load or reload one or more connection files from disk.](#orge80d9e6)
2.  [2) device](#org987d163)
    1.  [Show details of device(s)](#org445b7c7)
    2.  [Status for all devices](#orgb177798)
    3.  [Set device properties.](#org012e156)
    4.  [Connect the device.](#org015dfad)
    5.  [Disconnect the device](#org51311aa)
    6.  [Modify one or more properties on an active device](#org108daf3)
    7.  [Delete the software devices](#org46728ad)
    8.  [Perform operation on Wi-Fi devices](#org52a9e5c)
3.  [3) general](#org03ad232)
    1.  [Show overall status of NetworkManager.](#org4af237a)
4.  [4) networking](#org9413e79)
    1.  [Switch networking on.](#org7a79d71)
    2.  [Switch networking off.](#orgc0c9833)
    3.  [Get network connectivity state.](#org239c442)
5.  [5) radio](#orgd11ed78)
    1.  [Get status of **all** radio switches, or turn them on/off.](#org2f66c44)
    2.  [Get status of **Wi-Fi** radio switch, or turn it on/off.](#org47ddf24)
    3.  [Get status of **mobile broadband** radio switch, or turn it on/off.](#orgec15be4)

<div class="abstract">
This document contains the essential information for using
***<span class="underline">NetworkManager</span>***, a basic instruction guide set for operating with
***nmcli***.

For fully detailed information, please see ***man nmcli***.

</div>


<a id="orga5369cc"></a>

# 1) connection


<a id="org7290036"></a>

## Show details of connection profiles

    nmcli con show [--active, --show-secrets] [id | uuid | path] <ID>

The flag '&#x2013;active' will only show the profiles of the current
active profiles.

For displaying also the associated secrets use the '&#x2013;show-secrets'
option.


<a id="orgcfcafd4"></a>

## Up, activate a connection on a device

    nmcli con up ifname <ifname> [ap <BSSID>] [nsp <name>] [passwd-file <file with passwords>]


<a id="org8c534f3"></a>

## Down, deactivate a connection from a device

    nmcli con down [id | uuid | path | apath] <ID>


<a id="org6a088a1"></a>

## Add a new connection profile

This option is crucial since we manually define an entire
profile for an interface. 

The basic interfaces we'll be defining are

-   Ethernet profiles
-   Wi-Fi profiles
-   Bridge (master device) profiles
-   Bridge Slaves (slave devices) profiles

By adding a new connection profile we can define many properties
(everything on the man page) as the IPv4 addresses and gateways,
automatic addresses (from the DHCP) for dynamic IPs or static IPs
with manual configuration, we can define the DNS configuration, and
so on.

Basic properties:

1.  ****con-name****: The connection profile name
2.  ****ifname****: The interface name where the profile will be applied
3.  ****type****: The type of profile (ethernet, wifi, bridge,
    bridge-slave, &#x2026;)
4.  ****ipv4.addresses (or ip4)****: The IPv4 address
5.  ****ipv4.gateway (or gw4)****: The IPv4 gateway adress
6.  ****ssid****: The SSID of a network (also if it is hidden)
7.  ****wifi-sec.key-mgmt****: The key management as wpa-psk
    (preshared-key), wpa-eap, &#x2026;
8.  ****wifi-sec.psk****: The SSID preshared key (the "password" of the
    wifi network)

Examples:

-   Define a ethernet profile
    
        nmcli con add con-name ethProfile ifname eth0 type ethernet ip4 192.168.1.14/24 gw4 192.168.1.1

-   Define a wifi profile
    
        nmcli con add con-name wifiProfile ifname wl0 type wifi ip4 192.168.1.14/24 gw4 192.168.1.1 ssid "MiFibra-5C60" wifi-sec.key-mgmt wpa-psk wifi-sec.psk "password"

-   Define a bridge profile
    
        nmcli con add con-name myBridge type bridge ip4 192.168.1.14/24 gw4 192.168.1.1

-   Define a bridge-slave profile
    
        nmcli con add con-name brSlave type bridge-slave ifname eth0 master myBridge


<a id="org1d36e57"></a>

## Modify one or more properties of a connection profile

    nmcli con modify [id | uuid | path] <ID> ([+|-]<setting>.<property> <value>)+


<a id="org18cac42"></a>

## Clone an existing connection profile

    nmcli con clone [--temporary] [id | uuid | path] <ID> <new name>


<a id="orgf383cd9"></a>

## Delete a connection profile

    nmcli con delete [id | uuid | path] <ID>


<a id="org9aa0180"></a>

## Reload all connection files from disk

    nmcli con reload


<a id="orge80d9e6"></a>

## Load or reload one or more connection files from disk.

    nmcli con load <filename>


<a id="org987d163"></a>

# 2) device


<a id="org445b7c7"></a>

## Show details of device(s)

    nmcli dev show [<ifname>]

The command lists details for all devices, or for a given device.


<a id="orgb177798"></a>

## Status for all devices

    nmcli dev status

By default, the following columns are shown:

-   DEVICE     - interface name
-   TYPE       - device type
-   STATE      - device state
-   CONNECTION - connection activated on device (if any)

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">DEVICE</th>
<th scope="col" class="org-left">TYPE</th>
<th scope="col" class="org-left">STATE</th>
<th scope="col" class="org-left">CONNECTION</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">ens33</td>
<td class="org-left">ethernet</td>
<td class="org-left">connected</td>
<td class="org-left">Wired connection 1</td>
</tr>


<tr>
<td class="org-left">lo</td>
<td class="org-left">loopback</td>
<td class="org-left">unmanaged</td>
<td class="org-left">--</td>
</tr>
</tbody>
</table>


<a id="org012e156"></a>

## Set device properties.

    nmcli dev set [ifname] ifname [autoconnect {yes | no}]
    nmcli dev set [ifname] ifname [managed {yes | no}]


<a id="org015dfad"></a>

## Connect the device.

    nmcli dev connect [<ifname>]

NetworkManager will try to find a suitable connection that will be
activated.

It will also consider connections that are not set to
auto-connect. 


<a id="org51311aa"></a>

## Disconnect the device

    nmcli dev disconnect [<ifname>]

The command disconnects the device and prevents it from
auto-activating further connections without user/manual
intervention. 


<a id="org108daf3"></a>

## Modify one or more properties on an active device

Modify one or more properties currently active on the device without modifying
the connection profile. The changes have immediate effect. 

    nmcli dev modify <ifname> ([+|-]<setting>.<property> <value>)+

> ****<span class="underline">NOTE:</span>**** The changes do not modify the connection profile!


<a id="org46728ad"></a>

## Delete the software devices

    nmcli dev delete [<ifname>]

The command removes the interfaces. It only works for software
devices like:

-   Bonds
-   Brigdes
-   etc.

> ****<span class="underline">NOTE:</span>**** Hardware devices cannot be deleted by the command!


<a id="org52a9e5c"></a>

## Perform operation on Wi-Fi devices

-   List available Wi-Fi access points
    
        nmcli dev wifi list [ifname <ifname>] [bssid <BSSID>] [--rescan yes|no|auto]
    
    The options 'ifname' and 'bssid' can be used for listing and
    showing APs (access points) for a particular 'ifname'. 
    
    The &#x2013;rescan flag tells if a new scan should be done for listing
    APs.

-   Connect to a Wi-Fi network specified by SSID or BSSID
    
        sudo nmcli dev wifi connect connect <(B)SSID> [password <password>] [wep-key-type key|phrase] [ifname <ifname>]
        		[bssid <BSSID>] [name <name>] [private yes|no] [hidden yes|no]
    
    The most common use would be:
    
        sudo nmcli dev wifi connect <"SSID"> password <"PASSWORD">
    
    And for security purposes, for not displaying the 'SSID' network
    password we should run:
    
        sudo nmcli --ask dev wifi connect <"SSID">

-   Re-scan for available access points.
    
        nmcli dev wifi rescan [ifname <ifname>] [[ssid <SSID to scan>] ...]
    
    The option 'ssid' allows scanning for a specific SSID, which is
    useful for APs with hidden SSIDs.
    
    > ****<span class="underline">NOTE:</span>**** Performing a rescan would not show the APs!

-   Create a Wi-Fi hotspot
    
        nmcli dev wifi hotspot [ifname <ifname>] [con-name <name>] [ssid <SSID>]
        		[band a|bg] [channel <channel>] [password <password>]
    
    Parameters:
    
    -   ***<span class="underline">ifname:</span>*** Wi-Fi device to use
    -   ***<span class="underline">con-name:</span>*** Hotspot connection profile name
    -   ***<span class="underline">ssid:</span>*** SSID of the hotspot
    -   ***<span class="underline">band:</span>*** Wi-Fi band to use
    -   ***<span class="underline">channel:</span>*** Wi-Fi channel to use
    -   ***<span class="underline">password:</span>*** Password for the hotspot
    
    > ****<span class="underline">NOTE:</span>**** Use 'connection down' or 'device disconnect' to stop
    >   the hotspot.

-   Show a password of an interface
    
        nmcli dev wifi show-password <ifname>


<a id="org03ad232"></a>

# 3) general


<a id="org4af237a"></a>

## Show overall status of NetworkManager.

We can check the status by doing:

    nmcli gen status

Or also:

    nmcli gen


<a id="org9413e79"></a>

# 4) networking


<a id="org7a79d71"></a>

## Switch networking on.

    nmcli net on


<a id="orgc0c9833"></a>

## Switch networking off.

    nmcli net off


<a id="org239c442"></a>

## Get network connectivity state.

    nmcli net connectivity [check]

The optional **check** argument makes NetworkManager re-check the
connectivity.

Possible states are:

-   ***<span class="underline">none:</span>*** The host is not connected to any network.

-   ***<span class="underline">portal:</span>*** The host is behind a captive portal and cannot reach the full Internet.

-   ***<span class="underline">limited:</span>*** The host is connected to a network, but it has no access to the Internet.

-   ***<span class="underline">full:</span>*** The host is connected to a network and has full access to the Internet.

-   ***<span class="underline">unknown:</span>*** The connectivity status cannot be found out.


<a id="orgd11ed78"></a>

# 5) radio


<a id="org2f66c44"></a>

## Get status of **all** radio switches, or turn them on/off.

    nmcli radio all [on | off]


<a id="org47ddf24"></a>

## Get status of **Wi-Fi** radio switch, or turn it on/off.

    nmcli radio wifi [on | off]


<a id="orgec15be4"></a>

## Get status of **mobile broadband** radio switch, or turn it on/off.

    nmcli radio wwan [on | off]

