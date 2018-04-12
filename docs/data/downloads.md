Task-related data can be downloaded via the Data page of each collection
microsite. Downloads are available in JSON and CSV formats and contain varying
levels of detail, as described below.

Note that everything contained in these datasets is also available via the
[API](/data/api.md). Depending on the objective, the API may provide a more
suitable method of access.

## Project downloads

There are three types of downloadable dataset available at the project level,
task, task run and result. This is the raw data used by the platform and may
contain a lot of nested fields. Therefore, the JSON versions are likely
to be more usable than the CSV versions.

## Task

This data is used to configure the task and present it to users. It includes
links to the original source material, such as the IIIF manifest or Flickr
album ID.

## Task run

This is the contribution data provided by volunteers as the answers to each
task. The `info` field contains any user submitted data.

## Result

These are the final results generated once each task is complete and the
contributions analysed. The `info.annotations` field contains the final
annotations.
