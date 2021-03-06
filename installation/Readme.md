[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

# Installation
**PLEASE FOLLOW CAREFULLY AS THERE IS INFORMATION PRINTED IN THE TERMINAL THAT WILL NEED TO BE RETAINED**

**This tool currently supports Debian, RHEL, and SUSE based linux distributions.**
**Ubuntu 18.04 + is recommended.**

1. Clone this repository to the location where you want to run the web application from.  
```console
user@linux:~$ git clone https://github.com/matamorphosis/Scrummage
```
2. Navigate to the installation directory.
```console
user@linux:~$ cd installation
```
4. Run the dependencies.sh bash script with root privileges, to install all necessary dependencies. As part of this script it will install all python dependencies in the **"python_requirements.txt"** file and run the **"Create_Tables.py"** script to create all necessary tables in the back-end database. If you want to change the default username and database, which are both set to “scrummage” by default, change the following lines in the "dependencies.sh" script:  
```console
DATABASE="scrummage"  
USER="scrummage"  
```
Furthermore, by default an environment variable called "FLASK_ENV" is set to "development" as this variable is used by the web application to understand which environment it is running in. If the server is production change this variable to "production". To do this change the below line in the "dependencies.sh" script:  
```console
FLASK_ENVIRONMENT="development"
```
Command to run:
```console
user@linux:~$ sudo bash dependencies.sh
```

6. When the script finishes, it should **print out the username and database it has created; furthermore, a randomly generated password will also be printed to the screen**. While the script creates a new config.json file, located in the lib/plugins/common/configuration/ directory, please retain this information. Provide the details under **"postgresql"**. If you would like to create a new user, use the **"Create_User.py"** script located in the installation directory. The command is as follows:
```console
user@linux:~$ python3 Create_User.py --username/-u Username --password/-p Password --admin/-a [True | False] --blocked/-b [True | False]
```
7. Next you will either need to provide certificates **or** generate a self-signed certificate to use. In either case you will need to create a directory called "certs" in the root Scrummage directory:
```console
user@linux:~$ mkdir certs && cd certs
```
After which, you will then need to either provide a .key and .crt file to that directory **or** create the certificates with the command below:
```console
user@linux:~$ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt
```
8. Next, navigate to "/lib/plugins/common/config", and verify the web application details are correct under "web-app". Ensure the certificates are set correctly. Using the path "../certs/*FILE*":
```
"web-app": [
    {
        "debug": false,
        "host": "127.0.0.1",
        "port": 5000,
        "certificate-file": "../certs/certificate.crt",
        "key-file": "../certs/privateKey.key"
    }
],
```
9. Lastly, navigate to the parent directory and then to the bin directory and start the server. You should be able to access it on https://[HOST]:[PORT], [HOST] and [PORT] should match the JSON attributes above.
```console
user@linux:~$ cd ../bin
user@linux:~$ python3 main.py
```

# Tasks and APIs  
Refer to the Wiki Page https://github.com/matamorphosis/Scrummage/wiki/The-Long-List-of-Tasks

# Output Alert Options  
Refer to the Wiki Page https://github.com/matamorphosis/Scrummage/wiki/Output-Options

# Setting up Your First Task
Refer to the Wiki Page https://github.com/matamorphosis/Scrummage/wiki/Getting-Started-after-Installation
