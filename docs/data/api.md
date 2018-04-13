
The following section describes the various endpoints available for retrieving
the final results data from LibCrowds. This is the data generated once all
contributions for a task have been analysed.

TODO: write this!

## Domain objects

## Web Annotations

LibCrowds implements its own Annotation Server, which enables the reading of
all annotations generated via the platform. The server cannot be used to
create, update or delete endpoints, which happens via other means, but it does
comply fully with the
[Web Annotation protocol](https://www.w3.org/TR/annotation-protocol/) to ease
interoperability between systems. The available endpoints are presented
below.

#### Get a single annotation

``` http
GET https://www.libcrowds.com/lc/annotations/wa/{annotation-id}
```

!!! summary "Example response"

    ```json-ld
    {
        "@context": "http://www.w3.org/ns/anno.jsonld",
        "id": "http://127.0.0.1:8080/lc/annotations/wa/a6947486-98f1-48c8-a833-bcb0023c25a1",
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

#### Get an annotation collection for a volume

``` http
GET https://www.libcrowds.com/lc/annotations/wa/collection/volume/{volume_id}
```

!!! summary "Example response"

    ```json-ld
    {}
    ```

## IIIF Annotation Lists
