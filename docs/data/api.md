The final results for all LibCrowds projects are stored as lists of annotations
serialised according to the [Web Annotation](https://www.w3.org/annotation/)
data model. Web Annotations are a W3C standard used to make data more easily
reusable online.

To manage these Annotations, LibCrowds implements its own Annotation Server. As
well as the final results data this server is used to store supplementary
information, such as user-generated image tags.

By storing our data as Web Annotations and making it available via a
a standardised API we hope to make the efforts of our volunteers more easily
shareable and enable further research by programatic means. Importantly, this
data will always be live, so as soon as a task is completed and the
contributions analysed the result will be available via this API.

!!! tip "Data Model"

    The structure of the Annotations referenced below is described in our
    [Data Model](/data/model).

The Annotation Server used by LibCrowds is called
[Explicates](https://github.com/alexandermendes/explicates). The server
complies with the
[Web Annotation Protocol](https://www.w3.org/TR/annotation-protocol/) and
includes additional features for searching and exporting data. All POST,
PUT and DELETE requests are restricted, only GET requests are publically
available.

The following section describes the various endpoints available for retrieving
data from LibCrowds programatically.

## Annotation Collections

All Annotations are stored in an Annotation Collection. Each collection
microsite makes use of several of these Annotation Collections. For instance,
there will be one that contains all of the results and another that contains
all of the image tags.

### List all Annotation Collections

```http
GET https://annotations.libcrowds.com/annotations/
```

!!! summary "Example"

    Request:

    ```http
    GET https://annotations.libcrowds.com/annotations/
    ```

    Response:

    ```json
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/",
      "label": "All collections",
      "total": 3,
      "type": [
        "AnnotationCollection",
        "BasicContainer"
      ],
      "items": [
        {
          "created": "2018-05-18T00:04:15Z",
          "creator": "https://www.libcrowds.com/api/category/22",
          "generated": "2018-05-20T22:05:15Z",
          "id": "https://annotations.libcrowds.com/annotations/playbills-tags/",
          "label": "Playbills Image Tags",
          "total": 12,
          "type": [
            "AnnotationCollection",
            "BasicContainer"
          ]
        },
        {
          "created": "2018-05-18T00:04:37Z",
          "creator": "https://www.libcrowds.com/api/category/22",
          "generated": "2018-05-20T22:05:17Z",
          "id": "https://annotations.libcrowds.com/annotations/playbills-results/",
          "label": "Playbills Results",
          "total": 11926,
          "type": [
            "AnnotationCollection",
            "BasicContainer"
          ]
        }
      ]
    }
    ```

### Get an Annotation Collection

```http
GET https://annotations.libcrowds.com/annotations/<collection_id>/
```

!!! summary "Example"

    Request:

    ```
    GET https://annotations.libcrowds.com/annotations/playbills-results/
    ```

    Response:

    ```json
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/playbills-results/",
      "label": "Playbills Results",
      "total": 11926,
      "generated": "2018-05-20T22:12:03Z",
      "type": [
        "AnnotationCollection",
        "BasicContainer"
      ],
      "first": {
        "id": "https://annotations.libcrowds.com/annotations/playbills-results/?page=0",
        "items": [
          {
            "id": "https://annotations.libcrowds.com/annotations/playbills-results/963ebbaa-4602-4ea5-8a4e-3ad7fde23611/",
            "motivation": "describing",
            "type": "Annotation",
            "body": [
              {
                "format": "text/plain",
                "purpose": "describing",
                "type": "TextualBody",
                "value": "1816-01-27"
              },
              {
                "purpose": "tagging",
                "type": "TextualBody",
                "value": "date"
              }
            ],
            "created": "2018-05-20T19:15:31Z",
            "generated": "2018-05-20T22:12:03Z",
            "generator": [
              {
                "homepage": "https://www.libcrowds.com",
                "id": "https://github.com/LibCrowds/libcrowds",
                "name": "LibCrowds",
                "type": "Software"
              },
              {
                "id": "https://backend.libcrowds.com/api/task/82346",
                "type": "Software"
              }
            ],
            "target": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589024.0x000285"
          },
          ...
        ]
      },
      "last": "https://annotations.libcrowds.com/annotations/playbills-results/?page=12",
    }
    ```

## Annotation Pages

As an Annotation Collection could grow very large Annotations are paginated
using Annotation Pages, which can be traversed by following the `next`
and `prev` links between pages.

### Get an AnnotationPage

```http
GET https://annotations.libcrowds.com/annotations/<collection_id>/?page=0
```

!!! summary "Example"

    Request:

    ```
    GET https://annotations.libcrowds.com/annotations/playbills-results/?page=0
    ```

    Response:

    ```json
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/playbills-results/?page=0",
      "type": "AnnotationPage",
      "items": [
        {
          "id": "https://annotations.libcrowds.com/annotations/playbills-results/963ebbaa-4602-4ea5-8a4e-3ad7fde23611/",
          "motivation": "describing",
          "type": "Annotation",
          "body": [
            {
              "format": "text/plain",
              "purpose": "describing",
              "type": "TextualBody",
              "value": "1816-01-27"
            },
            {
              "purpose": "tagging",
              "type": "TextualBody",
              "value": "date"
            }
          ],
          "created": "2018-05-20T19:15:31Z",
          "generated": "2018-05-20T22:12:03Z",
          "generator": [
            {
              "homepage": "https://www.libcrowds.com",
              "id": "https://github.com/LibCrowds/libcrowds",
              "name": "LibCrowds",
              "type": "Software"
            },
            {
              "id": "https://backend.libcrowds.com/api/task/82346",
              "type": "Software"
            }
          ],
          "target": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589024.0x000285"
        },
          ...
      ],
      "startIndex": 0,
      "partOf": {
        "created": "2018-05-18T00:04:37Z",
        "creator": "https://www.libcrowds.com/api/category/22",
        "generated": "2018-05-20T22:26:39Z",
        "id": "https://annotations.libcrowds.com/annotations/playbills-results/",
        "label": "Playbills Results",
        "total": 12744,
        "type": [
          "AnnotationCollection",
          "BasicContainer"
        ]
      },
      "next": "https://annotations.libcrowds.com/annotations/playbills-results/?page=1"
    }
    ```

## Annotations

Each Annotation has a Body, which is a comment or other descriptive resource, and a Target that
the Body is somehow "about". See the [Data Model](/data/model) for further details.

### Get an Annotation

```http
GET https://annotations.libcrowds.com/annotations/<collection_id>/<annotation_id>/
```

!!! summary "Example"

    Request:

    ```
    GET https://annotations.libcrowds.com/annotations/playbills-results/963ebbaa-4602-4ea5-8a4e-3ad7fde23611/
    ```

    Response:

    ```json
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/playbills-results/963ebbaa-4602-4ea5-8a4e-3ad7fde23611/",
      "motivation": "describing",
      "type": "Annotation",
      "body": [
        {
          "format": "text/plain",
          "purpose": "describing",
          "type": "TextualBody",
          "value": "1816-01-27"
        },
        {
          "purpose": "tagging",
          "type": "TextualBody",
          "value": "date"
        }
      ],
      "created": "2018-05-20T19:15:31Z",
      "generated": "2018-05-20T22:12:03Z",
      "generator": [
        {
          "homepage": "https://www.libcrowds.com",
          "id": "https://github.com/LibCrowds/libcrowds",
          "name": "LibCrowds",
          "type": "Software"
        },
        {
          "id": "https://backend.libcrowds.com/api/task/82346",
          "type": "Software"
        }
      ],
      "target": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589024.0x000285"
    }
    ```

## Search

A search service for Annotations is provided at the following endpoint:

```
GET https://annotations.libcrowds.com/search/
```

The query parameters accepted by this search service are listed below.

### contains

Search for Annotations that contain the given value.

!!! summary "Example"

    Request:

    ```
    GET https://annotations.libcrowds.com/search/?contains={"motivation":"describing"}
    ```

### fts

Full text search...

!!! summary "Example"

    Request:

    ```
    GET https://annotations.libcrowds.com/search/?fts=body::Merchant:*
    ```

## Export

Collections can be exported for offline analysis or migration purposes via the following endpoint:

```
GET https://annotations.libcrowds.com/export/<collection_id>/?zip=1
```

Note that without the `zip` parameter the entire Annotation Collection will be streamed. This
is useful for exporting to a file programatically but may take a long time to
complete if run in a browser!

Here's an example of using this endpoint to download data to a JSON file:

```bash
curl https://annotations.libcrowds.com/export/playbills-tags > test.json
```
