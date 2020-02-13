# Cache-Management-API-for-EMT-Classic-mode-using-Cassandra
:Author: Altaf Hossain
:Email: alhossain@axway.com
:Email: altaf.hussain011@gmail.com

The idea is to use the TTL ( Time To Live - this is the time in sec till the data will be present in KPS tables ) feature of the Cassandra data storage and create 5 API's that could perform CRUD operation on Cassandra KPS tables to store data like a distributed cache.


Hence we created 5 API's based on the scripts and we changed it to make policy flow and error handling and tested it in EMT mode.


Note :-

    We have done some error handling that can be changed and exception handling based on the use case of the customers.
    The Scripts are in very generic structure that can be remodeled very easily.

 

Goals :-

We are trying to use these scripts with more complex user stories. 
Note these could be used in Classic and EMT mode hence do not hesitate to use it. 


== Team
image:https://raw.githubusercontent.com/Axway-API-Management-Plus/Common/master/img/AxwayLogoSmall.png[Axway Logo] Axway Team
