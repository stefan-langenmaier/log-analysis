Solr-Banana-Logstash
====================

This is a simple generic stack to analyse log data. The applications used are

- Logstash (reading the log files)
- Solr (storing the indexed data)
- Banana (visualize the logs)

Usage
-----

Make the images locally available. For this run:
	docker-compose build

Configure the docker-compose.yml file to reference the folders where:

- the log files to be analyzed are stored (they can be moved there later als the data in there is regularly polled)
- the logstash pipeline configurations for the analysis (there should be sample for different types in the examples folder, make sure to also provide the default pipeline configuration)

Start the container with the docker-compose.yml file:
	docker-compose run

Open the Banana interface at: http://localhost:8983/solr/banana

If no data shows up. Make sure to issue a commit on the Solr collection index:
	http://localhost:8983/solr/logstash/update?commit=true

Once the setup is no longer needed run the following to remove the containers again
	docker-compose rm

Persistent Data
---------------

If data is supposed to survive the containers the read the documentation about a custom home: https://github.com/docker-solr/docker-solr#custom-solr_home


Banana
------

This tool can be configured with its normal user interface after the data is indexed. Nothing particular about it.

Solr
----

It creates a default collection named "logstash" on creation. This collection is used by default by logstash to index the logs.

Logstash
--------

This parses the log data. At the start of the containers the pieline configuration and the folder where the log data will be provided need to be configured.