BiQ - User Journeys Lab
=======================

***[Estimated time required to complete this lab: 45 min]***

***NOTE: If you have not created your lab application in Ravello, please
execute the following
[steps](file:////display/ADGS/Create+a+new+app+for+Controller%252C+AD-Travel%252C+eCommerce+and+fulfillment+in+Ravello)***

1.  *On Ravello, copy the DNS name for the 4.4 Controller / Event
    Server.  Go to
    [http://](http://controller_ip:8090/)[CONTROLLER_DNS_NAME](http://CONTROLLER_IP:9191)[:8090](http://controller_ip:8090/)
    in a browser.  You can login to the Controller with the credentials
    appdadmin/d3m0@ppD*

> *Validate that you see active load for **AD-Travel**, **eCommerce**,
> and **fulfillment** applications (**It can take a few minutes for data
> to start flowing**)
> 
> *![](.//media/image1.jpeg)

2.  *To show customers key relevant metrics which have been identified
    during the BiQ Workshop we are going to use a template dashboard.
    The User Journeys template dashboard has been already uploaded to
    your ravello instance. 
    We should somehow work backward to understand which type of widgets
    may be useful and also what type of Health Rules, ADQL Metrics, ADQL
    Queries, Data Collectors, Business Transactions (and/or BRUM pages,
    MRUM network requests) we should create in order to populate our
    dashboard.*

3.  *Each artifact described before may have dependencies over other
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
    dashboard*

4.  *For the lab we are not going to spend time on configuring Business
    Transaction nor Data Collectors, as this should be good and well
    established practice on the PS team. Data Collectors have already
    been configured in the lab, please take your time to familiarize
    with them if you want. Thus, in the lab we will spend more time on
    creating all the other artifacts required to build our Use Case
    dashboard.*

5.  *We are going to create all the required artifacts, such ADQL
    queries, metrics and Health Rules. Let us start with ADQL queries.*

6.  *In the Controller UI, go to Analytics > Searches and create the
    required ADQL queries to answer the following questions:
    
    -What is the total Check Out processed? (PS: we want to consider TX
    with normal, slow and very slow user experience)
    
    SELECT sum(segments.userData.ProductPrice) FROM transactions WHERE
    application = "eCommerce" AND transactionName = "CheckOut" AND
    userExperience IN ("NORMAL","SLOW","VERY_SLOW")
    
    -What is the number of Check Out transactions?
    
    SELECT count(*) FROM transactions WHERE application = "eCommerce"
    AND transactionName = "CheckOut"
    
    -What is the number of defective Check Out  transactions?
    
    SELECT count(*) FROM transactions WHERE application = "eCommerce"
    AND transactionName = "CheckOut" and userExperience = "ERROR"
    
    -What is the average response time for Check Out transactions?
    
    SELECT avg(responseTime) FROM transactions WHERE application =
    "eCommerce" AND transactionName = "CheckOut"
    
    **NOTE**: We could have created a single ADQL query to calculate
    both total transactions and defective Check Out transactions.
    Actually, the filter function allows us to do this: 
    
    SELECT count(*) AS "All Tx", filter(count(*), WHERE
    userExperience = "ERROR") FROM transactions WHERE application =
    "eCommerce" AND transactionName = "CheckOut"
    
    But, we could not create metrics for both fields using "Create
    Metric" feature. If you try you will get an error message like
    this: "Only single-field queries are allowed as metrics."
    That is why we had to create two metrics in order to calculate the
    percentage of defective transactions. *

7.  *Create remaining ADQL queries to answer the following questions:
    
    -What is the number of Home Page transactions?  
    -What is the average response time for Home Page transactions?
    -What is the number of defective Home Page transactions?
    
    -What is the number of Login transactions?  
    -What is the average response time for Login transactions?
    -What is the number of defective Login transactions?
    
    -What is the number of Add To Cart transactions?  
    -What is the average response time for Add To Cart transactions?
    -What is the number of defective Add To Cart transactions?*

8.  *In the Controller UI, go to Analytics > Metrics and create the
    required metrics (you can use the ADQL queries created in the
    previous step): 
    
    -Number of Check Out transactions
    -Number of defective Check Out transactions 
    -Average response time for Check Out transactions 
    -Total Check Out processed in $
    
    -Number of Home Page transactions 
    -Number of defective Home Page transactions 
    -Average response time for Home Page transactions 
    
    -Number of Login transactions 
    -Number of defective Login transactions 
    -Average response time for Login transactions
    
    -Number of Add To Cart transactions 
    -Number of defective Add To Cart transactions 
    -Average response time for Add To Cart transactions *

9.  *In the Controller UI, go to Analytics > Alert & Respond > Health
    Rules and create the required Health Rules for the metrics defined
    in step 10:
    
    -eComm - Check Out Errors higher than expected
    
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    
    *![](.//media/image2.jpeg)*
    
    *![](.//media/image3.jpeg)*
    
    
    -eComm - Check Out RT higher than expected
    
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    *![](.//media/image4.jpeg)*
    
    
    *![](.//media/image5.jpeg)*
    
    -eComm - Check Out Processed lower than expected
    
    Critical condition: Check Out Processed < 100 ($)
    Warning condition: Check Out Processed < 200 ($)
    
    *![](.//media/image6.jpeg)*
    
    *![](.//media/image7.jpeg)*
    
    *

10. *Create the remaining Health Rules for the metrics created in step
    10:
    
    -eComm - Home Page Errors higher than expected
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    -eComm - Home Page RT higher than expected
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    -eComm - Login Errors higher than expected
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    -eComm - Login  RT higher than expected
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    -eComm - Add To Cart Errors higher than expected
    Critical condition: ({TXwithErrors}/{TX}*100) > 30 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 10 (%)
    
    -eComm - Add To Cart RT higher than expected
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)*

11. *In the Controller UI, go to Dashboards & Reports and edit your User
    Journeys dashboard. To add a new Funnel go to Add Widget >
    Analytics > Funnel Analysis and use a Funnel widget to answer the
    following questions:
    
    *![](.//media/image8.jpeg)*
    
    -Given the following user journey Home Page > Login > Add To
    Cart > Check Out, what is the conversion rate for eCommerce Check
    Outs?
    
    *![](.//media/image9.jpeg)*
    
    Use the following Funnel properties:
    
    Alignment: Center
    Show Health: checked 
    
    *![](.//media/image10.jpeg)*
    
    Use the following Funnel definitions:*

> Count Distinct of: SessionID
>
> Use the following criteria for the various steps: 
> 
> Step name: Home Page
> Application: eCommerce
> Business Transaction: HomePage
> 
> Step name: Login
> Application: eCommerce
> Business Transaction:  Login
> 
> Step name: Add To Cart
> Application: eCommerce
> Business Transaction:  AddToCart
> 
> Step name: Check Out
> Application: eCommerce
> Business Transaction:  CheckOut
> 
> Save the funnel and position it in the middle of your dashboard:
> 
> ![](.//media/image11.jpeg)

12. *In the Controller UI, go to Dashboards & Reports and edit your User
    Journeys dashboard:
    
    -On the top left side of your dashboard, use the metric value widget
    to show the Total Check Out processed in $
    
    *![](.//media/image12.jpeg)*
    
    *![](.//media/image13.jpeg)*
    
    *![](.//media/image14.jpeg)*
    
    -On the associated health status widget link the Health Rules
    created on step 11 (Check Out Processed lower than expected)
    
    *![](.//media/image15.jpeg)*
    
    *![](.//media/image16.jpeg)*
     *

13. *In the Controller UI, go to Dashboards & Reports and edit your User
    Journey dashboard:
    
    -On the top right side of your dashboard, use a time series graph
    chart widget to show the trend over time of Check Out Processed
    (include the baseline).
    
    *![](.//media/image17.jpeg)*
    
    *![](.//media/image18.jpeg)*
    
    *![](.//media/image19.jpeg)*
    
    *![](.//media/image20.jpeg)

14. *In the Controller UI, go to Dashboards & Reports and edit your User
    Journey dashboard:
    
    -On the right side of your dashboard, for each business transactions
    use the metric value widget to show average response time and the
    percentage of defective transactions
    
    To show average response time in second we can use a metric
    expression (divide RT by 1000).
    
    *![](.//media/image21.jpeg)*
    
    *![](.//media/image22.jpeg)*
    
    *![](.//media/image23.jpeg)*
    
    *![](.//media/image24.jpeg)*
    
    To show percentage of errors we can use metric expression ({# of TX
    with ERRORS}/{# of TX}*100):
    
    *![](.//media/image25.jpeg)*
    
    *![](.//media/image26.jpeg)*
    
    *![](.//media/image27.jpeg)*
    
    *![](.//media/image28.jpeg)

15. *Link the Health Status widget with the relative Health Rules
    
    -On the right side of your dashboard, for each business transactions
    use the health status widget to link with the respective average
    response time and the percentage of defective transactions Health
    Rules 
    
    *![](.//media/image29.jpeg)*
    
    *![](.//media/image30.jpeg)*
    
    *![](.//media/image31.jpeg)*
    
    *![](.//media/image32.jpeg)*
    
    *![](.//media/image33.jpeg)*
    
    *![](.//media/image34.jpeg)*
    
    -On the left side of your dashboard, for each business transactions
    use the health status widget to link with the respective average
    response time and the percentage of defective transactions Health
    Rules
    NOTE: use Ratio Graph as aggregation type. We want the health status
    widget to take into account both average response time and
    percentage of defective transactions 
    
    *![](.//media/image35.jpeg)*
    
    *![](.//media/image36.jpeg)*
    
    *![](.//media/image37.jpeg)

16. *Complete the design of the dashboard:
    -On the left side of the dashboard, for each BT use the Health
    Status widget to link with the respective average response time and
    the percentage of defective transactions Health Rules
    
    *![](.//media/image35.jpeg)*
    
    NOTE: use Ratio Graph as aggregation type. We want the health status
    widget to evaluate both average response time and percentage of
    defective transactions 
    
    *![](.//media/image38.jpeg)*
    
    *![](.//media/image39.jpeg)*
    
    NOTE: on Check Out BT make sure to evaluate three Health Rules:
    average response time, defective transactions and check outs
    processed
    
    *![](.//media/image40.jpeg)*
    
    -On the right side of the dashboard, for each BT use the two Health
    Status widgets to show the status of the respective Health Rules
    (created in step 12)
    
    *![](.//media/image32.jpeg)*
    
    -eComm - Home Page Errors higher than expected
    -eComm - Home Page RT higher than expected
    -eComm - Login Errors higher than expected
    -eComm - Login  RT higher than expected
    -eComm - Add To Cart Errors higher than expected
    -eComm - Add To Cart RT higher than expected*

17. *Align and change order of the widgets as required*

18. *This is how it should look our dashboard once completed
    
    *![](.//media/image41.png)
