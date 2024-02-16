---
id: hardware-ups-inmatics-sputnik-snmp
title: Inmatics PSU Sputnik
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Pack assets

### Templates

The Monitoring Connector **Inmatics PSU Sputnik** brings a host template:

* **HW-UPS-Inmatics-Sputnik-SNMP-custom**

The connector brings the following service templates (sorted by the host template they are attached to):

<Tabs groupId="sync">
<TabItem value="HW-UPS-Inmatics-Sputnik-SNMP-custom" label="HW-UPS-Inmatics-Sputnik-SNMP-custom">

| Service Alias  | Service Template                                   | Service Description                                 |
|:---------------|:---------------------------------------------------|:----------------------------------------------------|
| Alarms         | HW-UPS-Inmatics-Sputnik-Alarms-SNMP-custom         | Check if alarms are present                             |
| Battery-Status | HW-UPS-Inmatics-Sputnik-Battery-Status-SNMP-custom | Check battery status and remaining battery charge |
| Environment    | HW-UPS-Inmatics-Sputnik-Environment-SNMP-custom    | Monitor the temperature and the humidity percentage |
| Input-Lines    | HW-UPS-Inmatics-Sputnik-Input-Lines-SNMP-custom    | Check input lines metrics                           |
| Output-Lines   | HW-UPS-Inmatics-Sputnik-Output-Lines-SNMP-custom   | Check output lines metrics                          |
| Output-Source  | HW-UPS-Inmatics-Sputnik-Output-Source-SNMP-custom  | Check output source status                          |

> The services listed above are created automatically when the **HW-UPS-Inmatics-Sputnik-SNMP-custom** host template is used.

</TabItem>
</Tabs>

### Discovery rules

#### Host discovery

| Rule name       | Description                                                                                                                                                                                                                                                 |
|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SNMP Agents     | Discover your resources through an SNMP subnet scan. You need to install the [Generic SNMP](./applications-protocol-snmp.md) connector to get the discovery rule and create a template mapper for the **HW-UPS-Inmatics-Sputnik-SNMP-custom** host template |

More information about discovering hosts automatically is available on the [dedicated page](/docs/monitoring/discovery/hosts-discovery).

### Collected metrics & status

Here is the list of services for this connector, detailing all metrics linked to each service.

<Tabs groupId="sync">
<TabItem value="Alarms" label="Alarms">

| Metric name          | Unit  |
|:---------------------|:------|
| alarms.current.count | count |
| test-status          | N/A   |

</TabItem>
<TabItem value="Battery-Status" label="Battery-Status">

| Metric name                      | Unit    |
|:---------------------------------|:--------|
| status                           | N/A     |
| battery.charge.remaining.percent | %       |
| battery.charge.remaining.minutes | minutes |
| battery.current.ampere           | A       |
| battery.voltage.volt             | V       |
| battery.temperature.celsius      | C       |

</TabItem>
<TabItem value="Environment" label="Environment">

| Metric name                               | Unit  |
|:------------------------------------------|:------|
| *sensors*#environment.temperature.celsius | C     |
| *sensors*#environment.humidity.percentage | %     |

</TabItem>
<TabItem value="Input-Lines" label="Input-Lines">

| Metric name                       | Unit  |
|:----------------------------------|:------|
| *line*#line.input.frequence.hertz | Hz    |
| *line*#line.input.voltage.volt    | V     |
| *line*#line.input.current.ampere  | A     |
| *line*#line.input.power.watt      | W     |

</TabItem>
<TabItem value="Output-Lines" label="Output-Lines">

| Metric name                         | Unit  |
|:------------------------------------|:------|
| output.3phases.stdev.gauge          | N/A   |
| lines.output.frequence.hertz        | Hz    |
| *oline*#line.output.load.percentage | %     |
| *oline*#line.output.current.ampere  | A     |
| *oline*#line.output.voltage.volt    | V     |
| *oline*#line.output.power.watt      | W     |

</TabItem>
<TabItem value="Output-Source" label="Output-Source">

| Metric name   | Unit  |
|:--------------|:------|
| source-status | N/A   |

> To obtain this new metric format, include **--use-new-perfdata** in the **EXTRAOPTIONS** service macro.

</TabItem>
</Tabs>

## Prerequisites

### SNMP Configuration

The SNMP service must be configured and activated on the host. Please refer to the official documentation from the manufacturer/publisher.

### Network flow

The target resource must be reachable from the Centreon poller on the UDP/161 SNMP port.

## Installing the monitoring connector

### Pack

1. If the platform uses an *online* license, you can skip the package installation
instruction below as it is not required to have the connector displayed within the
**Configuration > Monitoring Connector Manager** menu.
If the platform uses an *offline* license, install the package on the **central server**
with the command corresponding to the operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-hardware-ups-inmatics-sputnik-snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-hardware-ups-inmatics-sputnik-snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-hardware-ups-inmatics-sputnik-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-hardware-ups-inmatics-sputnik-snmp
```

</TabItem>
</Tabs>

2. Whatever the license type (*online* or *offline*), install the **Inmatics PSU Sputnik** connector through
the **Configuration > Monitoring Connectors Manager** menu.

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
dnf install centreon-plugin-Hardware-Ups-Sputnik-Snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Hardware-Ups-Sputnik-Snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-hardware-ups-sputnik-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Hardware-Ups-Sputnik-Snmp
```

</TabItem>
</Tabs>

## Using the monitoring connector

### Using a host template provided by the connector

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill the **Name**, **Alias** & **IP Address/DNS** fields according to your ressource settings.
3. Apply the **HW-UPS-Inmatics-Sputnik-SNMP-custom** template to the host. 

> When using SNMP v3, use the **SNMPEXTRAOPTIONS** macro to add specific authentication parameters.
> More information in the [Troubleshooting SNMP](../getting-started/how-to-guides/troubleshooting-plugins.md#snmpv3-options-mapping) section.

| Macro            | Description                                                                                          | Default value     | Mandatory   |
|:-----------------|:-----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| SNMPEXTRAOPTIONS | Any extra option you may want to add to every command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

4. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The host appears in the list of hosts, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the host: it shows the values of the macros.

### Using a service template provided by the connector

1. If you have used a host template and checked **Create Services linked to the Template too**, the services linked to the template have been created automatically, using the corresponding service templates. Otherwise, [create manually the services you want](/docs/monitoring/basic-objects/services) and apply a service template to them.
2. Fill in the macros you want (e.g. to change the thresholds for the alerts). Some macros are mandatory (see the table below).

<Tabs groupId="sync">
<TabItem value="Alarms" label="Alarms">

| Macro                 | Description                                                                                                                                                             | Default value                       | Mandatory   |
|:----------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------|:-----------:|
| WARNINGALARMSCURRENT  | Thresholds                                                                                                                                                              |                                     |             |
| CRITICALALARMSCURRENT | Thresholds                                                                                                                                                              |                                     |             |
| WARNINGTESTSTATUS     | Define the conditions to match for the status to be WARNING (default: '%{status} =~ /doneWarning\|aborted/'). You can use the following variables: %{status}, %{detail} | %{status} =~ /doneWarning\|aborted/ |             |
| CRITICALTESTSTATUS    | Define the conditions to match for the status to be CRITICAL (default: '%{status} =~ /doneError/'). You can use the following variables: %{status}, %{detail}           | %{status} =~ /doneError/            |             |
| EXTRAOPTIONS          | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options).                                                                      | --verbose                           |             |

</TabItem>
<TabItem value="Battery-Status" label="Battery-Status">

| Macro               | Description                                                                                                                                        | Default value            | Mandatory   |
|:--------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------|:-----------:|
| UNKNOWNSTATUS       | Define the conditions to match for the status to be UNKNOWN (default: '%{status} =~ /unknown/i'). You can use the following variables: %{status}   | %{status} =~ /unknown/i  |             |
| WARNING             | Thresholds                                                                                                                                         |                          |             |
| CRITICAL            | Thresholds                                                                                                                                         |                          |             |
| WARNINGCURRENT      | Thresholds                                                                                                                                         |                          |             |
| CRITICALCURRENT     | Thresholds                                                                                                                                         |                          |             |
| WARNINGSTATUS       | Define the conditions to match for the status to be WARNING (default: '%{status} =~ /low/i'). You can use the following variables: %{status}       | %{status} =~ /low/i      |             |
| CRITICALSTATUS      | Define the conditions to match for the status to be CRITICAL (default: '%{status} =~ /depleted/i'). You can use the following variables: %{status} | %{status} =~ /depleted/i |             |
| WARNINGTEMPERATURE  | Thresholds                                                                                                                                         |                          |             |
| CRITICALTEMPERATURE | Thresholds                                                                                                                                         |                          |             |
| WARNINGVOLTAGE      | Thresholds                                                                                                                                         |                          |             |
| CRITICALVOLTAGE     | Thresholds                                                                                                                                         |                          |             |
| EXTRAOPTIONS        | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options).                                                 |                          |             |

</TabItem>
<TabItem value="Environment" label="Environment">

| Macro               | Description                                                                                        | Default value     | Mandatory   |
|:--------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNINGHUMIDITY     | Thresholds                                                                                         |                   |             |
| CRITICALHUMIDITY    | Thresholds                                                                                         |                   |             |
| WARNINGTEMPERATURE  | Thresholds                                                                                         |                   |             |
| CRITICALTEMPERATURE | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS        | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). | --verbose         |             |

</TabItem>
<TabItem value="Input-Lines" label="Input-Lines">

| Macro             | Description                                                                                        | Default value     | Mandatory   |
|:------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNINGCURRENT    | Thresholds                                                                                         |                   |             |
| CRITICALCURRENT   | Thresholds                                                                                         |                   |             |
| WARNINGFREQUENCE  | Thresholds                                                                                         |                   |             |
| CRITICALFREQUENCE | Thresholds                                                                                         |                   |             |
| WARNINGPOWER      | Thresholds                                                                                         |                   |             |
| CRITICALPOWER     | Thresholds                                                                                         |                   |             |
| WARNINGVOLTAGE    | Thresholds                                                                                         |                   |             |
| CRITICALVOLTAGE   | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS      | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). | --verbose         |             |

</TabItem>
<TabItem value="Output-Lines" label="Output-Lines">

| Macro                | Description                                                                                        | Default value     | Mandatory   |
|:---------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNINGCURRENT       | Threshold                                                                                          |                   |             |
| CRITICALCURRENT      | Threshold                                                                                          |                   |             |
| WARNINGFREQUENCE     |                                                                                                    |                   |             |
| CRITICALFREQUENCE    |                                                                                                    |                   |             |
| WARNINGLOAD          | Threshold                                                                                          |                   |             |
| CRITICALLOAD         | Threshold                                                                                          |                   |             |
| WARNINGPOWER         | Threshold                                                                                          |                   |             |
| CRITICALPOWER        | Threshold                                                                                          |                   |             |
| WARNINGSTDEV3PHASES  | Warning threshold for standard deviation of 3 phases                                               |                   |             |
| CRITICALSTDEV3PHASES | Critical threshold for standard deviation of 3 phases                                              |                   |             |
| WARNINGVOLTAGE       | Threshold                                                                                          |                   |             |
| CRITICALVOLTAGE      | Threshold                                                                                          |                   |             |
| EXTRAOPTIONS         | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). | --verbose         |             |

</TabItem>
<TabItem value="Output-Source" label="Output-Source">

| Macro                | Description                                                                                                                                                              | Default value                                    | Mandatory   |
|:---------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------|:-----------:|
| UNKNOWNSOURCESTATUS  | Define the conditions to match for the status to be UNKNOWN (default: '%{status} =~ /other/') You can use the following variables: %{status}                             | %{status} =~ /other/                             |             |
| WARNINGSOURCESTATUS  | Define the conditions to match for the status to be WARNING (default: '%{status} =~ /bypass\|battery\|booster\|reducer/') You can use the following variables: %{status} | %{status} =~ /bypass\|battery\|booster\|reducer/ |             |
| CRITICALSOURCESTATUS | Define the conditions to match for the status to be CRITICAL (default: '%{status} =~ /none/') You can use the following variables: %{status}                             | %{status} =~ /none/                              |             |
| EXTRAOPTIONS         | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options).                                                                       |                                                  |             |

</TabItem>
</Tabs>

3. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The service appears in the list of services, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the service: it shows the values of the macros.

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`). Test that the connector 
is able to monitor a resource using a command like this one (replace the sample values by yours):

```bash
/usr/lib/centreon/plugins/centreon_ups_sputnik_snmp.pl \
	--plugin=hardware::ups::inmatics::sputnik::snmp::plugin \
	--mode=environment \
	--hostname='10.0.0.1' \
	--snmp-version='2c' \
	--snmp-community='my-snmp-community' \
	--filter-id='' \
	--warning-temperature='' \
	--critical-temperature='' \
	--warning-humidity='' \
	--critical-humidity='' \
	--verbose
```

The expected command output is shown below:

```bash
OK: 'Sensor 1': temperature 20.06 C, humidity 33 % | 'Sensor 1#environment.temperature.celsius'=20.06C;;;; 'Sensor 1#environment.humidity.percentage'=33%;;;0;100
```

### Troubleshooting

Please find the [troubleshooting documentation](../getting-started/how-to-guides/troubleshooting-plugins.md)
for Centreon Plugins typical issues.

### Available modes

In most cases, a mode corresponds to a service template. The mode appears in the execution command for the connector.
In the Centreon interface, you don't need to specify a mode explicitly: its use is implied when you apply a service template.
However, you will need to specify the correct mode for the template if you want to test the execution command for the 
connector in your terminal.

All available modes can be displayed by adding the `--list-mode` parameter to
the command:

```bash
/usr/lib/centreon/plugins/centreon_ups_sputnik_snmp.pl \
	--plugin=hardware::ups::inmatics::sputnik::snmp::plugin \
	--list-mode
```

The plugin brings the following modes:

| Mode                                                                                                                                            | Linked service template                            |
|:------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------|
| alarms [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/hardware/ups/standard/rfc1628/snmp/mode/alarms.pm)]                | HW-UPS-Inmatics-Sputnik-Alarms-SNMP-custom         |
| battery-status [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/hardware/ups/standard/rfc1628/snmp/mode/batterystatus.pm)] | HW-UPS-Inmatics-Sputnik-Battery-Status-SNMP-custom |
| environment [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/hardware/ups/inmatics/sputnik/snmp/mode/environment.pm)]      | HW-UPS-Inmatics-Sputnik-Environment-SNMP-custom    |
| input-lines [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/hardware/ups/standard/rfc1628/snmp/mode/inputlines.pm)]       | HW-UPS-Inmatics-Sputnik-Input-Lines-SNMP-custom    |
| output-lines [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/hardware/ups/standard/rfc1628/snmp/mode/outputlines.pm)]     | HW-UPS-Inmatics-Sputnik-Output-Lines-SNMP-custom   |
| output-source [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/hardware/ups/standard/rfc1628/snmp/mode/outputsource.pm)]   | HW-UPS-Inmatics-Sputnik-Output-Source-SNMP-custom  |

### Available options

#### Generic options

All generic options are listed here:

| Option                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --mode                                     | Define the mode in which you want the plugin to be executed (see--list-mode).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --dyn-mode                                 | Specify a mode with the module's path (advanced).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --list-mode                                | List all available modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --mode-version                             | Check minimal version of mode. If not, unknown error.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --version                                  | Return the version of the plugin.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --pass-manager                             | Define the password manager you want to use. Supported managers are: environment, file, keepass, hashicorpvault and teampass.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --verbose                                  | Display extended status information (long output).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --debug                                    | Display debug messages.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --filter-perfdata                          | Filter perfdata that match the regexp. Example: adding --filter-perfdata='avg' will remove all metrics that do not contain 'avg' from performance data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --filter-perfdata-adv                      | Filter perfdata based on a "if" condition using the following variables: label, value, unit, warning, critical, min, max. Variables must be written either %{variable} or %(variable). Example: adding --filter-perfdata-adv='not (%(value) == 0 and %(max) eq "")' will remove all metrics whose value equals 0 and that don't have a maximum value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --explode-perfdata-max                     | Create a new metric for each metric that comes with a maximum limit. The new metric will be named identically with a '\_max' suffix). Example: it will split 'used\_prct'=26.93%;0:80;0:90;0;100 into 'used\_prct'=26.93%;0:80;0:90;0;100 'used\_prct\_max'=100%;;;;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Convert storage free perfdata into used:     --change-perfdata='free,used,invert()'      Convert storage free perfdata into used:     --change-perfdata='used,free,invert()'      Scale traffic values automatically:     --change-perfdata='traffic,,scale(auto)'      Scale traffic values in Mbps:     --change-perfdata='traffic\_in,,scale(Mbps),mbps'      Change traffic values in percent:     --change-perfdata='traffic\_in,,percent()'                                                                                                                                                                                                                                                                                                                                                                |
| --extend-perfdata-group                    | Add new aggregated metrics (min, max, average or sum) for groups of metrics defined by a regex match on the metrics' names. Syntax: --extend-perfdata-group=regex,namesofnewmetrics,calculation\[,\[ne wuom\],\[min\],\[max\]\] regex: regular expression namesofnewmetrics: how the new metrics' names are composed (can use $1, $2... for groups defined by () in regex). calculation: how the values of the new metrics should be calculated newuom (optional): unit of measure for the new metrics min (optional): lowest value the metrics can reach max (optional): highest value the metrics can reach  Common examples:      Sum wrong packets from all interfaces (with interface need     --units-errors=absolute):     --extend-perfdata-group=',packets\_wrong,sum(packets\_(discard     \|error)\_(in\|out))'      Sum traffic by interface:     --extend-perfdata-group='traffic\_in\_(.*),traffic\_$1,sum(traf     fic\_(in\|out)\_$1)'   |
| --change-short-output --change-long-output | Modify the short/long output that is returned by the plugin. Syntax: --change-short-output=pattern~replacement~modifier Most commonly used modifiers are i (case insensitive) and g (replace all occurrences). Example: adding --change-short-output='OK~Up~gi' will replace all occurrences of 'OK', 'ok', 'Ok' or 'oK' with 'Up'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --change-exit                              | Replace an exit code with one of your choice. Example: adding --change-exit=unknown=critical will result in a CRITICAL state instead of an UNKNOWN state.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --range-perfdata                           | Rewrite the ranges displayed in the perfdata. Accepted values: 0: nothing is changed. 1: if the lower value of the range is equal to 0, it is removed. 2: remove the thresholds from the perfdata.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-uom                               | Mask the units when they don't match the given regular expression.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --opt-exit                                 | Replace the exit code in case of an execution error (i.e. wrong option provided, SSH connection refused, timeout, etc). Default: unknown.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-ignore-perfdata                   | Remove all the metrics from the service. The service will still have a status and an output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --output-ignore-label                      | Remove the status label ("OK:", "WARNING:", "UNKNOWN:", CRITICAL:") from the beginning of the output. Example: 'OK: Ram Total:...' will become 'Ram Total:...'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --output-xml                               | Return the output in XML format (to send to an XML API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --output-json                              | Return the output in JSON format (to send to a JSON API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-openmetrics                       | Return the output in OpenMetrics format (to send to a tool expecting this format).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --output-file                              | Write output in file (can be combined with json, xml and openmetrics options). E.g.: --output-file=/tmp/output.txt will write the output in /tmp/output.txt.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-format                             | Applies only to modes beginning with 'list-'. Returns the list of available macros to configure a service discovery rule (formatted in XML).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-show                               | Applies only to modes beginning with 'list-'. Returns the list of discovered objects (formatted in XML) for service discovery.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --float-precision                          | Define the float precision for thresholds (default: 8).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --hostname                                 | Name or address of the host to monitor (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --snmp-community                           | SNMP community (default value: public). It is recommended to use a read-only community.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-version                             | Version of the SNMP protocol. 1 for SNMP v1 (default), 2 for SNMP v2c, 3 for SNMP v3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --snmp-port                                | UDP port to send the SNMP request to (default: 161).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --snmp-timeout                             | Time to wait before sending the request again if no reply has been received, in seconds (default: 1). See also --snmp-retries.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --snmp-retries                             | Maximum number of retries (default: 5).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --maxrepetitions                           | Max repetitions value (default: 50) (only for SNMP v2 and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --subsetleef                               | How many OID values per SNMP request (default: 50) (for get\_leef method. Be cautious when you set it. Prefer to let the default value).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --snmp-autoreduce                          | Progressively reduce the number of requested OIDs in bulk mode. Use it in case of SNMP errors (by default, the number is divided by 2).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-force-getnext                       | Use SNMP getnext function in SNMP v2c and v3. This will request one OID at a time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --snmp-cache-file                          | Use SNMP cache file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --snmp-username                            | SNMP v3 only: User name (securityName).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --authpassphrase                           | SNMP v3 only: Pass phrase hashed using the authentication protocol defined in the --authprotocol option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --authprotocol                             | SNMP v3 only: Authentication protocol: MD5\|SHA. Since net-snmp 5.9.1: SHA224\|SHA256\|SHA384\|SHA512.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --privpassphrase                           | SNMP v3 only: Privacy pass phrase (privPassword) to encrypt messages using the protocol defined in the --privprotocol option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --privprotocol                             | SNMP v3 only: Privacy protocol (privProtocol) used to encrypt messages. Supported protocols are: DES\|AES and since net-snmp 5.9.1: AES192\|AES192C\|AES256\|AES256C.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --contextname                              | SNMP v3 only: Context name (contextName), if relevant for the monitored host.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --contextengineid                          | SNMP v3 only: Context engine ID (contextEngineID), if relevant for the monitored host, given as a hexadecimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --securityengineid                         | SNMP v3 only: Security engine ID, given as a hexadecimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --snmp-errors-exit                         | Expected status in case of SNMP error or timeout. Possible values are warning, critical and unknown (default).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --snmp-tls-transport                       | Transport protocol for TLS communication (can be: 'dtlsudp', 'tlstcp').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-tls-our-identity                    | X.509 certificate to identify ourselves. Can be the path to the certificate file or its contents.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --snmp-tls-their-identity                  | X.509 certificate to identify the remote host. Can be the path to the certificate file or its contents. This option is unnecessary if the certificate is already trusted by your system.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --snmp-tls-their-hostname                  | Common Name (CN) expected in the certificate sent by the host if it differs from the value of the --hostname parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-tls-trust-cert                      | A trusted CA certificate used to verify a remote host's certificate. If you use this option, you must also define --snmp-tls-their-hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

#### Modes options

All available options for each service template are listed below:

<Tabs groupId="sync">
<TabItem value="Alarms" label="Alarms">

| Option                   | Description                                                                                                                                                               |
|:-------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --display-alarms         | Display alarms in verbose output.                                                                                                                                         |
| --unknown-test-status    | Define the conditions to match for the status to be UNKNOWN. You can use the following variables: %{status}, %{detail}                                                    |
| --warning-test-status    | Define the conditions to match for the status to be WARNING (default: '%{status} =~ /doneWarning\|aborted/'). You can use the following variables: %{status}, %{detail}   |
| --critical-test-status   | Define the conditions to match for the status to be CRITICAL (default: '%{status} =~ /doneError/'). You can use the following variables: %{status}, %{detail}             |
| --warning-* --critical-* | Thresholds. Can be: 'alarms-current'.                                                                                                                                     |

</TabItem>
<TabItem value="Battery-Status" label="Battery-Status">

| Option                   | Description                                                                                                                                          |
|:-------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|
| --unknown-status         | Define the conditions to match for the status to be UNKNOWN (default: '%{status} =~ /unknown/i'). You can use the following variables: %{status}     |
| --warning-status         | Define the conditions to match for the status to be WARNING (default: '%{status} =~ /low/i'). You can use the following variables: %{status}         |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (default: '%{status} =~ /depleted/i'). You can use the following variables: %{status}   |
| --warning-* --critical-* | Thresholds. Can be: 'charge-remaining' (%), 'charge-remaining-minutes', 'current' (A), 'voltage' (V), 'temperature' (C).                             |

</TabItem>
<TabItem value="Environment" label="Environment">

| Option                   | Description                                                                                                          |
|:-------------------------|:---------------------------------------------------------------------------------------------------------------------|
| --warning-* --critical-* | Thresholds. Can be: 'humidity' (%), 'temperature' (C).                                                               |
| --filter-id              | Define which sensors should be monitored based on their IDs. This option will be treated as a regular expression.    |

</TabItem>
<TabItem value="Input-Lines" label="Input-Lines">

| Option                   | Description                                                                             |
|:-------------------------|:----------------------------------------------------------------------------------------|
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='^power$'   |
| --exclude-id             | Define the IDs of the instances to exclude in result. Example: --exclude-id=2,3         |
| --warning-* --critical-* | Thresholds. Can be: 'frequence', 'voltage', 'current', 'power'.                         |

</TabItem>
<TabItem value="Output-Lines" label="Output-Lines">

| Option                   | Description                                                              |
|:-------------------------|:-------------------------------------------------------------------------|
| --ignore-zero-counters   | Ignore counters equals to 0.                                             |
| --warning-* --critical-* | Threshold. Can be: 'frequency', 'load', 'voltage', 'current', 'power'.   |
| --warning-stdev-3phases  | Warning threshold for standard deviation of 3 phases.                    |
| --critical-stdev-3phases | Critical threshold for standard deviation of 3 phases.                   |

</TabItem>
<TabItem value="Output-Source" label="Output-Source">

| Option                   | Description                                                                                                                                                                |
|:-------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --unknown-source-status  | Define the conditions to match for the status to be UNKNOWN (default: '%{status} =~ /other/') You can use the following variables: %{status}                               |
| --warning-source-status  | Define the conditions to match for the status to be WARNING (default: '%{status} =~ /bypass\|battery\|booster\|reducer/') You can use the following variables: %{status}   |
| --critical-source-status | Define the conditions to match for the status to be CRITICAL (default: '%{status} =~ /none/') You can use the following variables: %{status}                               |

</TabItem>
</Tabs>

All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins/centreon_ups_sputnik_snmp.pl \
	--plugin=hardware::ups::inmatics::sputnik::snmp::plugin \
	--mode=output-lines \
	--help
```