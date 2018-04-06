When a user submits a new template, or proposes an update to an existing one,
the template will be listed on this page for an administrator to approve or
reject.

??? warning "Administrator rights required"

    To request administrator rights please get in touch by clicking the email
    icon in the footer of this page.

!!! question "How do I open this page?"

    Admin rights are required to access this page. If you have admin rights:

    1. Sign in to your LibCrowds account.
    2. Select **Pending Templates** from the main menu.

![A screenshot of the site admin pending templates page](/assets/img/site/pending-templates.png?raw=true)
<br><small>*A screenshot of the site admin pending templates page*</small>

## Viewing the changes

Click the **Show Details** button to view the proposed changes, which will be
highlighted in green.

![A screenshot highlighting pending changes for a template](/assets/img/site/pending-template-details.png?raw=true)
<br><small>*A screenshot highlighting pending changes for a template*</small>

## Approving

Approved templates can be used to generate projects for a collection
microsite. To approve a template click the **Approve** button.

An email will then be sent to the creator of that template to let them know
that the changes have been accepted.

## Rejecting

If updates to a template are not deemed to be acceptable for some reason, you
can reject it by clicking the **Reject** button.

A popup will be shown asking for the reason for rejection and what could be
done before the template is accepted. This message will be sent to the
creator of that template. Note that the message will be wrapped with some
standard text. A markdown representation of that message is presented below,
where the `{{ reason }}` tag is replaced with the custom rejection message.

```markdown
Hello {{ user['fullname'] }},

You submitted a request to create or update the {{ template['name'] }}
template. Unfortunately, we didn't think that the proposed changes were
suitable for the following reason:

{{ reason }}

Please get in touch at
[{{ config.CONTACT_EMAIL }}](mailto:{{ config.CONTACT_EMAIL }})
for further guidance.

Regards,

{{ config.BRAND }} Team
```
