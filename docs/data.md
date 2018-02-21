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

!!! summary "Example tagging annotation"

    ```json
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://www.libcrowds.com/lc/annotations/ce67281d-5b2a-4bdc-ba33-cb46525d0625",
      "type": "Annotation",
      "motivation": "tagging",
      "created": "2017-08-31T04:25:28.178Z",
      "generated": "2017-08-31T04:25:28.178Z",
      "generator": {
        "id": "https://www.libcrowds.com",
        "type": "Software",
        "name": "LibCrowds",
        "homepage": "https://www.libcrowds.com"
      },
      "body": {
        "type": "TextualBody",
        "purpose": "tagging",
        "value": "title"
      },
      "target": {
        "source": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589158.0x00007f",
        "selector": {
          "conformsTo": "http://www.w3.org/TR/media-frags/",
          "type": "FragmentSelector",
          "value": "?xywh=245,1172,1789,270"
        }
      }
    }
    ```

### Describing

Describing annotations are used for user-submitted transcriptions. For example,
this type of annotation would be used in a IIIF Annotation project designed to
transcribe all of the titles on a page.

!!! summary "Example describing annotation"

    ```json
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://www.libcrowds.com/lc/annotations/7640ddcd-6e48-4a9c-a360-3383032593b6",
      "type": "Annotation",
      "motivation": "describing",
      "created": "018-02-08T22:15:07.152Z",
      "generated": "018-02-08T22:15:07.152Z",
      "generator": {
        "id": "https://www.libcrowds.com",
        "type": "Software",
        "name": "LibCrowds",
        "homepage": "https://www.libcrowds.com"
      },
      "body": [
        {
          "type": "TextualBody",
          "purpose": "tagging",
          "value": "title"
        }
        {
          "type": "TextualBody",
          "purpose": "describing",
          "value": "King Lear",
          "format": "text/plain"
        }
      ],
      "target": {
        "source": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589096.0x0002b7",
        "selector": {
          "conformsTo": "http://www.w3.org/TR/media-frags/",
          "type": "FragmentSelector",
          "value": "?xywh=7,1191,1962,359"
        }
      }
    }
    ```

### Commenting

Commenting annotations are used to store comments about a target. For example,
this type of annotation would be used to store any user-input provided via the
notes field of a IIIF Annotation project.

!!! summary "Example commenting annotation"

    ```json
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://www.libcrowds.com/lc/annotations/97b63351-c1a4-456e-8871-b299aa684639",
      "type": "Annotation",
      "motivation": "commenting",
      "created": "2017-09-05T11:07:32.273Z",
      "generated": "2017-09-05T11:07:32.273Z",
      "generator": {
        "id": "https://www.libcrowds.com",
        "type": "Software",
        "name": "LibCrowds",
        "homepage": "https://www.libcrowds.com"
      },
      "body": {
        "type": "TextualBody",
        "purpose": "commenting",
        "value": "Not a playbill",
        "format": "text/plain"
      },
      "target": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589158.0x000094"
    }
    ```

## Downloads

Data can be downloaded via the Data page of each collection microsite in JSON
and CSV formats. Downloads are available at the project, volume, and
collection levels.

### Project

### Volume

At the volume level, final results for all projects associated with each volume
are collated.

### Collection
