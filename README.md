# Ricoh Image Processing REST API

Ricoh Image Processing service is a cloud-based image processing service provided by Ricoh Company, Ltd.

Developers can access Ricoh Image Processing service features listed below, via its APIs.

* Apply image filtering to uploaded media data in the cloud storage

## Requirements

You  need

* Ricoh API Client Credentials (client_id & client_secret)
* Ricoh ID (user_id & password)

If you don't have them, please register yourself and your client from [THETA Developers Website](http://contest.theta360.com/).

## Access Token
Before a client can call an Image Processing API, the client needs to obtain an access token. <br> Please refer to the following document.

* [Authorization and Discovery Service](http://docs.ricohapi.com/docs/authorization-and-discovery-service)

An obtained access token should be set in the Authorization header of every API request.

```JavaScript
curl --request POST 'https://ips.ricohapi.com/v1/filter' \
    --header 'Authorization: Bearer <access token>' \
    --data '{ "version": "2016-06-29", "source": { "mss_id": "a39jcbc5-053c-4873-a7c0-0b20c3948472" }, "filter": [{"command": "resize", "parameters": "width": 256, "height": 128}}, {"command": "grayscale" }, { "command": "equalize" } ]}'
```

## APIs

* [Filter](filter.md)

## API Console

You can play with the Ricoh Image Processing REST API using its [API Console](http://docs.ricohapi.com/docs/image-processing-rest).
