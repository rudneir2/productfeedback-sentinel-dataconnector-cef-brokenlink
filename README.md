# productfeedback / sentinel / dataconnector / cef / broken link

## Intro / Description

To collect CEF logs from Security appliances that generate logs in CEF format, these are the steps:

1. create linux box
2. install CEF connector from content hub
3. in Data connectors, create the DCR and add Linux box to collect logs and have the AMA installed
4. if you are using Linux box on-premises, you will need to install Azure ARC before
5. after you have all steps above, you have to run a command from sentinel CEF data connector page on the linux box, so you have RSyslog daemon installed and configured

The issue/feedback below is regarding step 5 above.


## the issue / Customer impact

When you add CEF data connector via AMA, go to Connector page, you will find a command to run on linux CEF collector.

<img width="771" alt="image" src="https://github.com/rudneir2/productfeedback-sentinel-dataconnector-cef-brokenlink/assets/97529152/ef9db34a-4cc7-466b-8797-67bfd67c2de2">

If you simply copy / past on linux, this is the original command:

**sudo wget -O Forwarder_AMA_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py&&sudo python Forwarder_AMA_installer.py**

if we break down the command, we have two commands in the same line:

1) sudo wget -O Forwarder_AMA_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py
2) sudo python Forwarder_AMA_installer.py

## why the feedback/resolution is important?

many customers that run the command per Sentinel instruction don't observe the detail and the command run executing **only** the first command **wget**, and bring a very discrete error on Linux screen log.

**The issue:** if you have python3 installed on your Linux box, the command above will not work properly and you won't have rsyslog daemon configured!!

## Requested Product Group Action
as a suggestion, PG can provide a simple WARNING statement below the command, in the Sentinel page, explaining that if you use python3, the line command should be like this (see the highlighted part of command):

sudo wget -O Forwarder_AMA_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py&&sudo **python3** Forwarder_AMA_installer.py

## Work Around Details
below is a draft of how it could be:

<img width="769" alt="image" src="https://github.com/rudneir2/productfeedback-sentinel-dataconnector-cef-brokenlink/assets/97529152/c5559c6a-8874-429b-8362-84152035170b">



