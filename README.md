# Supported tags and respective `Dockerfile` links

- None

# What is scheduler?

Scheduler is part of a project of information service called Company Service. As its name implies, scheduler is a web server that schedules containers running in a specified consul cluster according to requests received from the binding port.

# How to use this image?

## Create the scheduler

```bash
    docker run -d -P -e "CONSUL=<consul server addr:8500>" companyservice/scheduler
```

The container starts the web server, which connects to the consul server and try to create the swarm manage service if not found.
Contaner also binds the port 8888, and make it possible to schedule containers by

## Make requests in RESTful style

```bash
    curl http://localhost:<scheduler port>/service/list
```
The server returns a list of services and their predifined actions. Check HTTP API to learn more.

# HTTP API

## Service

Service is the endpoint to get the info of service and take their actions. Activate some service's action in following endpoint:

```
    /service/<service>/<action>
```

The server only supports POST method. All services available and their actions are listed below: 

### List

```
    /service/list
```

List is a special service which doesn't schedule any containers. List service returns a list of available service and their actions.

### Crawler

Crawler is the service of web crawler.

-   crawl

```
    /service/crawler/crawl
```

The action starts a container using the image `companyservice/crawler` and container starts a crawler with the arguments in the request.

# Supported Docker versions

This image is officially supported on Docker version 1.6.0.

Support for older versions (down to 1.0) is provided on a best-effort basis.


