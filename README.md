<p align="center">
    <img src="src/web_interface/static/FACT_smaller.png" alt="FACT Logo" width="625" height="263"/>
</p>

# The Firmware Analysis and Comparison Tool (FACT)

[![codecov](https://codecov.io/gh/fkie-cad/FACT_core/branch/master/graph/badge.svg)](https://codecov.io/gh/fkie-cad/FACT_core)
[![Black Hat Arsenal](https://github.com/toolswatch/badges/blob/master/arsenal/asia/2018.svg)](http://www.toolswatch.org/2018/01/black-hat-arsenal-asia-2018-great-lineup/)

The Firmware Analysis and Comparison Tool (formerly known as Fraunhofer's Firmware Analysis Framework (FAF)) is intended to automate most of the firmware analysis process. 
It unpacks arbitrary firmware files and processes several analysis.
Additionally, it can compare several images or single files.  
Furthermore, Unpacking, analysis and compares are based on plug-ins guaranteeing maximal flexibility and expandability.  
More details and some screenshots can be found on our [project page](https://fkie-cad.github.io/FACT_core/).

## Requirments
### Hardware
FACT is designed as a multiprocess application, the more Cores and RAM, the better.
#### Minimal
* 4 Cores
* 8GB RAM

#### Recommended
* 16 Cores
* 64GB RAM

### Software
* Ubuntu 16.04 or 18.04
* Python 3.5 or above
* PIP
* git

It is possible to install FACT on any Linux distribution but the installer is limited to Ubuntu 16.04 and 18.04 at the moment.

## Installation

:exclamation: **Caution: FACT is not intended to be used as public internet service. The GUI is not a hardened WEB-application and it may take your server at risk!**

FACT consists of three components: frontend, database and backend. All components can be installed on one machine as well as on different machines. 
There is an automated installation program supporting Ubuntu 16.04 and 18.04 host systems.

### Pre-Install

```sh
$ sudo apt-get install git
$ git clone https://github.com/fkie-cad/FACT_core.git
$ cd FACT_core
$ src/bootstrap/pre_install.sh
```

Modify *src/config/main.cfg* and *src/config/mongod.conf* to suit your needs.
Especially, you should change the mongo passwords.
The database is initialized with these passwords on first start.  
Create the mongo data directory specified in *mongod.conf* and the firmware_file_storage_directory defined in *main.cfg*.
Make sure that the log directory exists as well.

If you have any additional plug-ins, copy/clone them into corresponding *src/plugins/* directory.  

:exclamation: **Reboot before executing the ./install.py** :exclamation:  
:exclamation: **You have to do the above steps before you do anything else** :exclamation:

### Simple One System Setup
:customs: **The installation script installs a lot of dependencies that may have different licenses**
  
After reboot, you can setup an all on one system installation by entering the FACT_core directory and executing:  

```sh
$ ./install.py
```
:beer: **Get a drink... Installation of the dependencies might take some time...** :tea:

For more advanced setups have a look at the help function of the installer:

```sh
$ ./install.py --help
```

### Installation with Nginx
The installer supports automated installation and configuration of nginx.
This will enable a ssl protected access to the frontend via port 443. 
Simply add the *-N* option to activate nginx support.

### Install Statistic Generation Cron Job
FACT provides statistics generated by triggering the *update_statistic* script. The install script can add a cronjob to trigger this script once an hour.
Just add the *-U* option on install.

## Usage
You can start FACT by executing the *start_all_installed_fact_components* scripts.
The script detects all installed components automatically.

```sh
$ ./start_all_installed_fact_components
```

Afterwards FACT can be accesed on <http://localhost:5000> and <https://localhost> (nginx), repspectively.  

You can shutdown the system by pressing *Ctrl + c* or by sending a SIGTERM to the *start_all_installed_faf_components* script.

### Advanced Usage

#### REST API
FACT provides a REST API. More information can be found [here](https://github.com/fkie-cad/FACT_core/wiki/rest-documentation).

#### User Management
FACT provides an optional basic authentication, role and user management. More information can be found [here](https://github.com/fkie-cad/FACT_core/wiki/Authentication).

## Update an older Installation
Checkout the new sources and rerun the installer.

## List of available community plug-ins and REST scripts
* Plug-ins
  * [Firmadyne](https://github.com/fkie-cad/FACT_firmadyne_analysis_plugin)
* REST
  * [PDF Report Generator](https://github.com/any333/FACT_analysis_report_pdf_convertor)

## Contribute
The easiest way to contribute is writing your own plug-in.
Our Developers Manual can be found [here](https://github.com/fkie-cad/FACT_core/wiki).

## Acknowledgments
This project is partly financed by [German Federal Office for Information Security (BSI)](https://www.bsi.bund.de) and others.  
The FACT project and the [Malware Analysis and Storage Sytem (MASS) project](https://mass-project.github.io/) form a code and plug-in sharing alliance.  

## License
```
    Firmware Analysis and Comparison Tool (FACT)
    Copyright (C) 2015-2018  Fraunhofer FKIE

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.
    
    Some plug-ins may have different licenses. If so, a license file is provided in the plug-in's folder.
```
