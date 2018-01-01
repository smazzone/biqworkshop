BiQ - Segment Health
====================

-   [Verticals](#BiQ-SegmentHealth-Verticals)

-   [Description](#BiQ-SegmentHealth-Description)

-   [Personas](#BiQ-SegmentHealth-Personas)

-   [Typical questions the use case help
    address](#BiQ-SegmentHealth-Typicalquestionstheus)

-   [Vertical used as an
    example](#BiQ-SegmentHealth-Verticalusedasanexamp)

-   [How to realize this use
    case](#BiQ-SegmentHealth-Howtorealizethisuseca)

-   [Sample dashboards](#BiQ-SegmentHealth-Sampledashboards)

Verticals
---------

-   Retail

-   Travel

-   Financial Services

-   Media & Telco

-   Automotive

Description
-----------

This use case helps customer understand end-to-end experience of
critical customer segments. With this use case customer can monitor,
control and prioritize segmented customer experiences to improve SLA,
service adoption, and other performance KPIs.

Personas
--------

VP of XYZ Services / Business:  Can manage the health of key customer
segments.

IT Ops: Can identify performance impact on high value segments, for
faster troubleshooting and resolution

Dev:  Have segmented experience insights which helps inform better
application logic (code diagnostics enables faster code fix / debug)

Typical questions the use case help address
-------------------------------------------

How can we move beyond SLAs and control performance to drive business?

How can we understand the experience of our most important customer
segments and partners?

How can we control experiences that drive business?

Vertical used as an example
---------------------------

A travel platform company manages applications in its portal that are
used to purchase travels products by end users. The company relies on
3rd party providers such as Kayak, Travelocity, Expedia, etc. 

**Problem:**
The end users (travelers) were complaining of slow performance.
Furthermore, users complaining who perceived poor performance, were the
largest revenue generators for the company.
The company is unable to understand how 3rd party providers slow
performances are impacting end users.

**Solution:**
Using AppDynamics, the company was able to extract response times
segmented by providers.
The company was able to identify and prove a correlation of slow
performance and errors with specific 3rd party providers.
The company was also able to create health rules around 3rd party
providers, and escalate issues with high priority on each respective
providers.

How to realize this use case
----------------------------

**Bill of Materials:**

* Business Transactions, BRUM pages and MRUM network requests relevant to
the use case have been identified and properly configured
* Customer has either in the code, in HTTP headers/parameters notion of
end-user segments (travel agency, customer type, product type, etc). It
is then possible to extract that information to slice data per different
segment.
* Data Collectors required to extract segment information
* ADQLs required to manipulate data by segment
* Metrics created with the ADQLs, required to build the Custom Dashboard
* Health Rules required to build the Custom Dashboard
* Health Status widgets
* Simple Column chart widgets

**Hands on Lab:**


[BiQ - Segment Health
Lab](file:../01_segmenthealthlab/segmenthealthlab.md)

Sample dashboards
-----------------

![](.//media/image1.png)
