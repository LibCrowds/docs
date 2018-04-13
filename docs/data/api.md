
The following section describes the various endpoints available for retrieving
the final results data from LibCrowds. This is the data generated once all
contributions for a task have been analysed.

TODO: write this!

## Domain objects

## Web Annotations

LibCrowds implements its own basic Annotation Server that complies with the
[Web Annotation Protocol](https://www.w3.org/TR/annotation-protocol/).
Annotations can be retrieved via the endpoints listed below.

#### Retrieving a single annotation

``` http
GET https://www.libcrowds.com/lc/annotations/wa/{annotation-id}
```

## IIIF Annotation Lists
