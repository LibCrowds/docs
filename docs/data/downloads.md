Task-related data can be downloaded via the Data page of each collection
microsite. Downloads are available in JSON and CSV formats and contain varying
levels of detail, as described below.

Note that everything contained in these datasets is also available via the
[API](/data/api.md). Depending on the objective, the API may provide a more
suitable method of access.

## Annotation downloads

These datasets contain the final Annotations that are produced during the
[results analysis](/analysis.md) processes. The datasets are seperated by
motivation, as follows:

- **Describing:** The user-submitted transcriptions.
- **Tagging:** The regions marked up by users.
- **Commenting:** The comments or notes submitted by users.

See the [data model](/data/model.md) for details of how the Annotations are
structured.

## Project downloads

This is the raw data used by or generated via the platform. As this data may
contain a lot of nested fields the JSON versions are likely to be more usable
than the CSV versions. There are three types of dataset available for each
project:

- **Tasks:** The data used to configure tasks and present them to users.
- **Contributions:** The user-submitted data provided as answers to each task.
- **Results:** The final results produced during the
[results analysis](/analysis.md) processes.
