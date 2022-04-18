# Artifact Wizard

## Table of Contents

- [Overview](#overview)
- [What is Artifact Wizard](#what-is-artifact-wizard)
  - [Create Gitlab Repository](#Create-Gitlab-Repository)
  - [Install into Admin Essentials and Download](#Install-into-Admin-Essentials-and-Download)
  - [Zero Touch](#Zero-Touch)
- [Requirements](#requirements)
- [How to Install](#how-to-install)
- [Supported Components](#supported-components)
- [How To Contribute](#how-to-contribute)
  - [Creating A New Artifact](#creating-a-new-artifact)
- [Additional Information](#additional-information)

## Overview

Itential is very thankful that you are willing to contribute! We welcome the awesome workflows and use cases you have built to grow our library of pre-built automations and to make them available to anyone who might need them.

This pre-built includes both the Artifact Wizard automation catalog and the Shallow Remove automation catalog. The Shallow Remove AC focuses on wiping an installed pre-built from Admin-Essentials without removing its components, while the Artifact Wizard AC focuses on pre-built export. More information can be found in the [What is Artifact Wizard section](#what-is-artifact-wizard) 

>**Note**: The terms `Artifact` and `Pre-built` are synonyms.

## What is Artifact Wizard

The Artifact Wizard pre-built is composed of two automation catalogs to help you create and contribute pre-builts: the Artifact Wizard automation catalog and the Shallow Remove automation catalog. Artifact Wizard allows to create new bundles (shown as installed prebuilt in admin essentials) from pre-defined entrypoint list (Automation Catalog(s) and/or Workflow(s)), after performing discovery, Artifact Wizard will display the full list of components in which then can be downloaded or promote (contributed) to Itential Open Source project .
In case of wanting to remove an installed artifact (in Admin Essentials) without removing its components (workflows, templates, forms, etc.) you may use the shallow remove functionality. Navigate to Automation Catalog and start the Shallow Remove Artifact agenda.

<!-- ![options](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/options.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/options.png" alt="options" width="400px">
</td></tr></table>


### Create Gitlab Repository

To make contributions easy, Itential has included an option to create a Gitlab Repository for your artifact. In summary, when you run the Artifact Wizard from our **Automation Catalog** app, you will need to select the **Create Gitlab Repository** checkbox as well as the Automation Catalog or Workflow item you want to contribute. As long as your Automation Catalog item has a valid form and workflow attached, we can discover all the other objects (Command Templates, Forms, Child Workflows, Transformations, etc.) and dependencies that are needed to successfully run your automation. After you confirm that Itential has discovered all the components you want to contribute, Artifact Wizard will prompt you to provide a category, description, README, license information, and keywords. Then Artifact Wizard will bundle your automation, push it to our staging folder in GitLab, and provide you a link to the newly created repository.

All the components you should provide are described below.

#### Files

All files you want to contribute (workflows, forms, templates, etc.) should follow this naming schema: `<Artifact Name> <title/use of file>`.

Examples:

- `L2VPN create form`
- `L3VPN create form`
- `Banner-Management IOSXR subflow`
- `Banner-Management Pre-check`

#### Workflows

Since workflows are a central part of any Itential automation, we want to keep them easy to read and understand. Here are a couple of guidelines to follow:

- The main workflow should provide a high level view of what the entire artifact is doing. All functionality must be put into child workflows. Ideally a main workflow consists only of a couple of child workflow tasks and stub tasks. A 20 task maximum limit for main workflows will be enforced.
- Only use IAP tasks that are shipped with our bundles as well as essential tasks from open source adapters. For example, the Meraki SDWAN artifact needs tasks from the Meraki adapter, but tasks from a ServiceNow or Slack adapter should be replaced by the `stub` task, which should be renamed to explain the stubbed action. Ansible modules, scripts or roles can only be used starting with IAP 2020.1.
- Rename all titles for tasks according to what they do in your workflow. Use "Query device name" rather than "Query", or "Apply new interface config" rather than "apply template".
- Choose a task layout that helps other people understand the flow of your automation.
- Try to keep the happy path on a straight line from left to right, add error handling at the bottom, and loops at the top.
- When using eval tasks, both success and failure transitions should be drawn at a 45 degree angle; the success transition should point up, the failure transition should point down.
- Do not mix NSO and Ansible tasks in the same workflow! It will break for customers with only one of the adapters. Instead, use child workflows for each integration.
- Provide a description for each task. Just like commenting your code, this is very helpful to understand your automation.

#### Name

Provide a short and descriptive name of what your artifact is used for.

Examples:

- `Banner Management`
- `Device Health Check`
- `Cisco IOS Upgrade`

#### Categories

Pre-built automations are tracked in different categories. Here is a list of all categories:

- Authentication
- Cloud
- Controller / Orchestration
- DevOps
- NetOps
- Inventory
- ITSM / Testing
- Notification / Messaging
- Persistence
- SD-WAN
- Security
- Telemetry / Analytics
- Utilities

Be sure to select the category that fits your contribution. If your pre-built covers multiple categories, you can select additional ones. For examples on which artifact should be in which category, refer to the [Itential pre-built automations page](https://developer.itential.io/pre-built-automations/).

#### Description

This is a description of the pre-built you will contribute, as shown in the project/repo in GitLab, as well as in the preview of an pre-built within Admin Essentials. Please describe the use case that your pre-built is solving and why people should be excited about it. Your description not exceed 200 characters.

Example:

>`Manage network banners across multiple device types and execute automations against Ansible managed network devices.`

#### README File

Please provide a comprehensive README file in markdown format, that includes:

- Overview of the use case
- Key features/benefits
- Pre-requisites
- How to install the pre-built
- How to run this pre-built
  - Which form inputs are necessary?
  - Are there stubbed tasks that can be replaced?
  - What is the expected output?

Example:

[Itential pre-built automations - Service Provisioning](https://gitlab.com/itentialopensource/pre-built-automations/service-provisioning)

#### License File

If you want to provide a specific license for your contribution, you can do so here. If you leave this field blank, [Apache License Version 2](http://www.apache.org/licenses/LICENSE-2.0) will be automatically used.

#### Keywords

Please provide keywords related to your pre-built so that users can find it.

Examples:

`Configuration Management`, `Policy`, `Compliance`, `Audit`, `Device Onboarding`

>**Note**: At least one keyword is required.

### Install into Admin Essentials and Download

This feature allows you to create a pre-built that will be imported into admin essentials. Following the same methodology as [Create Gitlab Repository](#create-gitlab-repository), you will select either an automation, workflow, or transformation to use as a base, then create the necessary metadata for the pre-built. The automation catalog will then import the necessary components into your Admin Essentials app and create a link for you to download a resulting artifact.json file. This file can be used to import the pre-built into another IAP environment via its Admin Essentials import functionality.

### Zero Touch

This feature is supplimentary to the **Create Gitlab Repository** and **Install into Admin Essentials and Download** features. When selected with one of the other options, it allows the automation catalogs to act without manual tasks. This means you will only have to select the automation catalog, workflow, or transformation in the initial form stage and the remaining input information will be stubbed out. This is especially useful if you would like to run the Artifact Workflow wizard as a child job in another workflow.

## Requirements

The following is required to run Artifact Wizard, and is compatible with the following versions:

- Itential Automation Platform
  - `^2020.2.x`
- App-Artifacts
  - `^6.0.x`

## How to Install

To install Artifact Wizard, verify you are running a supported version of Itential Automation Platform (IAP) as listed above in the [Requirements](#requirements) section. If you do not currently have App-Artifacts installed as a service on your node, the `.tgz` file or "tarball" can be obtained from the [Nexus repository](https://registry.aws.itential.com/#browse/browse:app-prebuilt_automations). Please refer to the instructions included in the App-Artifacts README to install it.

Artifact Wizard can be installed from within Admin Essentials. Simply search for `artifact-wizard` and click the **Install** button as shown below.

<!-- ![install](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/install.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/install.png" alt="install" width="800px">
</td></tr></table>

Alternatively, you may download the `artifact.json` file, and import it through admin essentials app.

## Supported Components

The Itential Automation Platform components that Artifact Wizard can currently consume include:

- Automation Catalog items
- Form Builder Forms
- JSON-Forms
- Mop-Templates
- Mop-Analytic Templates
- Workflows
- Transformations
- Jinja2 Templates
- TextFSM Templates

## How To Contribute

Artifact Wizard can be launched from **Automation Catalog**, and the jobs must be run as an admin user. To begin, click the **Run** button.

<!-- ![automation catalog](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/ac.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/ac.png" alt="automation catalog" width="400px">
</td></tr></table>

### Creating A New Artifact

To create a new artifact, you must supply a name and an entry point for the automation.

<!-- ![create new artifact](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/run_new.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/run_new.png" alt="create new artifact" width="600px">
</td></tr></table>

If desired, one can also specify pre-built scope of the pre-built from its default value - @itentialopensource. 
Pre-builts must have a scope specified. 
Pre-builts' scope will take affect in admin-essentials display once installed.

It is important to remember that the entry point to the bundle for the Artifact Wizard automation Catalog _must_ be an Automation Catalog(s) and/or Workflow item(s). The item(s) should supply both a workflow and a form as an entry point for the artifact. Any job variables required for the workflow to run should be supplied by the accompanying form, and will be accessible to the workflow via the `formData` object.

After you click the **Run** button, Artifact Wizard will discover all dependencies required by the workflow selected in the Automation Catalog item, as well as version information for each IAP application required to install the bundled artifact. The results of the discovery will be displayed for you to confirm (when not running in Zero Touch mode).

<!-- ![discovery](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/discovery.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/discovery.png" alt="discovery" width="400px">
</td></tr></table>

Next, the catalogs will prompt you for artifact metadata and give you the opportunity to provide a short description, a README, license information, and a list of keywords (at least one keyword is required) relevant to the artifact. If no license is provided, the catalogs will bundle [Apache License Version 2](http://www.apache.org/licenses/LICENSE-2.0) by default. Refer to the [Contribution Guidelines](#contribution-guidelines) section regarding best practices and naming conventions.

At this current time, Artifact Wizard must perform a health check to gather module information in order to properly bundle the artifact. Hence, you will be prompted to perform the health check as an admin user. Of note, this step is skipped for Zero Touch mode.

<!-- ![health check](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/healthcheck.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/healthcheck.png" alt="health check" width="600px">
</td></tr></table>

Workflow will then bundle all your dependencies, create a `package.json` file, and push the pre-built to a new repository on GitLab under our `staging` directory. Upon successful completion of the job, a link to the repository will be provided.

<!-- ![view repo](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/view_repo.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/view_repo.png" alt="view repo" width="600px">
</td></tr></table>

Click the provided link to direct your browser to the newly created repository. The repository UI will display, which should look similar to the following:
Note, Itential Open Source staging folder is not public, and one may have no access to. Once published, every pre-built is taken out of staging onto a publicly availabel folder.

<!-- ![new repo](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/repo.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/repo.png" alt="new repo" width="800px">
</td></tr></table>

The `bundles` directory contains all components of the automation that were exported with the pre-built.

<!-- ![bundles](https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/bundles.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/artifact-wizard/-/raw/release/2021.1/images/bundles.png" alt="bundles" width="800px">
</td></tr></table>

Finally, press the **Continue** button to complete the job.

**Congratulations on creating your very first pre-built, and thank you for contributing!** 🎉

## Additional Information

Please use your Itential Service Desk account if support is needed when using the Artifact Wizard.
