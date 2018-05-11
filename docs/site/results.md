The results admin page contains a summary of all collections and a count of
their unanalysed results. It can be used to monitor the outcome of the
automated [results analysis](/analysis.md) process, or to manually trigger
that process for a particular collection.

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

## Analysing empty results

By default, results are generated with no content. It is only when the results
analysis process runs that all associated contributions are checked and the
results updated accordingly. If migrating from an old version of the software,
or if the backend server has failed at a critical moment, you may end up with
results for which the analysis process was not completed. A count of these
is listed in the *Unanalysed Results* column.

To trigger the analysis process for all unanalysed results, click the
**Analyse Empty** button.

## Analysing all results

There may occasions where you want to trigger the analysis process
for all results associated with a collection. For instance, if the analysis
process has undergone major changes since your results were last processed.

To trigger the analysis process for all results, click the **Analyse All**
button.
