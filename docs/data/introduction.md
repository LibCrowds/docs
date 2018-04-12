All task-related data stored on the LibCrowds platform is made publically
available for further research or integration into other systems. There are
several ways of accessing this data, which are described further below.

## Data model

In the majority of cases, the final result data is likely to be the
most useful. This is the data produced once a task has been completed and
all contributions analysed. In their raw form, these final results are
serialised according to the
[Web Annotatations data model](https://www.w3.org/TR/annotation-model/) and
wrapped with additional information about the tasks that produced them. See
the [Data Model](/data/model.md) section for more details.

## Downloads

All task and contribution data is made avialable for direct download in CSV
and JSON formats. The structure of each dataset varies according to its
purpose. For example, the task datasets contain information required to
configure each task, whereas the contribution datasets contain the information
submitted as answers to those tasks. See the [Downloads](/data/downloads.md)
section for more details.


## API

A range of API endpoints are provided to further transform these datasets. For
instance, the final results data can be retrived as Annotation Lists that
can be consumed by IIIF compatible image viewers. See the [API](/data/api.md)
section for more details.

---

- To find out how the data is structured see the
[Data Model](/data/model.md) guide.
- To find out how to download the data in JSON or CSV formats see the
[Downloads](/data/downloads.md) guide.
- To find out how to consume the data programatically, see the
[API](/data/api.md) guide.