
The following section describes the various endpoints available for retrieving
the final results data from LibCrowds. This is the data generated once all
contributions for a task have been analysed.

## Web Annotations

LibCrowds implements its own Annotation Server, via which all annotations
generated through the platform can be retrieved programatically. By storing
the results of each task as Web Annotations and making them available via a
server that complies with the
[Web Annotation Protocol](https://www.w3.org/TR/annotation-protocol/) we make
the efforts of our volunteers more easily shareable between platforms and
enable further research by programatic means. For instance, the function below
shows how we can retrieve and process a set of current annotations using
Python.

```python
import requests

def get_annotations(url):
    r = requests.get(url)
    page = r.json()
    annotations = page['items']
    # Do interesting stuff with annotations
    next_page = page.get('next')
    if next_page:
        get_annotations(next_page)

get_annotations('https://annotations.libcrowds.com/container-key/?page=0')
```

Importantly, this data will always be live, so as soon as a task is completed
and the contributions analysed the result will be available via this API.

The available public endpoints are described below. Note that only GET
requests will be accepted by the annotations server, all other requests are
restricted.

!!! tip "Data Model"

    The structure of the Annotations referenced below is described in our
    [Data Model](/data/model.md).

### Container Discovery

TODO

#### Get a single Annotation

Use the following endpoint to retrieve a single annotation.

``` http
GET https://www.libcrowds.com/lc/annotations/wa/{annotation-id}
```

!!! summary "Example"

    Example request:

    ``` http
    https://www.libcrowds.com/lc/annotations/wa/a6947486-98f1-48c8-a833-bcb0023c25a1
    ```

    Example response:

    ```json-ld
    {
        "@context": "http://www.w3.org/ns/anno.jsonld",
        "id": "https://www.libcrowds.com/lc/annotations/wa/a6947486-98f1-48c8-a833-bcb0023c25a1",
        "type": "Annotation",
        "body": {
            "type": "TextualBody",
            "purpose": "tagging",
            "value": "title"
        },
        "motivation": "tagging",
        "target": {
            "source": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589158.0x00007f",
            "selector": {
                "conformsTo": "http://www.w3.org/TR/media-frags/",
                "type": "FragmentSelector",
                "value": "?xywh=245,1172,1789,270"
            }
        },
        "generator": {
            "homepage": "https://www.libcrowds.com",
            "type": "Software",
            "id": "https://github.com/LibCrowds/libcrowds",
            "name": "LibCrowds"
        },
        "created": "2018-04-03T12:21:24Z",
        "generated": "2018-04-03T12:21:24Z"
    }
    ```

#### Get an Annotation Collection

Use the following endpoint to return a summary of all annotations for a
collection.

``` http
GET https://www.libcrowds.com/lc/annotations/wa/collection/{collection_id}
```

!!! summary "Example"

    Example request:

    ``` http
    https://www.libcrowds.com/lc/annotations/wa/collection/22
    ```

    Example response:

    ```json-ld
    {
        "@context": "http://www.w3.org/ns/anno.jsonld",
        "id": "https://www.libcrowds.com/lc/annotations/wa/collection/22",
        "label": "In the Spotlight Annotations",
        "type": "AnnotationCollection",
        "total": 752,
        "first": "https://www.libcrowds.com/lc/annotations/wa/collection/22/1",
        "last": "https://www.libcrowds.com/lc/annotations/wa/collection/22/8"
    }
    ```

!!! tip "Query Parameters"

    See [Annotation Queries](/data/api.md#annotation-queries) for
    details of the available query parameters for this endpoint.

#### Get an Annotation Page

Use the following endpoint to return a page of Annotations for a collection.

``` http
GET https://www.libcrowds.com/lc/annotations/wa/collection/{collection_id}/{page}
```

!!! summary "Example"

    Example request:

    ``` http
    https://www.libcrowds.com/lc/annotations/wa/collection/22/1
    ```

    Example response:

    ```json-ld
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "type": "AnnotationPage",
      "id": "http://127.0.0.1:8080/lc/annotations/wa/collection/22/1",
      "items": [
        {
          "@context": "http://www.w3.org/ns/anno.jsonld",
          "id": "http://127.0.0.1:8080/lc/annotations/5947918d-0f9b-4e13-8382-e8c94e173722",
          "type": "Annotation",
          "body": [
            {
              "type": "TextualBody",
              "purpose": "tagging",
              "value": "genre"
            },
            {
              "type": "TextualBody",
              "purpose": "describing",
              "value": "Nautical Drama",
              "format": "text/plain"
            }
          ],
          "motivation": "describing",
          "target": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589096.0x0002cf",
          "created": "2018-01-23T21:34:50.667Z",
          "modified": "2018-02-14T01:15:06.845152",
          "generated": "2018-01-23T21:34:50.667Z"
        },
        ...
      ],
      "next": "http://127.0.0.1:8080/lc/annotations/wa/collection/22/2",
      "startIndex": 0,
      "partOf": {
        "id": "http://127.0.0.1:8080/lc/annotations/wa/collection/22",
        "label": "In the Spotlight Annotations",
        "total": 2860
      }
    }
    ```

!!! tip "Query Parameters"

    See [Web Annotation Queries](/data/api.md#web-annotation-queries) for
    details of the available query parameters for this endpoint.

### Annotation Queries

The query parameters available for Annotation Collection or Annotation Page
endpoints are described below.

#### iris

Return the Annotation IRIs only, rather than the full Annotations.

#### orderby

Order the results by the value of an Annotation attribute, the default is
`created`.

#### limit

Limit the results on each page by, the default is `100`.

#### contains

Search for Annotations that contain a given value.

For example, to return Annotations with the commenting motivation we could use:

```
contains={"motivation":"commenting"}
```

Or, to return Annotations with the genre tag we could use:

```
contains={"body":[{"purpose":"tagging","value":"genre"}]}
```

See the [Data Model](/data/model.md) for details of how the Annotations are
structured.
