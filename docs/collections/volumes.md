Each volume is tracked as a name against a URI that will later provide the
resources for a project, or multiple projects. Keeping a list of all volumes
that will be used to generate the projects for a collection microsite helps
with later project generation and the aggregation of results.

??? info "Administrator rights required"

    To request administrator rights please get in touch by clicking the email
    icon in the footer of this page.

??? question "How do I open this page?"

    Admin rights are required to access this page. If you have admin rights:

    1. Sign in to your LibCrowds account.
    2. Click your username at the right of the naviation bar.
    3. Select **Collection Admin** from the dropdown menu.
    4. Locate the collection in the table and click **Open**.
    5. Select **Volumes** from dashboard menu on the left-hand side.

![A screenshot of the collection volumes admin page](/assets/img/admin-collection-volumes.png?raw=true)
<br><small>*A screenshot of the collection volumes admin page*</small>

## Updating the list of volumes

The list of volumes can be updated in bulk, via CSV by clicking the
**Upload CSV** button at the top of the page.

The form that is displayed will expain which columns are required in the
CSV file for the task presenter type that is currently set for the collection.

??? tip "Updating a collection's task presenter"
    See the [Collection Details](/collection/details.md) guide to find out
    how to change the collection's task presenter.

To upload a new list of volumes select your CSV file and click **Submit**.

Following is an explanation of the details required for each type of task
presenter.

### IIIF Annotation projects

IIIF manifests provide the input for IIIF annotation projects. These manifests
contain the metadata required to display content served via the IIIF APIs,
such as a set of images.

A manifest URI should look like this:

```
# pattern
{scheme}://{host}/{prefix}/{identifier}/manifest

# example
http://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022588857.0x000002/manifest.json
```

Each row in the CSV file should therefore contain a name in the first column
and a IIIF manifest URI in the second.

### Z39.50 projects

The images for Z39.50 projects are loaded from
[Flickr](https://www.flickr.com), which provides 1TB of image storage for free.

A Flickr album URI should look like this:

```
# pattern
{scheme}://www.flickr.com/photos/{user_id}/albums/{album_id}

# example
{scheme}://www.flickr.com/photos/132066275@N04/albums/72157653533516031
```

Each row in the CSV file should therefore contain a name in the first column
and a Flickr album URI in the second.
