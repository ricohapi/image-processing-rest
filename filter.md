## Filter

All API endpoints are listed below.

| Method | Description |
|--------|-------------|
| [POST  /filter](#PostFilter) | Apply image processing (filter) to uploaded media data |

<a name="PostFilter"></a>
### POST /filter

Apply image processing (filter) to uploaded media data

#### URL Structure

```
https://ips.ricohapi.com/v1/filter

ips - image processing service
```

### Parameters

|Header | Description |
|----|----|
| Authorization | (required) Authorization Header<br>Put the resource owner's OAuth2 access token |

#### Request Body

|Field Name|Type|Description|
|----|----|----|
|version|string|(optional) version of this API.|
|source|object(Source)|(required) Media to be filtered |
|filter[]|object(Command)|(required) Filters to apply |

#### Object(Source)

|Field Name|Type|Description|
|----|----|----|
|mss_id|string|(required) ID of media data on media storage service to be filtered. |

#### Object(Command)

|Field Name|Type|Description|
|----|----|----|
|command|string|(required) command to apply, with values 'resize', 'grayscale', and 'equalize'. Commands are applied in written order. No more than 3 commands are passed. Commands and their parameters must be valid, otherwise no command are processed.|
|parameters|object(Parameters)|(optional) parameters for command.|

#### Object(Parameters)

|Field Name|Type|Description|
|----|----|----|
|width|integer|(optional) Parameter for 'resize'. Width of image, with values between 1 and original size. Height automatically scaled in proportion if it is not set. Either width or height must be passed.|
|height|integer|(optional) Parameter for 'resize'. Height of image, with values between 1 and original size. Width automatically scaled in proportion if it is not set. Either width or height must be passed.|

#### Example (Resize)

Resize input image data with passed parameters.
Example of parameter is as follows.

```JavaScript
{
  "version": "2016-06-29",
  "source": {
    "mss_id": "a39jcbc5-053c-4873-a7c0-0b20c3948472"
  },
  "filter": [
    {
      "command": "resize",
      "parameters": {
        "width": 256,
        "height": 128
      }
    }
  ]
}
```

#### Example (Grayscale)

Convert input image data to grayscale. No parameters are required.
Example of parameter is as follows.

```JavaScript
{
  "version": "2016-06-29",
  "source": {
    "mss_id": "a39jcbc5-053c-4873-a7c0-0b20c3948472"
  },
  "filter": [
    {
      "command": "grayscale"
    }
  ]
}
```

#### Example (Histogram Equalization)

Apply histogram equalization to input image data. No parameters are required.
Example of parameter is as follows.

```JavaScript
{
  "version": "2016-06-29",
  "source": {
    "mss_id": "a39jcbc5-053c-4873-a7c0-0b20c3948472"
  },
  "filter": [
    {
      "command": "equalize"
    }
  ]
}
```

#### Exif and XMP

The following Exif and XMP information are updated after filter processed. Other tags are copied from original image data.

|Tag|Changed Value|
|----|----|
|Software|"RICOH Cloud API"|
|CroppedAreaImageHeightPixels|Resized height|
|FullPanoHeightPixels|Resized height|
|CroppedAreaImageWidthPixels|Resized width|
|FullPanoWidthPixels|Resized width|
|PixelXDimension|Resized width|
|PixelYDimension|Resized height|
|ImageWidth|Resized width|
|ImageLength|Resized height|
|CreateDate|Filter processed time|
|DateTimeDigitized|Filter processed time|
|SubSecTimeDigitized|Filter processed time|
|DateTime|Filter processed time|
|SubSecTime|Filter processed time|
|ModifyDate|Filter processed time|

### Response

#### Example Response

Returns media id of image processed data.

```JavaScript
{
  "id":"string",
  "content_type":"string",
  "bytes": 3944775,
  "created_at":"2016-02-24T00:56:46Z"
}
```

|Header|Description|
|---|---|
|Content-Type|application/json; charset=utf-8|
|Location|The URI of the generated media data|

|Field Name|Description|Type|
|----|----|----|
|id|Media ID|string|
|content_type|Media Content Type|string|
|bytes|bytes|integer|
|created_at|Created Datetime ISO8601-formatted with timezone offset|string|

#### Status Codes

| Code | Reason |
|----|----|
| 200 | OK |
| 400 | Bad request. |
| 401 | Unauthorized. The access token is invalid or expired. |
| 403 | Forbidden. |
| 404 | Not found. |
| 408 | Request Timeout |
| 429 | Too Many Requests. |
| 500 | Internal server error. |
