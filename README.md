## Overview
An experimental Docker image, which allows you to connect an ELK stack running in a container on Windows 10, to your local Azure Storage Emulator.

## Prerequisites
You should read the prerequisites section of using this container available at http://elk-docker.readthedocs.io/.

**Some things to note:**
* When the contaniner has started for the first time, no index will exist for Elastic Search.
  You need some data in the table you have configured to monitor, before you can create the elastic search index.

* You need to assign at least 4096MB of RAM to Docker or Elastic Search won't start.

## Build and Run Docker Image
1. Ensure Docker for Windows is running
2. Ensure you are in Linux mode for running containers
3. Clone the repository
4. Copy the template config file __/logstash-input-azurewadtable/azurewadtable.conf.template__ to a config file called __/logstash-input-azurewadtable/azurewadtable.conf__
5. Add as many input sections as you need, for the table(s) you wish to monitor
6. Run build.cmd and an image called __*elk_azure_storage_emulator*__ will be created
7. Run run.cmd to start the image for the first time and load it into the container

## Running
* *run.cmd* - start up a new container (access Kibana via http://localhost:5601)
* *start.cmd* - start a stopped container
* *stop.cmd* - stop the container
* *remove.cmd* - remove the container
* *delete.cmd* - delete the container image

## Todo
* Add some tests to the modified azurewadtable plugin
* Refactor customised azurewadtable.rb to take advantage of using some of the other Azure Storage clients ctro's

## Note on Security Warning
When building the image you will receive a security warning:

*SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to double check and reset permissions for sensitive files and directories*

A change was made to output the warning to stdout and isn't considered a major security issue:

See https://github.com/moby/moby/issues/29209 for discussion and origins.
