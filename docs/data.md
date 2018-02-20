All task-related data stored on the LibCrowds platform is made available in a
variety of ways, each of which will be suitable for different audiences.

In most cases, the final result data is likely to be the most useful. This is
the data produced once a task has been completed and all contributions
analysed. In its raw form, a final result is stored as Web Annotatation wrapped
with information about the task that produced it.

This section provides details about the structure of these final results and
how they can be consumed.

## Web Annotations

Web Annotations became a W3C standard on the 23rd February, 2017.

> The Web Annotation Data Model specification describes a structured model and
format to enable annotations to be shared and reused across different hardware
and software platforms. Common use cases can be modeled in a manner that is
simple and convenient, while at the same time enabling more complex
requirements, including linking arbitrary content to a particular data point
or to segments of timed multimedia resources.

-- <cite>Web Annotation Data Model</cite>

The LibCrowds platform currently produces annotations with three motivations:
tagging, describing and commenting.

### Tagging

Tagging annotations are used to associate a tag with a specific target. For
example, this type of annotation would be used in a IIIF Annotation project
designed to mark up all of the titles on a page.

??? summary "Example tagging annotation"

### Describing

Describing annotations are used for user-submitted transcriptions. For example,
this type of annotation would be used in a IIIF Annotation project designed to
transcribe all of the titles on a page.

??? summary "Example describing annotation"

### Commenting

Commenting annotations are used to store comments about a target. For example,
this type of annotation would be used to store any user-input provided via the
notes field of a IIIF Annotation project.

??? summary "Example commenting annotation"

## Downloads

Data can be downloaded via the Data page of each collection microsite in JSON
and CSV formats. Downloads are available at the project, volume, and
collection levels.

### Project

### Volume

At the volume level, final results for all projects associated with each volume
are collated.

### Collection
