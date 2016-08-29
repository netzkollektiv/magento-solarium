Solr search extension for Magento
================
**We are sorry but we cannot offer customer support for this extension, and it is provided "as-is" for free.**

The default MySQL Fulltext search is not performing very well on more serious shops. It is slow and the results aren't very relevant. Apache's Solr does a much better job in delivering fast and relevant results. We have used the Solarium PHP library to build Solr into Magento CE.

**This project is abandoned. Please do NOT contact any of the developers for support.**

## Features

  * Free and Open Source
  * Fast results
  * Can handle high number of products
  * Fast autocomplete search query while typing
  * Optional: Show products with images as suggestions
  * Autocorrect typos in search terms
  * "Did you mean..." suggestions
  * Solr 3 & 4 support
  * Solr HTTP authentication support

## Requirements

  * Magento Community Edition 1.6+
  * A working Solr 3.x or 4.x server

## Installation & Usage

setup-solr-magento-community
============================

How to setup Solr for Magento Community edition version 1.9

This How-To describes the necessary steps to setup Solr in Magento community edition 1.9 using the excellent module which integrates Solr into Magento by Jeroen Vermeulen: https://github.com/jelqui/magento-solarium.git.

It took me some time to get this running, so maybe it will help some of you.

In case, anything is missing or you have further improvements / caveats - feel free to submit pull requests :)

I used Ubuntu 14 / 12 for this.

The following steps are needed:

* Install Java: ```sudo apt-get install openjdk-7-jdk```
* ```sudo apt-get update```
* Install Tomcat server to serve Solr: ```sudo apt-get install tomcat7 tomcat7-admin```
* Download Solr: ```wget http://archive.apache.org/dist/lucene/solr/4.10.1/solr-4.10.1.tgz``` (or other version)
* Extract it: ```tar -xzf solr-4.10.1.tgz```
* Create a directory for Solr: ```sudo mkdir /opt/solr```
* ```sudo cp -r solr-4.10.1/example/solr/* /opt/solr/```
* ```sudo cp solr-4.10.1/example/webapps/solr.war /opt/solr/```
* ```sudo cp -r solr-4.10.1/example/lib/ext/* /var/lib/tomcat7/shared/```
* Install Jeroen's extension into your magento store, e.g. using modman inside /var/www/magento: ```modman init``` ```modman clone https://github.com/jeroenvermeulen/magento-solarium```
* Copy necessary config files from the module: ```sudo cp /var/www/magento/.modman/magento-solarium/app/code/community/JeroenVermeulen/Solarium/docs/schema.xml /opt/solr/collection1/conf/.```
* ```sudo cp /var/www/magento/.modman/magento-solarium/app/code/community/JeroenVermeulen/Solarium/docs/solrconfig.xml /opt/solr/collection1/conf/.```
* Create data directory: ```sudo mkdir /opt/solr/data```
* Make it readable/writable for Tomcat: ```sudo chown tomcat7 /opt/solr/data```
* Add the data directory to Solr Config: ```sudo vi /opt/solr/collection1/conf/solrconfig.xml -> "<dataDir>${solr.data.dir:/opt/solr/data}</dataDir>"``` (With -> I will imply that you edit the appropriate line in vi text editor)

* Make Tomcat serve Solr: ```sudo vi /etc/tomcat7/Catalina/localhost/solr.xml``` -> 
```
    <?xml version="1.0" encoding="utf-8"?>
    <Context docBase="/opt/solr/solr.war" debug="0" crossContext="true">
    <Environment name="solr/home" type="java.lang.String" value="/opt/solr" override="true"/>.
    </Context>
```
* Setup the logging (otherwise Solr won't run):
  * ```sudo cp /solr-4.10.1/example/lib/ext/* /usr/share/tomcat7/lib```
  * ```sudo cp solr-4.10.1/example/resources/log4j.properties /usr/share/tomcat7/lib/```
  * ```sudo vi /usr/share/tomcat7/lib/log4j.properties -> solr.log=/var/log/solr```
  * ```sudo mkdir /var/log/solr```
  * ```sudo chown tomcat7:tomcat7 /var/log/solr```
  * ```sudo vi /etc/logrotate.d/solr -> /var/log/solr/solr.log { copytruncate daily rotate 5 compress missingok create 640 tomcat7 tomcat7 }``` (This will make sure the log file does not grow indefinitely)
* Restart Tomcat ```sudo /etc/init.d/tomcat7 restart```
* Optional: Secure your Tomcat to only use given IPs:
  * ```sudo vi /etc/tomcat7/context.xml``` -> Add ```<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.0\.0\.1|65\.182\.48\.139"/>``` within ```<Context>``` node to allow only localhost and our IP address
  * Restart Tomcat again
* Check if Solr is working: http://localhost:8080/solr should show Solr admin panel
* Configure the module by inputting your Solr connection data in the Magento backend in System Configuration
* Afterwards reindex the search index
* Then check if it is working -> should have an auto suggest with images and should be error tolerant, e.g. search for Jacet instead of Jacket should give you results.

* Make sure you run Magento 1.6 or newer
* Install a Solr Server, version 3.x or 4.x
* Make sure it is running, for example check the Solr web interface.
* Copy schema.xml and solrconfig.xml to the solr/config dir inside the Solr Server dir. For a multi-core or Solr 4.x server, by default the dir is solr/collection1/config.
* Restart the Solr Server
* Install this extension in Magento, using one of these methods:
* Magento Connect
* The extension key for the latest beta is http://connect20.magentocommerce.com/community/JeroenVermeulen_Solarium
* The extension key for the latest stable (1.5.0) is http://connect20.magentocommerce.com/community/JeroenVermeulen_Solarium-1.5.0
* or (Best way) clone/download from githud https://github.com/jelqui/magento-solarium.git
* Download and unpack a release ZIP or TGZ file
* Use Modman
* In Magento Admin: Flush Cache Storage
* Log out from Magento Admin and log back in
* Configure, test and enable via: System > Configuration > CATALOG > Solarium Search
* Reindex the Catalog Search Index, this will update Solr (if enabled)
* Test normal searching in the webshop
* Test searching with a small typo in a larger word, this must return results


## Support

**We are sorry but we cannot offer customer support for this extension, and it is provided "as-is" for free.**
**This project is abandoned. Please do NOT contact any of the developers for support.**

A lot of info can be found in our [Wiki Pages](https://github.com/jeroenvermeulen/magento-solarium/wiki)

## Core Developers

  * [Jeroen Vemeulen](http://www.jeroenvermeulen.eu/)
  * [Toon van Dooren](http://www.magentocommerce.com/certification/directory/dev/172433/)
