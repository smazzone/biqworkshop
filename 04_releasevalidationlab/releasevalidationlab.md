BiQ - Release Validation Lab
============================

***[Estimated time required to complete this lab: 45 min]{.underline}***

**NOTE: If you have not created your lab application in Ravello, please
execute the following
[steps](https://singularity.jira.com/wiki/spaces/ADGS/pages/300647380/Create+a+new+Application+in+Ravello)**

1.  On Ravello, copy the DNS name address for the 4.4 Controller / Event
    Server.  Go to
    [http://](http://controller_ip:8090/)[CONTROLLER_DNS_NAME](http://CONTROLLER_IP:9191)[:8090](http://controller_ip:8090/)
    in a browser.  You can login to the Controller with the credentials
    appdadmin / d3m0@ppD. 

> Validate that you see active load for **AD-Travel**, **eCommerce**,
> and **fulfillment** applications (**It can take a few minutes for data
> to start flowing**)
> 
> ![](.//media/image1.jpeg)

2.  To show customers key relevant metrics which have been identified
    during the BiQ Workshop we are going to use a template dashboard.
    The Release Validation template dashboard has been already uploaded
    to your ravello instance. 
    We should somehow work backward to understand which type of widgets
    may be useful and also what type of Health Rules, ADQL Metrics, ADQL
    Queries, Data Collectors, Business Transactions (and/or BRUM pages,
    MRUM network requests) we should create in order to populate our
    dashboard.

3.  Each artifact described before may have dependencies over other
    artifacts.
    A quick description of the sequence may be:
    -Identify key Business Transactions, BRUM pages, MRUM network
    requests which will be used in the dashboard
    -Identify and define any required Data Collectors, Custom Events
    which will be used in the dashboard
    -Identify and define ADQL queries which may or may not produce
    additional metrics
    -Identify and define ADQL metrics which will be used in the
    dashboard
    -Identify and define Drag and Drop queries and widgets which will be
    used in the dashboard
    -Identify and create Health Rules which will be used in the
    dashboard

4.  For the lab we are not going to spend time on configuring Business
    Transaction nor Data Collectors, as this should be good and well
    established practice on the PS team. Data Collectors have already
    been configured in the lab, please take your time to familiarize
    with them if you want. Thus, in the lab we will spend more time on
    creating all the other artifacts required to build our Use Case
    dashboard.

5.  We are going to create all the required artifacts, such ADQL
    queries, metrics and Health Rules. Let us start with ADQL queries.

6.  In the Controller UI, go to Analytics > Searches and create the
    required ADQL queries to answer the following questions:
    
    NOTE: Customer uses canary release on node eCom2. We can then
    compare KPi between node eCom1 (release v1) and node eCom2 (release
    v2)
    
    -What is the number of Unique Visitors for release v1?
    
    SELECT distinctcount(segments.userData.SessionID) FROM transactions
    WHERE application = "eCommerce" and segments.node = "eCom1"
    
    -What is the number of Orders Placed for release v1?
    
    SELECT count(*) FROM transactions WHERE application = "eCommerce"
    AND transactionName = "CheckOut" AND userExperience != "ERROR"
    and segments.node = "eCom1"
    
    -What is the number of Check Out transactions for release v1?
    
    SELECT count(*) FROM transactions WHERE application = "eCommerce"
    AND transactionName = "CheckOut" AND segments.node = "eCom1"
    
    -What is the number of defective Check Out  transactions for release
    v1?
    
    SELECT count(*) FROM transactions WHERE application = "eCommerce"
    AND transactionName = "CheckOut" and userExperience = "ERROR"
    AND segments.node = "eCom1"
    
    -What is the average response time for Check Out transactions for
    release v1?
    
    SELECT avg(responseTime) FROM transactions WHERE application =
    "eCommerce" AND transactionName = "CheckOut" AND segments.node =
    "eCom1"
    
    **NOTE**: We could have created a single ADQL query to calculate
    both total transactions and defective Check Out transactions.
    Actually, the filter function allows us to do this: 
    
    SELECT count(*) AS "All Tx", filter(count(*), WHERE
    userExperience = "ERROR") FROM transactions WHERE application =
    "eCommerce" AND transactionName = "CheckOut" AND segments.node =
    "eCom1"
    
    But, we could not create metrics for both fields using "Create
    Metric" feature. If you try you will get an error message like
    this: "Only single-field queries are allowed as metrics."
    That is why we had to create two metrics in order to calculate the
    percentage of defective transactions. 

7.  Create remaining ADQL queries to answer the following questions:
    
    -What is the number of Unique Visitors for release v2?
    -What is the number of Orders Placed for release v2?
    -What is the number of Check Out transactions for release v2?
    -What is the number of defective Check Out  transactions for release
    v2?
    -What is the average response time for Check Out transactions for
    release v2?
    
    -What is the number of Home Page transactions for release v1?  
    -What is the average response time for Home Page transactions for
    release v1?
    -What is the number of defective Home Page transactions for release
    v1?
    
    -What is the number of Login transactions for release v1?  
    -What is the average response time for Login transactions for
    release v1?
    -What is the number of defective Login transactions for release v1?
    
    -What is the number of Add To Cart transactions for release v1?  
    -What is the average response time for Add To Cart transactions for
    release v1?
    -What is the number of defective Add To Cart transactions for
    release v1?
    
    -What is the number of Home Page transactions for release v2?  
    -What is the average response time for Home Page transactions for
    release v2?
    -What is the number of defective Home Page transactions for release
    v2?
    
    -What is the number of Login transactions for release v2?  
    -What is the average response time for Login transactions for
    release v2?
    -What is the number of defective Login transactions for release v2?
    
    -What is the number of Add To Cart transactions for release v2?  
    -What is the average response time for Add To Cart transactions for
    release v2?
    -What is the number of defective Add To Cart transactions for
    release v2?

8.  In the Controller UI, go to Analytics > Metrics and create the
    required metrics (you can use the ADQL queries created in the
    previous step): 
    
    -Number of Unique Visitors for release v1
    -Number of Orders Placed for release v1
    -Number of Check Out transactions for release v1
    -Number of defective Check Out transactions for release v1
    -Average response time for Check Out transactions for release v1
    
    -Number of Home Page transactions for release v1
    -Number of defective Home Page transactions for release v1
    -Average response time for Home Page transactions for release v1
    
    -Number of Login transactions for release v1
    -Number of defective Login transactions for release v1
    -Average response time for Login transactions for release v1
    
    -Number of Add To Cart transactions for release v1
    -Number of defective Add To Cart transactions for release v1
    -Average response time for Add To Cart transactions for release v1
    
    -Number of Unique Visitors for release v2
    -Number of Orders Placed for release v2
    -Number of Check Out transactions for release v2
    -Number of defective Check Out transactions for release v2
    -Average response time for Check Out transactions for release v2
    
    -Number of Home Page transactions for release v2
    -Number of defective Home Page transactions for release v2
    -Average response time for Home Page transactions for release v2
    
    -Number of Login transactions for release v2
    -Number of defective Login transactions for release v2
    -Average response time for Login transactions for release v2
    
    -Number of Add To Cart transactions for release v2
    -Number of defective Add To Cart transactions for release v2
    -Average response time for Add To Cart transactions for release v2

9.  In the Controller UI, go to Analytics > Alert & Respond > Health
    Rules and create the required Health Rules for the metrics defined
    in step 10:
    
    -eComm - Check Out Errors higher than expected - v1
    
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    ![](.//media/image2.jpeg)
    
    ![](.//media/image3.jpeg)
    
    -eComm - Check Out RT higher than expected - v1
    
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    ![](.//media/image4.jpeg)
    
    ![](.//media/image5.jpeg)
    
    -eComm - Home Page Errors higher than expected - v1
    
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    ![](.//media/image6.jpeg)
    
    ![](.//media/image7.jpeg)
    
    
    -eComm - Home Page RT higher than expected - v1
    
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    ![](.//media/image8.jpeg)
    
    ![](.//media/image9.jpeg)
    
    -eComm - Login Errors higher than expected - v1
    
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    ![](.//media/image10.jpeg)
    
    ![](.//media/image11.jpeg)
    
    
    -eComm - Login  RT higher than expected - v1
    
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    ![](.//media/image12.jpeg)
    
    ![](.//media/image13.jpeg)
    
    -eComm - Add To Cart Errors higher than expected - v1
    
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    ![](.//media/image14.jpeg)
    
    ![](.//media/image15.jpeg)
    
    -eComm - Add To Cart RT higher than expected - v1
    
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    ![](.//media/image16.jpeg)
    
    ![](.//media/image17.jpeg)

10. Create the remaining Health Rules for the metrics defined in step
    10:
    
    -eComm - Check Out Errors higher than expected - v2
    -eComm - Check Out RT higher than expected - v2
    -eComm - Home Page Errors higher than expected - v2
    -eComm - Home Page RT higher than expected - v2
    -eComm - Login Errors higher than expected - v2
    -eComm - Login  RT higher than expected - v2
    -eComm - Add To Cart Errors higher than expected - v2
    -eComm - Add To Cart RT higher than expected - v2

11. In the Controller UI, go to Dashboards & Reports and edit your
    Release Validation dashboard.
    
    On the top side of your dashboard, use the metric value widgets to
    show:
    
    -Active Sessions for v1
    
    ![](.//media/image18.jpeg)
    
    ![](.//media/image19.jpeg)
    
    -% Sales Conversion for v1
    
    NOTE: use metric expression ({# of Sales}/{# of Unique
    Visitors} * 100)
    
    ![](.//media/image20.jpeg)
    
    ![](.//media/image21.jpeg)
    
    ![](.//media/image22.jpeg)
    
    -# of Orders for v1
    
    ![](.//media/image23.jpeg)
    
    ![](.//media/image24.jpeg)

12. Complete the top side of your Release Validation dashboard, use the
    metric value widgets to show the remaining metrics:
    
    -Active Sessions for v2
    
    -% Sales Conversion for v2
    NOTE: use metric expression ({# of Sales}/{# of Unique
    Visitors} * 100)
    
    -# of Orders for v2

13. In the Controller UI, go to Dashboards & Reports and edit your
    Release Validation dashboard. We are going to add two Time
    series Graph widgets to show % Sales Conversion trend for release v1
    and v2
    
    ![](.//media/image25.jpeg)
    
    On the left time series graph widget use the metric
    expression: ({Sales}/{UniqueVisitors}*100)
    NOTE: Order Placed on release v1 divided by UniqueVisitors on
    release v1
    
    
    ![](.//media/image26.jpeg)
    
    ![](.//media/image27.jpeg)
    
    ![](.//media/image28.jpeg)
    
    On the right time series graph widget use the metric
    expression: ({Sales}/{UniqueVisitors}*100)
    NOTE: Order Placed on release v2 divided by UniqueVisitors on
    release v2

14. In the Controller UI, go to Dashboards & Reports and edit your
    Release Validation dashboard. We are going to add two funnel widgets
    to compare release v1 with v2.
    To add a new Funnel go to Add Widget > Analytics > Funnel Analysis
    and use a Funnel widget to answer the following questions:
    
    ![](.//media/image29.jpeg)
    
    
    -Given the following user journey Home Page > Login > Add To
    Cart > Check Out, what is the conversion rate for eCommerce Check
    Outs on release v1?
    
    ![](.//media/image30.jpeg)
    
    Use the following Funnel properties:
    
    Alignment: Center
    Show Health: checked 
    
    ![](.//media/image31.jpeg)
    
    Use the following Funnel definitions:

> Count Distinct of: SessionID
>
> Use the following criteria for the various steps: 
> 
> Step name: Home Page
> Application: eCommerce
> Business Transaction: HomePage
> Nodes: eCom1
> 
> Step name: Login
> Application: eCommerce
> Business Transaction:  Login
> Nodes: eCom1
> 
> Step name: Add To Cart
> Application: eCommerce
> Business Transaction:  AddToCart
> Nodes: eCom1
> 
> Step name: Check Out
> Application: eCommerce
> Business Transaction:  CheckOut
> Nodes: eCom1
>
> Save the funnel and position it on the bottom left of your dashboard:
> 
> ![](.//media/image32.jpeg)
> 
> -Given the following user journey Home Page > Login > Add To Cart >
> Check Out, what is the conversion rate for eCommerce Check Outs on
> release v2?
> 
> ![](.//media/image33.jpeg)
> 
> Use the following Funnel properties:
> 
> Alignment: Center
> Show Health: checked 
> 
> ![](.//media/image31.jpeg)
> 
> Use the following Funnel definitions:
>
> Count Distinct of: SessionID
>
> Use the following criteria for the various steps: 
> 
> Step name: Home Page
> Application: eCommerce
> Business Transaction: HomePage
> Nodes: eCom2
> 
> Step name: Login
> Application: eCommerce
> Business Transaction:  Login
> Nodes: eCom2
> 
> Step name: Add To Cart
> Application: eCommerce
> Business Transaction:  AddToCart
> Nodes: eCom2
> 
> Step name: Check Out
> Application: eCommerce
> Business Transaction:  CheckOut
> Nodes: eCom2
>
> Save the funnel and position it on the bottom right of your
> dashboard:
> 
> ![](.//media/image34.jpeg)

15. In the Controller UI, go to Dashboards & Reports and edit your
    Release Validation dashboard. Link the Health Status widget with the
    relative Health Rules  -Next to the left funnel widget, for each
    business transactions, use the health status widget to link with the
    respective average response time and the percentage of defective
    transactions Health Rules for release v1 (created in step 11):
    
    ![](.//media/image35.jpeg)
    
    -eComm - Add To Cart RT higher than expected - v1
    
    ![](.//media/image36.jpeg)
    
    ![](.//media/image37.jpeg)
    
    -eComm - Add To Cart Errors higher than expected - v1  
    
    ![](.//media/image38.jpeg)
    
    ![](.//media/image39.jpeg)

16. Complete the mapping for the following Health Status widgets to the
    respective Health Rules for release v1 (created in step 11):
    
    -eComm - Check Out RT higher than expected - v1
    -eComm - Check Out Errors higher than expected - v1  
    -eComm - Home Page RT higher than expected - v1
    -eComm - Home Page Errors higher than expected - v1  
    -eComm - Login RT higher than expected - v1
    -eComm - Login Errors higher than expected - v1  

17. Next to the right funnel widget, use the health status widget to
    link with the respective average response time and the percentage of
    defective transactions Health Rules for release v2 (created in step
    12):
    
    ![](.//media/image40.jpeg)
    
    
    -eComm - Add To Cart RT higher than expected - v2
    
    ![](.//media/image41.jpeg)
    
    ![](.//media/image42.jpeg)
    
    -eComm - Add To Cart Errors higher than expected - v2  
    
    ![](.//media/image43.jpeg)
    
    ![](.//media/image44.jpeg)

18. Complete the mapping for the following Health Status widgets to the
    respective Health Rules for release v2 (created in step 12):
    
    -eComm - Check Out RT higher than expected - v2
    -eComm - Check Out Errors higher than expected - v2
    -eComm - Home Page RT higher than expected - v2
    -eComm - Home Page Errors higher than expected - v2  
    -eComm - Login RT higher than expected - v2
    -eComm - Login Errors higher than expected - v2  

19. Align and change order of the widgets as required

20. This is how it should look our dashboard once completed
    
    ![](.//media/image45.png)
