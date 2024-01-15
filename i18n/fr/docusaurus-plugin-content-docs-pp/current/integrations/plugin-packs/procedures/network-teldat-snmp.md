---
id: network-teldat-snmp
title: Teldat SNMP
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Contenu du pack

### Modèles

Le connecteur de supervision **Teldat Edge Routers SNMP** apporte un modèle d'hôte :

* **Net-Teldat-SNMP-custom**

Le connecteur apporte les modèles de service suivants
(classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="Net-Teldat-SNMP-custom" label="Net-Teldat-SNMP-custom">

| Alias       | Modèle de service                  | Description                                               |
|:------------|:-----------------------------------|:----------------------------------------------------------|
| Cells-Radio | Net-Teldat-Cells-Radio-SNMP-custom | Contrôle les modules radio cellulaires                    |
| Cpu         | Net-Teldat-Cpu-SNMP-custom         | Contrôle du taux d'utilisation du CPU de la machine       |
| Memory      | Net-Teldat-Memory-SNMP-custom      | Contrôle du taux d'utilisation de la mémoire vive         |
| Uptime      | Net-Teldat-Uptime-SNMP-custom      | Durée depuis laquelle le serveur tourne sans interruption |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **Net-Teldat-SNMP-custom** est utilisé.

</TabItem>
<TabItem value="Non rattachés à un modèle d'hôte" label="Non rattachés à un modèle d'hôte">

| Alias      | Modèle de service                 | Description             | Découverte |
|:-----------|:----------------------------------|:------------------------|:----------:|
| Interfaces | Net-Teldat-Interfaces-SNMP-custom | Contrôle les interfaces | X          |

> Les services listés ci-dessus ne sont pas créés automatiquement lorsqu'un modèle d'hôte est appliqué. Pour les utiliser, [créez un service manuellement](/docs/monitoring/basic-objects/services) et appliquez le modèle de service souhaité.

> Si la case **Découverte** est cochée, cela signifie qu'une règle de découverte de service existe pour ce service.

</TabItem>
</Tabs>

### Règles de découverte

#### Découverte d'hôtes

| Nom de la règle | Description                                                                                                                                                                                                                             |
|:----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SNMP Agents     | Découvre les ressources via un scan réseau SNMP. Installez le connecteur [Generic SNMP](./applications-protocol-snmp.md) pour obtenir la règle de découverte et créer un modèle mapper pour le modèle d'hôte **Net-Teldat-SNMP-custom** |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/hosts-discovery) pour en savoir plus sur la découverte automatique d'hôtes.

#### Découverte de service

| Nom de la règle                | Description                                                            |
|:-------------------------------|:-----------------------------------------------------------------------|
| Net-Teldat-SNMP-Interface-Name | Découvre les interfaces réseau et supervise le statut et l'utilisation |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/services-discovery)
pour en savoir plus sur la découverte automatique de services et sa [planification](/docs/monitoring/discovery/services-discovery/#règles-de-découverte).

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Cells-Radio" label="Cells-Radio">

| Métrique                          | Unité |
|:----------------------------------|:------|
| modules.cellradio.detected.count  | count |
| *cells*~status                    | N/A   |
| *cells*~module.cellradio.rsrp.dbm | dBm   |
| *cells*~module.cellradio.rsrq.dbm | dBm   |
| *cells*~module.cellradio.snr.db   | dB    |
| *cells*~module.cellradio.rscp.dbm | dBm   |
| *cells*~module.cellradio.csq.dbm  | dBm   |

</TabItem>
<TabItem value="Cpu" label="Cpu">

| Métrique                       | Unité |
|:-------------------------------|:------|
| cpu.utilization.5s.percentage  | %     |
| cpu.utilization.1m.percentage  | %     |
| cpu.utilization.15m.percentage | %     |

</TabItem>
<TabItem value="Interfaces" label="Interfaces">

| Métrique                                                  | Unité |
|:----------------------------------------------------------|:------|
| *interface_name*#status                                   | N/A   |
| *interface_name*#interface.traffic.in.bitspersecond       | b/s   |
| *interface_name*#interface.traffic.out.bitspersecond      | b/s   |
| *interface_name*#interface.packets.in.discard.percentage  | %     |
| *interface_name*#interface.packets.in.error.percentage    | %     |
| *interface_name*#interface.packets.out.discard.percentage | %     |
| *interface_name*#interface.packets.out.error.percentage   | %     |

</TabItem>
<TabItem value="Memory" label="Memory">

| Métrique                         | Unité |
|:---------------------------------|:------|
| *memory*#memory.usage.bytes      | B     |
| *memory*#memory.free.bytes       | B     |
| *memory*#memory.usage.percentage | %     |

</TabItem>
<TabItem value="Uptime" label="Uptime">

| Métrique              | Unité |
|:----------------------|:------|
| system.uptime.seconds | s     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
</Tabs>

## Prérequis

### Configuration SNMP

Afin de superviser votre équipement, le SNMP v2 ou v3 doit être configuré.

### Flux réseau

La communication doit être possible sur le port UDP 161 depuis le collecteur Centreon vers le serveur supervisé.

## Installer le connecteur de supervision

### Pack

1. Si la plateforme est configurée avec une licence *online*, l'installation d'un paquet
n'est pas requise pour voir apparaître le connecteur dans le menu **Configuration > Gestionnaire de connecteurs de supervision**.
Au contraire, si la plateforme utilise une licence *offline*, installez le paquet
sur le **serveur central** via la commande correspondant au gestionnaire de paquets
associé à sa distribution :

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-network-teldat-snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-network-teldat-snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-network-teldat-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-network-teldat-snmp
```

</TabItem>
</Tabs>

2. Quel que soit le type de la licence (*online* ou *offline*), installez le connecteur **Teldat Edge Routers SNMP**
depuis l'interface web et le menu **Configuration > Gestionnaire de connecteurs de supervision**.

### Plugin

À partir de Centreon 22.04, il est possible de demander le déploiement automatique
du plugin lors de l'utilisation d'un connecteur. Si cette fonctionnalité est activée, et
que vous ne souhaitez pas découvrir des éléments pour la première fois, alors cette
étape n'est pas requise.

> Plus d'informations dans la section [Installer le plugin](/docs/monitoring/pluginpacks/#installer-le-plugin).

Utilisez les commandes ci-dessous en fonction du gestionnaire de paquets de votre système d'exploitation :

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Network-Teldat-Snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Network-Teldat-Snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-network-teldat-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Network-Teldat-Snmp
```

</TabItem>
</Tabs>

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **Net-Teldat-SNMP-custom**.

> Si vous utilisez SNMP en version 3, vous devez configurer les paramètres spécifiques associés via la macro **SNMPEXTRAOPTIONS**.
> Plus d'informations dans la section [Troubleshooting SNMP](../getting-started/how-to-guides/troubleshooting-plugins.md#snmpv3-options-mapping).

| Macro            | Description                                                                                                                                                                   | Valeur par défaut | Obligatoire |
|:-----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| SNMPEXTRAOPTIONS | N'importe quelle option que vous souhaiteriez ajouter à toutes les commandes (une option --verbose par exemple). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

4. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte). Les macros indiquées ci-dessous comme requises (**Obligatoire**) doivent être renseignées.

<Tabs groupId="sync">
<TabItem value="Cells-Radio" label="Cells-Radio">

| Macro                            | Description                                                                                                                                                                     | Valeur par défaut                                         |  Obligatoire  |
|:---------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------|:-------------:|
| WARNINGMODULECELLRADIOCSQ        | Thresholds on cellular mobile reception signal quality (+CSQ).                                                                                                                  |                                                           |               |
| CRITICALMODULECELLRADIOCSQ       | Thresholds on cellular mobile reception signal quality (+CSQ).                                                                                                                  |                                                           |               |
| WARNINGMODULECELLRADIORSCP       | Thresholds on cellular mobile received signal code power (RSCP).                                                                                                                |                                                           |               |
| CRITICALMODULECELLRADIORSCP      | Thresholds on cellular mobile received signal code power (RSCP).                                                                                                                |                                                           |               |
| WARNINGMODULECELLRADIORSRP       | Thresholds on cellular mobile reference symbol received power (RSRP).                                                                                                           |                                                           |               |
| CRITICALMODULECELLRADIORSRP      | Thresholds on cellular mobile reference symbol received power (RSRP).                                                                                                           |                                                           |               |
| WARNINGMODULECELLRADIORSRQ       | Thresholds on cellular mobile reference signal received quality (RSRQ).                                                                                                         |                                                           |               |
| CRITICALMODULECELLRADIORSRQ      | Thresholds on cellular mobile reference signal received quality (RSRQ).                                                                                                         |                                                           |               |
| WARNINGMODULECELLRADIOSNR        | Thresholds on cellular mobile signal versus noise ratio (SINR).                                                                                                                 |                                                           |               |
| CRITICALMODULECELLRADIOSNR       | Thresholds on cellular mobile signal versus noise ratio (SINR).                                                                                                                 |                                                           |               |
| WARNINGMODULESCELLRADIODETECTED  | Thresholds on detected cellular mobile(s)                                                                                                                                       |                                                           |               |
| CRITICALMODULESCELLRADIODETECTED | Thresholds on detected cellular mobile(s)                                                                                                                                       |                                                           |               |
| WARNINGSTATUS                    | Define the conditions to match for the status to be WARNING. You can use the following variables: %{simStatus}, %{interfaceState}, %{cellId}, %{simIcc}, %{operator}, %{imsi}   | '%{interfaceState} =~ /disconnect/'                       |               |
| CRITICALSTATUS                   | Define the conditions to match for the status to be CRITICAL.  You can use the following variables: %{simStatus}, %{interfaceState}, %{cellId}, %{simIcc}, %{operator}, %{imsi} | '%{simStatus} =~ /LOCKED/ or %{simStatus} =~ /DETECTING/' |               |
| EXTRAOPTIONS                     | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                | --verbose                                                 |               |

</TabItem>
<TabItem value="Cpu" label="Cpu">

| Macro        | Description                                                                                                                                      | Valeur par défaut  | Obligatoire |
|:-------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNINGCPUUTILIZATION1M  | Thresholds on cpu utilization 1 min ago                                                                                                 |                   |             |
| CRITICALCPUUTILIZATION1M | Thresholds on cpu utilization 1 min ago                                                                                                 |                   |             |
| WARNINGCPUUTILIZATION5M  | Thresholds on cpu utilization 5 min ago                                                                                                 |                   |             |
| CRITICALCPUUTILIZATION5M | Thresholds on cpu utilization 5 min ago                                                                                                 |                   |             |
| WARNINGCPUUTILIZATION5S  | Thresholds on cpu utilization 5 sec ago                                                                                                 |                   |             |
| CRITICALCPUUTILIZATION5S | Thresholds on cpu utilization 5 sec ago                                                                                                 |                   |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                    |             |

</TabItem>
<TabItem value="Interfaces" label="Interfaces">

| Macro              | Description                                                                                                                                      | Valeur par défaut                                    | Obligatoire |
|:-------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------|:-----------:|
| OIDFILTER          | Choose OID used to filter interfaces (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr)                                                  | ifname                                               |             |
| OIDDISPLAY         | Choose OID used to display interfaces (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr)                                                 | ifname                                               |             |
| INTERFACENAME      | Define which interfaces to monitor (number expected). Example: 1,2... (empty means 'check all interfaces').                                                              |                                                      |             |
| WARNINGINDISCARD   | Thresholds                                                                                                                                       |                                                      |             |
| CRITICALINDISCARD  | Thresholds                                                                                                                                       |                                                      |             |
| WARNINGINERROR     | Thresholds                                                                                                                                       |                                                      |             |
| CRITICALINERROR    | Thresholds                                                                                                                                       |                                                      |             |
| WARNINGINTRAFFIC   | Thresholds                                                                                                                                       |                                                      |             |
| CRITICALINTRAFFIC  | Thresholds                                                                                                                                       |                                                      |             |
| WARNINGOUTDISCARD  | Thresholds                                                                                                                                       |                                                      |             |
| CRITICALOUTDISCARD | Thresholds                                                                                                                                       |                                                      |             |
| WARNINGOUTERROR    | Thresholds                                                                                                                                       |                                                      |             |
| CRITICALOUTERROR   | Thresholds                                                                                                                                       |                                                      |             |
| WARNINGOUTTRAFFIC  | Thresholds                                                                                                                                       |                                                      |             |
| CRITICALOUTTRAFFIC | Thresholds                                                                                                                                       |                                                      |             |
| CRITICALSTATUS     | Set critical threshold for status. You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display}                   | %{admstatus} eq "up" and %{opstatus} !~ /up\dormant/ |             |
| WARNINGSTATUS      | Set warning threshold for status. You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display}                    |                                                      |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). | --verbose                                            |             |

</TabItem>
<TabItem value="Memory" label="Memory">

| Macro        | Description                                                                                                                                                  | Valeur par défaut | Obligatoire |
|:------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
|  WARNINGUSAGE      | Thresholds on memory usage                                                                                                                                   |                   |             |
| CRITICALUSAGE     | Thresholds on memory usage                                                                                                                                   |                   |             |
| WARNINGUSAGEFREE  | Thresholds on free memory usage                                                                                                                              |                   |             |
| CRITICALUSAGEFREE | Thresholds on free memory usage                                                                                                                              |                   |             |
| WARNINGUSAGEPRCT  | Thresholds on memory percent usage                                                                                                                           |                   |             |
| CRITICALUSAGEPRCT | Thresholds on memory percent usage                                                                                                                           |                   |             
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).             |                   |             |

</TabItem>
<TabItem value="Uptime" label="Uptime">

| Macro        | Description                                                                                                                                      | Valeur par défaut | Obligatoire |
|:-------------|:-------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNING      | Threshold warning                                                                                                                                |                   |             |
| CRITICAL     | Threshold critical                                                                                                                               |                   |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). | --check-overload  |             |

</TabItem>
</Tabs>

3. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). Le service apparaît dans la liste des services supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails du service : celle-ci montre les valeurs des macros.

## Comment puis-je tester le plugin et que signifient les options des commandes ?

Une fois le plugin installé, vous pouvez tester celui-ci directement en ligne
de commande depuis votre collecteur Centreon en vous connectant avec
l'utilisateur **centreon-engine** (`su - centreon-engine`). Vous pouvez tester
que le connecteur arrive bien à superviser une ressource en utilisant une commande
telle que celle-ci (remplacez les valeurs d'exemple par les vôtres) :

```bash
/usr/lib/centreon/plugins/centreon_teldat_snmp.pl \
	--plugin=network::teldat::snmp::plugin \
	--mode=memory \
	--hostname=10.0.0.1 \
	--snmp-version='2c' \
	--snmp-community='my-snmp-community'  \
	--warning-usage='' \
	--critical-usage='' \
	--warning-usage-free='' \
	--critical-usage-free='' \
	--warning-usage-prct='' \
	--critical-usage-prct='' 
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: All memory usages are ok | '*memory*#memory.usage.bytes'=B;;;0;total'*memory*#memory.free.bytes'=B;;;0;total'*memory*#memory.usage.percentage'=%;;;0;100
```

### Diagnostic des erreurs communes

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/troubleshooting-plugins.md)
pour le diagnostic des erreurs communes des plugins Centreon.

### Modes disponibles

Dans la plupart des cas, un mode correspond à un modèle de service. Le mode est renseigné dans la commande d'exécution 
du connecteur. Dans l'interface de Centreon, il n'est pas nécessaire de les spécifier explicitement, leur utilisation est
implicite dès lors que vous utilisez un modèle de service. En revanche, vous devrez spécifier le mode correspondant à ce
modèle si vous voulez tester la commande d'exécution du connecteur dans votre terminal.

Tous les modes disponibles peuvent être affichés en ajoutant le paramètre
`--list-mode` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_teldat_snmp.pl \
	--plugin=network::teldat::snmp::plugin \
	--list-mode
```

Le plugin apporte les modes suivants :

| Mode                                                                                                                         | Modèle de service associé          |
|:-----------------------------------------------------------------------------------------------------------------------------|:-----------------------------------|
| cells-radio [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/teldat/snmp/mode/cellsradio.pm)]   | Net-Teldat-Cells-Radio-SNMP-custom |
| cpu [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/teldat/snmp/mode/cpu.pm)]                  | Net-Teldat-Cpu-SNMP-custom         |
| interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/teldat/snmp/mode/interfaces.pm)]    | Net-Teldat-Interfaces-SNMP-custom  |
| list-interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/listinterfaces.pm)] | Used for service discovery         |
| memory [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/teldat/snmp/mode/memory.pm)]            | Net-Teldat-Memory-SNMP-custom      |
| uptime [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/teldat/snmp/mode/uptime.pm)]            | Net-Teldat-Uptime-SNMP-custom      |

### Options disponibles

#### Options génériques

Les options génériques sont listées ci-dessous :

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
| --filter-perfdata                          | Keep only perfdata that match the regexp. Eg: adding --filter-perfdata='avg' will remove all metrics that do not contain 'avg' from performance data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-perfdata-adv                      | Filter perfdata based on a "if" condition using the following variables: label, value, unit, warning, critical, min, max. Variables must be written either %{variable} or %(variable). Eg: adding --filter-perfdata-adv='not (%(value) == 0 and %(max) eq "")' will remove all metrics whose value equals 0 and that don't have a maximum value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --explode-perfdata-max                     | Create a new metric for each metric that comes with a maximum limit. The new metric will be named identically with a '\_max' suffix). Eg: it will split 'used\_prct'=26.93%;0:80;0:90;0;100 into 'used\_prct'=26.93%;0:80;0:90;0;100 'used\_prct\_max'=100%;;;;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Convert storage free perfdata into used:     --change-perfdata=free,used,invert()      Convert storage free perfdata into used:     --change-perfdata=used,free,invert()      Scale traffic values automatically:     --change-perfdata=traffic,,scale(auto)      Scale traffic values in Mbps:     --change-perfdata=traffic\_in,,scale(Mbps),mbps      Change traffic values in percent:     --change-perfdata=traffic\_in,,percent()                                                                                                                                                                                                                                                                                                                                                                          |
| --extend-perfdata-group                    | Add new aggregated metrics (min, max, average or sum) for groups of metrics defined by a regex match on the metrics' names. Syntax: --extend-perfdata-group=regex,namesofnewmetrics,calculation\[,\[ne wuom\],\[min\],\[max\]\] regex: regular expression namesofnewmetrics: how the new metrics' names are composed (can use $1, $2... for groups defined by () in regex). calculation: how the values of the new metrics should be calculated newuom (optional): unit of measure for the new metrics min (optional): lowest value the metrics can reach max (optional): highest value the metrics can reach  Common examples:      Sum wrong packets from all interfaces (with interface need     --units-errors=absolute):     --extend-perfdata-group=',packets\_wrong,sum(packets\_(discard     \|error)\_(in\|out))'      Sum traffic by interface:     --extend-perfdata-group='traffic\_in\_(.*),traffic\_$1,sum(traf     fic\_(in\|out)\_$1)'   |
| --change-short-output --change-long-output | Modify the short/long output that is returned by the plugin. Syntax: --change-short-output=pattern~replacement~modifier Most commonly used modifiers are i (case insensitive) and g (replace all occurrences). Eg: adding --change-short-output='OK~Up~gi' will replace all occurrences of 'OK', 'ok', 'Ok' or 'oK' with 'Up'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --change-exit                              | Replace an exit code with one of your choice. Eg: adding --change-exit=unknown=critical will result in a CRITICAL state instead of an UNKNOWN state.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --range-perfdata                           | Rewrite the ranges displayed in the perfdata. Accepted values: 0: nothing is changed. 1: if the lower value of the range is equal to 0, it is removed. 2: remove the thresholds from the perfdata.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-uom                               | Mask the units when they don't match the given regular expression.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --opt-exit                                 | Replace the exit code in case of an execution error (i.e. wrong option provided, SSH connection refused, timeout, etc). Default: unknown.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-ignore-perfdata                   | Remove all the metrics from the service. The service will still have a status and an output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --output-ignore-label                      | Remove the status label ("OK:", "WARNING:", "UNKNOWN:", CRITICAL:") from the beginning of the output. Eg: 'OK: Ram Total:...' will become 'Ram Total:...'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-xml                               | Return the output in XML format (to send to an XML API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --output-json                              | Return the output in JSON format (to send to a JSON API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-openmetrics                       | Return the output in OpenMetrics format (to send to a tool expecting this format).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --output-file                              | Write output in file (can be combined with json, xml and openmetrics options). E.g.: --output-file=/tmp/output.txt will write the output in /tmp/output.txt.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-format                             | Applies only to modes beginning with 'list-'. Returns the list of available macros to configure a service discovery rule (formatted in XML).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-show                               | Applies only to modes beginning with 'list-'. Returns the list of discovered objects (formatted in XML) for service discovery.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --float-precision                          | Define the float precision for thresholds (default: 8).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource. Default: 'UTF-8'.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --hostname                                 | Name or address of the host to monitor (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --snmp-community                           | SNMP community (default value: public). It is recommended to use a read-only community.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-version                             | Version of the SNMP protocol. 1 for SNMP v1 (default), 2 for SNMP v2c, 3 for SNMP v3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --snmp-port                                | UDP port to send the SNMP request to (default: 161).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --snmp-timeout                             | Time to wait before sending the request again if no reply has been received, in seconds (default: 1). See also --snmp-retries.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --snmp-retries                             | Maximum number of retries (default: 5).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --maxrepetitions                           | Max repetitions value (default: 50) (only for SNMP v2 and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --subsetleef                               | How many OID values per SNMP request (default: 50) (for get\_leef method. Be cautious when you set it. Prefer to let the default value).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --snmp-autoreduce                          | Progressively reduce the number of requested OIDs in bulk mode. Use it in case of SNMP errors (By default, the number is divided by 2).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
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

#### Options des modes

Les options disponibles pour chaque modèle de services sont listées ci-dessous :

<Tabs groupId="sync">
<TabItem value="Cells-Radio" label="Cells-Radio">

| Option                      | Description                                                                                                                                                                                                                                             |
|:----------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-cell-id            | Filter cell modules by IMEI ID.                                                                                                                                                                                                                         |
| --custom-perfdata-instances | Define perfdata instances (default: '%(cellId) %(operator)'). You can use the following variables: %{cellId}, %{simIcc}, %{operator}                                                                                                                    |
| --unknown-status            | Define the conditions to match for the status to be UNKNOWN. You can use the following variables: %{simStatus}, %{interfaceState}, %{cellId}, %{simIcc}, %{operator}, %{imsi}                                                                           |
| --warning-status            | Define the conditions to match for the status to be WARNING (default: '%{interfaceState} =~ /disconnect/'). You can use the following variables: %{simStatus}, %{interfaceState}, %{cellId}, %{simIcc}, %{operator}, %{imsi}                            |
| --critical-status           | Define the conditions to match for the status to be CRITICAL (default: '%{simStatus} =~ /LOCKED/ \|\| %{simStatus} =~ /DETECTING/'). You can use the following variables: %{simStatus}, %{interfaceState}, %{cellId}, %{simIcc}, %{operator}, %{imsi}   |
| --warning-* --critical-*    | Thresholds. Can be: 'modules-cellradio-detected', 'module-cellradio-rsrp', ''module-cellradio-rsrq', 'module-cellradio-rscp', 'module-cellradio-csq' 'module-cellradio-snr'.                                                                            |

</TabItem>
<TabItem value="Cpu" label="Cpu">

| Option                   | Description                                                                              |
|:-------------------------|:-----------------------------------------------------------------------------------------|
| --warning-* --critical-* | Thresholds. Can be: 'cpu-utilization-5s', 'cpu-utilization-1m', 'cpu-utilization-5m'.    |

</TabItem>
<TabItem value="Interfaces" label="Interfaces">

| Option                   | Description                                                                                                                                                                                                                                                                                |
|:-------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached              | Memcached server to use (only one server).                                                                                                                                                                                                                                                 |
| --redis-server           | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                                                                            |
| --redis-attribute        | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                                                                    |
| --redis-db               | Set Redis database index.                                                                                                                                                                                                                                                                  |
| --failback-file          | Failback on a local file if redis connection failed.                                                                                                                                                                                                                                       |
| --memexpiration          | Time to keep data in seconds (Default: 86400).                                                                                                                                                                                                                                             |
| --statefile-dir          | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                                                                     |
| --statefile-suffix       | Define a suffix to customize the statefile name (Default: '').                                                                                                                                                                                                                             |
| --statefile-concat-cwd   | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.                                                |
| --statefile-format       | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                                                                      |
| --statefile-key          | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                                                               |
| --statefile-cipher       | Define the cipher algorithm to encrypt the cache (Default: 'AES').                                                                                                                                                                                                                         |
| --add-global             | Check global port statistics (By default if no --add-* option is set).                                                                                                                                                                                                                     |
| --add-status             | Check interface status.                                                                                                                                                                                                                                                                    |
| --add-duplex-status      | Check duplex status (with --warning-status and --critical-status).                                                                                                                                                                                                                         |
| --add-traffic            | Check interface traffic.                                                                                                                                                                                                                                                                   |
| --add-errors             | Check interface errors.                                                                                                                                                                                                                                                                    |
| --add-cast               | Check interface cast.                                                                                                                                                                                                                                                                      |
| --add-speed              | Check interface speed.                                                                                                                                                                                                                                                                     |
| --add-volume             | Check interface data volume between two checks (not supposed to be graphed, useful for BI reporting).                                                                                                                                                                                      |
| --check-metrics          | If the expression is true, metrics are checked (Default: '%{opstatus} eq "up"').                                                                                                                                                                                                           |
| --warning-status         | Set warning threshold for status. You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display}                                                                                                                                                              |
| --critical-status        | Set critical threshold for status. (Default: '%{admstatus} eq "up" and %{opstatus} ne "up"'). You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display}                                                                                                   |
| --warning-* --critical-* | Thresholds. Can be: 'total-port', 'total-admin-up', 'total-admin-down', 'total-oper-up', 'total-oper-down', 'in-traffic', 'out-traffic', 'in-error', 'in-discard', 'out-error', 'out-discard', 'in-ucast', 'in-bcast', 'in-mcast', 'out-ucast', 'out-bcast', 'out-mcast', 'speed' (b/s).   |
| --units-traffic          | Units of thresholds for the traffic (Default: 'percent\_delta') ('percent\_delta', 'bps', 'counter').                                                                                                                                                                                      |
| --units-errors           | Units of thresholds for errors/discards (Default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                          |
| --units-cast             | Units of thresholds for communication types (Default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                      |
| --nagvis-perfdata        | Display traffic perfdata to be compatible with nagvis widget.                                                                                                                                                                                                                              |
| --interface              | Define which interfaces to monitor (number expected). Example: 1,2... (empty means 'check all interfaces').                                                                                                                                                                                                       |
| --name                   | Allows to use interface name with option --interface instead of interface OID index (can be a regexp).                                                                                                                                                                                       |
| --speed                  | Define the actual maximum traffic speed you can have on the interfaces in megabits per second.                                                                                                                                                                                                                                 |
| --speed-in               | Define the actual maximum incoming traffic speed you can have on the interfaces in megabits per second.                                                                                                                                                                                                                                          |
| --speed-out              | Define the actual maximum outgoing traffic speed you can have on the interfaces in megabits per second.                                                                                                                                                                                                                                          |
| --map-speed-dsl          | Get interface speed configuration for interface types 'adsl' and 'vdsl2'.  Syntax: --map-speed-dsl=interface-src-name,interface-dsl-name  E.g: --map-speed-dsl=Et0.835,Et0-vdsl2                                                                                                            |
| --force-counters64       | Force to use 64-bit counters only. Can be used to improve performance.                                                                                                                                                                                                                    |
| --force-counters32       | Force to use 32-bit counters (even in snmp v2c and v3). Should be used when 64-bit counters are buggy.                                                                                                                                                                                   |
| --reload-cache-time      | Time in minutes before reloading cache file (default: 180).                                                                                                                                                                                                                                |
| --oid-filter             | Choose OID used to filter interfaces (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                                           |
| --oid-display            | Choose OID used to display interface (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                                          |
| --oid-extra-display      | Add an OID to display.                                                                                                                                                                                                                                                                     |
| --display-transform-src  | Modify the interface name displayed by using a regular expression. Example: adding --display-transform-src='eth' --display-transform-dst='ens'  will replace all occurrences of 'eth' with 'ens'                                                                                                                                                                                                                                                      |
| --display-transform-dst  | Modify the interface name displayed by using a regular expression. Example: adding --display-transform-src='eth' --display-transform-dst='ens'  will replace all occurrences of 'eth' with 'ens'                                                                                                                                                                                                                                                       |
| --show-cache             | Display cache interface data.                                                                                                                                                                                                                                                             |

</TabItem>
<TabItem value="Memory" label="Memory">

| Option                   | Description                                                             |
|:-------------------------|:------------------------------------------------------------------------|
| --warning-* --critical-* | Thresholds. Can be: 'usage' (B), 'usage-free' (B), 'usage-prct' (%).    |

</TabItem>
<TabItem value="Uptime" label="Uptime">

| Option                 | Description                                                                                                                                                                                                                                   |
|:-----------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached            | Memcached server to use (only one server).                                                                                                                                                                                                    |
| --redis-server         | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                               |
| --redis-attribute      | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                       |
| --redis-db             | Set Redis database index.                                                                                                                                                                                                                     |
| --failback-file        | Failback on a local file if redis connection failed.                                                                                                                                                                                          |
| --memexpiration        | Time to keep data in seconds (Default: 86400).                                                                                                                                                                                                |
| --statefile-dir        | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                        |
| --statefile-suffix     | Define a suffix to customize the statefile name (Default: '').                                                                                                                                                                                |
| --statefile-concat-cwd | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.   |
| --statefile-format     | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                         |
| --statefile-key        | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                  |
| --statefile-cipher     | Define the cipher algorithm to encrypt the cache (Default: 'AES').                                                                                                                                                                            |
| --warning-uptime       | Warning threshold.                                                                                                                                                                                                                            |
| --critical-uptime      | Critical threshold.                                                                                                                                                                                                                           |
| --add-sysdesc          | Display system description.                                                                                                                                                                                                                   |
| --force-oid            | Replace the default OID in order to retrieve the uptime (the OID must return a numeric value).  |
| --check-overload       | The uptime counter limit is 4294967296 centiseconds (~497 days). This option makes the plugin store the actual uptime by incrementing the number of revolutions of the counter when it resets to zero.                                                                                          |
| --reboot-window        | To be used with check-overload option. Time in milliseconds (default: 5000). You increase the chance of not missing a reboot if you decrease that value.                                                                                       |
| --unit                 | Select the unit for performance data and thresholds. May be 's'for seconds, 'm' for minutes, 'h' for hours, 'd' for days, 'w' for weeks. Default is seconds                                                                                   |

</TabItem>
</Tabs>

Pour un mode, la liste de toutes les options disponibles et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_teldat_snmp.pl \
	--plugin=network::teldat::snmp::plugin \
	--mode=memory \
	--help
```