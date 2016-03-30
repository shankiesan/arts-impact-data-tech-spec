#Phase 2 – Adds input form and "My Data" portal

##Phase overview

([Phase 1]((../master/phases/1-minimum-viable-product.md))) has three major shortcomings:

1. Arts organisations have to contact the system administrator to add their data – they can't do it themselves
2. Arts organisations can't see what they've already submitted
3. End-users (i.e. any consumer of *open data* – arts organisations, government departments, other funders, interested individuals etc.) can't easily query and report on the data without fairly advanced technical skills

This phase addresses points (1) and (2) above by:

* Adding a comprehensive data submission form
* Adding a "My Data" portal where arts organisations can manage their existing data

The purpose of this phase is to refine the data model to ensure that it can cope with the outcomes of real-world projects. If ([Phase 1]((../master/phases/1-minimum-viable-product.md))) was successful, it will have proved that an administrator can add project outcome data into the model. Once the front-end form is implemented, this phase will attempt to prove that unexperienced users can do the same by making the data-entry tool available to a progressively wider audience. We will test the tool with each group below and tweak according to feedback:

1. Sample/hypothetical data entered by administrators
2. Real data entered by administrators
3. Real data entered by government agencies
4. Real data entered by arts organisations

##Functional requirements

The form built in this stage needs to be able to populate all objects in the data model (approximately represented by the [Mock API](../master/mocked-api))\*:

* Build user registration process
* Build data review/approval process – analogous to editorial flow. New data submissions aren't immediately published, but go into a holding area
* Build data entry process
  * Project information
    * Funding organisation (choose from list defined at `/organisations`)
    * Funding source (choose from list defined at `/funds`)
    * Outcome (choose from list defined at `/outcomes`)
    * Project contacts
      * Name
      * Email
      * etc.
    * Location (exact spec of location to be determined)
    * Title
    * Description
    * Delivery organisation (choose from list defined at `/organisations`)
  * Participant information (a single "row" per participant with the following information)
    * Gender
    * Age
    * Result. This *result* section forms the core of the performance data against which most reporting and analysis will be performed. Suggest a set of generic indicators to indicate how the person performed relative to the desired outcomes, e.g.:
      1. Did not meet
      2. Partially met
      3. Met
      4. Exceeded
      5. Significantly exceeded
    * Other socioeconomic indicators if required
* Build "my data portal"
  * Show existing submissions
  * Edit existing submissions
  * Edit contact details
  * Edit details for "my organisation"
* Further develop API endpoints to support other HTTP verbs, e.g. `POST`, `PUT`, `DELETE`
* Add authentication solution for POST, PUT and DELETE request (GET requests should always remain public). Easy solution here is WordPress cookies for in-domain apps, or OAuth2 if the apps will be hosted elsewhere (or we want to provide 'edit' API access to third-party apps)
* Update API documentation

\* The exceptions are the [Outcomes](../master/mocked-api/outcomes.json) and [Artforms](../master/mocked-api/artforms.json) objects. These objects exist in order to help group the projects, and so need to be centrally managed by the project adminstrator to ensure data normality.

## Technical solution

This phase should use the Phase 1 endpoints, but add additional HTTP verbs, e.g. `POST`, `PUT`, `DELETE` so that data can be added, edited, and deleted.

The forms and user portal should each be built as separate single-page apps using a JavaScript framework such as React or Angular. The apps should make requests to the REST API endpoints, rather than a POST to the individual page's URL (and hence processed by PHP). This approach has two advantages:

1. More responsive UI for the user – no waiting for full page loads
2. In the principles of open data, it forces our applications (e.g. the portal and the submission form) to act as any other application would and use the web-facing API. This has the added benefit of ensuring that the API is feature-complete and functional, rather than a "nice to have" bolt-on to comply with an open data aspiration

##Technical implementation – estimated person-days

Activity | Estimated days
--- | ---
Build Phase 1 | 20
Build registration | 3
Build review/approval process | 3
Build data entry forms | 15
Build portal | 10
Extend API | 3
**Total** | **54 days**

##Technical implmentation – estimated elapsed time

3-4 months, including build of *Phase 1*

##On-going effort

While there's less administrative overhead than Phase 1, some small amount of review/approval and querying will be needed for self-submitted data. We suggest 0.5 days per arts project added.

##Advantages

* Reduced reliance on a central administrator
* Greater engagement of arts organisations – they can manage their own data

##Disadvantages

* Increased cost
* Reporting and analysis still relies on technical know-how