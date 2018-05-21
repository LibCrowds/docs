The results admin page provides an overview of all results Annotations on the
site. Links to the Annotations for each collection microsite are provided,
along with buttons to export as JSON, or manually trigger the results analysis
process for a particular collection.

Note that there are certain scenarios where results will be excluded from the
processes below, see [Results Analysis: Exclusion](/analysis.md#exclusion)
for details.

??? warning "Administrator rights required"

    To request administrator rights please get in touch by clicking the email
    icon in the footer of this page.

!!! question "How do I open this page?"

    Admin rights are required to access this page. If you have admin rights:

    1. Sign in to your LibCrowds account.
    2. Select **Results** from the main menu.

![A screenshot of the site admin results page](/assets/img/site/results.png?raw=true)
<br><small>*A screenshot of the site admin results page*</small>

The options listed below assume that an AnnotationCollection has been
configured to store the results for a collection microsite. If this is not the
case then the buttons mentioned below will not appear, instead you will see
a button to guide you to **Setup Results Annotations** for the collection.

## Analysing empty results

Once a task is complete, it is only when the results analysis process runs
that all associated contributions are checked and the final result annotations
generated. If you are migrating from an old version of the software,
or if the backend server has failed at a critical moment, you may end up with
results for which the analysis process was not completed.

To trigger the analysis process for all unanalysed results, click the
**Analyse Empty** button. This function will not destroy any current
Annotations. It will only process the results to which no Annotations are
currently linked.

## Analysing all results

There may be occasions where you want to trigger the analysis process to be
re-run for all results associated with a collection. For instance, if you
need to migrate all of your data to a new annotation server and do not need
to maintain the current Annotation IDs for any reason.

To trigger the analysis process for all results, click the **Analyse All**
button.

!!! warning "WARNING"

    This function is destructive, it will destroy all current Annotations and
    recreate them with new IDs. If for any reason you need to refer back to
    the current Annotations by ID then this function should not be run.

## Downloading results

For the purposes of migration or offline analysis, all result Annotations can
be downloaded as a zipped JSON file.

To trigger the download, click the **Download** button alongside the
relevant collection.
