---
id: using-virtual-machines
title: Using a virtual machine (VM)
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

On its [download page](https://download.centreon.com), Centreon provides a ready-to-use virtual machine. This virtual machine is available in OVA format for VMware environments and for Oracle VirtualBox. It is based on the **Linux CentOS 7** operating system and includes a Centreon installation that allows you to easily start your first monitoring.

> The virtual machine is only suitable to use Centreon IT-100 or to test the solution.

The VM uses the **Thin Provision** option to save as much free space as possible on the disk (this is best practice).

## Prerequisites

The host machine must have the following characteristics:

- Processor: any recent Intel or AMD processor with at least 2 vCPUs.
- Memory: depending on your operating system, you will need at least 1 GB of RAM. To fully enjoy the Centreon experience, you need at least 2 GB of free memory.
- Hard Disk storage: The virtual machine requires at least 6.5 GB of free space on your hard disk. However, if you want keep using Centreon, it is recommended to have at least 10 GB as its size will grow over time.

## Step 1: Downloading the virtual machine

1. Make sure your virtualization tool (VMWare or VirtualBox) is installed on your machine and up to date.

2. Depending on the type of license you want to use, go to either of the following pages:

<Tabs groupId="sync">
<TabItem value="Download page (all types of license)" label="Download page (all types of license)">

1. Go to the [Centreon download page](https://download.centreon.com). In section 1, **Appliances** is already selected.

2. In section 2, select which version of Centreon you want to download.

3. In section 3, **Download your image**, click the **Download** button next to the type of VM you want (be careful not to mix up images for VMWare and VirtualBox). A new page opens.

    - If you want Centreon to contact you, fill in your details, then click **Download**.

    - Otherwise, click **Direct download**.

4. The file you have downloaded is an archive file. Extract its contents to the folder you want.

</TabItem>
<TabItem value="IT-100 free trial page" label="IT-100 free trial page">

1. Go to the [IT-100 free trial page](https://www.centreon.com/free-trial/).

2. Fill in the form to request your free IT-100 token, then follow the instructions you have received by email.

3. Further down the page, in the **Download Centreon** section, download the correct image for the type of VM you want (be careful not to mix up images for VMWare and VirtualBox).

4. The file you have downloaded is an archive file. Extract its contents to the folder you want.

</TabItem>
</Tabs>

## Step 2 : Installing the virtual machine

<Tabs groupId="sync">
<TabItem value="VMware" label="VMware">

1. Import the **centreon-central.ova** file into VMWare. A terminal window opens: wait for the server to start. When it is ready, the terminal shows the following message:

    ![image](../../assets/installation/VMW1.png)

2. According to how your network is set up, in the configuration of your virtual machine, add a network adapter and select the network through which the virtual machine can communicate with the resources it will monitor. Here is an example of configuration in VSphere 6:

    ![image](../../assets/installation/VMW_network_adapter.png)

</TabItem>
<TabItem value="Oracle VirtualBox" label="Oracle VirtualBox">

1. Import the **centreon-central.ova** file into VirtualBox. The VM is added to your list of VMs in VirtualBox.

    ![image](../../assets/installation/VB2.png)

2. In the right-hand panel, click **Settings**. The **Settings** dialog box opens.

3. On the **System** tab, check the **Hardware Clock in UTC Time** box.

4. According to how your network is set up, add a network adapter and select the network through which the virtual machine can communicate with the resources it will monitor. For instance:

    1. On the **Network** tab, select **Enable Network Adapter**.

    2. In the **Attached to** list, select **Bridged Adapter**.

    3. In the **Name** list, select the network card you want.

5. Click **OK**.

6. In the right-hand panel, click **Start** to start the VM. A terminal window opens: wait for the server to start. When it is ready, the terminal shows the following message:

    ![image](../../assets/installation/terminal_ready.png)

</TabItem>
</Tabs>

## Step 3 : Completing the configuration

1. Log in to the Centreon server using the following credentials: login: `root`, password: `centreon`.

2. To know your server's IP address, type `ip addr`. (By default, the VM has a qwerty keyboard: if you have an azerty keyboard, enter `ip qddr`.) The VM is configured to obtain an IP address from the DHCP server automatically.

    ![image](../../assets/installation/ip_addr.png)

3. Log in to the server from another machine, as user `root`, using the terminal you want and the IP address you obtained at the previous step.

4. The first time you connect to the server, instructions are displayed to help you complete the configuration.

    Change the following settings:

    - The timezone for the Centreon server. By default, it is set to UTC. This will set the time for the various Centreon logs.

        Use the following command:

        ```shell
        timedatectl set-timezone your_timezone
        ```

        For example, to set the timezone to Europe/London, type:

        ```shell
        timedatectl set-timezone Europe/London
        ```

        You can get a list of all available timezones using this command:

        ```shell
        timedatectl list-timezones
        ```

    - The timezone for the PHP server. To avoid errors, this should be the same as the timezone of the server. By default, it is set to Europe/London.

        1. Open the following file:

            ```shell
            /etc/php.d/50-centreon.ini
            ```

        2. In `date.timezone`, define the timezone you want.

        3. Restart the PHP server:

            ```shell
            systemctl restart php-fpm
            ```

    - The hostname of your server (this is optional). The default name is `centreon-central`. To change it, use the following command:

        ```shell
        hostnamectl set-hostname your-hostname
        ```

        For example, if you want your machine to be called `monitoring`, type:

        ```shell
        hostnamectl set-hostname monitoring
        ```

5. Add a MariaDB table partition: this step is mandatory. Your Centreon server will not work if this isn't done.

    1. Connect as user `centreon`:

        ```shell
        su - centreon
        ```

    2. Type the following command:

        ```shell
        /bin/php /usr/share/centreon/cron/centreon-partitioning.php
        ```

        The partition is created:

        ![image](../../assets/installation/partition_created.png)

    3. Connect back as user `root`:

        ```shell
        exit
        ```

    4. Restart the Centreon broker process so that changes are taken into account:

        ```shell
        systemctl restart cbd centengine gorgoned
        ```

        Your Centreon server is now ready to use.

        >Once those operations have been carried out, you can get rid of the message that describes them in the terminal. To do so, delete the following file:
        >
        >`/etc/profile.d/centreon.sh`

6. To log in to the web interface, go to `http://ip_address/centreon` or `http://FQDN/centreon`. (For example, a valid URL would be `http://192.168.1.44/centreon`.) 

7. Log in using the following credentials: Login: `admin`, password: `Centreon123!`. By default, your server has a predefined configuration to monitor the Centreon server itself.

8. According to your Centreon edition, you may have to [add a license](../../administration/licenses.md#add-your-license) (for exemple, a free IT-100 token: go to **Administration > Extensions > Manager** and click **Add Token**).

9. [Update](../../update/update-centreon-platform.md) your Centreon platform.

10. Change the passwords for the root and admin accounts. This is mandatory as the default passwords are available publicly in this documentation. You must also define a password for the MariaDB database.

11. [Secure your Centreon platform](../../administration/secure-platform.md).

12. You can now [monitor your first host](../../getting-started/first-supervision.md).

## Default credentials

- To log in to the Centreon web interface, the default credentials are: `admin`/`Centreon123!`.
- The server administration account (using SSH) is: `root`/`centreon`.
- The root password of the DBMS is not initialized.

> For security reasons, change these passwords after you complete the installation.

## Troubleshooting

If your VM will not start, check that you used the correct image for your virtualization tool (OVA format for VMware environments and OVF format for Oracle VirtualBox). You may also want to visit our community platform [The Watch](https://thewatch.centreon.com/).
