The final results for all LibCrowds are stored as Web Annotations. Web
Annotations became a W3C standard on the 23rd February, 2017. The
[Web Annotation Data Model](https://www.w3.org/TR/annotation-model/) provides
the following abstract:

> Annotations are typically used to convey information about a resource or
associations between resources. Simple examples include a comment or tag on
a single web page or image, or a blog post about a news article.

> The Web Annotation Data Model specification describes a structured model
and format to enable annotations to be shared and reused across different
hardware and software platforms. Common use cases can be modeled in a manner
that is simple and convenient, while at the same time enabling more complex
requirements, including linking arbitrary content to a particular data point
or to segments of timed multimedia resources.

> The specification provides a specific JSON format for ease of creation and
consumption of annotations based on the conceptual model that accommodates
these use cases, and the vocabulary of terms that represents it.

By using this structure for our final results we aim to make the crowdsourced
data generated via the platform more easily reusable online and provide a way
for researchers to answer specific questions via programmatic means (see the
[API](/data/api.md) section for details).

As we as the final results data, we use Web Annotations to store additional
user-generated data, such as image tags. The various types of annotation are
described further below.

## Result Annotations

These annotations are created once a task is completed and all related
contributions analysed (see the [Results Analysis](/analysis.md) section for
details).

Each annotation contains a motivation, which provides an indication of why
it was created. The LibCrowds platform currently produces result annotations
with three motivations: tagging, describing and commenting.

### Tagging

Tagging annotations are used to associate a tag with a specific target, such
as a region of an image. For example, this type of annotation would be used in
a IIIF Annotation project designed to mark up all of the titles on a page.

!!! summary "Example tagging annotation"

    ```json-ld
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/playbills-results/ce67281d-5b2a-4bdc-ba33-cb46525d0625",
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

Describing annotations are used for any user input that can be stored as text,
such as transcriptions. For example, this type of annotation would be used in
a IIIF Annotation project designed to transcribe all of the titles on a page.

!!! summary "Example describing annotation"

    ```json-ld
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/playbills-results/7640ddcd-6e48-4a9c-a360-3383032593b6",
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

    ```json-ld
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/playbills-results/97b63351-c1a4-456e-8871-b299aa684639",
      "type": "Annotation",
      "motivation": "commenting",
      "created": "2017-09-05T11:07:32.273Z",
      "creator": {
        "id": "https://www.libcrowds.com/api/user/1",
        "type": "Person",
        "name": "Joe Bloggs"
        "nickname": "joebloggs"
      },
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

## Image Tag Annotations

As the title suggests, image tag annotations are used to associated a tag with
an image. All image tag annotations are generated with the tagging motivation.

### Tagging

Tagging annotations are used to associate a tag with an image. They contain
enough data for them to later be used to build an image album, or potentially
a IIIF manifest.

The target's `source` contains a the image URI and the target's `scope`
contains the IIIF manifest URI, if available. If a IIIF manifest URI was not
available at the time of tagging (e.g. if the image being tagged was from
another source, such as Flickr) then the target will contain only the URI
of the image.

!!! summary "Example tagging annotation"

    ```json-ld
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://annotations.libcrowds.com/annotations/playbills-image-tags/ce67281d-5b2a-4bdc-ba33-cb46525d0625",
      "type": "Annotation",
      "motivation": "tagging",
      "created": "2017-08-31T04:25:28.178Z",
      "creator": {
        "id": "https://www.libcrowds.com/api/user/1",
        "type": "Person",
        "name": "Joe Bloggs",
        "nickname": "joebloggs"
      },
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
        "value": "foo"
      },
      "target": {
        "scope": "https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589060.0x000002/manifest.json",
        "source": {
          "id": "https://api.bl.uk/image/iiif/ark:/81055/vdc_100022589059.0x00004b/full/max/0/default.jpg"
        }
      },
    }
    ```


## Full model

The following tables detail how the LibCrowds platform implements Web
Annotations.

| Property       | Type             | Description                                                                                                                       |
|----------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| @context       | String           | The JSON-LD context (always [http://www.w3.org/ns/anno.jsonld](http://www.w3.org/ns/anno.jsonld))                                 |
| id             | String           | An IRI where the Web Annotation can be retrieved                                                                                  |
| type           | String           | The class for Web Annotations (always 'Annotation')                                                                               |
| motivation     | String           | The relationship between the Annotation and a Motivation                                                                          |
| created        | String           | The time at which the Annotation was created                                                                                      |
| creator        | Object           | The creator of the Annotation                                                                                                     |
| generated      | String           | The time at which the Annotation serialization was generated                                                                      |
| generator      | String or Object | The agent responsible for generating the serialization of the Annotation (typically software)                                     |
| modified       | String           | The time at which the Annotation was modified, after its creation                                                                 |
| target         | String or Object | The target of the Annotation                                                                                                      |
| body           | List or Object   | The relationship between the Annotation and its Body                                                                              |

### creator

The creator contains information about the person that created the annotation. This is currently only used for commenting annotations, which are created by a single
authenticated user.

| Property       | Type             | Description                                                                        |
|----------------|------------------|------------------------------------------------------------------------------------|
| id             | String           | An IRI that identifies the person                                                  |
| type           | String           | The type of the creator (always 'Person')                                          |
| name           | String           | The full name of the person                                                        |
| nickname       | String           | The nickname of the person                                                         |

!!! summary "Example of a creator"

    ```json-ld
    {
      "id": "https://www.libcrowds.com/api/user/1",
      "type": "Person",
      "name": "Joe Bloggs",
      "nickname": "joebloggs"
    }
    ```

### generator

The generator contains information about the software used to generated the
annotation, which in this case is LibCrowds.

| Property       | Type             | Description                                                                        |
|----------------|------------------|------------------------------------------------------------------------------------|
| id             | String           | An IRI that identifies the software (always main LibCrowds GitHub repository )     |
| type           | String           | The type of the generator (always 'Software')                                      |
| name           | String           | The name of the generator (always 'LibCrowds')                                     |
| homepage       | String           | The base URL that the software was running from when the annotation was generated  |

!!! summary "Example of a generator"

    ```json-ld
    {
      "id": "https://github.com/LibCrowds/libcrowds",
      "type": "Software",
      "name": "LibCrowds",
      "homepage": "https://www.libcrowds.com"
    }
    ```

### target

The target identifies the resource being annotated. For instance, this may
be an image, in which case the target will be a URL. Or, the target may be a
specific region of an image, in which case the target will be an object with
the properties below.

| Property            | Type             | Description                                                                                                                       |
|---------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| source              | String or Object | The URL of the resource being annotated                                                                                           |
| selector            | Object           | The relationship between the resource and a selector                                                                              |
| selector.type       | String           | The class of the selector (always 'FragmentSelector')                                                                             |
| selector.conformsTo | String           | The fragment selector syntax IRI (always [http://www.w3.org/TR/media-frags/](http://www.w3.org/TR/media-frags/))                  |
| selector.value      | String           | The contents of the fragment component                                                                                            |
| scope               | String           | A resource that provides the scope for the context of an Annotation                                                               |

!!! summary "Example of a media fragment target"

    ```json-ld
    {
      "target": {
        "source": "http://example.org/iiif/book1/canvas/p1",
        "selector": {
          "type": "FragmentSelector",
          "conformsTo": "http://www.w3.org/TR/media-frags/",
          "value": "xywh=100,100,100,100"
        }
      },
      ...
    }
    ```

### body

The body contains information that describes the target, for example, a tag or
a transcription.

#### Tags

Tags are used to associate some label, generally as plain text, with the target.

| Property       | Type             | Description                                     |
|----------------|------------------|-------------------------------------------------|
| type           | String           | The type of the resource (always 'TextualBody') |
| purpose        | String           | The reason for the inclusion (always 'tagging') |
| value          | String           | The tag text                                    |

!!! summary "Example of a tag"

    ```json-ld
    {
      "type": "TextualBody",
      "purpose": "tagging",
      "value": "title"
    }
    ```

#### Semantic Tags

Semantic Tags are used to link the annotation to a URI that identifies a
specific resource.

| Property       | Type             | Description                                          |
|----------------|------------------|------------------------------------------------------|
| type           | String           | The type of the resource (always 'SpecificResource') |
| purpose        | String           | The reason for the inclusion (always 'classifying')  |
| source         | String           | A URI identifying the specific resource              |

!!! summary "Example of a semantic tag"

    ```json-ld
    {
      "type": "SpecificResource",
      "purpose": "classifying",
      "source": "http://purl.org/dc/terms/title"
    }
    ```

#### Descriptions

Descriptions are used to describe the target in plain text.

| Property       | Type             | Description                                         |
|----------------|------------------|-----------------------------------------------------|
| type           | String           | The type of the resource (always 'TextualBody')     |
| purpose        | String           | The reason for the inclusion (always 'describing')  |
| format         | String           | The format of the description (always 'text/plain') |
| value          | String           | The description text                                |

!!! summary "Example of a description"

    ```json-ld
    {
      "type": "TextualBody",
      "purpose": "describing",
      "format": "text/plain",
      "value": "The Merchant of Venice"
    }
    ```

#### Linking

| Property       | Type             | Description                                          |
|----------------|------------------|------------------------------------------------------|
| type           | String           | The type of the resource (always 'SpecificResource') |
| purpose        | String           | The reason for the inclusion (always 'classifying')  |
| source         | String           | A URI identifying the specific resource              |

## Parent-child relationships

Some LibCrowds projects can be built with a parent-child relationship. For
example, the results of a IIIF *tagging* project can be used to generate tasks
for a IIIF *describing* project.

A body will be added to all child annotations with the
[`linking`](/data/model.md#linking) purpose. The value of this body will be
the `id` of the parent annotation from which the task was built. This helps
with later identifying the relationships between entities.

!!! summary "Example parent-child relationship"

    An annotation from parent project:

    ```json-ld
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://www.libcrowds.com/lc/annotations/wa/ce67281d-5b2a-4bdc-ba33-cb46525d0625",
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

    An annotation from child project:

    ```json-ld
    {
      "@context": "http://www.w3.org/ns/anno.jsonld",
      "id": "https://www.libcrowds.com/lc/annotations/wa/7640ddcd-6e48-4a9c-a360-3383032593b6",
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
        },
        {
          "source": "https://www.libcrowds.com/lc/annotations/wa/ce67281d-5b2a-4bdc-ba33-cb46525d0625",
          "type": "SpecificResource",
          "purpose": "linking"
        }
      ],
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
