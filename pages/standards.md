# Standards for automated Data Collection
  
<p align="justify">Generally speaking, a standard is something established by an authority, a custom, or by general consent as a model or as an example.
Standards in computer science define conventions and procedures by broadly recognized bodies (e.g. standards organizations). They exist for operating systems, programming languages, data formats, communications protocols and electronic interfaces<sup>1</sup>. Standards help to build solutions (e.g. software) that works on different computers. They are usually available as printed or electronic public documents in the internet or libraries.</p>

<sup>1</sup> <a href="https://www.webopedia.com/TERM/S/standard.html"> https://www.webopedia.com/TERM/S/standard.html</a>

## OGC
<p align="justify">The abbreviation OGC stands for Open Geospatial Consortium. It is a international voluntary standards organization, formed in 1994. In the OGC more than 500 members are working together on a consensus process for the development and implementation of open standards for geospatial data and services.
Among the standards of the OGC are WMS (Web Map Services), WFS (Web Feature Service), KML (Keyhole Markup Language) or SOS (Sensor Observation Service).</p>

## SOS
### Overview

<p align="justify">The abbreviation SOS means Sensor Observation Service. It is a standard first defined by the OGC in 2007. The main objective of the SOS is to provide a possibility for accessing observations (or measurements) from sensors in a standardized and consistent way. Sensor systems may include in-situ, remote-sensing, fixed or mobile sensors. This is realized by providing an API (Application Programming Interface) for managing the connected sensors and retrieving the measurement data collected by the sensors.
The SOS acts like an intermediary between a client and a physical sensor device or an repository containing measurements (Fig. 1). SOS can also be understood as a web service in this context may be defined as a service offered by an electronic device (e.g. computer) to one another electronic device, which communicating with each other via the World Wide Web of the internet.</p>
                 
<img src="../images/sos1.jpg" alt="Tree rings" class="inline" width="500"/>

###### Fig. 1: Illustration of SOS as intermediary between a sensor system and a client
  
<p align="justify">The sensor data consist of a description of the sensors themselves realized using the Sensor Model Language (SensorML) and the actual measured values given in the Observations and Measurements (O&M) encoding format.  
The SOS consist of three core operations that must be provided by each implementation:</p>

1. GetCapabilities
- to query a service for a description of the service interface and the available sensor data
2. GetObservation: 
- to retrieve data for specific sensors
- measured values and their metadata is returned in the Observations and Measurements encoding format (O & M).
3. DescribeSensor:
- to return detailed information about a sensor or a sensor system
- uses the Sensor Model Language (SensorML)

Besides the three core operations, there are also “Transactional operations” and “Extended operations”.

More information about the OGC SOS standard can be found at:  
<a href="https://www.opengeospatial.org/standards/sos"> https://www.opengeospatial.org/standards/sos</a>

A detailed description of the SOS can be downloaded from here:  
<a href="https://portal.opengeospatial.org/files/?artifact_id=47599"> https://portal.opengeospatial.org/files/?artifact_id=47599 </a>

More information about the SensorML is provided at this website:  
<a href="https://www.opengeospatial.org/standards/sensorml"> https://www.opengeospatial.org/standards/sensorml</a>

The documentation for the SensorML can be retrieved following this link:  
<a href="https://portal.opengeospatial.org/files/?artifact_id=55939"> https://portal.opengeospatial.org/files/?artifact_id=55939</a>

Inforamtion about O&M are available here:  
<a href="https://www.opengeospatial.org/standards/om"> https://www.opengeospatial.org/standards/om</a>

The documentation for the O&M encoding system can be found here:  
<a href="http://portal.opengeospatial.org/files/?artifact_id=41510"> http://portal.opengeospatial.org/files/?artifact_id=41510 </a>

###	Example implementation with “istSOS”  

istSOS is an OGC SOS server implementation realized in the  Python language istSOS and is released under the GPL v2 l. It allows for managing and transmitting observations from sensors according to the OGC-SOS standard. istSOS comes with a Graphical User Interface for administration.

The project website is: <a href="http://istsos.org/"> http://istsos.org/ </a>

In the following, the installation of istSOS is described using the instructions provided here:  
<a href="http://istsos.org/en/latest/doc/installation.html"> http://istsos.org/en/latest/doc/installation.html</a>

Assuming that an installation of PostgreSQL database server exists and is running, the SOS implementation requires an Apache web server. The module “mod-wsgi” will enable the execution of Python scripts by the Apache-HTTP-Server.
```
sudo apt-get install apache2 libapache2-mod-wsgi
```

---  
* [Back to index page](../index.md)
