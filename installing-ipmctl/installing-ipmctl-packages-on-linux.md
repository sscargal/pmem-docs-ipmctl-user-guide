# Installing IPMCTL packages on Linux

The `ipmctl` utility is available in many Linux distribution package repositories.  This approach is the easiest to implement and maintain, compared with [building and installing ipmctl from source](building-and-installing-ipmctl-from-source-on-linux.md). However, the version of ipmctl available in the package repository may not be current.

{% tabs %}
{% tab title="Fedora" %}

{% endtab %}

{% tab title="RHEL & CentOS" %}
The ipmctl package is available on CentOS, RHEL, and RHEL for SAP HANA v7.5 or later in the EPEL repository \(Extra Packages for Enterprise Linux\).

1\) Verify the EPEL repository is active:

```text
$ yum repolist
```

Example:

```text
$ sudo yum repolist
repo id                                                       repo name                                                                                          status
epel/x86_64                                                   Extra Packages for Enterprise Linux 7 - x86_64                                                     13,217
```

If the EPEL repository is not listed, install and activate it using:

```text
$ sudo yum install epel-release
```

2\) Query the package repository to confirm that ipmctl is available:

```text
sudo yum search ipmctl
```

Example:

```text
$ sudo yum info ipmctl 

Available Packages
Name        : ipmctl
Arch        : x86_64
Version     : 01.00.00.3474
Release     : 2.el7
Size        : 70 k
Repo        : epel/x86_64
Summary     : Utility for managing Intel Optane DC persistent memory modules
URL         : https://github.com/intel/ipmctl
License     : BSD
Description : Utility for managing Intel Optane DC persistent memory modules
            : Supports functionality to:
            : Discover DCPMMs on the platform.
            : Provision the platform memory configuration.
            : View and update the firmware on DCPMMs.
            : Configure data-at-rest security on DCPMMs.
            : Monitor DCPMM health.
            : Track performance of DCPMMs.
            : Debug and troubleshoot DCPMMs.
```

3\) Install the ipmctl package:

```text
sudo yum install ipmctl
```

4\) Review the help and man pages or continue to the [Basic Usage](../basic-usage.md) section of this user guide for a quick introduction and more information.

```text
$ sudo ipmctl help
```
{% endtab %}

{% tab title="SLES & OpenSUSE" %}
The ipmctl package is available in the default package repository on SUSE, OpenSUSE, and SUSE for SAP HANA 12.4 or later.

Step 1\) Query the package repository to confirm that ipmctl is available:

```text
sudo zypper search ipmctl
```

Example:

```text
$ sudo zypper info ipmctl 

Information for package ipmctl:
-------------------------------
Repository     : SLES12-SP4-Updates                                            
Name           : ipmctl                                                        
Version        : 01.00.00.3440-3.8.2                                           
Arch           : x86_64                                                        
Vendor         : SUSE LLC <https://www.suse.com/>                              
Support Level  : Level 3                                                       
Installed Size : 3.2 MiB                                                       
Installed      : No                                                            
Status         : not installed                                                 
Source package : ipmctl-01.00.00.3440-3.8.2.src                                
Summary        : Utility for managing Intel Optane DC persistent memory modules
Description    :                                                               
    Utility for managing Intel Optane DC persistent memory modules
    Supports functionality to:
    * Discover PMMs on the platform.
    * Provision the platform memory configuration.
    * View and update the firmware on PMMs.
    * Configure data-at-rest security on PMMs.
    * Monitor PMM health.
    * Track performance of PMMs.
    * Debug and troubleshoot PMMs.
```

3\) Install the ipmctl package:

```text
sudo zypper install ipmctl
```

4\) Review the help and man pages or continue to the [Basic Usage](../basic-usage.md) section of this user guide for a quick introduction and more information.

```text
$ sudo ipmctl help
```
{% endtab %}

{% tab title="Ubuntu" %}

{% endtab %}

{% tab title="Debian" %}

{% endtab %}
{% endtabs %}

### Using ipmctl

Go to the [Basic Usage](../basic-usage.md) section of this user guide for more information.
