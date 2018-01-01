BiQ - Release Validation
========================

-   [Verticals](#BiQ-ReleaseValidation-Verticals)

-   [Description](#BiQ-ReleaseValidation-Description)

-   [Personas](#BiQ-ReleaseValidation-Personas)

-   [Typical questions the use case help
    address](#BiQ-ReleaseValidation-Typicalquestionst)

-   [Vertical used as an
    example](#BiQ-ReleaseValidation-Verticalusedasane)

-   [How to realize this use
    case](#BiQ-ReleaseValidation-Howtorealizethisu)

-   [Sample dashboards](#BiQ-ReleaseValidation-Sampledashboards)

Verticals
---------

-   Retail

-   Travel

-   Financial Services

-   Media & Telco

-   Automotive

Description
-----------

This use case helps customer compare, interrogate, and validate
production code releases based on application, customer experience, and
business KPIs 

Personas
--------

Business: Can compare and validate that application releases are driving
the intended business results

IT Ops: Get real time validation of the impact of application
optimization

Dev: Can quantify the impact of feature improvements and bug fixes. 

Typical questions the use case help address
-------------------------------------------

How does our code impact the business?

Did updates actually fix or optimize performance?

Is our conversion and retention the same with the new release?

Are updates to the application driving the right outcomes?

Vertical used as an example
---------------------------

An online e-Commerce retail company with presence in Asia, Europe and
USA is migrating their website to AWS. They have been experiencing lower
conversion rate than expected as number of end users dropped their
transactions due to slow performances.
Because of that, a second key initiative is happening: DevOps team has
been asked to release a new version of the e-Commerce website. The team
is on-track and plan to use canary deployment. (The use case also
applies to blue-green deployment). They will deploy the new release side
by side with the old version. But, they lack visibility and cannot
compare easily the result of their deployment. Basically, DevOps team
would like to understand if the new release would optimize performances
and also the impact of the new code on the business. DevOps team has
also been asked to provide evidence that the new release would drive the
intended business results.

**Problem:**
The company DevOps team lack visibility and cannot easily compare two
application releases. They cannot easily understand if the new release
would optimize performances and more importantly would drive the
intended business results.  

**Solution:**
With AppDynamics they can configure transaction analytics and create
dashboards to report on their key business metrics. They can
differentiate metrics by application release.
They can create two funnel conversions for their eCommerce website,
using key business metrics side by side for old and new release.

How to realize this use case
----------------------------

**Bill of Materials:**

-Business Transactions, BRUM pages and MRUM network requests relevant to
the use case have been identified and properly configured**
**-Assess if the process that Customer wants to measure is a good fit
for a funnel. (*)
-Data Collectors required to extract the notion of application release
information (or an alternative way to differentiate application
releases) 
-ADQLs required to manipulate business data 
-Metrics created with the ADQLs, required to build the Custom Dashboard
-Health Rules required to build the Custom Dashboard
-Health Status widgets
-2 x Funnel widget

(*)
Funnel is a set of occurrences or transactions that happen that are all
sequential i.e. Home Page > Login > Search Product > Product Detail
Page > Checkout
All steps are in order and the next steps is always going to be a subset
of the previous set or at least an equal number to the previous set 
NOTE: It is not a funnel if someone can start at step1 and choose
different paths to go to the next step. Basically, it needs to follow
always the same path.
NOTE: You need a count distinct field - This is a unique value that goes
through the funnel, a value which is present and unique across each step
(i.e. SessionId, LoadId, etc)
NOTE: A unique value is not an identifier of unique transaction.
Because, the next step in the funnel may not have the same identifier.
Usually, SessionId is a good candidate.  

**Hands on Lab:**

[BiQ - Release Validation
Lab](file:../04_releasevalidationlab/releasevalidationlab.md)

Sample dashboards  ![](.//media/image1.png)
------------------------------------------
