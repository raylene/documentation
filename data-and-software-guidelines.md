# Data and Software Guidelines

This document describes how we manage data and write software at U.S. Digital Response ("USDR"). If you have a good reason to request diverging from these policies, we need to hear from you at [info@usdigitalresponse.org](mailto:info@usdigitalresponse.org).

## Guiding Principles

#### Open and Accessible by Default

USDR data, code, documentation, and projects are open and accessible by default. USDR efforts are meant to be replicated, reused, adapted, and otherwise available for collaboration. USDR data, code, documentation, and projects should be easily discoverable, and projects with a website should dedicate a public-facing point of contact with whom potential collaborators can get in touch with questions.

#### Consistent Design

Any website that will be operated by or represent a government entity should use the [U.S. Web Design System](https://designsystem.digital.gov/). This design framework allows for rapid development using a standard pattern library, and ensures visual consistency between projects and with existing government design practices.

## Data Guidelines

Given the nature of COVID-19 relief work and close collaboration with government partners, data is a critical component of many USDR projects. In all cases (even when the data itself has restricted access for good reasons), the use cases, access restrictions, and descriptions of any relevant datasets should be well-documented and shared openly.

### Open Data

Data used for USDR projects should be available in open and machine-readable formats wherever possible. The potential use cases, access mechanisms and descriptions of the data should be well-documented and made available with a [Creative Commons Zero](https://creativecommons.org/share-your-work/public-domain/cc0/) (CC0) license.

If the data is sensitive (e.g., PII, PHI, proprietary data, etc.) and access must be restricted, those reasons should be clearly explained in the documentation and the storage compliant with regulatory guidelines. Whenever applicable, the data should be accessible (via API or clear export pipelines) and made available to trusted government partners. All data collection, storage, retention, and access controls should be designed with privacy and security in mind.

### USDR Team Data

USDR collects limited data from USDR volunteers, government, and organizational partners, collectively referred to as "project partners." All data is provided voluntarily with the team and will only be shared with team members and project partners when required to facilitate volunteer work. This data will be retained and used only as necessary and for the time required to undertake USDR projects in support of project partners.

USDR will take reasonable steps to protect this data from unauthorized modification, disclosure, and destruction. USDR will not share volunteer or partner data (or any data about volunteers or partners) for any other purposes without permission.

## Software Guidelines

### Source Control

[The U.S. Digital Response GitHub organization](https://github.com/usdigitalresponse) houses any USDR repositories, and — as needed — forks of software developed elsewhere. For questions or access to our repository, email [tools-team@usdigitalresponse.org](mailto:tools-team@usdigitalresponse.org).

When assisting government partners through staff augmentation to perform software development, we recognize that source control is rare, and that we are unlikely to be in a position to influence licensing decisions. Whenever possible, we should encourage partners to develop in accessible GitHub accounts or make documentation publicly available.

### Licensing

For a project that originated elsewhere but will be built with active collaboration from USDR (e.g. relies on connections to our government partners for user research and feedback, has volunteer support), the work must be published under [an OSI-approved license](https://opensource.org/licenses), a [Creative Commons Zero license](https://creativecommons.org/choose/zero/), or committed to the public domain.

Projects originating with USDR must be licensed under the [Apache 2.0 License](https://opensource.org/licenses/Apache-2.0).

### Repository Standards

A `README.md` file should be present, identifying the purpose of the software and its creators, linking to documentation, providing screenshots (if relevant), a link to an example instance of the software (if relevant), a link to API documentation (if relevant), and a link to the license file. If the software is the work of an organization, also provide a link back to a page on that organization’s website to demonstrate the software’s provenance.
Soon we hope to support a self-service threat model so that teams can diagram
A `LICENSE.md` file should be present, specifying the licensing terms.

A `CODE_OF_CONDUCT.md` file should be present, defining the standards for the community, per [GitHub’s specs](https://help.github.com/en/github/building-a-strong-community/adding-a-code-of-conduct-to-your-project). USDR-originated projects should use the [Contributor Covenant](https://www.contributor-covenant.org/version/1/4/code-of-conduct/code_of_conduct.txt).

A `CONTRIBUTING.md` file should be present, describing how to contribute to the project (if, indeed, contributions are welcome). That should make clear the license status of the software, which all contributors’ work will be released under when it is incorporated into the larger work.

### Documentation

All dependencies must be listed and the licenses documented. (This can be done in the form of a machine-readable manifest, e.g. `package.json`, `requirements.txt`, `composer.json`, etc.) Major functionality in the software/source code must be documented. Individual methods should be documented inline using comments that permit the use of documentation-generation tools, such as [JSDoc](https://jsdoc.app/).

The `README.md` file should provide (or link to) step-by-step instructions for standing up the site locally (in Docker or a common equivalent), and likewise provide step-by-step instructions for deploying the site to a hosting environment. When relevant, infrastructure should be defined as code in e.g. Terraform or Kubernetes.

The `README.md` is required to include a ["Data Inventory" section](https://github.com/usdigitalresponse/documentation/examples/data-inventory.md) that lists 1) all data that will be collected or stored by the system, 2) how its stored, and 3) whether the data is intended to be publically accessible. This is extremely important to make sure we properly secure any data we collect.

> #### Example Data Inventory
>
> Our app collects information from a state's citizens and shares the contact information of doctors who have partnered with us.
>
> | name                           | data store | public |
> | ------------------------------ | ---------- | ------ |
> | citizen emails                 | S3 bucket  | false  |
> | citizen names                  | S3 bucket  | false  |
> | citizen social security number | AWS RDS    | false  |
> | doctor names                   | AWS RDS    | true   |
> | doctor emails                  | AWS RDS    | true   |

### Commits

Commit messages should contain:

1. A single line summary of the change. Imagine some future engineer is skimming down a list of commits; will your summary tell them enough to decide whether they need to read it in detail?
2. A description that includes, at least, the goal (the "why" not "what") of the change. Depending on complexity you might also include a description of how it works, alternative approaches that were rejected, benchmarks etc.
3. A test plan: Whatever actions you took to verify the change was correct. These should be detailed enough so that another person could perform the same test. Without automated testing, this at least gives future engineers a chance to do a manual regression test on your changes.

### Code Review and Automated Testing

**Code review** ensures we don’t have a single point of failure, have a shared understanding of how our systems work, and maintain a consistent level of quality across the codebase. All software commits should be reviewed by another engineer, e.g via a pull request. Given the time sensitivity of our work, responding to assigned reviews should be everyone’s top priority (i.e., review first, do your own work second).

**Security review and threat modeling** ensures that we consider all of the security risks that an application may face. Before going live with a project, please reach out in the #security Slack channel to partner with a security team member to review your project.

**Automated testing** ensures we can move fast with safety. However, effective testing is a substantial time commitment that needs to be weighed against our need to ship as fast as possible. Use good judgment here, and consider a) the consequences of something failing, b) how fragile it’s likely to be, and c) how much time investment is needed to correctly test the component.

**Automated security testing** ensures that we protect the applications we create and the data they will collect. All public repositories should have [Snyk](https://app.snyk.io/org/usdigitalresponse/) vulnerability and dependency scanning integrated. Snyk will automatically run on every PR and fail on high severity vulnerabilities that have a fix (dependency upgrade) available.

## Contact Us

If you have any questions or concerns about these guidelines, contact us at [info@usdigitalresponse.org](mailto:info@usdigitalresponse.org).
