BiQ - Business Health Lab
=========================

***[Estimated time required to complete this lab: 45 min]{.underline}***

**NOTE: If you have not created your lab application in Ravello, please
execute the following
[steps](file:////display/ADGS/Create+a+new+app+for+Controller%252C+AD-Travel%252C+eCommerce+and+fulfillment+in+Ravello)**

1.  On Ravello, copy the DNS name for the 4.4 Controller / Event
    Server.  Go to
    [http://](http://controller_ip:8090/)[CONTROLLER_DNS_NAME](http://CONTROLLER_IP:9191)[:8090](http://controller_ip:8090/)
    in a browser.  You can login to the Controller with the credentials
    appdadmin/d3m0@ppD

> Validate that you see active load for **AD-Travel**, **eCommerce**,
> and **fulfillment** applications (**It can take a few minutes for data
> to start flowing**)
> 
> ![](.//media/image1.jpeg)

2.  To show customers key relevant metrics which have been identified
    during the BiQ Workshop we are going to use a template dashboard.
    The Business Health template dashboard has been already uploaded to
    your ravello instance. 
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
    
    -What is the number of Unique Visitors?
    
    SELECT distinctcount(segments.userData.SessionID) FROM transactions
    WHERE application = "eCommerce"
    
    -What is the number successful Orders Placed? (PS: we want to
    consider TX with normal, slow and very slow user experience)
    
    SELECT count(*) FROM transactions WHERE application = "eCommerce"
    AND transactionName = "CheckOut" AND userExperience != "ERROR"
    
    -What is the total amount of Revenues at risk? (PS: we want to
    consider defective TXs. Basically, those TXs with userExperience =
    "ERROR")
    
    SELECT sum(segments.userData.ProductPrice) FROM transactions WHERE
    application = "eCommerce" AND transactionName = "CheckOut" AND
    userExperience = "ERROR"
    
    -What is the total amount of Sales processed? (PS: we want to
    consider TX with normal, slow and very slow user experience)
    NOTE: we may have already this metric as it was collected during
    other labs
    
    SELECT sum(segments.userData.ProductPrice) FROM transactions WHERE
    application = "eCommerce" AND transactionName = "CheckOut" AND
    userExperience != "ERROR"

7.  In the Controller UI, go to Analytics > Metrics and create the
    required metrics (you can use the ADQL queries created in the
    previous step): 
    
    -# of Orders Placed
    -# of Unique Visitors
    -Check Out Total Processed (we may have already this metric as it
    was collected during other labs)
    -Check Out Total Revenues at Risk

8.  In the Controller UI, go to Analytics > Searches > Drag and Drop
    Search > Visualization and use a column chart (simple) widget to
    answer the following questions:
    (Use basic mode. But, please take time to look at the resulting ADQL
    query in the advance mode)
    
    -What is the user experience (Normal, Slow, Very Slow, Error) for
    top 10 customer types?
    
    Use the following criteria: 
    
    Application: e-Commerce
    
    Use the following fields on X Axis: 
    
    CustomerType (Top 10), User Experience (Top 10)
    
    ![](.//media/image2.jpeg)
    
    Look at the resulting ADQL query in advanced mode:
    
    [NOTE: You will be able to see "Advanced" link only within your
    Custom Dashboard in Edit mode. (You should edit the
    widget)]{.underline}
    
    SELECT segments.userData.CustomerType AS "CustomerType",
    userExperience AS "User Experience", count(*) FROM transactions
    WHERE application = "eCommerce" LIMIT 10, 10
    
    -What is the user experience (Normal, Slow, Very Slow, Error) for
    top 10 business transactions?
    
    Use the following criteria: 
    
    Application: e-Commerce
    
    Use the following fields on X Axis: 
    
    Business Tranaction (Top 10), User Experience (Top 10)
    
    ![](.//media/image3.jpeg)
    
    Look at the resulting ADQL query in advanced mode:
    
    SELECT transactionName AS "Business Transaction", userExperience
    AS "User Experience", count(*) FROM transactions WHERE
    application = "eCommerce" LIMIT 10, 10

9.  Take your time to explore what other simple chart types could be
    used here. 

10. In the Controller UI, go to Analytics > Alert & Respond > Health
    Rules and create the required Health Rules for the metrics created
    in step 6:
    
    -eComm - Orders lower than expected
    
    Critical condition: # of Orders Placed < 700
    Warning condition: # of Orders Placed < 800
    
    ![](.//media/image4.jpeg)
    
    ![](.//media/image5.jpeg)
    
    -eComm - Unique Visitors lower than expected
    
    Critical condition: # of Unique Visitors < 10
    Warning condition: # of Unique Visitors < 60
    
    ![](.//media/image6.jpeg)
    
    ![](.//media/image7.jpeg)
    
    -eComm - Check Out Processed lower than expected
    NOTE: we may have already this Health Rules as it was defined during
    other labs
    
    Critical condition: Check Out Total Processed < 200
    Warning condition: Check Out Total Processed < 100
    
    
    ![](.//media/image8.jpeg)
    
    ![](.//media/image9.jpeg)
    
    
    -eComm - Revenues at risk higher than expected
    
    Critical condition:
    ({RevenuesAtRisk}/{CheckOutTotalProcessed}*100) > 10 (%)
    Warning
    condition: ({RevenuesAtRisk}/{CheckOutTotalProcessed}*100) >
    2 (%)
    
    ![](.//media/image10.jpeg)
    
    ![](.//media/image11.jpeg)
    
    -eComm - Conversion lower than expected
    
    Critical condition: ({Sales}/{UniqueVisitors}*100) < 10 (%)
    Warning condition: ({Sales}/{UniqueVisitors}*100) < 30 (%)
    
    ![](.//media/image12.jpeg)
    
    ![](.//media/image13.jpeg)

11. In the Controller UI, go to Dashboards & Reports and edit your
    Business Health dashboard. 
    
    -For each box located at the top of the dashboard use the metric
    value widget to show the following:
    
    -# of Unique Visitors
    -# of Orders Placed
    -% Conversion Rate
    -$ Revenues at Risk
    -$ Total Sales
    
    ![](.//media/image14.jpeg)
    
    # of Unique Visitors
    
    ![](.//media/image15.jpeg)
    
    ![](.//media/image16.jpeg)
    
    # of Orders Placed
    
    ![](.//media/image17.jpeg)
    
    ![](.//media/image18.jpeg)
    
    % Conversion Rate
    
    To show conversion percentage we can use metric expression ({# of
    Sales}/{# of Unique Visitors} * 100):
    
    ![](.//media/image19.jpeg)
    
    ![](.//media/image20.jpeg)
    
    ![](.//media/image21.jpeg)
    
    $ Revenues at Risk
    
    ![](.//media/image22.jpeg)
    
    ![](.//media/image23.jpeg)
    
    $ Total Sales
    
    ![](.//media/image24.jpeg)
    
    ![](.//media/image25.jpeg)

12. Link the Health Status widget with the relative Health Rules
    
    -For each box located at the top of the dashboard use the health
    status widget to link with the respective Health Rules (defined in
    step 10):
    
    ![](.//media/image14.jpeg)
    
    ![](.//media/image26.jpeg)
    
    ![](.//media/image27.jpeg)
    
    ![](.//media/image28.jpeg)
    
    ![](.//media/image29.jpeg)
    
    ![](.//media/image30.jpeg)
    
    ![](.//media/image31.jpeg)
    
    ![](.//media/image32.jpeg)
    
    ![](.//media/image33.jpeg)
    
    ![](.//media/image34.jpeg)
    
    ![](.//media/image35.jpeg)

13. Complete the design for the middle section of the dashboard:  
    
    ![](.//media/image36.jpeg)
    
    
    -Use pie chart widget to show Sales vs Revenues at Risk
    
    ![](.//media/image37.jpeg)
    
    -Use timeseries graph widget to show the trend of Sales vs Revenues
    at Risk
    
    ![](.//media/image38.jpeg)
    
    -Use pie chart widget to show Orders vs Leads
    
    ![](.//media/image39.jpeg)
    
    -Use timeseries graph widget to show the trend of Orders vs Leads
    
    ![](.//media/image40.jpeg)

14. Complete the design for the lower section of the dashboard:   
    
    ![](.//media/image41.jpeg)
    
    -Use column widget (simple) created in step 10 to show user
    Experience by Customer Type
    
    ![](.//media/image42.jpeg)
    
    -Use column widget (simple) created in step 10 to show user
    Experience by Business Transaction
    
    ![](.//media/image43.jpeg)

15. Align and change order of the widgets as required

16. This is how it should look our dashboard once completed
    
    ![](.//media/image44.png)
