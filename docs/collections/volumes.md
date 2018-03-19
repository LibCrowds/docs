The available volumes for a collection are managed via this section.

Volumes provide the input source used to build new projects. For example, a
IIIF manifest URI from which images are pulled. They are also used to group
related projects within a collection, helping with the aggregation of results
data.

??? warning "Administrator rights required"

    To request administrator rights please get in touch by clicking the email
    icon in the footer of this page.

??? question "How do I open this page?"

    Admin rights are required to access this page. If you have admin rights:

    1. Sign in to your LibCrowds account.
    2. Click the **Menu** button at the top of any page.
    3. Select **Open Collection**.
    4. Locate the collection in the table and click **Open**.
    5. Select **Volumes** from main menu.

![A screenshot of a collection's volumes admin page](/assets/img/collection/volumes.png?raw=true)
<br><small>*A screenshot of a collection's volumes admin page*</small>

## Adding a volume

To add a new volume click the **New** button at the top of the volumes table.

![A screenshot of the new volume page](/assets/img/collection/volumes-new.png?raw=true)
<br><small>*A screenshot of the new volume page*</small>

Volumes are added using the following form fields:

- **Name:** The name of the volume.
- **Short Name:** An identifier used, for example, in the file names of
volume-level downloads.
- **Source:** The input source, for example, the location of the images
(see below).

As we want to avoid defining duplicate volumes, all of the form fields above
must contain unique values. That is, the details entered don't already exist
for other volumes listed for the collection.

The format of the **source** depends on the type of task presenter chosen
for the collection. This will be indicated on the page as one of the following:

!!! summary "IIIF Annotation"

    For collections using the IIIF Annotation task presenter, the source
    should be a IIIF manifest that contains the metadata required to
    display content served via the IIIF APIs.

    A manifest URI should look like this:

    ```
    # pattern
    {scheme}://{host}/{prefix}/{identifier}/manifest

    # example
    http://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022588857.0x000002/manifest.json
    ```

!!! summary "Z39.50"

    For collections using the Z39.50 task presenter, the source should be
    the URI of a Flickr album.

    A Flickr album URI should look like this:

    ```
    # pattern
    {scheme}://www.flickr.com/photos/{user_id}/albums/{album_id}

    # example
    {scheme}://www.flickr.com/photos/132066275@N04/albums/72157653533516031
    ```

Once you have completed the form, click the **Add Volume** button. See below
for details of how to update the volume's metadata or add a thumbnail image.

## Updating a volume

To update a volume, locate it in the table and click **Update**.

![A screenshot of the update volume page](/assets/img/collection/volumes-update.png?raw=true)
<br><small>*A screenshot of the update volume page*</small>

A form with two tabs will be displayed, one to update the volume's metadata
and one to add a thumbnail image. The thumbnail image will be used for all
projects subsequently generated using the volume.

## Deleting a volume

In the rare case that you want to remove a volume, locate it in the table
and click **Delete**.

Note that deleting a volume will affect the aggregation of results for any
projects that have already been built using that volume.

!!! warning
    Deletion is final, there is no undo.
