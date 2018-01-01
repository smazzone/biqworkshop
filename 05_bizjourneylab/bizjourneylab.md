BiQ - Business Journeys Lab - Order Fulfillment
===============================================

***[Estimated time required to complete this lab: 45 min]***

**NOTE: If you have not created your lab application in Ravello, please
execute the following
[steps](https://singularity.jira.com/wiki/spaces/ADGS/pages/300647380/Create+a+new+Application+in+Ravello)**

1.  On Ravello, copy the DNS name for the 4.4 Controller / Event
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
    The Business Journeys template dashboard has been already uploaded
    to your ravello instance. 
    We should somehow work backward to understand which type of widgets
    may be useful and also what type of Health Rules, ADQL Metrics, ADQL
    Queries, Business Outcomes, Data Collectors, Business Transactions
    (and/or BRUM pages, MRUM network requests) we should create in order
    to populate our dashboard.

3.  Each artifact described before may have dependencies over other
    artifacts.
    A quick description of the sequence may be:
    -Identify key Business Transactions, BRUM pages, MRUM network
    requests which will be used in the dashboard
    -Identify and define any required Data Collectors, Custom Events
    which will be used in the dashboard
    -Identify and define Business Outcomes which are going to produce
    additional events
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

5.  We are going to create all the required artifacts, such Business
    Outcomes, ADQL queries, metrics and Health Rules. Let us start with
    Business Outcomes.

6.  In the Controller UI, go to Analytics > Business Outcomes and
    create a new Business Outcome for our commerce order fulfillment
    process.  
    
    ![](.//media/image2.png)

7.  Click the Add button:
    
    ![](.//media/image3.png)

8.  Please, give your Business Outcome the name **orderfulfillment**
    (and a description if you choose).
    
    ![](.//media/image4.png)

9.  We are going to define the different steps (aka milestones) of the
    fulfillment process. The first milestone of this Business Outcome is
    when users complete Checkout transaction on the eCommerce website
    and an order got created. Click Add Milestone, and enter the
    following configuration:

> **Name**: Purchased
>
> **Type**: Transaction -> Application = eCommerce -> Tier =
> eComServices -> Business Transaction = CheckOut (you can add
> additional criteria but we want all orders)
>
> **Primary Key** = Field(OrderID) & Name(OrderID) ... this is the field
> that must have the same value across all milestones.
>
> **Add Fields** = CustomerType, ProductName, ProductPrice (these fields
> are useful for building visualizations and querying for certain types
> of Business Outcomes .. you could add fields for other steps as well
> and they show up on the new event that gets created).
> 
> 
> ![](.//media/image5.png)

10. Let us create the other three milestones to track the following
    steps: Order Received, Order Prepared and Order Shipped. These ara
    transactions of the Fulfillment application. Click Add Milestone
    three more times and fill in the form with the following
    configurations (in order):

> **Name**: Received
>
> **Type**: Transaction -> Application = fulfillment -> Tier =
> fulfillmentServices -> Business Transaction = OrderReceived
>
> **Primary Key** = Field(OrderID) & Name(OrderID)
>
> ![](.//media/image6.png)
>
> **Name**: Prepared
>
> **Type**: Transaction -> Application = fulfillment -> Tier =
> fulfillmentServices -> Business Transaction = OrderPrepared
>
> **Primary Key** = Field(OrderID) & Name(OrderID)
>
> ![](.//media/image7.png)
>
> **Name**: Shipped
>
> **Type**: Transaction -> Application = fulfillment -> Tier =
> fulfillmentServices -> Business Transaction = OrderShipped
>
> **Primary Key** = Field(OrderID) & Name(OrderID)
> 
> ![](.//media/image8.png)
>
>  

11. You can also edit the Health Thresholds for a specific Business
    Outcome (we will leave the defaults for now)
    
    ![](.//media/image9.png)

12. Click **Validate And Save. **
    
    ![](.//media/image10.png)

13. In order to use the newly created Business Outcome we need to enable
    it. Select the Business Outcome and click the Enable button.
    
    ![](.//media/image11.png)

14. Now that we have the Business Outcome created and enabled, we are
    going to create all the remaining artifacts, such ADQL queries,
    metrics and Health Rules. Let us explore ADQL queries.

15. In the Controller UI, go to Analytics > Searches and create a new
    ADQL query that uses the **orderfulfillment** event type (this is
    the new event type created for our new Business Outcome). 
    Let us use the following query:
    
    ![](.//media/image12.png)

16. orderfulfillment is also available as new event type in basic mode
    searches:
    
    ![](.//media/image13.png)

17. By default, Business Outcomes DO NOT show a flowmap for individual
    transactions. We are going to enable this feature. Please, go to
    <http://CONTROLLER_IP:8090/controller/admin.jsp> (password =
    **d3m0@ppD**) and edit the following property to **true**:
    
    ![](.//media/image14.png)

18. After a few minutes if you run the previous query, you should see
    your new event types being populated, with all their associated meta
    data.  They can be queried and visualized just like any other
    analytics event type.
    
    ![](.//media/image15.png)

19. Double clicking on an event will show you the flowmap for the
    Business Outcome, including the time between events (this is
    calculated by subtracting the event time stamp between each step).
    NB: that does not include the execution time of each step from a
    response time standpoint.
    
    ![](.//media/image16.png)

20. Click on the data tab. The data tab will show more details about
    each step in the process.  These are the data extracted from the
    event fields we have defined in our Business Outcome milestones. 
    
    ![](.//media/image17.png)

21. In the Controller UI, go to Analytics > Searches > Query Language
    Search and create the required ADQL query/queries to answer the
    following questions:
    
    ![](.//media/image18.jpeg)
    **
    **-How many orders are about to be received?
    (PS: Querying the new **orderfulfillment** event type we are going
    to look at totalTime and milestoneReached fields to understand in
    which steps our events sit)
    -How many orders are about to be prepared?
    -How many orders are about to be shipped?
    -How many orders are actually shipped?

22. Actually, we can answer all the above questions with a single query
    using the
    [filter](https://docs.appdynamics.com/display/PRO44/Analytics+Functions)
    function. (NOTE: You need first of all to input the following query:
    SELECT count(*) from orderfulfillment and then select a Column
    chart.
    
    ![](.//media/image19.jpeg)
    
    Then paste the query below and click Search button again. NB: For
    some reason you cannot currently switch this query to a Column chart
    after the fact:
    
    SELECT filter(count(*), totalTime IS NULL AND
    Received.milestoneReached IS NULL) AS "Orders to be received",
    filter(count(*), totalTime IS NULL AND Prepared.milestoneReached IS
    NULL) AS "Orders to be prepared", filter(count(*), totalTime IS
    NULL AND Shipped.milestoneReached IS NULL) AS "Orders to be
    shipped", filter(count(*), totalTime IS NOT NULL) AS "Orders
    shipped" FROM orderfulfillment
    
    In this example we can see how many events (orders) are currently
    waiting in each step (milestone) to move to the next, including how
    many have finished shipping.
    
    ![](.//media/image20.jpeg)

23.  Click on Actions and select Add to Dashboard
    
    ![](.//media/image21.jpeg)

24. Select Add to existing Dashboard and then choose your Business
    Journeys - Order Fulfillment dashboard. 
    
    ![](.//media/image22.jpeg)

25. Click OK to save the widget and position it in the middle-right part
    of your dashboard, just below the label Order to Ship Pipeline. 
    
    ![](.//media/image23.jpeg)

26. Let us work on the Order to Ship User Experience section. In the
    Controller UI, go to Analytics > Searches > Drag and Drop
    Search > Visualization and use a simple pie chart widget to answer
    the following questions:
    (Use basic mode)
    
    -What is the distribution of orderfulfillment's End User
    Experience? What percentage of Business Outcomes has User Experience
    Normal? What percentage has Error?
    
    Use the following criteria: 
    
    X Axis: User Experience
    
    ![](.//media/image24.jpeg)

27. Add the widget to your Custom Dashboard
    
    ![](.//media/image25.jpeg)
    
    ![](.//media/image26.jpeg)

28. Click OK to save the widget and position it in the middle-left part
    of your dashboard, just below the label Order to Ship User
    Experience. 
    
    ![](.//media/image27.jpeg)

29. Let us work on the Order to Ship Conversion section. In the
    Controller UI, edit your dashboard and add a new Funnel Analysis
    widget to answer the following questions:
    (Use basic mode)
    
    -How many drop/conversion do we have at each step (milestone) of
    the orderfulfillment process?
    
    ![](.//media/image28.jpeg)
    
    Use the following Funnel properties:
    
    Event Type: orderfulfillment
    
    ![](.//media/image29.jpeg)
    
    Alignment: Center
    Show Health: unchecked 
    
    ![](.//media/image30.jpeg)
    Use the following Funnel definitions:

> Count Distinct of: OrderID
>
> Use the following criteria for the various steps: 
> 
> Step name: Purchased
> Purchased.milestoneReached = true
> 
> Step name: Received
> Received.milestoneReached = true
> 
> Step name: Prepared
> Prepared.milestoneReached = true
> 
> Step name: Shipped
> Shipped.milestoneReached = true
> 
> ![](.//media/image31.jpeg)

30. Save the funnel and position it in the lower-left part of your
    dashboard, just below the label Order to Ship Conversion. 
    
    ![](.//media/image32.jpeg)

31. Let us work on the the Products shipped section. In the Controller
    UI, edit your dashboard and add a new widget (click on Custom Widget
    Builder) to answer the following questions:
    (Use basic mode)
    
    -Which products have the company shipped? From which product shipped
    are the majority of the company's incomes coming? (Look at the
    ProductPrice)
    
    ![](.//media/image33.jpeg)
    
    Select a Treemap widget
    
    Use the following widget properties:
    
    Event Type: orderfulfillment
    
    Use the following criteria: 
    
    X Axis: ProductPrice(Sum)
    Y Axis: ProductName
    
    ![](.//media/image34.jpeg)

32. Save the widget and position it in the lower-right part of your
    dashboard, just below the label Products shipped.
    
    ![](.//media/image35.jpeg)

33. Let us complete the top part of the dashboard. 
    
    ![](.//media/image36.jpeg)

34. We are going to create all the required artifacts, such ADQL
    queries, metrics and Health Rules. Let us start with ADQL queries.

35. In the Controller UI, go to Analytics > Searches and create the
    required ADQL queries to answer the following questions:
    
    -What is the average time from Order to Ship in the orderfulfillment
    process?
    
    SELECT avg(totalTime) AS "AVG Total Time" FROM orderfulfillment
    
    -What is the number of Orders to be received? Basically, orders
    waiting to be received and further processed. (Look at the milestone
    reached and total time fields)
    
    SELECT count(*) FROM orderfulfillment WHERE
    Prepared.milestoneReached != true AND totalTime is NULL
    
    -What is the number of Orders to be prepared? Basically, orders
    waiting to be prepared and further processed. (Look at the milestone
    reached and total time fields)
    
    SELECT count(*) FROM orderfulfillment WHERE
    Prepared.milestoneReached != true AND totalTime is NULL
    
    -What is the number of Orders to be shipped? Basically, orders
    waiting to be shipped. (Look at the milestone reached and total time
    fields)
    
    SELECT count(*) FROM orderfulfillment WHERE
    Shipped.milestoneReached != true AND totalTime is NULL
    
    -What is the number of Orders shipped? (Look at the milestone
    reached and total time fields)
    
    SELECT count(*) FROM orderfulfillment WHERE
    Shipped.milestoneReached = true AND totalTime IS NOT NULL

36. In the Controller UI, go to Analytics > Metrics and create the
    required metrics (you can use the ADQL queries created in the
    previous step): 
    
    -eComm - Order Fulfillment - AVG Total Time
    -eComm - Order Fulfillment - # waiting to be received
    -eComm - Order Fulfillment - # waiting to be prepared
    -eComm - Order Fulfillment - # waiting to be shipped
    -eComm - Order Fulfillment - # shipped

37. In the Controller UI, go to Analytics > Alert & Respond > Health
    Rules and create the required Health Rules for the metrics created
    in the previous step:
    
    -eComm - Order Fulfillment - Order To Ship - AVG Time higher than
    expected
    Critical condition: Order Fulfillment - AVG Total Time > 28000
    Warning condition: Order Fulfillment - AVG Total Time > 27000
    
    ![](.//media/image37.jpeg)
    
    -eComm - Order Fulfillment - # waiting to be received
    Critical condition: Order Fulfillment - # waiting to be received >
    220
    Warning condition: Order Fulfillment - # waiting to be received >
    178
    
    ![](.//media/image38.jpeg)
    
    -eComm - Order Fulfillment - To be prepared higher than expected
    Critical condition: Order Fulfillment - # waiting to be prepared >
    220
    Warning condition: Order Fulfillment - # waiting to be prepared >
    178
    
    ![](.//media/image39.jpeg)
    
    -eComm - Order Fulfillment - To be shipped higher than expected
    Critical condition: Order Fulfillment - # waiting to be shipped >
    220
    Warning condition: Order Fulfillment - # waiting to be shipped >
    178
    
    ![](.//media/image40.jpeg)
    
    -eComm - Order Fulfillment - shipped lower than expected
    Critical condition: Order Fulfillment - # shipped < 10
    Warning condition: Order Fulfillment - # shipped < 50
    
    ![](.//media/image41.jpeg)
     

38. In the Controller UI, go to Dashboards & Reports and edit your
    Business Journey dashboard. 
    
    -For each box located at the top of the dashboard use the metric
    value widget to show the following:
    
    -Order Fulfillment - Order to Ship AVG Time
    -Order Fulfillment - # Orders waiting to be received
    -Order Fulfillment - # Orders waiting to be prepared
    -Order Fulfillment - # Orders waiting to be shipped
    -Order Fulfillment - # Orders shipped
    
    ![](.//media/image36.jpeg)
    
    
    -Order Fulfillment - Order to Ship AVG Time
    
    ![](.//media/image42.jpeg)
    
    ![](.//media/image43.jpeg)
    
    -Order Fulfillment - # Orders waiting to be received
    
    ![](.//media/image44.jpeg)
    
    ![](.//media/image45.jpeg)
    
    -Order Fulfillment - # Orders waiting to be prepared
    
    ![](.//media/image46.jpeg)
    
    ![](.//media/image47.jpeg)
    
    -Order Fulfillment - # Orders waiting to be shipped
    
    ![](.//media/image48.jpeg)
    
    ![](.//media/image49.jpeg)
    
    -Order Fulfillment - # Orders shipped

39. Link the Health Status widget with the relative Health Rules
    
    -For each box located at the top of the dashboard use the health
    status widget to link with the respective Health Rules (defined in
    step 37):
    
    ![](.//media/image36.jpeg)

40. Align and change order of the widgets as required

41. This is how it should look our dashboard once completed
