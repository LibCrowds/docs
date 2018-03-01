Volumes provide the input sources used to build new projects (e.g. a
IIIF manifest URI). They are also used to group related projects
within a collection, helping with the aggregation of results data. The
available volumes for a collection are managed via this section.

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

Volumes are added using a name and an input source, both of which must be
unique (i.e. they don't already exist in the volumes listed for the
collection).

To add a new volume click the **New** button at the top of the volumes table,
fill in the form, and click the **Add Volume** button.

![A screenshot of the new volume page](/assets/img/collection/volumes-new.png?raw=true)
<br><small>*A screenshot of the new volume page*</small>

The format of the input source depends on the type of task presenter chosen
for the collection.

#### IIIF Annotation

For collections using the IIIF Annotation task presenter, the input source
should be a IIIF manifest. These manifests contain the metadata required to
display content served via the IIIF APIs.

A manifest URI should look like this:

```
# pattern
{scheme}://{host}/{prefix}/{identifier}/manifest

# example
http://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022588857.0x000002/manifest.json
```

#### Z39.50

For collections using the Z39.50 task presenter, the input source should be
the URI of a Flickr album.

A Flickr album URI should look like this:

```
# pattern
{scheme}://www.flickr.com/photos/{user_id}/albums/{album_id}

# example
{scheme}://www.flickr.com/photos/132066275@N04/albums/72157653533516031
```

## Updating a volume

To update a volume, locate it in the table and click **Update**.

![A screenshot of the update volume page](/assets/img/collection/volumes-update.png?raw=true)
<br><small>*A screenshot of the update volume page*</small>

A form with two tabs will be displayed, one to update the volume's metadata
and one to add a thumbnail image. This thumbnail image will be used for all
projects subsequently generated using the volume.

## Deleting a volume

In the rare case that you want to remove a volume, locate it in the table
and click **Delete**.

Note that deleting a volume will affect the aggregation of results for any
projects that have already been built using that volume.

!!! warning
    Deletion is final, there is no undo.
