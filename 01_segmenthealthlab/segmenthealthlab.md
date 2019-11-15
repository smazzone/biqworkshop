BiQ - Segment Health Lab
========================

***[Estimated time required to complete this lab: 45 min]{.underline}***

**NOTE: If you have not created your lab application in Ravello, please
execute the following
[steps](file:////display/ADGS/Create+a+new+app+for+Controller%252C+AD-Travel%252C+eCommerce+and+fulfillment+in+Ravello)**

1.  On Ravello, copy the DNS name for the 4.4 Controller / Event
    Server.  Go to
    [http://](http://controller_ip:8090/)[CONTROLLER_DNS_NAME](http://CONTROLLER_IP:9191)[:8090](http://controller_ip:8090/)
    in a browser.  You can login to the Controller with the credentials
    \***

> Validate that you see active load for **AD-Travel**, **eCommerce**,
> and **fulfillment** applications (**It can take a few minutes for data
> to start flowing**)
> 
> ![](.//media/image1.jpeg)

2.  To show customers key relevant metrics which have been identified
    during the BiQ Workshop we are going to use a template
    dashboard. The Segment Health template dashboard has been already
    uploaded to your ravello instance. 
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
    
    -What is the number of transactions executed by end users that went
    through the system and had travel agency Kayak?
    
    ADQL query: SELECT count(*) FROM transactions WHERE application =
    "AD-Travel" AND segments.userData.TravelAgency = "Kayak"
    
    -What is the average response time for transactions executed by end
    users that went through the system and had travel agency Kayak?
    
    ADQL query: SELECT avg(responseTime) FROM transactions WHERE
    application = "AD-Travel" AND segments.userData.TravelAgency =
    "Kayak"
    
    -What is the number of defective transactions executed by end users
    that went through the system and had travel agency Kayak?
    
    ADQL query: SELECT count(*) FROM transactions WHERE application =
    "AD-Travel" AND segments.userData.TravelAgency = "Kayak" AND
    userExperience = "ERROR"
    
    **NOTE**: We could have created a single ADQL query to calculate
    both total transactions and defective transactions per travel
    agency.
    Actually, the filter function allows us to do this: 
    
    SELECT count(*) AS "All Tx", filter(count(*), WHERE
    userExperience = "ERROR") FROM transactions WHERE application =
    "AD-Travel" AND segments.userData.TravelAgency = "Kayak"
    
    But, we could not create metrics for both fields using "Create
    Metric" feature. If you try you will get an error message like
    this: "Only single-field queries are allowed as metrics."
    That is why we had to create two metrics in order to calculate the
    percentage of defective transactions. 

7.  Create remaining ADQL queries to answer the following questions:
    
    -What is the number of transactions executed by end users that went
    through the system and had travel agency Travelocity?
    -What is the average response time for transactions executed by end
    users that went through the system and had travel
    agency Travelocity?
    -What is the number of defective transactions executed by end users
    that went through the system and had travel agency Travelocity?
    
    -What is the number of transactions executed by end users that went
    through the system and had travel agency Priceline?
    -What is the average response time for transactions executed by end
    users that went through the system and had travel agency Priceline?
    -What is the number of defective transactions executed by end users
    that went through the system and had travel agency Priceline?
    
    -What is the number of transactions executed by end users that went
    through the system and had travel agency Expedia?
    -What is the average response time for transactions executed by end
    users that went through the system and had travel agency Expedia?
    -What is the number of defective transactions executed by end users
    that went through the system and had travel agency Expedia?
    
    -What is the number of transactions executed by end users that went
    through the system and had travel agency Orbitz?
    -What is the average response time for transactions executed by end
    users that went through the system and had travel agency Orbitz?
    -What is the number of defective transactions executed by end users
    that went through the system and had travel agency Orbitz?

8.  In the Controller UI, go to Analytics > Metrics and create the
    required metrics (you can use the ADQL queries created in the
    previous step): 
    
    -Completed transactions that had travel agency Kayak
    -Defective transactions that had travel agency Kayak
    -Average response time for transactions that had travel
    agency Kayak
    
    -Completed transactions that had travel agency Travelocity
    -Defective transactions that had travel agency Travelocity
    -Average response time for transactions that had travel
    agency Travelocity
    
    -Completed transactions that had travel agency Priceline
    -Defective transactions that had travel agency Priceline
    -Average response time for transactions that had travel
    agency Priceline
    
    -Completed transactions that had travel agency Expedia
    -Defective transactions that had travel agency Expedia
    -Average response time for transactions that had travel
    agency Expedia
    
    -Completed transactions that had travel agency Orbitz
    -Defective transactions that had travel agency Orbitz
    -Average response time for transactions that had travel
    agency Orbitz

9.  In the Controller UI, go to Analytics > Searches > Drag and Drop
    Search > Visualization and use a column chart (simple) widget to
    answer the following questions:
    (Use basic mode)
    
    -What are the top 10 error codes by travel agency?
    
    Use the following criteria: 
    
    TravelAgency: Kayak,Priceline,Orbitz,Expedia,Travelocity
    ApiErrorDescription: Malformed Request,Cache Out of Synch,Failure to
    Get Connection
    
    Use the following fields on X Axis: 
    
    TravelAgency (Top 10), ApiErrorDescription (Top 10)
    
    ![](.//media/image2.jpeg)

10. Add the widget to your Custom Dashboard
    
    ![](.//media/image3.jpeg)

11. Look at the resulting ADQL query in advanced mode:
    
    [NOTE: You will be able to see "Advanced" link only within your
    Custom Dashboard in Edit mode. (You should edit the
    widget)]{.underline}
    
    SELECT segments.userData.TravelAgency AS "TravelAgency",
    segments.userData.ApiErrorDescription AS "ApiErrorDescription",
    count(*) FROM transactions WHERE segments.userData.TravelAgency IN
    ("Kayak","Priceline","Orbitz","Expedia","Travelocity") AND
    segments.userData.ApiErrorDescription IN ("Malformed
    Request","Cache Out of Synch","Failure to Get Connection")
    LIMIT 10, 10

12. Take your time to explore what other simple chart types could be
    used here. 

13. Use column chart (simple) widgets to answer the remaining
    questions:
    
    -What are the top 10 slowest (including very slow) transactions by
    travel agency?
    
    Use the following criteria: 
    
    TravelAgency: Kayak,Priceline,Orbitz,Expedia,Travelocity
    User Experience: Slow, Very Slow
    HotelBrand: Marriott,Hyatt,Hilton Garden Inn,Four Seasons
    
    Use the following fields on X Axis: 
    
    TravelAgency (Top 10), Business Transaction (Top 10)
    
    ![](.//media/image4.jpeg)
    
    Add the widget to your Custom Dashboard
    
    -What are the top 10 most defective reservations by travel agency
    and hotel class?
    
    Use the following criteria: 
    
    TravelAgency: Kayak,Priceline,Orbitz,Expedia,Travelocity
    User Experience: Error
    
    Use the following fields on X Axis: 
    
    TravelAgency (Top 10), HotelClass (Top 10)
    
    
    ![](.//media/image5.jpeg)
    
    Add the widget to your Custom Dashboard
    
    -What are the top 10 slowest (including very slow) transactions by
    hotel brand?
    
    Use the following criteria: 
    
    TravelAgency: Kayak,Priceline,Orbitz,Expedia,Travelocity
    User Experience: Slow, Very Slow
    HotelBrand: Marriott,Hyatt,Hilton Garden Inn,Four Seasons
    
    Use the following fields on X Axis: 
    
    TravelAgency (Top 10), HotelBrand (Top 10)
    
    ![](.//media/image6.jpeg)
    
    Add the widget to your Custom Dashboard

14. In the Controller UI, go to Analytics > Alert & Respond > Health
    Rules and create the required Health Rules for the metrics created
    in step 10:
    
    -AD-Travel - Kayak Errors higher than expected
    
    Critical condition: ({TXwithErrors}/{TX}*100) > 40 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 20 (%)
    
    ![](.//media/image7.jpeg)
    
    ![](.//media/image8.jpeg)
    
    -AD-Travel - Kayak RT higher than expected
    
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    ![](.//media/image9.jpeg)
    
    ![](.//media/image10.jpeg)

15. Create the remaining Health Rules for the metrics created in step
    10:
    
    -AD-Travel - Travelocity Errors higher than expected
    Critical condition: ({TXwithErrors}/{TX}*100) > 40 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 20 (%)
    
    -AD-Travel - Travelocity RT higher than expected
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    -AD-Travel - Priceline Errors higher than expected
    Critical condition: ({TXwithErrors}/{TX}*100) > 40 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 20 (%)
    
    -AD-Travel - Priceline RT higher than expected
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    -AD-Travel - Expedia Errors higher than expected
    Critical condition: ({TXwithErrors}/{TX}*100) > 40 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 20 (%)
    
    -AD-Travel - Expedia RT higher than expected
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)
    
    -AD-Travel - Orbitz Errors higher than expected
    Critical condition: ({TXwithErrors}/{TX}*100) > 40 (%)
    Warning condition: ({TXwithErrors}/{TX}*100) > 20 (%)
    
    -AD-Travel - Orbitz RT higher than expected
    Critical condition: AVG RT > 2000 (ms)
    Warning condition: AVG RT > 1000 (ms)

16. In the Controller UI, go to Dashboards & Reports and edit your
    Segment Health dashboard:
    
    -For each travel agency use the metric value widget to show average
    response time and the percentage of defective transactions
    
    To show average response time in second we can use a metric
    expression (divide RT by 1000).
    
    ![](.//media/image11.jpeg)
    
    
    ![](.//media/image12.jpeg)
    
    ![](.//media/image13.jpeg)
    
    ![](.//media/image14.jpeg)
    
    To show percentage of errors we can use metric expression ({# of TX
    with ERRORS}/{# of TX}*100):
    
    ![](.//media/image15.jpeg)
    
    ![](.//media/image16.jpeg)
    
    ![](.//media/image17.jpeg)
    
    ![](.//media/image18.jpeg)

17. Link the Health Status widget with the relative Health Rules
    
    -For each travel agency use the health status widget to link with
    the respective average response time and the percentage of defective
    transactions Health Rules 
    
    ![](.//media/image19.jpeg)
    
    ![](.//media/image20.jpeg)
    
    ![](.//media/image21.jpeg)
    
    ![](.//media/image22.jpeg)
    
    ![](.//media/image23.jpeg)
     

18. Complete the design of the dashboard:
    -For each travel agency use the two Health Status widgets to show
    the status of the respective Health Rules (created in step 15)
    -Use column widget (simple) to show the top 10 error codes by travel
    agency
    -Use column widget (simple) to show the top 10 slowest
    (including very slow) transactions by travel agency
    -Use column widget (simple) to show the top 10 most defective
    reservations by travel agency and hotel class
    -Use column widget (simple) to show the top 10 slowest
    (including very slow) transactions by hotel brand

19. Align and change order of the widgets as required

20. This is how it should look our dashboard once completed
    
    ![](.//media/image24.png)
