All results and user tags generated by LibCrowds are stored as Web Annotations
(see the [Data Model](/data/model) for details) on a server that complies
with the
[Web Annotation Protocol](https://www.w3.org/TR/annotation-protocol).

On this server, we create two AnnotationCollections for each LibCrowds
collection microsite, one to contain the results and another to contain the
tags. These Annotations are accessible via a standardised API (see the
[API](/data/api) page for details).

The AnnotationCollections for a collection microsite can be managed via this
section. Before a microsite is published you will need to visit this page to
create the AnnotationCollections. This should only need to be done once.

??? warning "Administrator rights required"

    To request administrator rights please get in touch by clicking the email
    icon in the footer of this page.

!!! question "How do I open this page?"

    Admin rights are required to access this page. If you have admin rights:

    1. Sign in to your LibCrowds account.
    2. Click the **Menu** button at the top of any page.
    3. Select **Collections** from the Admin section.
    4. Locate the collection in the table and click **Open**.
    5. Select **Annotations** from the main menu.

![A screenshot of a collection microsite's annotations admin page](/assets/img/collection/annotations.png?raw=true)
<br><small>*A screenshot of a collection microsite's annotations admin page*</small>

!!! tip "Settings"

    AnnotationCollections will be created on the server that is linked
    to via the `annotations` setting in your main configuration file. If you
    need to use a different server see
    [Configuring LibCrowds](/setup/configuring-libcrowds).

## Creating a new AnnotationCollection

To create an AnnotationCollection, click the **New** button at the top of the
page. A modal will be displayed containing some options for creating the
collection, as below.

![A screenshot of the new AnnotationCollection modal](/assets/img/collection/annotations-new.png?raw=true)
<br><small>*A screenshot of the new AnnotationCollection modal*</small>

Once you have filled in the form, click **OK** to create the
AnnotationCollection and link it to the collection microsite. The URI for the
new Annotation will appear in the read-only form field for the selected
purpose.

It will now be possible for Annotations to be stored for the given purpose.

!!! warning "Settings"

    Once projects are underway and Annotations are being stored the
    AnnotationCollection IRIs generated on this page should not normally be
    changed, especially without first migrating the data in the original
    AnnotationCollection.
