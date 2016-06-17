Solr search extension for Magento
================

The default MySQL Fulltext search is not performing very well on more serious shops. It is slow and the results aren't very relevant. Apache's Solr does a much better job in delivering fast and relevant results. We have used the Solarium PHP library to build Solr into Magento CE.

## Features

  * Free and Open Source
  * Fast results
  * Can handle high number of products
  * Fast autocomplete search query while typing
  * Optional: Show products with images as suggestions
  * Autocorrect typos in search terms
  * "Did you mean..." suggestions
  * Solr 5.3 support
  * Solr HTTP authentication support

## Requirements

  * Magento Community Edition 1.6 - 1.9.2.3
  * a working **Solr 5.3 server**

## Installation & Usage

### Install Apache Solr

To use this extension an Apache Solr server is required. The Solr server can be set up quickly using the [Docker Solr image](docker-solr/docker-solr).
In order to create a new *core* in your Solr server, copy the following files to the directory of the core to be created. When using the Docker Solr image, these are:

* [/opt/solr/server/solr/magento/conf/schema.xml](solr/conf/schema.xml)
* [/opt/solr/server/solr/magento/conf/solrconfig.xml](solr/conf/solrconfig.xml)

After a restart of the Solr Server, your core should be shown in the backend of Solr.

### Install the extension

Install the extension from this repository in Magento using modman and clear the cache. 

* Do not forget to checkout the submodule.
* Do not use the extension from the old repository or Magento Connect.
* If you do not use modman, you need to copy the Solarium libray by hand to lib/Solarium

### Get it running

* Configure, test and enable via: **System > Configuration > Catalog > Solarium Search**
* Reindex the Catalog Search Index, this will update Solr (if enabled)
* Test normal searching in the webshop
* Test searching with a small typo in a larger word, this must return results

### Additional support

Please also check the [Wiki pages of the old repository](https://github.com/jeroenvermeulen/magento-solarium/wiki).


## Developer

We just got the extension running for one of our customers and wanted to share our efforts. 
If you need any help, we can support you implementing it on a paid basis.

  * [Dominik Krebs, NETZKOLLEKTIV GmbH](http://netzkollektiv.com)

## Initial Developers

Thanks to the initial developers of this extension, who decided not to support it anymore.

  * [Jeroen Vemeulen](http://www.jeroenvermeulen.eu/)
  * [Toon van Dooren](http://www.magentocommerce.com/certification/directory/dev/172433/)

**We are sorry but we cannot offer customer support for this extension, and it is provided "as-is" for free.**
**This project is abandoned. Please do NOT contact any of the developers for support.**
