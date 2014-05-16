Docker Base Image
=================
A slightly improved base image on top of Phusion's baseimage.

What's Better?
--------------
We do these things on top of Phusion's baseimage:
- Add an app user and group to run services in.
- Set up sane logging and easily redirect that logging to a remote server.
- Rotate logs faster since logs are supposed to be shipped off.

Building
--------
It's as easy as:

    git clone https://github.com/BlueDragonX/docker-baseimage.git
    docker build --rm -t bluedragonx/baseimage docker-baseimage

Running
-------
By default the image logs to /var/log/messages. You may set the SYSLOG_REMOTE
environment variable to "enable" to log messages to the host running Docker:

    docker run -e SYSLOG_REMOTE=enable bluedragonx/baseimage

Alternatively you may specify a host and (optional) port number to log to:

    docker run -e SYSLOG_REMOTE=log.example.net:514 bluedragonx/baseimage

If the port is omitted then the default port of 514 is used. If the host is
omitted the default of 172.17.42.1 is used.

Local logging may be disabled through the use of the SYSLOG_LOCAL environment
variable:

    docker run -e SYSLOG_LOCAL=disable bluedragonx/baseimage

They can be combined to log remotely and not locally:

    docker run -e SYSLOG_REMOTE=enable -e SYSLOG_LOCAL=disable bluedragonx/baseimage

License
-------
Copyright (c) 2014 Ryan Bourgeois. Licensed under BSD-Modified. See the LICENSE
file for a copy of the license.
