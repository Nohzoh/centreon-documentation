---
id: cloud-microsoft-office365-onedrive
title: Office365 OneDrive
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Overview

Microsoft’s Office365 suite includes Onedrive, which is a file hosting and
syncronisation service.

The monitoring information of Microsoft's Office365 is available
through the Office365 API Management.

> The data provided by the Office365 Management API are not real-time.
> They're based on a 7 days reporting period

## Monitoring Connector assets

### Monitored objects

* Onedrive site usage

### Monitored metrics

See link for details about metrics : https://docs.microsoft.com/en-us/microsoft-365/admin/activity-reports/onedrive-for-business-usage?view=o365-worldwide

<Tabs groupId="sync">
<TabItem value="Site-Usage" label="Site-Usage">

| Metric name                                  | Description                              | Unit  |
| :------------------------------------------- | :--------------------------------------- | :-----|
| active\_sites                                | Number of active sites                   | Count |
| onedrive.sites.active.usage.total.bytes      | Total usage space (active sites)         | Bytes |
| onedrive.sites.inactive.usage.total.bytes    | Total usage space (inactive sites)       | Bytes |
| onedrive.sites.active.files.total.count      | Total number of files (active sites)     | Count |
| onedrive.sites.inactive.files.total.count    | Total number of files (inactive sites )  | Count |
| onedrive.sites.files.active.total.count      | Total number of active files             | Count |

</TabItem>
</Tabs>

Once the host created, you can configure some macros on the services to filter
information by site or by user. More information in the [Configuration](#Configuration)
section.

## Prerequisites

Refer to the official documentation of Office365 Management or follow the link
in the 'More information' section to create an Office365 account and get help
about the management features.

### Register an application

The Office365 Management API use Azure AD to authenticate against Office365. To
access the Office365 Management API, you need to register your application in
Azure AD. *Application* is here used by Microsoft as a conceptual term,
referring not only to the application software, but also to the Azure AD
registration and role in authentication/authorization "conversations" at runtime.
(https://docs.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals)

More detailed information is available [here](./cloud-microsoft-office365-management.md#prerequisites).

### Office365 Management API authorization

To collect data from Onedrive Online, you need to specify the following
authorization:

* Microsoft Graph :
    * Reports.Read.All (Type : Application)
    * User.Read (Type : Delegated)
* Office365 Management APIs :
    * ServiceHealth.Read (Type : Application)
    * ActivityFeed.Read (Type : Application)

### More information

You can access to the official documentation to register your application,
get your *ID client*, *ID secret* and your *Tenant ID* by following this link:
https://docs.microsoft.com/en-us/office/office-365-management-api/get-started-with-office-365-management-apis

## Setup

### Monitoring Pack

If the platform uses an *online* license, you can skip the package installation
instruction below as it is not required to have the pack displayed within the
**Configuration > Monitoring Connector Manager** menu.
If the platform uses an *offline* license, install the package on the **central server**
with the command corresponding to the operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-cloud-microsoft-office365-onedrive
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-cloud-microsoft-office365-onedrive
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-cloud-microsoft-office365-onedrive
```

</TabItem>
</Tabs>

Whatever the license type (*online* or *offline*), install the **Office365 OneDrive** Pack through
the **Configuration > Monitoring Connector Manager** menu.

### Plugin

Since Centreon 22.04, you can benefit from the 'Automatic plugin installation' feature.
When this feature is enabled, you can skip the installation part below.

You still have to manually install the plugin on the poller(s) when:
- Automatic plugin installation is turned off
- You want to run a discovery job from a poller that doesn't monitor any resource of this kind yet

> More information in the [Installing the plugin](/docs/monitoring/pluginpacks/#installing-the-plugin) section.

Use the commands below according to your operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Cloud-Microsoft-Office365-Onedrive-Api
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Cloud-Microsoft-Office365-Onedrive-Api
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-cloud-microsoft-office365-onedrive-api
```

</TabItem>
</Tabs>

## Configuration

* Log into Centreon and add a new Host through "Configuration > Hosts".
* Apply the *Cloud-Microsoft-Office365-Onedrive-Api-custom* template and configure all the mandatory Macros :

| Mandatory | Name                  | Description                                                                |
| :-------- | :-------------------- | :------------------------------------------------------------------------- |
| X         | OFFICE365CUSTOMMODE   | Access mode for the Plugin (default: 'graphapi')                           |
| X         | OFFICE365TENANT       | Tenant-id of your Office365 organization                                   |
| X         | OFFICE365CLIENTID     | Client-id of your registered application                                   |
| X         | OFFICE365CLIENTSECRET | Secret-if of your registered application                                   |
|           | OFFICE365EXTRAOPTIONS | Any extra option you may want to add to the command (eg. a --verbose flag) |

The metric *perfdate* will record the date the metric was collected. You can 
filter it by entering ```--filter-perfdata='^(?!.*perfdate).*$'``` into the
*OFFICE365EXTRAOPTIONS* macro.

Once the host created, you can configure some Macros on the services to filter
information:

| Mandatory | Name          | Description                                              |
| :-------- | :------------ | :------------------------------------------------------- |
|           | FILTERURL     | Filter specific sites by URLs                            |
|           | FILTEROWNER   | Filter file by specific owners                           |
|           | FILTERCOUNTER | Filter specific counters (default:'active-sites\|total') |

## FAQ

### How can I test the Plugin in the CLI and what do the main parameters stand for ?

Once the Centreon Plugin installed, you can test it directly in the CLI of the
Centreon poller by logging with the *centreon-engine* user:

```bash
/usr/lib/centreon/plugins//centreon_office365_onedrive_api.pl \
  --plugin=cloud::microsoft::office365::onedrive::plugin \
  --mode=site-usage \
  --tenant='abcd1234-5678-90ab-cd12-34567890abcd' \
  --client-id='9876dcba-5432-10dc-ba98-76543210dcba' \
  --client-secret='8/RON4vUGhAcg6DRmSxc4AwgxSRoNfKg4d8xNizIMnwg='
```

```bash
OK: Active sites on 2020-09-27 : 3/1031 (0.29%) - Total Usage (active sites)
893.84 MB, Usage (inactive sites): 149.03 GB, File Count (active sites): 154,
File Count (inactive sites): 26643, Active File Count (active sites): 5 |
'active_sites'=3sites;;;0;1031
'total_usage_active'=937260440B;;;0;
'total_usage_inactive'=160024822615B;;;0;
'total_file_count_active'=154;;;0;
'total_file_count_inactive'=26643;;;0;
'total_active_file_count'=5;;;0;
```

The available thresholds as well as all of the options that can be used with
this Plugin can be displayed by adding the ```--help``` parameter to the command:

```bash
/usr/lib/centreon/plugins//centreon_office365_onedrive_api.pl \
  --plugin=cloud::microsoft::office365::onedrive::plugin \
  --mode=site-usage \
  --custommode='graphapi'\
  --help
```

You can display all of the modes that come with the Plugin with the command below:

```bash
/usr/lib/centreon/plugins//centreon_office365_onedrive_api.pl \
  --plugin=cloud::microsoft::office365::onedrive::plugin \
  --list-mode
```

### Why do I get the following error:

#### ```UNKNOWN: 500 Can't connect to ...:443```

This error message means that the Centreon Plugin couldn't successfully connect
to the Office365 Management API. Check that no third party device
(such as a firewall) is blocking the request. A proxy connection may also be
necessary to connect to the API. This can be done by using the ```--proxyurl```
option in the command.

#### ```UNKNOWN: 501 Protocol scheme 'connect' is not supported |```

When using a proxy to connect to the Office365 Management API, this error
message means that the Centreon Plugin library does not support the proxy
connection protocol.

In order to prevent this issue, use the *curl* HTTP backend by adding the
following option to the command: ```--http-backend='curl'```.
