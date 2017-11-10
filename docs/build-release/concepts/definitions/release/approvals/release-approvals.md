---
title: Release approvals in VSTS and TFS
description: Understand release approvals in Release Management for Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.assetid: 3725541F-FC36-42E2-8153-21D2F9CA755B
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.manager: douge
ms.author: ahomer
ms.date: 09/26/2017
---

# Release approvals

[!INCLUDE [version-rm-dev14](../../../../_shared/version-rm-dev14.md)]

You can enable manual approvals for each environment in a release definition.
When a release is created from a release definition that defines
approvals, the deployment stops at each point where approval is required
until the specified approver grants approval or rejects the release (or
re-assigns the approval to another user).

[What's the difference between a release definition and a release?](../../../releases/index.md)

## Define manual approvals

You can define pre-deployment approvers, post-deployment approvers, or both for an environment.

![Pre-deployment approvals settings](_img/environments-01.png)

![Post-deployment approvals settings](_img/environments-01a.png)

You can select one or more approvers for an approval step, and add multiple approvers for both pre-deployment
and post-deployment settings. These approvers can be individual users or groups of users. 
When a group is specified as an approver, only one of the users in that group needs to approve
for the release to move forward.

* If you are using **Visual Studio Team Services** (VSTS), you
  can use local groups managed in VSTS or
  Azure Active Directory (AAD) groups if they have been
  added into VSTS.

* If you are using **Team Foundation Server** (TFS),
  you can use local groups managed in TFS or Active
  Directory (AD) groups if they have been added into TFS.


The creator of a deployment is considered to be a separate user
role for deployments. For more details,
see [Release permissions](../../../policies/permissions.md#release-permissions).
Either the release creator or the deployment creator can be restricted from approving deployments. 

### Approval options

If no approval is granted within the **Timeout** period you specify, the release is rejected.

You can implement a release approvals policy by specifying that the user who requested (initiated or created) the release cannot approve it.

You can reduce user workload by automatically approving subsequent prompts if the specified
user has already approved the release to a previous environment in the pipeline. Take care
when using this option; for example, you may want to require a user to physically approve a release
to production even though that user has previously approved a release to a QA environment
in the same release pipeline.  

### Approval notifications

Release Management can send notifications such as an email message to the approver(s) defined for
each approval step. 

![configuring notifications for manual approvals](_img/notifications.png)
  
The link in the email message opens the **Summary** page for the release
where the user can approve or reject the release.

<a name="approve-release"></a>

## Approve or reject a release

During a release, the deployment pipeline will stop at any stage that requires approval, and
will display an alert or indicator to the user. In the **Releases**, **Summary**, and **Logs** pages
and lists, it displays the ![Waiting for approver icon](_img/approve-icon.png)
icon when the release is waiting for approval by the current user, or the
![Waiting for different user icon](_img/approve-other-icon.png) icon
when the release is waiting for approval by a different user.
This link or icon displays the approval dialog.
 
![A release in the Releases page paused waiting for approval](_img/approve-01.png)

A notification bar is also shown in the release details page, with a link that displays the approval dialog.      

![Approving a task step for a release in the Summary page](_img/approve-01c.png)

If there is more than one approval waiting for the same user, the reminder will
contain two links, **All** and **Selected environments**. This saves the user
from needing to interact with each approval request individually.

Use the approvers pop-up dialog to:

* Enter a comment
* Approve or reject the release
* Reassign the approval to somebody else
* Defer the deployment to a specified date and time

![Defering a deployment to a specified date and time](_img/approve-03.png)

An administrator can approve a deployment step even
if the approval was originally defined for a different user.
In this case, the approvers pop-up dialog contains an
**Override** link instead of a **Reassign** link.
This enables the administrator to enter comments, approve,
reject, reassign, or defer the deployment.

You can also approve and reject pending releases by accessing the
[Release Management REST API](../../../../../integrate/index.md).

## View and monitor manual approvals

During and after a deployment, the **Logs** page shows comprehensive information
about the progress and status of the release. Pre-deployment and post-deployment
items are included; choose the **Action** icon next to them to see the approval
action log entry.

For example, in this screenshot pre-deployment approval was granted, and the
**Action** link displays the name of the approver and the message entered by that user
when approving (or rejecting) the release.  

![Gates log results ](_img/approve-05.png)

Notice that this release is now waiting for post-deployment approval.
Choosing the **Action** item for this will display the approval dialog where 
the release can be approved or rejected.

## Related topics

* [Approvals overview](index.md)
* [Release gates](release-gates.md)
* [Manual intervention](../../../../tasks/utility/manual-intervention.md)
* [Environments](../environments.md)
* [Triggers](../triggers.md)

## See also

* [Work with release definitions](../../../../actions/work-with-release-definitions.md)
* [View and manage releases](../../../../actions/view-manage-releases.md)
* [Monitor releases and debug deployment issues](../../../../actions/debug-deployment-issues.md)
* [Configure your release pipelines for safe deployments](https://blogs.msdn.microsoft.com/visualstudioalm/2017/04/24/configuring-your-release-pipelines-for-safe-deployments/)

[!INCLUDE [rm-help-support-shared](../../../../_shared/rm-help-support-shared.md)]