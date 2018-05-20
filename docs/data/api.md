LibCrowds implements its own Annotation Server, which is used to store, among
other things, all of the data generated once the contributions for a task have
been analysed.

By storing the results as Web Annotations and making them available via a
a standardised API we hope to make the efforts of our volunteers more easily
shareable between platforms and enable further research by programatic means.
Importantly, this data will always be live, so as soon as a task is completed
and the contributions analysed the result will be available via this API.

The following section describes the various endpoints available for retrieving
the final results data from LibCrowds programatically.

!!! tip "Data Model"

    The structure of the Annotations referenced below is described in our
    [Data Model](/data/model.md).

## Annotation Server

The Annotation Server used by LibCrowds is called
[Explicates](https://github.com/alexandermendes/explicates). The server
complies with the
[Web Annotation Protocol](https://www.w3.org/TR/annotation-protocol/) and
includes some additional features for searching and exporting data.

All POST, PUT and DELETE requests are restricted, only GET requests are
publically available.

## AnnotationCollections

All Annotations are stored in an AnnotationCollection. Each collection
microsite makes use of several AnnotaitonCollections. For instance, there will
be one that contains all of the results and another that contains all of
the image tags.

### List all AnnotationCollections

```http
GET https://annotations.libcrowds.com/annotations/
```

### Get an AnnotationCollection

```http
GET https://annotations.libcrowds.com/annotations/<collection_id>/
```

## AnnotationPages

### Get an AnnotationPage

```http
GET https://annotations.libcrowds.com/annotations/<collection_id>/?page=0
```

## Annotations

### Get an Annotation

```http
GET https://annotations.libcrowds.com/annotations/<collection_id>/<annotation_id>/
```

## Search

### contains

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
