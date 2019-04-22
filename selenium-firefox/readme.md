# Selenium Load testing

Contains a selenium image to perform web testing with.


# Usage

## Build docker
First you have to build the container by executing the following command:

```
docker build . -t selenium-testing
```

## Run the container
You can launch a container by executing  

```
docker run -d --name my_selenium_container selenium-testing
```

