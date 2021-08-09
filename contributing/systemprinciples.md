# System principles

The Open Technology Fund (OTF) commissioned Hypha with the aim that the platform would fulfil their core needs and provide a platform for other organisations to better administer their funds.

As such the application was built with the following core principles in mind and this should provide some reasoning as to why several decisions in the code were made, future development should keep these in mind as the system evolves.

# Security
Due to the nature of the work that OTF funds, the security and privacy of its applicants and fundees was of higher importance than normal. In order to ensure this security the following key concepts were implemented throughout the project:
* View logic should be separated by permission level as soon as is possible
  * Rely on the View to handle the major permission checks:
    * Can this person see the page?
    * What version of the page should the person see (e.g. applicant, review, staff)?
  * Template logic should avoid reuse and if statements for permission checks as much as possible
    * This will avoid accidental permission escalation
    * The additional work required to maintain the duplication was considered reasonable for the added security it provided
* Permission levels should allow specific behaviour on applications based on the user's group 
  * Avoid per application exceptions where possible
* Never trust the content of a user submission
  * Django provides excellent protection from attacks such as SQL injection. Developers should familiarise themselves with [Django's Security features](https://docs.djangoproject.com/en/3.0/topics/security/) to avoid adding vulnerabilities 
  * All data coming out of the database is cleaned on render
* Separate public content from user submitted content
  * Use of separate storage for private and public media to avoid access slip ups, private media requires authentication
  * Applications should not be made accessible through the Wagtail admin interface

# Generic solution
Many of the features that have been added to the app were created with OTF in mind, however the app was written so that the system isn't entirely bespoke to them and can be used by other funds. When features are evaluated they should consider the following aspects:
* What is the more general problem that needs to be solved? Does a more generic solution still fulfil the needs of OTF and provide useful features to other funding organisations?
* Can this feature be easily configured through the admin or environment variables to allow other organisations to use it?

# Extensible
The initial phases of the project focused on delivery a MVP solution that fulfilled the needs of OTF and allowed them to migrate from their legacy platform while new features continued to be added to the application. This meant that features should be easy to extend and new features should be easily integrated with the existing features. 

# Installable App
In order to facilitate the desire for other organisations to use the app, the long term intention of the project was to separate out the core aspects of the application into its own installable Django application. New funding organisations would then be able to create their own Django project where they could add the more custom implementations to the application, especially workflows.

## Public facing Site
In order to facilitate making the app installable, the "public", unauthenticated, site has the smallest integration with the "apply" site as possible. This was done to simplify the extraction of the main "apply" site from the "public" when the application was moved to a standalone installable application. The "apply" site could then expose an API to allow any public-like site to pull information on the open funds and display that.

Long term this would allow total decoupling of the public site which could be a heavily cached or static site reducing the attack surface of the application and preventing DDOS style attacks impacting on the apply site.
