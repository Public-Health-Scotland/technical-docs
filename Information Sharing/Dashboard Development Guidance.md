# Dashboard Development Guidance

> [!NOTE]
> This guidance is currently in draft. Please feel free to contribute by [raising an issue](https://github.com/Public-Health-Scotland/technical-docs/issues/new/choose).

This document aims to set out key considerations throughout the development of dashboards, including the design, development, and deployment phases. Further research and guidance should be sought for specific areas as it would not be possible to cover all aspects in this document.

The term 'dashboard' is used to refer to any visualisation tool that presents data in an interactive graphical format, such as R Shiny or Tableau but relevance will apply to other formats, such as R Markdown or Excel. When considering development of a new dashboard, there are some initial considerations of the format in general:

| Pros                                                                                      |     | Cons                                                                                               |
| ----------------------------------------------------------------------------------------- | --- | -------------------------------------------------------------------------------------------------- |
| High-level indicators are well-suited to dashboards                                       |     | Specific insights or complex data are not well suited                                              |
| High priority topics can be easily accessed                                               |     | Existing knowledge and context is required to interpret                                            |
| Data can be updated frequently                                                            |     | There is a high degree of maintenance                                                              |
| Data can be updated automatically                                                         |     | Development requires technical expertise                                                           |
| Multiple breakdowns or filters can be applied that would overwise be difficult to present |     | Prevents the charts being used in other formats, such as social media                              |
| Interactivity gives users autonomy to explore insights                                    |     | Interactivity puts the burden of interpretation on the user, potentially hiding important insights |
| The focus is on the data                                                                  |     | Explanation and storytelling is missed                                                             |
| Shared online                                                                             |     | Limitations for security and ensuring accessibility                                                |

## Contents

- [Design](#design) - before any development work begins, it is important to consider the design of the dashboard and project, ensuring objectives are clear and the right resource is in place.
  - [User Needs](#user-needs)
  - [Data](#data)
  - [Interface Design](#interface-design)
  - [Project Requirements](#project-requirements)
- [Development](#development) - once the design has been agreed, the development phase can begin. This section covers key considerations throughout the development process.
  - [Code Quality](#code-quality)
  - [Version Control](#version-control)
  - [Data Management](#data-management)
  - [Testing](#testing)
  - [Documentation](#documentation)
  - [Data Protection](#data-protection)
  - [Feedback](#feedback)
- [Deployment](#deployment) - once the dashboard has been developed, it needs to be deployed to a production environment. This section covers key considerations throughout the deployment process.
  - [Test Access](#test-access)
  - [Pre-Release Access (PRA)](#pre-release-access-pra)
  - [Monitoring](#monitoring)
- [Reference](#reference) - a list of references and further reading for additional guidance.

## Design

There are a number of reasons why a team may decide to develop a new dashboard.
Commonly the dashboard is replacing another format such as an Excel spreadsheet in order to make the data more accessible for users or a team is deciding to publish the data for the first time. However, it is important for teams to consider the following areas before development.

### User Needs

Before any development work begins, it is important to understand the needs of the users who will be using the dashboard. This could involve conducting user research, such as interviews or surveys, to understand what users need from the dashboard. At this point, generating user personas can be helpful to ensure that everyone is on the same page about who the users are and what they need. During this process, it's also important to consider if a new dashboard is needed or if an existing dashboard already exists or could be updated to meet the needs of the users.

The [UKSA Code of Practice for Statistics](https://code.statisticsauthority.gov.uk/) outlines the importance of user engagement in the development of statistics and data products. This includes engaging with users to understand their needs and preferences, as well as testing products with users to ensure they are fit for purpose. This should be an ongoing process that continues beyond the development stage and the first release. It is important that feedback mechanisms are put in place to ensure all statistical releases continue to be fit for purpose.

### Data

The data that will be used in the dashboard is a key consideration. It is important to understand where the data comes from, how it is collected, and how it is processed. This will help to ensure that the data is accurate, reliable, and up-to-date. It is also important to consider how the data will be stored, accessed, and maintained over time. This could be through a database, Open Data, API, or other data source.

If related to a specific health topic or publication, Open Data should be considered for release alongside or as the primary source for the dashboard, in line with the [Open Data Strategy for Scotland](https://www.gov.scot/publications/open-data-strategy/).

### Interface Design

There are several elements to consider as part of the interface design of a dashboard. While each project will bring varying expertise on the data, users, context, and even technical expertise, a strong foundation in interface design is vital to ensure that the dashboard is fit for purpose, including accessibility, usability, and user experience.

Key areas are explored in more detail below but should be considered in context by creating wireframes or prototypes to explore information hierarchy and layout, and test different design ideas and gather feedback from users. Brand guidelines, accessibility, and consistency across all PHS products should be considered throughout the design process. To support this, a template for Shiny apps exists within the [{phstemplates} package](https://public-health-scotland.github.io/phstemplates/) with further guidance available on the [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/). The [UK Government Service Manual](https://www.gov.uk/service-manual) and [The Interaction Design Founction - User Research article](https://www.interaction-design.org/literature/topics/user-research) contains excellent resources for this too.

#### Visualisation

Visualisations are likely to form the most significant proportion of any dashboard so it's vital to optimise their layout and choose the right options for the data being presented, such as bar charts, line charts, maps, or tables. It is also important to consider the design of the visualisation, including colours, fonts, and layout, you may find the [{phsstyles} package](https://public-health-scotland.github.io/phsstyles/) useful for this. This has a significant impact on user engagement and trust so should be prioritised as part of the design process.

#### Interactivity

Interactivity can help to make the data more engaging and easier to explore, and is mostly expected within a dashboard format. This could include features such as filters, drill-downs, or tooltips. It is important to consider what level of interactivity is needed for the dashboard and how this can be implemented in a way that is intuitive, user-friendly, and accessible.

#### Accessibility

Providing accessible web content, including dashboards, is a legal requirement in the UK but ultimately provides an optimal product for everyone. As a public sector organisation, we must ensure that our digital services are accessible to all users, including those with disabilities. It is therefore important to consider accessibility throughout the design process, including the use of colour, text, and interactive elements. The [Dashboard Accessibility Guidance](https://public-health-scotland.github.io/knowledge-base/docs/Information%20Sharing?doc=Dashboard%20Accessibility%20Guidance.md) provides further information on this topic.

#### Performance

While often thought of as a development consideration, performance should be considered from the design phase. This could involve optimising the design of the dashboard codebase to maximise efficiency, ensuring that the dashboard loads quickly and is responsive to user interactions. Looking at data pipelines, optimising queries, and considering how to reduce the size of images or other assets, caching data, or using lazy loading.

### Project Requirements

Last, but definitely not least, it is important to consider the requirements of the project as a whole. Depending on the contents and release type, different options will be available and different processes will need to be followed. Which technologies and deployment options that are available can be explored with the [Data Science team](mailto:phs.datascience@phs.scot). Every release should consider security and compliance regulations to protect confidential data and algorithms, with specific considerations for the following release types:

- **Management Information** usually contains data that is not for public consumption due to confidentiality, quality, or nature. This means certain formats are not appropriate due to the insecure options for sharing. There are also specified processes for the release of management information that should be discussed with the [Statistics Governance team](mailto:phs.statsgov@phs.scot).
- **Publication** dashboards are those that are intended for public consumption and should align with standing publication processes. Where the release is not part of an existing scheduled and pre-announced publication, guidance on the [publication process](https://spark.publichealthscotland.org/corporate-guidance/statistical-governance/statistical-and-research-publications-process/) and [publication timetable](https://spark.publichealthscotland.org/downloads/statistical-publications-timetable/) should be reviewed with support from the [Statistics Governance team](mailto:phs.statsgov@phs.scot). Depending on the expected results and integration on the PHS website, this should be discussed with the [Web & Publications team](mailto:phs.statspublications@phs.scot).
- **Co-Production** with other organisations or stakeholders may require additional considerations, such as data sharing agreements, branding, or other requirements. This should be discussed first with the [Statistics Governance team](mailto:phs.statsgov@phs.scot).

At this stage, other project requirements should be considered such as the timeline and resources available for the project. It is important to ensure that the project is feasible and that the team has the skills and expertise needed to deliver the dashboard. It is also important to consider how the dashboard will be maintained and updated over time. A number of teams exist in the organisation that can support these discussions if required:

- [Customer Focus team](mailto:phs.cfteamrequest@phs.scot) - for user research and engagement, and technical resource support through a demand management process.
- [Data Science team](mailto:phs.datascience@phs.scot) - for technical support and guidance on data workflows, visualisation, and dashboard development.
- [Statistics Governance team](mailto:phs.statsgov@phs.scot) - for guidance on statistical releases, data governance, and compliance with the Code of Practice for Statistics.
- [Web & Publications team](mailto:phs.statspublications@phs.scot) - for guidance on integration to the PHS website, accessibility, and publication standards.

## Development

Ensuring the pre-development phase is followed will support a smooth transition to the development phase. The general recommendations for these development projects is to use an iterative approach with version control, with regular feedback from users and stakeholders. The following sections provide guidance on key considerations throughout the development process.

### Code Quality

Code quality is relevant to the development from the start and can impact maintainability and performance. This involves writing clean, well-documented codebases that are easy to read, navigate and maintain. Certain dashboard technologies are more supportive of this than others, such as R Shiny or Dash by Plotly, even R Markdown and Quarto. This is because these are code/plain-text structured and open source, which in itself offers another set of advantages, such as support, expandability, and transparency. 

Designing a dashboard pulls on skills outside of the data and analytics domain, such as web development, user experience, and design. As such, considering how interfaces are designed and built is important. Similarly, using loading bars and skeleton components while content is loading can improve the user experience and perception of performance.

It is important to follow best practices for coding, such as using consistent naming conventions, commenting code, and using appropriate functions. This will help to ensure that the code is robust, reliable, and easy to understand. The [{phstemplates} package](https://public-health-scotland.github.io/phstemplates/) provides a template for getting started, and other guidance is available on the [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/).

### Version Control

Version control is a key part of the development process and should be used from the start of the project. This allows for changes to be tracked, reviewed, and reverted if necessary. It also enables collaboration between team members and ensures that everyone is working on the same version of the codebase.

The recommended version control system is Git, with GitHub as the hosting platform, adding a layer of open collaboration and transparency. Where this isn't suitable, Gitea is available as an alternative. Both of these allow for easy collaboration, code review, and integration with other tools. Further guidance is available on the [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/).

### Data Management

A significant component of performance in dashboards is the data management. This includes the data storage and data processing. It is important to consider how the data will be accessed, processed, and stored, and how this will impact the performance of the dashboard. This should involve appropriate dataset design (reducing redundancy), optimised processing and queries, caching data, or using lazy loading to ensure that the dashboard loads quickly and is responsive to user interactions.

### Testing

Testing includes multiple areas to consider, including basic checks through to automated testing pipelines.

- **Code Review** is the first line of defence in ensuring code quality. This should be done by a team member, promoting knowledge sharing, to ensure that the code is well-written, follows best practices, and security considerations are met.
- **Functional Testing** ensures that the dashboard works as expected. This could involve testing individual components to ensure that they work as expected and across browsers and devices, under load, and with accessibility tools.
- **Unit Testing** is a more granular level of testing, ensuring that individual components of the codebase work as expected. This can be done using testing frameworks such as the [`{testthat}` package](https://testthat.r-lib.org/) in R.
- **Integration Testing** involves testing how different components of the codebase work together. This could involve testing how the dashboard interacts with the data source.
- **User Acceptance Testing** involves testing the dashboard with users to ensure that it meets their needs and expectations. This could involve conducting usability testing, surveys, or interviews with users.

### Documentation

Documentation can often be left to the end of the development phase but should be considered and elements generated from the design phase of the project. This includes documenting the design, codebase, data sources, and any other relevant information, and ideally stored alongside the codebase using version control. This will help to ensure that the project is well-documented and easy to understand for other team members or stakeholders. As the project moves to Business as Usual (BAU) or into maintenace, other documentation may be required such as a Standard Operating Procedure (SOP). A README file should also be included in the repository too, providing an overview of the project, how to set up the project, and how to contribute.

### Data Protection

Prior to releasing any statistics, every project should ensure that no sensitive or potentially disclosive information is included in the dashboard. It is important to consider how the data will be used and who will have access to it, and to ensure that appropriate safeguards are in place to protect the data. All projects should review the [Statistics Disclosure Control Protocol](https://spark.publichealthscotland.org/downloads/statistical-disclosure-control-protocol/) and complete a [Disclosure Risk Assessment Form](https://spark.publichealthscotland.org/downloads/disclosure-risk-assessment-form-and-statistical-disclosure-control-flowchart/) as necessary.

### Feedback

Feedback is a key part of the development process and should be sought throughout the project. This could involve seeking feedback from users, stakeholders, or other team members to ensure that the project is on track and meeting the needs of the users. It is important to consider how feedback will be collected and acted upon, and to ensure that the project is responsive to feedback.

## Deployment

Once the dashboard has been developed, getting it into the hands of users is the next step. Deployment is the process of moving the dashboard from a development environment to a production environment, and is often referenced as "publishing" the dashboard.

In some cases, a dashboard may simply be shared directly with users via email or secure file transfer (i.e. a flexdashboard or Excel). However, in most cases, the dashboard will be hosted on a server and accessed via a web browser. The format used will depend on the requirements of the project, security and governance implications, and the needs of the users.

Specific deployment guidance is available for the following formats:

- **Shiny apps** - [Deploying a Shiny app guidance](https://public-health-scotland.github.io/knowledge-base/docs/Information%20Sharing?doc=Deploying%20a%20Shiny%20app.md)

### Test Access

It's important to test the dashboard in a production-like environment before it is released as live. This could involve testing the dashboard on different devices and browsers, under load, with accessibility tools, and with different user groups. This will help to ensure that the dashboard works as expected and is accessible to all users. As the deployment itself is part of the test, the dashboard needs to be 'deployed' for this testing phase.

For R Shiny apps, we currently only have one option for deployment which is the live server, [shinyapps.io](shinyapps.io). This server should be considered public for all deployments, even those with PHS-developer-implemented authentication. As such, security and data protection considerations should be taken into account for non-live deployments:

- Use only dummy or anonymised data
- Add password protection
- Add a disclaimer to the dashboard
- Limit access to the dashboard to only those who require it

### Pre-Release Access (PRA)

PRA is the term used to describe the access provided to specific individuals to statistical outputs in their final form immediately prior to publication. In PHS PRA is managed by the [Statistics Governance team](mailto:phs.statsgov@phs.scot).

#### R Shiny apps

At PHS, we currently only have one option for deployment which is the live server, [shinyapps.io](shinyapps.io). This server should be considered public for all deployments, even those with PHS-developer-implemented authentication. As such, security and data protection considerations should be taken into account for non-live deployments:

- Add password protection
- Add a disclaimer to the dashboard
- Limit access to the dashboard to only those who require it

Full deployment details are outlined in [Deploying a Shiny app](https://public-health-scotland.github.io/knowledge-base/docs/Information%20Sharing?doc=Deploying%20a%20Shiny%20app.md). The main points to consider for dashboard development are:

- Minimise deployed versions, most dashboards will require only 2 versions, a PRA version and a live version, some may have a test version for new feature testing
- All deployed apps should follow standard naming standards, namely be prefixed with `phs-`, lowercase, and hyphenated. The PRA version of the app should be suffixed with `-pra`.
  - e.g. `phs-app-name` and `phs-app-name-pra`.
- The PRA version should remain password protected.
- The live version of the dashboard should never be password protected and be updated as per the publication timetable or as required. This should overwrite the previous version, not be an additional version on the server.
- On the week of the key messages handling meeting, send the following information to the [Statistics Governance team](mailto:phs.statsgov@phs.scot):
  - The R Shiny app PRA URL, e.g. `https://scotland.shinyapps.io/phs-app-name-pra/`
  - PRA username and password for access
  - The R Shiny app live URL, e.g. `https://scotland.shinyapps.io/phs-app-name/`
- On publication day, the dashboard should be deployed to the live URL at 09:30

#### Tableau dashboards

Tableau dashboards are deployed to the Tableau server. No PRA access is available for Tableau dashboards.

Along with the rest of your publication files, please place a copy of the Tableau dashboard(s) into your SharePoint folder. Any data in the dashboard must be extracted so it is no longer connected to a live source. To do this, select 'Data' from the top navigation bar > hover over each data source > select 'Extract Data...'. To confirm this has worked, you will see a tick next to 'Use Extract' in the data source submenu. You must do this for all data sources.

The final step is to save the dashboard as a Tableau packaged workbook (.twbx) in your SharePoint folder.

On publication day, the Stats publications team will publish your dashboard to Tableau Public and ensure it is embedded on your publication page at 09:30.

### Monitoring

Once the dashboard has been deployed, it is useful to monitor its performance and usage. Mostly statistics available are related to the server performance and usage, such as sessions and memory utilisation. With R Shiny apps, these statistics are available using the [{rsconnect} pacakge](https://rstudio.github.io/rsconnect/).

Other metrics such as page views, user interactions, and load times can be significantly useful but require other tools. Google Analytics can be useful for this, however, it is important to consider the data protection and legal implications of tracking user data and cookie usage. The [Web & Publications team](phs.statspublications@phs.scot) may be able to provide some high level usage statistics from the PHS website, or provide further guidance on using Google Analytics.

## Reference

- [Dashboard Accessibility Guidance](https://public-health-scotland.github.io/knowledge-base/docs/Information%20Sharing?doc=Dashboard%20Accessibility%20Guidance.md)
- [Deploying a Shiny app guidance](https://public-health-scotland.github.io/knowledge-base/docs/Information%20Sharing?doc=Deploying%20a%20Shiny%20app.md)
- [Interaction Design Foundation - User Research](https://www.interaction-design.org/literature/topics/user-research)
- [ONS Service Manual - Data visualisation](https://service-manual.ons.gov.uk/data-visualisation)
- [Open Data Strategy for Scotland](https://www.gov.scot/publications/open-data-strategy/)
- [PHS Chart & Dashboard Accessibility Guidance](http://spark.publichealthscotland.org/media/2176/chart-and-dashboard-accessibility-guidance-version-12.pdf)
- [PHS Content & Accessibility Guidance](https://spark.publichealthscotland.org/downloads/content-and-accessibility-guidance/)
- [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/)
- [PHS Disclosure Risk Assessment Form](https://spark.publichealthscotland.org/downloads/disclosure-risk-assessment-form-and-statistical-disclosure-control-flowchart/)
- [PHS Statistical and Research Publications Process](https://spark.publichealthscotland.org/corporate-guidance/statistical-governance/statistical-and-research-publications-process/)
- [PHS Statistical Disclosure Control (SDC) Overview](https://spark.publichealthscotland.org/corporate-guidance/statistical-governance/statistical-disclosure-control/overview-of-disclosure-control-protocol/)
- [PHS Statistical Disclosure Control (SDC) Protocol](https://spark.publichealthscotland.org/downloads/statistical-disclosure-control-protocol/)
- [PHS Statistical Publications Timetable](https://spark.publichealthscotland.org/corporate-guidance/statistical-governance/releasing-statistics/)
- [UK Government Service Manual](https://www.gov.uk/service-manual)
- [UKSA Code of Practice for Statistics](https://code.statisticsauthority.gov.uk/)
