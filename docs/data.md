Once each task is completed and all contributions have been analysed the final
result for each task is stored in the results table as a list of Web
Annotations wrapped with some additional information related to the task.

## Exports

The final results data can be exported at project, volume or collection level.

TODO: Update this page

??? summary "Example result fragment"

    Here is an example of a comment annotation added to the `annotations` key
    of the final result.

    ```json
    {
      "annotations": [
        {
          "body":{
            "type":"TextualBody",
            "purpose":"commenting",
            "value":"I like turtles.",
            "format":"text/plain"
          },
          "motivation":"commenting",
          "target":"https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589092.0x0001a3",
          "created":"2017-11-17T15:28:15.088Z",
          "modified":"2017-11-17T15:28:16.255Z",
          "generated":"2017-11-17T15:28:15.088Z",
          "@context":"http://www.w3.org/ns/anno.jsonld",
          "type":"Annotation",
          "id":"4b4ffe2a-b1a4-456f-8bf8-2c02660a3fe5"
        }
        ...
      ]
    }
    ```

??? summary "Example result fragment"

    Here is an example of two selections added to the `annotations`
    key of the final result.

    ```json
    {
      "annotations": [
        {
          "body":[
            {
              "type":"TextualBody",
              "purpose":"tagging",
              "value":"title"
            },
            {
              "source":"http://purl.org/dc/terms/title",
              "type":"SpecificResource",
              "purpose":"classifying"
            }
          ],
          "motivation":"tagging",
          "target":{
            "source":"https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589092.0x000255",
            "selector":{
              "conformsTo":"http://www.w3.org/TR/media-frags/",
              "type":"FragmentSelector",
              "value":"?xywh=123,333,1462,214"
            }
          },
          "created":"2017-09-16T18:13:31.690Z",
          "modified":"2017-11-17T10:03:40.753139",
          "generated":"2017-09-16T18:13:31.690Z",
          "@context":"http://www.w3.org/ns/anno.jsonld",
          "type":"Annotation",
          "id":"6b55e881-2d8a-4fa7-b983-8428d63df54e"
        },
        {
          "body":[
            {
              "type":"TextualBody",
              "purpose":"tagging",
              "value":"title"
            },
            {
              "source":"http://purl.org/dc/terms/title",
              "type":"SpecificResource",
              "purpose":"classifying"
            }
          ],
          "motivation":"tagging",
          "target":{
            "source":"https://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022589092.0x000255",
            "selector":{
              "conformsTo":"http://www.w3.org/TR/media-frags/",
              "type":"FragmentSelector",
              "value":"?xywh=138,1097,1481,222"
            }
          },
          "created":"2017-09-16T18:13:37.282Z",
          "modified":"2017-11-17T10:03:40.753250",
          "generated":"2017-09-16T18:13:37.282Z",
          "@context":"http://www.w3.org/ns/anno.jsonld",
          "type":"Annotation",
          "id":"ffaa8ac9-1352-4fc9-a78e-4c7f9e9881ba"
        }
      ...
      ]
    }
    ```