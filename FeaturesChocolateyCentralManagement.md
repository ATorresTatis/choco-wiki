# Chocolatey Central Management (CCM) (Business Editions Only)

<!-- TOC -->

- [Usage](#usage)
- [Requirements](#requirements)
- [Installation Source](#installation-source)
  - [Use Specific Version](#use-specific-version)
- [Setup](#setup)
  - [Pre-Requisites](#pre-requisites)
  - [FQDN Usage](#fqdn-usage)
  - [Install CCM Components](#install-ccm-components)
    - [Installing chocolatey-management-database](#installing-chocolatey-management-database)
      - [Package Parameters](#package-parameters)
      - [Example](#example)
    - [Installing chocolatey-management-service](#installing-chocolatey-management-service)
      - [Package Parameters](#package-parameters-1)
      - [Example](#example-1)
    - [Installing chocolatey-management-web](#installing-chocolatey-management-web)
      - [Package Parameters](#package-parameters-2)
      - [Example](#example-2)
    - [Complete Installation Script](#complete-installation-script)
- [Chocolatey Configuration for CCM](#chocolatey-configuration-for-ccm)
  - [centralManagementReportPackagesTimerIntervalInSeconds](#centralmanagementreportpackagestimerintervalinseconds)
  - [centralManagementServiceUrl](#centralmanagementserviceurl)
  - [centralManagementReceiveTimeoutInSeconds](#centralmanagementreceivetimeoutinseconds)
  - [centralManagementSendTimeoutInSeconds](#centralmanagementsendtimeoutinseconds)
  - [centralManagementCertificateValidationMode](#centralmanagementcertificatevalidationmode)
- [Chocolatey Clients](#chocolatey-clients)
- [See It In Action](#see-it-in-action)
- [FAQ](#faq)
  - [Will this become available for lower editions of Chocolatey?](#will-this-become-available-for-lower-editions-of-chocolatey)
  - [What's the minimum version of the Chocolatey packages I need to use CCM?](#whats-the-minimum-version-of-the-chocolatey-packages-i-need-to-use-ccm)
  - [How can I add SQL Server Permissions through PowerShell](#how-can-i-add-sql-server-permissions-through-powershell)
- [Common Errors and Resolutions](#common-errors-and-resolutions)
  - [The specified path, file name, or both are too long](#the-specified-path-file-name-or-both-are-too-long)

<!-- /TOC -->

## Usage

Chocolatey Central Management (CCM) works in conjunction with [Chocolatey Agent](https://chocolatey.org/docs/features-agent-service) to bring full details of all Chocolatey controlled machines in your environment into one location, which is then accessible by the CCM Website.  Chocolatey Agent will regularly report information about what is installed on each machine, and whether any of that software is outdated, based on packages in available sources.

## Requirements

* Chocolatey (`chocolatey` package) v0.10.14+
* Chocolatey for Business (C4B) Edition
* Chocolatey Licensed Extension (`chocolatey.extension` package) v2.0.0+
* Chocolatey Agent (`chocolatey-agent` package) v0.9.0+
* CCM Database (`chocolatey-management-database` package) v0.1.0+
  * This deploys the CCM database schema to the specified SQL Server instance
* CCM Service (`chocolatey-management-service` package) v0.1.0+
  * This installs the CCM Service, which the Chocolatey Agent will communicate with.
* CCM Website (`chocolatey-management-web` package) v0.1.0+
  * This is the CCM front end website that is the main user interface of the application

## Installation Source

All the packages required to install CCM onto a machine(s) on your environment are located on the `chocolatey.licensed` feed.  This is the same place that you would install [Chocolatey Agent](https://chocolatey.org/docs/features-agent-service) and the [Chocolatey Extension](https://chocolatey.org/docs/installation-licensed) from.

The `chocolatey.licensed` source is automatically added to your Chocolatey instance when you install the Chocolatey Extension, however, as per the recommended installation best practices, this source is typically [disabled in an organisational context](https://chocolatey.org/docs/installation-licensed#installing-upgrading-in-secure-environments-without-internet-access).  As such, it may be necessary to first download the required nupkg's from the licensed source, and place them into your own internal repository.

### Use Specific Version

During the CCM Beta phase, it is necessary to download the CCM packages using a specific version.  For example:

~~~
choco download chocolatey-management-database --version 0.1.0-beta-20181009
~~~

**NOTE:** If the `chocolatey.licensed` source is disabled in your environment, it will be necessary to also use `--source https://licensedpackages.chocolatey.org/api/v2/` in the above commands.

## Setup

While it is envisioned that CCM will be installed across multiple servers, it is certainly possible to run CCM on a single server.

Currently, the CCM packages do not provision the SQL Server Database Permissions that are required for the CCM components to function.  It is assumed that the necessary permissions have already been provided (see the [FAQ](#how-can-i-add-sql-server-permissions-through-powershell) for one method of doing it).  By default, two users will require read/write permissions to the CCM Database:

* ChocolateyLocalAdmin - which, by default, runs the CCM Service
* IIS APPPOOL/ChocolateyCentralManagment - which, by default, runs the CCM IIS Application Pool

**NOTE:** If either of these users are changed during the installation of these components, the database permissions will need to be updated to reflect this.

Or, the required username/password for connecting to the CCM database are added as part of the connection string that is passed into the CCM packages during installation.

### Pre-Requisites

In order to install CCM, it is assumed that the following applications/software are installed:

* At least .Net Framework 4.6.1 on all machines
* IIS on the machine where the `chocolatey-management-web` package will be installed
* SQL Server on the machine where the `chocolatey-management-database` package will be installed

IIS can be installed using the following commands:

~~~
choco install IIS-WebServer --source windowsfeatures
choco install IIS-ApplicationInit --source windowsfeatures
~~~

We will not provide specific instruction on installing SQL Server. Any database platform that supports Entity Framework (EF) Core is supported, and as such there are too many scenarios to cover in this document.

For a list of Database products that support EF Core you can view the Microsoft Docs page [here](https://docs.microsoft.com/en-us/ef/core/providers/#current-providers)

### FQDN Usage

When installing the CCM Service, the default is to use the Fully Qualified Domain Name (FQDN) of the machine that it is being installed on.  As a result, there is an expectation that the certificate (either the self signed certificate that is created during installation, or the existing certificate which is configured with the [CertifcateThumbprint](#package-parameters-1) parameter) that is used to secure the transport layer of this service, also uses the same FQDN.

If this is not the case, it will be necessary to use the information the installer about the actual name for the machine that is being used.  When using a self signed certificate, this can be specified using the `CertifcateDnsName`, and when using an existing certificate, no additional parameters are required.  In both cases, it will be necessary to also set the `centralManagementServiceUrl` [configuration parameter](#centralmanagementserviceurl).  This can be done using the following command:

~~~
choco config set CentralManagementServiceUrl https://<accessible_name_of_machine>:24020/ChocolateyManagementService
~~~

### Install CCM Components

The CCM Components should be installed in the following order:

1. [chocolatey-management-database](#installing-chocolatey-management-database)
1. [chocolatey-management-service](#installing-chocolatey-management-service)
1. [chocolatey-management-web](#installing-chocolatey-management-web)

#### Installing chocolatey-management-database

**NOTE:** It is likely that additional package parameters are required which are specific to your environment.  Please carefully review the available [package parameters](#package-parameters) before proceeding.

In order to successfully install the chocolatey-management-database package onto a machine (using all default values), the following steps are required:

~~~
choco upgrade chocolatey --version 0.10.14-beta-20190402
choco upgrade chocolatey.extension --version 2.0.0-beta-20181009
choco upgrade chocolatey-agent --version 0.9.0-beta-20181009
choco upgrade chocolatey-management-database --version 0.1.0-beta-20181009
~~~

##### Package Parameters

This package creates the CCM Database with the following defaults:

* Database Connection String:   **Server=&lt;LOCAL COMPUTER FQDN NAME&gt;; Database=ChocolateyManagement; Trusted_Connection=True;**

You can override the package defaults using the following parameters:

* `/ConnectionString`
  * The SQL Server database connection string to be used to connect to the CCM database.
  * **NOTE:** Default Value: **Server=&lt;LOCAL COMPUTER FQDN NAME&gt;; Database=ChocolateyManagement; Trusted_Connection=True;**
* `/Database`
  * Name of the SQL Server database to use. Note that if you do not also pass `/ConnectionString`, it will be generated using this parameter value and `/SqlServerInstance` (using defaults for missing parameters);
  * **NOTE:** Default Value: **ChocolateyManagement**
* `/SqlServerInstance`
  * Instance name of the SQL Server database to connect to. Note that if you do not also pass `/ConnectionString`, it will be generated using this parameter value and `/Database` (using defaults for missing parameters);
  * **NOTE:** Default Value: **&lt;LOCAL COMPUTER FQDN NAME&gt;**

##### Example

Let's assume that you want to install the CCM Database onto a machine that will access a SQL Server instance called `SQLSERVERCCM`, on a domain machine called `MACHINE1` which is part of the domain `ccmtest`, using a specific user name (ccmservice) and password combination.  In this scenario, the installation command would look like the following:

~~~
choco upgrade chocolatey-management-database --package-parameters-sensitive="'/ConnectionString=""Server=MACHINE1\SQLSERVERCCM;Database=ChocolateyManagement;User ID=ccmtest\ccmservice;Password=Password01;""'"
~~~

**NOTE:** This command makes use of `package-parameters-sensitive` to ensure that the sensitive information is not leaked out into log files.

#### Installing chocolatey-management-service

**NOTE:** It is likely that additional package parameters are required which are specific to your environment.  Please carefully review the available [package parameters](#package-parameters-1) before proceeding.

In order to successfully install the chocolatey-management-service package onto a machine (using all default values), the following steps are required:

**NOTE:** Due to an issue that was identified in the initial release of CCM, the port number parameter is required.

~~~
choco upgrade chocolatey --version 0.10.14-beta-20190402
choco upgrade chocolatey.extension --version 2.0.0-beta-20181009
choco upgrade chocolatey-agent --version 0.9.0-beta-20181009
choco upgrade chocolatey-management-service --version 0.1.0-beta-20181009 --params="'/PortNumber=24020'"
~~~

##### Package Parameters

This package creates the CCM Service with the following defaults:

* Service Name:                         **chocolatey-management-service**
* Service Displayname                   **Chocolatey Management Service**
* Description:                          **Chocolatey Management Service is a background service for Chocolatey.**
* Service Startup:                      **Automatic**
* Service Username:                     **ChocolateyLocalAdmin**
* Database Connection String:           **Server=&lt;LOCAL COMPUTER FQDN NAME&gt;; Database=ChocolateyManagement; Trusted_Connection=True;**
* Service Listening Port:               **24020**
* Self-Signed Certificate Domain Name:  **DNS name of the local computer**

You can override the package defaults using the following parameters:

* `/Username`
  * Username to install the management service as;
  * **NOTE:** Default Value: **ChocolateyLocalAdmin**
* `/Password`
  * Password to use for the management service account;
  * **NOTE:** Automatically generated secure password
* `/EnterPassword`
  * This will prompt you to enter the password, during install, for the username (provided via the `/Username` parameter) the management service will run under;
  * **NOTE:** Default Value: Not provided
* `/ConnectionString`
  * The SQL Server database connection string to be used to connect to the CCM database;
  * **NOTE:** Default Value: **Server=&lt;LOCAL COMPUTER FQDN NAME&gt;; Database=ChocolateyManagement; Trusted_Connection=True;**
* `/Database`
  * Name of the SQL Server database to use. Note that if you do not also pass `/ConnectionString`, it will be generated using this parameter value and `/SqlServerInstance` (using defaults for missing parameters);
  * **NOTE:** Default Value: **ChocolateyManagement**
* `/SqlServerInstance`
  * Instance name of the SQL Server database to connect to. Note that if you do not also pass `/ConnectionString`, it will be generated using this parameter value and `/Database` (using defaults for missing parameters);
  * **NOTE:** Default Value: **&lt;LOCAL COMPUTER FQDN NAME&gt;**
* `/PortNumber`
  * The port the Chocolatey Management Service will listen on. This will automatically create a rule to open the firewall on this port;
  * **NOTE:** Default Value **24020**
* `/CertificateDnsName`
  * The DNS name of the self-signed certificate that is generated if no existing certificate thumbprint is provided using the `/CertificateThumbprint` parameter is provided;
  * **NOTE:** Default Value: **&lt;LOCAL COMPUTER FQDN NAME&gt;**
* `/CertificateThumbprint`
  * By default the CCM Service uses a self-signed SSL certificate to secure communication with the clients. Use this parameter to provide the thumbprint of a certificate to use instead. **Note that if you use this the certificate must already be in the LocalMachine\TrustedPeople Certificate Store on the Chocolatey Management Service computer**;
  * **NOTE:** Default Value: Not applicable as if not provided, a new Self Signed Certificate will be generated
* `/NoRestartService`
  * Explicit request not to restart the service
  * **NOTE:** Default Value: Not provided
* `/DoNotReinstallService`
  * Explicit request not to reinstall the service
  * **NOTE:** Default Value: Not provided

##### Example

Let's assume that you want to install the CCM Service with a specific connection string in order to connect to the CCM Database, as well as configure the CCM Service to use a specific user name and password, as well as alter the Port number that the CCM Service will be hosted on.  The necessary installation command would look like the following:

~~~
choco upgrade chocolatey-management-service --package-parameters-sensitive="'/PortNumber=24021 /Username=ccmtest\ccmservice /Password=Password01 /ConnectionString=""Server=MACHINE1\SQLSERVERCCM;Database=ChocolateyManagement;User ID=ccmtest\ccmservice;Password=Password01;""'"
~~~

**NOTE:** This command makes use of `package-parameters-sensitive` to ensure that the sensitive information is not leaked out into log files.

#### Installing chocolatey-management-web

**NOTE:** It is likely that additional package parameters are required which are specific to your environment.  Please carefully review the available [package parameters](#package-parameters-2) before proceeding.

In order to successfully install the chocolatey-management-web package onto a machine (using all default values), the following steps are required:

~~~
choco upgrade aspnetcore-runtimepackagestore
choco upgrade dotnetcore-windowshosting
choco upgrade chocolatey --version 0.10.14-beta-20190402
choco upgrade chocolatey.extension --version 2.0.0-beta-20181009
choco upgrade chocolatey-agent --version 0.9.0-beta-20181009
choco upgrade chocolatey-management-web --version 0.1.0-beta-20181009
~~~

**NOTE:** Once installed, when you access the CCM Website you will be prompted to provide a username and password to access the site.  By default, the username is `ccmadmin` and the password is `123qwe`.  After you input this, you will be prompted to change the password.

##### Package Parameters

This package creates the CCM Website and Application Pool with the following defaults:

* IIS Web Application Pool:                 **ChocolateyCentralManagement**
  * enable32BitAppOnWin64:                **True**
  * managedPipelineMode:                  **Integrated**
  * managedRuntimeVersion:                &lt;blank&gt;
  * startMode:                            **AlwaysRunning**
  * processModel.idleTimeout:             **0**
  * recycling.periodicRestart.schedule:   **Disabled**
  * recycling.periodicRestart.time:       **0**
* Website Name:                             **ChocolateyCentralManagement**
  * PortBinding:                          **80**
  * applicationDefaults.preloadEnabled:   **True**
* SQL Server Instance:                      **&lt;LOCAL COMPUTER FQDN NAME&gt;**
* Connection String:                        **Server=&lt;LOCAL COMPUTER FQDN NAME&gt;; Database=ChocolateyManagement; Trusted_Connection=True;**

You can override the package defaults using the following parameters:

* `/ConnectionString`
  * The SQL Server database connection string to be used to connect to the CCM Database;
  * **NOTE:** Default Value: **Server=&lt;LOCAL COMPUTER FQDN NAME&gt;; Database=ChocolateyManagement; Trusted_Connection=True;**
* `/Database`
  * Name of the SQL Server database to use. Note that if you do not also pass `/ConnectionString`, it will be generated using this parameter value and `/SqlServerInstance` (using defaults for missing parameters);
  * **NOTE:** Default Value: **ChocolateyManagement**
* `/SqlServerInstance`
  * Instance name of the SQL Server database to connect to. Note that if you do not also pass `/ConnectionString`, it will be generated using this parameter value and `/Database` (using defaults for missing parameters);
  * **NOTE:** Default Value: **&lt;LOCAL COMPUTER FQDN NAME&gt;**
* `/Username`
  * The username that the IIS WebApplicationPool will run under. If this is not provided the pool will run under the default account. Note that if you provide this you must also provide either the `/Password` or `/EnterPassword` parameter;
  * **NOTE:** Default Value: **IIS APPPOOL\ChocolateyCentralManagement**
* `/Password`
  * The password for the username (provided via the `/Username` parameter) the IIS WebApplicationPool will run under;
  * **NOTE:** Automatically generated secure password
* `/EnterPassword`
  * This will prompt you to enter the password, during install, for the username (provided via the `/Username` parameter) the IIS WebApplicationPool will run under;
  * **NOTE:** Default Value: Not provided

##### Example

Let's assume that you want to install the CCM Website with a specific connection string in order to connect to the CCM Database, as well as configure the IIS Application Pool to use a specific user name and password.  The
necessary installation command would look like the following:

~~~
choco upgrade chocolatey-management-web --package-parameters-sensitive="'/ConnectionString=""Server=MACHINE1\SQLSERVERCCM;Database=ChocolateyManagement;User ID=ccmtest\ccmservice;Password=Password01;"" /Username=ccmwebserver\ccmserviceuser /Password=Password01'"`
~~~

**NOTE:** This command makes use of `package-parameters-sensitive` to ensure that the sensitive information is not leaked out into log files.

#### Complete Installation Script

The following is a complete installation script that can be used as an example of how to install all necessary CCM components and configuration on a single machine, using all the default values.  To use values other than the default, see the relevant parameters section for the [chocolatey-management-database](#package-parameters), [chocolatey-management-service](#package-parameters-1) and [chocolatey-management-web](#package-parameters-2) packages.  And refer to the [Chocolatey Configuration](#chocolatey-configuration-for-ccm) for further information about global settings for CCM.

~~~
# Find FDQN for current machine
$hostName = [System.Net.Dns]::GetHostName()
$domainName = [System.Net.NetworkInformation.IPGlobalProperties]::GetIPGlobalProperties().DomainName

if(-Not $hostName.endswith($domainName)) {
  $hostName += "." + $domainName
}

choco upgrade chocolatey -y --version 0.10.14-beta-20190402
choco upgrade chocolatey.extension -y --version 2.0.0-beta-20181009
choco upgrade chocolatey-agent -y --version 0.9.0-beta-20181009

choco upgrade chocolatey-management-database -y --version 0.1.0-beta-20181009

choco upgrade chocolatey-management-service -y --version 0.1.0-beta-20181009 --params="'/PortNumber=24020'"

choco upgrade aspnetcore-runtimepackagestore -y
choco upgrade dotnetcore-windowshosting -y 
choco upgrade chocolatey-management-web -y --version 0.1.0-beta-20181009

# CCM Configuration
choco config set --name="'centralManagementReportPackagesTimerIntervalInSeconds'" --value="'1860'"
choco config set --name="'centralManagementServiceUrl'" --value="'https://$($hostname):24020/ChocolateyManagementService'"
choco config set --name="'centralManagementReceiveTimeoutInSeconds'" --value="'60'"
choco config set --name="'centralManagementSendTimeoutInSeconds'" --value="'60'"
choco config set --name="'centralManagementCertificateValidationMode'" --value="'PeerOrChainTrust'"
choco feature enable --name="'useChocolateyCentralManagement'"
~~~

> Best practices in scripts are noted here:
> * Use `upgrade` instead of `install` - upgrade is more making the script reusable when newer versions are available.
> * Always use `-y` to ensure nothing stops and prompts for more than 30 seconds.
> * When using options prefer a longer name (`--name` versus the short `-n`) to make the scripts more self-documenting
> * When using options that have a value passed, add an `=` between and surround the value with `"''"` (`--name="'value'"`). This ensures that the argument is not split between different versions/editions of Chocolatey. This also ensures that values like `.` and `\\` are not escaped by PowerShell.

## Chocolatey Configuration for CCM

The following configuration values, with their default values, are added into the chocolatey.config file after installing CCM and it's dependent packages.

### centralManagementReportPackagesTimerIntervalInSeconds

This is the length of time, in seconds, that the Chocolatey Background Agent will wait between each attempt to report into CCM.

**Default Value:** 1800

### centralManagementServiceUrl

This is the URL that is used by the Chocolatey Background Agent to report into CCM, and also by the CCM Service to register the URL that it is listening for incoming reports on.

**Default Value:** _blank_

**NOTE:** If left blank, the CCM Service will construct a URL based on the default Port number which is 24020, and the FQDN of the machine that the service is being executed on.  However, Chocolatey Agent will not be able to report into CCM, if a value is not provided.

**NOTE:** Due to the fact that both the Chocolatey Background Agent and CCM Service use this configuration value, if both of these services are located on the same machine, the Chocolatey Background Service on that machine has to report into the CCM Service on that machine.  It can't report into another instance.

### centralManagementReceiveTimeoutInSeconds

This is the length of time, in seconds, that a connection to CCM can remain inactive, during which no application messages are received, before it is dropped.

**Default Value:** 30

### centralManagementSendTimeoutInSeconds

This is the length of time, in seconds, that a write operation against CCM has to complete before the transport raises an exception.

**Default Value:** 30

### centralManagementCertificateValidationMode

This captures the options for determining the validity of the CCM Service certificate obtained using SSL/TLS negotiation.

**Default Value:** PeerOrChainTrust

**Valid Values:** None, PeerTrust, ChainTrust, PeerOrChainTrust, Custom

## Chocolatey Clients

Once CCM has been set up and configured, each machine that you want to report into CCM will have to be enabled.  This can be done by doing the following:

~~~powershell
choco config set CentralManagementServiceUrl https://MACHINE1:24020/ChocolateyManagementService
choco feature enable --name="'useChocolateyCentralManagement'"
~~~

Here, the full URL, including the port number, to where the CCM service was installed to is being set, and then the `useChocolateyCentralManagement` feature is being enabled. In your environment you would replace `MACHINE1:24020` with the FQDN name of your server and the port being used.

**NOTE:** By default, this feature is disabled, and will need to be turned on.

**NOTE:** If not set, the CCM Service will construct a URL based on the default Port number which is 24020, and the FQDN of the machine that the service is being executed on.  However, Chocolatey Agent will not be able to report into CCM, if a value is not provided.

[Additional configuration](#chocolatey-configuration-for-chocolatey-central-management) exists for CCM Service, which allows fine grained control of how Chocolatey Agent will report into CCM.

## See It In Action

## FAQ

### Will this become available for lower editions of Chocolatey?

CCM will only be available in Chocolatey for Business (C4B).

### What's the minimum version of the Chocolatey packages I need to use CCM?

See [Requirements](#requirements).

### How can I add SQL Server Permissions through PowerShell

The following script is an example of how to add `db_owner` permissions to a SQL Server Database

**NOTE:** You will need to change `MACHINE1\SQLSERVERCCM` and `ChocolateyManagement` to the actual name of the SQL Server Instance and Database being used, and this script will have to be run by someone who has the correct permissions to the SQL Server Instance.  In addition, change the `$username` variable for each user that requires permission to the database.
~~~
$username = 'CCMSERVER\ChocolateyLocalAdmin'
$database = 'ChocolateyManagement'
$chocolateyLocalAdminQuery = "
USE [master]
CREATE LOGIN [$username] FROM WINDOWS WITH DEFAULT_DATABASE=[master]
USE [$database]
CREATE USER [$username] FOR LOGIN [$username]
USE [$database]
ALTER ROLE [db_owner] ADD MEMBER [$username]
"

$Connection = New-Object System.Data.SQLClient.SQLConnection
$Connection.ConnectionString = "server='MACHINE1\SQLSERVERCCM';database='master';trusted_connection=true;"
$Connection.Open()
$Command = New-Object System.Data.SQLClient.SQLCommand
$Command.CommandText = $chocolateyLocalAdminQuery
$Command.Connection = $Connection
$Command.ExecuteNonQuery()
$Connection.Close()
~~~

## Common Errors and Resolutions

### The specified path, file name, or both are too long

This error can occur when installing the `chocolatey-management-web` package.  Due to the nested folder structure contained within this package, when extracting to the default cache location, the path can become too long.  This problem is known is occur in the 0.1.0-beta-20181009 release of this package, and it should be corrected in subsequent releases.  As a workaround, adding the following parameters to the install command should allow the installation to complete successfully:

~~~
--cache-location="'C:\Temp\choco'"
~~~
