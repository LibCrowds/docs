
The following section describes the various endpoints available for retrieving
the final results data from LibCrowds. This is the data generated once all
contributions for a task have been analysed.

## Web Annotations

LibCrowds implements its own Annotation Server, which enables the reading of
all annotations generated via the platform. The server cannot be used to
create, update or delete endpoints, which happens via other means, but it does
comply fully with the
[Web Annotation protocol](https://www.w3.org/TR/annotation-protocol/) to ease
interoperability between systems. The available endpoints are presented
below.

#### Get a single Annotation

Use the following endpoint to retrieve a single annotation.

``` http
GET https://www.libcrowds.com/lc/annotations/wa/{annotation-id}
```

Available Parameters:

- `motivation`: Filter by motivation (e.g. `?motivation=describing`)
- `iris`: Return the Annotation IRIs only (e.g. `?iris=1`)

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

#### Get all Annotations for a collection

Use the following endpoint to return a summary of all annotations for a
collection.

``` http
GET https://www.libcrowds.com/lc/annotations/wa/collection/{short_name}
```

Available Parameters:

- `motivation`: Filter by motivation (e.g. `?motivation=describing`)
- `iris`: Return the Annotation IRIs only (e.g. `?iris=1`)

!!! summary "Example"

    Example request:

    ``` http
    https://www.libcrowds.com/lc/annotations/wa/collection/b3735005-1bac-4a27-af08-61b62d708fdb
    ```

    Example response:

    ```json-ld
    {
        "@context": "http://www.w3.org/ns/anno.jsonld",
        "id": "https://www.libcrowds.com/lc/annotations/wa/volume/b3735005-1bac-4a27-af08-61b62d708fdb",
        "label": "In the Spotlight Annotations",
        "type": "AnnotationCollection",
        "total": 752,
        "first": "https://www.libcrowds.com/lc/annotations/wa/volume/b3735005-1bac-4a27-af08-61b62d708fdb/1",
        "last": "https://www.libcrowds.com/lc/annotations/wa/volume/b3735005-1bac-4a27-af08-61b62d708fdb/8"
    }
    ```

#### Get all Annotations for a volume

Use the following endpoint to return a summary of all annotations for a
volume.

``` http
GET https://www.libcrowds.com/lc/annotations/wa/volume/{volume_id}
```

Available Parameters:

- `motivation`: Filter by motivation (e.g. `?motivation=describing`)
- `iris`: Return the Annotation IRIs only (e.g. `?iris=1`)

!!! summary "Example"

    Example request:

    ``` http
    https://www.libcrowds.com/lc/annotations/wa/volume/b3735005-1bac-4a27-af08-61b62d708fdb
    ```

    Example response:

    ```json-ld
    {
        "@context": "http://www.w3.org/ns/anno.jsonld",
        "id": "https://www.libcrowds.com/lc/annotations/wa/volume/b3735005-1bac-4a27-af08-61b62d708fdb",
        "label": "Theatre Royal, Margate 1796-1797 Annotations",
        "type": "AnnotationCollection",
        "total": 752,
        "first": "https://www.libcrowds.com/lc/annotations/wa/volume/b3735005-1bac-4a27-af08-61b62d708fdb/1",
        "last": "https://www.libcrowds.com/lc/annotations/wa/volume/b3735005-1bac-4a27-af08-61b62d708fdb/8"
    }
    ```
