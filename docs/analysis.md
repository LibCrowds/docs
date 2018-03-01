
LibCrowds implements a real-time results analysis process that is triggered
whenever a task recieves the minimum number of required contributions.
According to the normalisation and analysis rules specified for the project,
there two possible outcomes of this process:

1. A final result for the task is established and stored.
2. The task is marked as requiring an additional contribution, after which the
process will be triggered again.

## Data structure

The final results for all LibCrowds projects are stored as lists of annotations
serialised according to the [Web Annotation](https://www.w3.org/annotation/)
data model. Web Annotations are a W3C standard used to make data more easily
reusable online. For information about the data and how it can be reused see
the [Data section](/data/introduction.md).

## Normalisation

Each project template provides custom normalisation options that are applied
during the results analysis process. These options include case-conversion,
trimming of punctuation and formatting dates consistently. Details of the
available normalisation rules are given in the
[Templates Analysis Rules](/templates/analysis.md) guide.

## Task redundancy

The analysis process is first triggered when the minimum number of required
contributions for a task is reached.

For tagging tasks is the point at which the tags are clustered together and
those clusters used to create a final result.

For all other tasks this minimum refers to the number of contributions that
must match (following normalisation) before an answer will be stored as a final
result. If the minimum is not met then the number of answers required for a
task will be increased until the maximum is reached, after which no answer
will be stored.

Guidance on how to set the minimum and maximum contributions for a set
of projects is given in the [Templates Core Details](/templates/details.md)
guide.

## Example scenarios

Let's image that your project requires a minimum of 3 and a maximum of 5
contributions and that at least 3 of these contributions must match before an
answer is considered valid, then the following scenarios could apply.

??? summary "Scenario one: Valid result established during the first pass"

    1. 3 contributions are submitted for a task.
    2. The analysis process is triggered.
    3. We find that 3 out of 3 contributions match (following normalisation).
    4. The final result is stored as a list of the matching annotations.

??? summary "Scenario two: Valid result found during the second pass"

    1. 3 contributions are submitted for a task.
    2. The analysis process is triggered.
    3. We find that 2 out of 3 contributions match (following normalisation).
    4. The task is marked as now requiring 4 contributions.
    5. Another contribution is submitted.
    6. The analysis process is triggered.
    7. We find that 3 out of 4 contributions match (following normalisation).
    8. The final result is stored as a list of the matching annotations.

??? summary "Scenario three: No valid result established"

    1. 3 contributions are submitted for a task.
    2. The analysis process is triggered.
    3. We find that 2 out of 3 contributions match (following normalisation).
    4. The task is marked as now requiring 4 contributions.
    5. Another contribution is submitted.
    6. The analysis process is triggered.
    7. We find that 2 out of 4 contributions match (following normalisation).
    8. The task is marked as now requiring 5 contributions.
    9. Another contribution is submitted.
    10. The analysis process is triggered.
    11. We find that 2 out of 4 contributions match (following normalisation).
    12. The final result is stored as an empty list.

## Annotation types

There are three main types of annotation produced by the platform, each of
which are analysed in different ways.

### Tagging

Tagging annotations are used to mark up areas of an image. For example, this
type of annotation would be used in a IIIF Annotation project designed to
mark up all of the titles on a page.

If area selections are found during the analysis process then we cluster
together any selections that overlap by a given amount and add an annotation
for each cluster to the final result.

So, if three users marked up the same title, with slightly different regions,
then these three regions should be detected as similar and clustered into one
marked up region. The area for that clustered region is the smallest region
that contains all three sets of original coordinates.

Similarity is determined using the
[Jaccard index](https://en.wikipedia.org/wiki/Jaccard_index), with a result
greater than 0.5. That is, we take two regions, calculate the intersection
over the union, and if the result is greater than 0.5 we merge the two
regions.

### Describing

Describing annotations are used for any user-submitted transcriptions. One
annotation is created for each form field submitted. For example, this type of
annotation would be used in a Z39.50 project designed to associate control
numbers with a reference for an image.

If transcriptions are found during the analysis process they are normalised
according to the rules specified for the project and any that then match
exactly are grouped together and a count taken of the value with the highest
number of matches. If this value is greater than or equal to the minimum
number of matching answers required for the project an annotation is added
to the final result.

### Commenting

Commenting annotations are used to store user-submitted comments. These
comments are associated with the image as a whole rather than a specific field.

Comments are not modified during the analysis process. A commenting annotation
is added to the final result for each comment found.
