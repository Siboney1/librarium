---
title: "Projects"
metaTitle: "Concept: Projects"
metaDescription: "Understanding what Spectro Cloud projects are"
icon: "cog"
hideToC: false
fullWidth: false
---

import WarningBox from 'shared/components/WarningBox';
import Tooltip from "shared/components/ui/Tooltip";

# Projects

A **Project** helps to organize the cluster resources in a logical grouping. The resources which are created within a project are scoped to that specific project and not available to other projects. Users and teams with specific roles can be associated with the project.

## Creating a Project

1. Navigate to **Tenant Admin** > **Projects** and click on the **Create Project** button to show the Project Creation form.

1. Enter the **Name**, **Description**, and **Tags** to create a Project.

## Associating Users and Teams to a Project

The <Tooltip trigger={<u>Users</u>}><a href="/glossary-all/#users">Users</a> are members of a tenant who are assigned roles that control their access within the platform.</Tooltip> and <Tooltip trigger={<u>Teams</u>}>A <a href="/glossary-all/#team">Team</a> is a group of users.</Tooltip> can be associated via **Admin** > **User & Teams** page. Select the **User** or **Team** and under **Project Roles**, select *Add Roles* for the project association.

The user permission is always the union of the Tenant and Project roles along with the roles inherited from the team association. Hence, if a user is a *Tenant Admin*, then the user has the *Project Admin* role to all the projects, even if an explicit project role is not assigned. If a user has the *Project Viewer* role at the Tenant scope, then the user gets *View* permissions on all the projects, and the user can be provided a *Project Admin* role for a specific project using the *Project Roles*.

# Project Dashboard

The **Tenant Admin** > **Projects** page displays the projects-related dashboard cards, capturing the usage and metrics about the projects.


## Monthly kilo-Core hours Usage

The **Monthly Usage** card shows the Daily Cluster Usage in kilo-Core hours (kCh) for a month across all the projects.  The kilo-Core hours is an aggregate measure of how many core hours the worker nodes consume, while under management, across all your deployments. The metering of the kilo-Core hours for the node is done in increments of seconds. The monthly usage card also shows project-wide kilo-Core hours. Based on the plan type, the kilo-Core hours' subscription information will be shown. A tenant starts with a Trial plan and can upgrade to a Monthly On-Demand plan or an Annual Subscription plan.

## Cores per Project Usage

The usage of the active worker nodes' CPU **Cores** is grouped across all projects and shown at an hourly interval, by default. The interval can be changed to days or months.

## Project Card

Every **Project Card** shows the cluster's state information grouped by its health and error states. Cluster health is derived based on the cluster nodes' health. The health of each node is determined based on several conditions such as node state, memory & disk pressure, and network availability.
