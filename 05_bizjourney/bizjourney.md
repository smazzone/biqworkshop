BiQ - Business Journeys
=======================

-   [Verticals](#BiQ-BusinessJourneys-Verticals)

-   [Personas](#BiQ-BusinessJourneys-Personas)

-   [Typical questions the use case help
    address](#BiQ-BusinessJourneys-Typicalquestionsth)

-   [Verticals used as an
    example](#BiQ-BusinessJourneys-Verticalsusedasane)

    -   [Scenario 1 - Retail](#BiQ-BusinessJourneys-Scenario1-Retail)

    -   [Sample dashboard](#BiQ-BusinessJourneys-Sampledashboard)

    -   [Scenario 2 - Financial
        Services:](#BiQ-BusinessJourneys-Scenario2-Financia)

-   [How to realize this use
    case](#BiQ-BusinessJourneys-Howtorealizethisus)

Verticals
---------

-   Retail

-   Travel

-   Financial Services

-   Media & Telco

-   Automotive

Description

This use case helps customer analyze and measure how application
performance impacts complex business processes that span multiple
business events. 

Business Journeys (aka Business Outcomes) are a way to monitor and
correlate the data flow across multiple event sources and track the
total end-to-end time for defined business workflows
Typical multi-step workflows from different industries include:

-   Order and fulfillment process, from checkout to item shipped

-   Payment transfers, credit card approval, and loan approval in
    financial services industries

-   Cellphone Activation and data recharge (pre-paid) in the Telco
    sector

-   Insurance application through policy approval and insurance claims
    approval for insurance companies

NOTE: a workflow can span across multiple applications and event type.

Personas
--------

CIO / Business: Have access to end-to-end metrics on specific business
processes.

IT Ops: Can use critical metrics to inform Business and Dev partners
with conversion Analysis. Can visualize and understand the drop-off rate
at each milestones.

Dev: Understand how his/her service is impacting larger business
processes, can optimize impact

Typical questions the use case help address
-------------------------------------------

How is each milestones impacting the overall business process?

How do we know if app performance on each milestone is impacting
conversions / dropoff ?

Conversions are down.  What is the risk?

If we optimize this overall business process, how many customers could
we serve?

Verticals used as an example
----------------------------

### **Scenario 1 - Retail**

For a retail company heavily relying on its eCommerce website the
fulfillment process typically spans different event types, services, and
applications. This process is an important workflow where "Items
Purchased" information could come from the eCommerce website business
transaction, whereas, "Order Received" status could come from a
Fulfillment application and potentially from logs. "Order Prepared" and
"Order Shipped", on the other hand, may be performed by the Fulfillment
application or potentially a third-party application, and their status
could be updated by a third party provider either in transactions or
logs. 

**Problem:**
Application teams need to find a way to identify performance latency
within the entire business process for both individual applications and
operational gaps. In addition to that, there is tremendous complexity in
monitoring these individual milestones and performing analytics on the
aggregated business workflow. This is mainly because there are different
sources of truth as well as the overall process could last for several
minutes, hours and sometimes days.

**Solution:**
AppDynamics Business Journeys enables the Application teams to link
together those multiple milestones as a business journey. This provides
visibility of the performance of the entire approval process. In
addition to that, the Application team can easily assess performances of
each individual milestone throughout the overall process. Apart from the
default information collected by Business Journeys, such as total time
taken, event time stamp, etc., the Application teams can also extract
additional business information (such as customer details, product name,
product price, etc.) from the various milestones.

**Hands on Lab:**

[BiQ - Business Journey Lab](file:../05_bizjourneylab/bizjourneylab.md)

### Sample dashboard

![](.//media/image1.jpeg)

### **Scenario 2 - Financial Services:**

For an insurance company a loan application approval process typically
spans different event types, services, and applications. This approval
process is an important workflow where "Application Submission"
information could come from business transaction events, whereas,
"Document Verification" status could come from logs. "Credit Approval"
and "Underwriting", on the other hand, are performed by third-party
service providers, and the status could be updated in logs as well.
"Final Approval" status could then be updated in transaction events.

**Problem:**
Application teams need to find a way to identify performance latency
within the entire business process for both individual applications and
operational gaps. In addition to that, there is tremendous complexity in
monitoring these individual milestones and performing analytics on the
aggregated business workflow. This is mainly because there are different
sources of truth as well as the overall process could last for several
minutes, hours and sometimes days.

**Solution:**
AppDynamics Business Journeys enables the Application teams to link
together those multiple milestones as a business journey. This provides
visibility of the performance of the entire approval process. In
addition to that, the Application team can easily assess performances of
each individual milestone throughout the overall process. Apart from the
default information collected by Business Journeys, such as total time
taken, event time stamp, etc., the Application teams can also extract
additional business information (such as customer details, loan amount,
loan type, etc.) from the various milestones.

How to realize this use case
----------------------------

**Bill of Materials:**


* Business Transactions, BRUM pages and MRUM network requests relevant
to the use case have been identified and properly configured
* Log analytics (optional)
* Assess if the process that Customer wants to measure is a good fit for
a funnel. (*)
* Data Collectors required to extract information relevant to identify
the different milestones
* Business Outcomes definition (this is a one-time activity. where we
define the data for key milestones)
* ADQLs required to manipulate business data 
* Metrics created with the ADQLs, required to build the Custom Dashboard
* Health Rules required to build the Custom Dashboard
* Health Status widgets
* Funnel widget

(*)
Funnel is a set of occurrences or transactions that happen that are all
sequential i.e. Application Submission > Data Verification > Credit
Check > Underwriting > Final Approval
All steps are in order and the next steps is always going to be a subset
of the previous set or at least an equal number to the previous set 
NOTE: It is not a funnel if someone can start at step 1 and choose
different paths to go to the next step. Basically, it needs to follow
always the same path.
NOTE: You need a count distinct field - This is a unique value that goes
through the funnel, a value which is present and unique across each step
(i.e. SessionId, LoanId, etc)
NOTE: A unique value is not an identifier of unique transaction.
Because, the next step in the funnel may not have the same identifier.  


