BiQ - Business Health
=====================

-   [Verticals](#BiQ-BusinessHealth-Verticals)

-   [Description](#BiQ-BusinessHealth-Description)

-   [Personas](#BiQ-BusinessHealth-Personas)

-   [Typical questions the use case help
    address](#BiQ-BusinessHealth-Typicalquestionstheu)

-   [Vertical used as an
    example](#BiQ-BusinessHealth-Verticalusedasanexam)

-   [How to realize this use
    case](#BiQ-BusinessHealth-Howtorealizethisusec)

-   [Sample dashboards](#BiQ-BusinessHealth-Sampledashboards)

Verticals
---------

-   Retail

-   Travel

-   Financial Services

-   Media & Telco

-   Automotive

Description
-----------

This use case helps customer understand and act on real-time mission
critical and strategic business insights to improve outcomes, protect
and optimize revenues. 

Personas
--------

CIO / Business: Get alerts on real-time business metrics

IT Ops: Can correlate application and business performance for key
business transactions

Dev: Can measure impact on users as a result of poor or high performing
applications - have more time to write higher quality code as a result

Typical questions the use case help address
-------------------------------------------

How application performance is impacting our customers?

Is revenue healthy today?

Why revenue is dropping?

Vertical used as an example
---------------------------

An eCommerce company is transforming to incorporate digital services
involved with their portal (3rd party payment providers). This leads to
a change where payment providers become digital service companies.

**Problem:**
Currently neither ITOPS nor Business have the capacity to monitoring the
business health of the portal application in real time.
The application architecture is complicated and IT OPS need visibility
to be quickly alerted when there is potential impact on sales, revenues
and conversion. IT OPS wants to understand the **what** and the
**why**.
The portal application is connected to multiple third-party services
(such as Facebook, weather apps, payment providers, etc) and they need
to analyze the integrations of those libraries into their applications
to reduce costly war rooms.
Business need to identify revenues at risk.

**Solution:**
Using AppDynamics the company is monitoring the business health in real
time, for their eCommerce sites.
Business, IT OPS and DEV are alerted to the fact that there is a
potential issue with $ sales, # orders and % conversion. 
The company can drill in to see if loyalty customers (Platinum and Gold)
are having a much higher error % than guests (Silver). They can also see
that errors or performance issues are only impacting a certain type of
transactions (in our lab Add To Cart). 

How to realize this use case
----------------------------

**Bill of Materials:**

* Business Transactions, BRUM pages and MRUM network requests relevant to the use case have been identified and properly configured
* Customer has either in the code, in HTTP headers/parameters notion of end-user segments. It is then possible to extract that information to slice data per different segment.
* Data Collectors required to extract business indicators such as # of orders, # of unique users, $ sales amount, etc.
* ADQLs required to manipulate business data 
* Metrics created with the ADQLs, required to build the Custom Dashboard
* Health Rules required to build the Custom Dashboard
* Health Status widgets
* Pie Chart widgets

**Hands on Lab:**


[BiQ - Business Health
Lab](https://github.com/smazzone/biqworkshop/blob/master/03_bizhealthlab/bizhealthlab.md)

Sample dashboards  ![](.//media/image1.png)
------------------------------------------
