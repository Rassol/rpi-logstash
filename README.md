# About this Repo

This is just another forked Git repo of the Docker [official image](https://docs.docker.com/docker-hub/official_repos/) for [logstash](https://registry.hub.docker.com/_/logstash/). 

The aim of this repo is to make the official Docker image for logstash compatible with Raspberry Pi.

See [the official Docker Hub page](https://registry.hub.docker.com/_/logstash/) for the full readme on how to use this Docker image based on the official one.

This Docker Image have been tested on Raspberry Pi 2.

# How to use this image

## Start Logstash with commandline configuration

If you need to run logstash with configuration provided on the commandline, you can use the logstash image as follows:

```console
$ docker run -it --rm ind3x/rpi-logstash -e 'input { stdin { } } output { stdout { } }'
```

## Start Logstash with configuration file

If you need to run logstash with a configuration file, `logstash.conf`, that's located in your current directory, you can use the logstash image as follows:

```console
$ docker run -it --rm -v "$PWD":/config-dir ind3x/rpi-logstash -f /config-dir/logstash.conf
```

### Using a `Dockerfile`

If you'd like to have a production Logstash image with a pre-baked configuration file, use of a `Dockerfile` is recommended:

```dockerfile
FROM ind3x/rpi-logstash

COPY logstash.conf /some/config-dir/

CMD ["-f", "/some/config-dir/logstash.conf"]
```

Then, build with `docker build -t my-logstash .` and deploy with something like the following:

```console
$ docker run -it --rm my-logstash
```