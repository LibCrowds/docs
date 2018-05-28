The available volumes for a collection are managed via this section.

Volumes provide details of the input sources from which data can be pulled
during the creation of new projects. For example, a volume might be linked
to a IIIF manifest containing details of a set of images.

Each volume can have a different importer type, meaning that one volume within
a collection can import data via IIIF, while another imports data from Flickr.

Volumes are also used to group related projects within a collection, helping
with the aggregation of results data.

??? warning "Administrator rights required"

    To request administrator rights please get in touch by clicking the email
    icon in the footer of this page.

!!! question "How do I open this page?"

    Admin rights are required to access this page. If you have admin rights:

    1. Sign in to your LibCrowds account.
    2. Click the **Menu** button at the top of any page.
    3. Select **Collections** from the Admin section.
    4. Locate the collection in the table and click **Open**.
    5. Select **Volumes** from the main menu.

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
- **Importer:** The importer type, for example, iiif or flickr.

As we want to avoid defining duplicate volumes, the name and short name
must contain unique values. That is, the details entered don't already exist
for other volumes listed for the collection.

After adding a volume you will be taken to the **Update** page. Here you will
be given additional options to update the volume with a thumbnail and an import
source. The format of the input source will depend on the type of **Importer**
chosen; this is covered further below.


## Updating a volume

To update a volume, locate it in the table and click **Update**.

Note that if projects have already been built using the volume you will only
be able to update the thumbnail. Otherwise, we would risk breaking functions
that rely on consistent volume details, such as results aggregation.

![A screenshot of the update volume page](/assets/img/collection/volumes-update.png?raw=true)
<br><small>*A screenshot of the update volume page*</small>

A form with three tabs will be displayed: one to update the volume's metadata,
one to update the import source and another to update the thumbnail image.

### Updating the core details

Here you can update the details described in the *Adding a volume* section,
above.

To update the core details, edit the form and click **Update Details**.

### Updating the import source

The input source points to the data used to generate tasks for any projects
built using the volume, for example, a set of images.

The fields on this page will change according to the type of importer chosen.
The available importers are:

!!! summary "iiif"

    For volumes using the **iiif** importer, the source should be a
    IIIF manifest that contains the metadata required to display content
    served via the IIIF APIs.

    ```
    # example
    http://api.bl.uk/metadata/iiif/ark:/81055/vdc_100022588857.0x000002/manifest.json
    ```

!!! summary "flickr"

    For volumes using the **flickr** importer, the source should be
    the ID of a Flickr album. Flickr album IDs can be extracted from the end
    of a Flickr album URL.

    ```
    # example
    72157653533516031

    # Flickr album URI
    https://www.flickr.com/photos/132066275@N04/albums/72157653533516031
    ```

!!! summary "gdocs"

    For volumes using the **gdocs** importer, the source should be
    the shareable URL of a Google Docs spreadsheet.

    ```
    # example
    https://docs.google.com/spreadsheets/d/key/edit?usp=sharing
    ```

    It is important that this spreadsheet contains the following columns:

    - **link:** A shareable link to the data source
    - **url:** An image URL
    - **url_b:** A large-sized version of the image (can also be the same as **url**)
    - **url_m:** A medium-sized version of the image (can also be the same as **url**)

To update the import source, edit the form and click **Update Import Source**.


### Updating the thumbnail

The thumbnail image will be used for all projects subsequently generated using
the volume.

To update the thumbnail, select an image and click **Update Thumbnail**.

## Deleting a volume

In the rare case that you want to remove a volume, locate it in the table
and click **Delete**.

Note that deleting a volume would affect the aggregation of results for any
projects already built using that volume. Therefore, you will only be able to
delete volumes that are not associated with any projects.

!!! warning
    Deletion is final, there is no undo.
