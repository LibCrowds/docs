
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

#### Retrieving a single annotation

``` http
GET https://www.libcrowds.com/lc/annotations/wa/{annotation-id}
```

## IIIF Annotation Lists
