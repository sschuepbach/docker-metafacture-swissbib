# Dockerfiles for Metafacture Runner

## About

> Metafacture is a toolkit for processing semi-structured data with a focus on library metadata. It provides a versatile set of tools for reading, writing and transforming data. Metafacture can be used as a stand-alone application or as a Java library in other applications. The name Metafacture is a portmanteau of the words meta data and manufacture.

> Metafacture includes a large number of modules for operating on semi-structured data. These modules can be combined to build pipelines to perform complex metadata processing tasks. The pipelines can be constructed either in Java code or with the domain-specific language Flux. One of the core features of Metafacture is the Metamorph module. Metamorph is an xml-based language for specifying transformations of semi-structured data. It can be seamlessly integrated into Java code.

s. https://github.com/metafacture/metafacture-core

## Usage

This reposiory provides to Dockerfiles to run standalone instances of
Metafacture (so called Metafacture runners). In order to effectively use
Metafacture, one needs at least provide a Flux file and which must be given
as argument to the Docker container. If there is some interaction with the
local filesystem for input/output, the image provides some dedicated mount
points, namely `/in` and `out`. Additional files (Morph definitions, maps
etc.) can be provided via the `/mfwf` mount point. Finally you can bind to
Metafacture plugins via mounting on the internal `/app/plugins`
directory.

The Dockerfile comes in two flavors: One targeted at production
environments and one for debugging / testing purposes. The latter exposes
the default port `50505` for remote debugging and issues also logs on `DEBUG`
level (logs can be followed via `docker logs -f <container_name>)`.

To make the two images clearly distinct, it is recommended to build them
with explicit names, e.g.

  docker build -t mfrunner-prod prod

and

  docker build -t mfrunner-debug debug


## Examples

### Start a production-ready container

  docker run \
  -v /my/host/input/dir:/in:ro \
  -v /my/host/output/dir:/out \
  -v /my/morph/dir:/mfwf:ro \
  -v /my/plugins/dir:/app/plugins:ro \
  mfrunner-prod \
  /my/flux/dir \
  flux_var1=value1 flux_var2=value2

### Start a container for a debugging session

  docker run \
  -v /my/host/input/dir:/in:ro \
  -p 50505:50505 \
  mfrunner-prod \
  /my/flux/dir

