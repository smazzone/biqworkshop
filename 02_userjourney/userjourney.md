BiQ - User Journeys
===================

-   [Verticals](#BiQ-UserJourneys-Verticals)

-   [Personas](#BiQ-UserJourneys-Personas)

-   [Typical questions the use case help
    address](#BiQ-UserJourneys-Typicalquestionstheuse)

-   [Vertical used as an
    example](#BiQ-UserJourneys-Verticalusedasanexampl)

-   [How to realize this use
    case](#BiQ-UserJourneys-Howtorealizethisusecas)

-   [Sample dashboards](#BiQ-UserJourneys-Sampledashboards)

Verticals
---------

-   Retail

-   Travel

-   Financial Services

-   Media & Telco

-   Automotive

Description

This use case helps customer understand performance metrics and business
impact of a sequential order of customer events. 

Personas
--------

CIO / Business: Have access to end-to-end metrics on specific business
events correlated with a customer journey.

IT Ops: Can use critical metrics to inform Business and Dev partners
with conversion Analysis. Can visualize and understand the drop-off rate
at each step.

Dev: Understand how his/her service is impacting larger business
processes, can optimize impact

Typical questions the use case help address
-------------------------------------------

How is each transaction impacting the business?

How do we know if app performance is impacting conversions / dropoff ?

Conversions are down.  What is the risk?

If we optimize this journey, how many customers could we serve?

Vertical used as an example
---------------------------

For an online e-Commerce retail company, moments are key events in a
customer's lifecycle (such as a Black Friday, Cyber Monday, Back to
School, etc) which enables the company to engage the customer in a
deeper relationship while also maximizing the attach rate of products
relevant to that key moment.

**Problem:**
The company currently has 2 seasonal moments and they would like to have
greater insight into the specifics of a moment, such as when a customer
buys a product. In addition to that the company cannot easily understand
if conversions are down and what is the cause, nor can the company
understand and optimize the experience of the end-user throughout the
entire journey. 

**Solution:**
With AppDynamics, the company can track moment engagement to see how it
flows through other channels for conversion at a customer level.
This allows the company to prove value, enable the return on investment
on different moments and understand the depth of customer engagement.
The company can understand and easily optimize user journeys to remove
any friction and enable better management of call center resources to
reduce complaints.

How to realize this use case
----------------------------

**Bill of Materials:**

* Business Transactions, BRUM pages and MRUM network requests relevant
to the use case have been identified and properly configured
* Assess if the process that Customer wants to measure is a good fit
for a funnel. (*)
* Data Collectors required to extract business data information
* ADQLs required to manipulate business data 
* Metrics created with the ADQLs, required to build the Custom Dashboard
* Health Rules required to build the Custom Dashboard
* Health Status widgets
* Funnel widget

(*)
Funnel is a set of occurrences or transactions that happen that are all
sequential i.e. Home Page > Login > Search Product > Product Detail
Page > Checkout
All steps are in order and the next steps is always going to be a subset
of the previous set or at least an equal number to the previous set 
NOTE: It is not a funnel if someone can start at step 1 and choose
different paths to go to the next step. Basically, it needs to follow
always the same path.
NOTE: You need a count distinct field - This is a unique value that goes
through the funnel, a value which is present and unique across each step
(i.e. SessionId, LoadId, etc)
NOTE: A unique value is not an identifier of unique transaction.
Because, the next step in the funnel may not have the same identifier.
Usually, SessionId is a good candidate.  

**Hands on Lab:**


[BiQ - User Journeys Lab](file:../02_userjourneylab/userjourneylab.md)

Sample dashboards
-----------------

![](.//media/image1.png)
