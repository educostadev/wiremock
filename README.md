
# Mock Services With Wiremock

Wiremock is a tool for mocking call to external services.

## Pre requirements

- Docker (or Podman) and Docker Compose 

## How to start

Start the wiremock
```
docker-compose up wiremock
```

Test if the default mock is working
```
curl --location --request GET 'localhost:8086/echo'
```

Stop the wiremock
```
docker-compose down
```

## How to record and replay external calls

Look into the folder `./data/wiremock-recording/mappings` and see the mappings for httpbin and postman-echo services. You can add your service mappings like theses ones.

Start the wiremock in recording mode
```
docker-compose up wiremock-recording
```

Run the following requests to Wiremock

```
curl --location 'http://localhost:8086/httpbin/get?foo1=bar1&foo2=bar2'
```

```
curl --location 'http://localhost:8086/postman/get?foo1=bar1&foo2=bar2'
```

Both requests will return success.

New json files named `mapping-*.json` and `body-*.json` was created into the folder `./wiremock-recording/mappings` and `./wiremock-recording/files` respectively. 

Copy these file into the `wiremock-helper` folder.

Stop the wiremock
```
docker-compose down
```

Start the wiremock for replay the mappings
```
docker-compose up wiremock
```

Disconnect your internet connection just to make sure you have no external communication and perform the previous curl commands. Both request should be returned with success that show us that the mock worked!


### Useful Links and Documentation

- http://localhost:8086/__admin/mappings - See mappings
- http://localhost:8086/__admin/recorder/ - See [Recording](https://wiremock.org/docs/record-playback/) and [Proxing](https://wiremock.org/docs/proxying/) page.

- https://wiremock.org/docs/api/ - Swagger Doc
- https://wiremock.org/docs/running-standalone/ - Wiremock parameters

