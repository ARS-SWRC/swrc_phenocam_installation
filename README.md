# Instructions for enabling image transferring to Phenocam network
**USDA-ARS, Southwest Watershed Research Center**<br>
Guillermo Ponce<br>
guillermo.ponce@ars.usda.gov

This notebook is for documenting the steps for setting up the camera 
**StarDot NetCam-SC-IR** regarding *how to enable image transferring 
to the Phenocam network server*.  This should work as a "living document" for 
keeping track of future camera installations/updates details. All the 
information contained in this document comes from the Phenocam network 
documentation (see references) and this is just intended to be a quick reference 
for the USDA-ARS-SWRC personnel. 


### Adding a new camera?

If you have a completely new camera, never installed as part of the Phenocam 
network before, the first step is to contact [Bijan Seyednasrollah - seyednasrollah@fas.harvard.edu](mailto:seyednasrollah@fas.harvard.edu) and fill 
out this Phenocam survey:

https://docs.google.com/forms/d/e/1FAIpQLSdElsiEKj2W3L0Lwd8fi0XbmNmz4wspR9MtEdy05Xlw4Fw65w/viewform?c=0&w=1 


### Setting up the camera for transferring images
Follow these steps before running the Phenocam Installation Tool (PIT): 

1. Connect the camera to the network (*More details can be added here*)
2. The camera should be behind a firewall
3. Get the IP-address  (eg. 10.1.1.xxx)
4. Test telnet connection to the camera from command line (Linux/OSx) 
telnet 10.1.1.xxx  

If telnet connection works, continue with the next step, otherwise work with
the network administrator to make the camera available within the network. 

### The  Phenocam Installation Tool (PIT)

By using "git" software, clone/download the software shared for the Phenocam 
network installation, instructions can be found at:
(http://khufkens.github.io/phenocam-installation-tool/).

**Git** can be downloaded at https://git-scm.com/downloads

Git the PIT project.  At the command line type:

`git clone https://github.com/khufkens/phenocam-installation-tool.git`

This will create the folder `phenocam-installation-tool`. Now, change to that 
folder by typing:

`cd phenocam-installation-tool`


At this folder there is a shell script that should be used to setup the 
transferring options
`./PIT.sh IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE`
where:

Parameter     | Description
------------- | ------------------------------
IP            | ip address of the camera
USER          | user name (admin - if not set)
PASSWORD      | user password (on a new Stardot NetCam this is admin)
CAMERA        | the name of the camera / site
TIME_OFFSET   | difference in hours from UTC of the timezone in which the camera resides (always use + or - signs to denote differences from UTC)
TZ            | a text string corresponding to the local time zone (e.g. EST)
CRON_START    | first hour of the scheduled image acquisitions (e.g. 4 in the morning)
CRON_END      | last hour of the scheduled image acquisitions (e.g. ten at night, so 22 in 24-h notation)
CRON_INT      | interval at which to take pictures (e.g. 15, every 15 minutes - default phenocam setting is 30)
FTP_MODE      | active or passive (default = passive)
[all parameters are required!]

An example, at the command line:

`./PIT.sh 10.1.1.xxx admin xyz luckyhills -7 MST 4 22 30 passive`

This script configures the camera named `luckyhills`, located in the MST time 
zone (UTC -7) to take images every half hour between 4 and 22h. Also, it will 
output several messages, verify that the "upload images" section works well 
without showing any error messages.

> **Notes:**

> - Tests were made on the camera model **StarDot NetCam-SC-IR**
> - Inspect camera information by typing the IP-address of the camera in a web-browser, e.g. http://10.1.1.xxx/
> - Details related to the hardware/network setup can be added to this document

### References:

- https://phenocam.sr.unh.edu/pdf/PhenoCam_Install_Instructions.pdf 
- http://khufkens.github.io/phenocam-installation-tool/
