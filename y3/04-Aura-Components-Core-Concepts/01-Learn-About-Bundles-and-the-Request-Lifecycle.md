# Learn About Bundles and the Request Lifecycle

## Before You Go Further

[Quick Start: Lightning Web Components](./Quick-Start-Lightning-Web-Components). There, you'll set up your Salesforce DX environment and Visual Studio Code.

## Core Concepts

Visualforce and Aura have fundamental differences in architecture, and different requirements for how you use them to build apps.

Note that we’re not explaining how to use Aura components features in detail here. (That’s the [Aura Components Basics](./Aura-Components-Basics) module.)

## Concept: Page vs. Bundle

Visualforce pages (and Visualforce components, but let’s set those aside for now) are stored on Salesforce as a single entity, an ApexPage. When you use Salesforce Extensions for Visual Studio Code or another tool to copy your Visualforce pages to your local storage to work on them, an individual Visualforce page is represented as two files in the metadata/pages directory:

- yourPageName.page
- yourPageName.page-meta.xml

The first is the code for the page, and the second is the page metadata (API version, mobile settings, and so on).
