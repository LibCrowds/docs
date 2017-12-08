Core details for the project can be updated via this page. This includes the
the name, shortname and description of the project, as well as security
requirements, the webhook URL and a button to publish the project.

??? question "How do I open this page?"

    Administrator or editor rights are required to access this page. If you
    have the correct rights:

    1. Sign in to your LibCrowds account.
    2. Click your username at the right of the naviation bar.
    3. Select **Project Admin** from the dropdown menu.
    4. Locate the project in the table and click **Open**.
    5. Select **Details** from dashboard menu on the left-hand side.

![A screenshot of the project details admin page](/assets/img/admin-project-details.png?raw=true)
<br><small>*A screenshot of the project details admin page*</small>

## Updating the project metadata

The project name and description will appear on the project card as presented
to all users via the collection microsite. Modify these by updating the
form fields and clicking the **Update** button

## Updating the webhook URL

Each time a task is completed a payload is sent to the URL specified here, so
that additional actions such as results analysis can be triggered.

During project creation this URL will be set automatically to an endpoint
setup to analyse results for the project's task presenter.

!!! warning
    You should not usually need to edit this URL and the option is provided
    here mostly for troubleshooting purposes. Changing the URL to an endpoint
    other than one that has been setup for LibCrowds core analysis will
    probably break the automated results analysis.

## Restricting access

By default, all users (registered and anonymous) will be able to contribute to
the project. However, you can password protect the project or restrict it
to registered users by editing the password field and toggles on this form
and clicking **Update**.
