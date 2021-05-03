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
If not already done, psycopg2, a PostgreSQL adapter for Python is installed:  
```
sudo apt-get install python-psycopg2
```
Then the istSOS is downloaded from:  
<a href="https://sourceforge.net/projects/istsos/files/latest/download?source=files">https://sourceforge.net/projects/istsos/files/latest/download?source=files</a>

and will be extracted to /usr/local/:  
```
sudo tar -zxvf istSOS-2.1.1.tar.gz -C /usr/local/
```
Then, some permission need to be changed:  
```
sudo chmod 755 -R /usr/local/istsos
sudo chown -R www-data:www-data /usr/local/istsos/services
sudo chown -R www-data:www-data /usr/local/istsos/logs
sudo chown -R www-data:www-data /usr/local/istsos/wns
```

Now Apache and WSGI are configured:  
```
sudo vi /etc/apache2/sites-enabled/000-default.conf
```

These lines are added just before the last VirtualHost tag:  

```
#ServerName www.example.com
ServerAdmin webmaster@localhost
DocumentRoot /var/www/html

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined

WSGIScriptAlias /istsos /usr/local/istsos/application.py
Alias /istsos/admin /usr/local/istsos/interface/admin
Alias /istsos/modules /usr/local/istsos/interface/modules

<LocationMatch /istsos>
  Options +Indexes +FollowSymLinks +MultiViews
  AllowOverride all
  Require all granted
</LocationMatch>
```

Now the Apache server is restarted:  
```
sudo service apache2 restart
```
Finally, a PostGIS database “istsos” is created:  
```
sudo -u postgres createdb -E UTF8 istsos
sudo -u postgres psql -d istsos -c 'CREATE EXTENSION postgis'
```

### Example implementation with “52°North”  

A reference implementation of the OGC SOS specification has been published by 52°North (https://52north.org/). It is an interoperable interface for publishing and querying sensor data and metadata.  

The installation guide can be found here:  
<a href="https://wiki.52north.org/SensorWeb/SensorObservationServiceIVDocumentation#Installation">https://wiki.52north.org/SensorWeb/SensorObservationServiceIVDocumentation#Installation</a>  

#### Installation requirements  

-	Java Runtime environment (JRE) or Java Development Kit (JDK)
-	Apache Tomcat Open-Source Webserver and –container
-	A running DBMS, in this case the previously installed PostgreSQL database system

1)	Create database „sos“ in PostgreSQL using pgadmin4


<img src="../images/52north.jpg" alt="Databse “sos” in pgadmin 4" class="inline" width="450"/>

###### Fig. 1: Databse “sos” in pgadmin 4





---  
* [Back to index page](../index.md)
