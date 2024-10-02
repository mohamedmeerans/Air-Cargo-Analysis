# Air-Cargo-Analysis


# Case Study - Air Cargo Analysis - MYSQL 

**DESCRIPTION**

Air Cargo is an aviation company that provides air transportation services for passengers and freight. Air Cargo uses its aircraft to provide different services with the help of partnerships or alliances with other airlines. The company wants to prepare reports on regular passengers, busiest routes, ticket sales details, and other scenarios to improve the ease of travel and booking for customers.

**Project Objective:**

You, as a Data Analyst, need to focus on identifying the regular customers to provide offers, analyse the busiest route which helps to increase the number of aircraft required and prepare an analysis to determine the ticket sales details. This will ensure that the company improves its operability and becomes more customer-centric and a favourable choice for air travel.


**Technology Used :**

* MYSQL

--------------------------------------------------------------------------------------------------------------------------------------------  

**Dataset description:**

**Customer: Contains the information of customers**

•	customer – ID of the customer

•	first name – First name of the customer

•	last name – Last name of the customer

•	date_of_birth – Date of birth of the customer

•	gender – Gender of the customer

------------------------------------------------------------------------------------------------------------------------------------------------

**passengers_on_flights: Contains information about the travel details**

•	aircraft – ID of each aircraft in a brand

•	route_id – Route ID of from and to location

•	customer_id – ID of the customer

•	depart – Departure place from the airport

•	arrival – Arrival place in the airport

•	seat_num – Unique seat number for each passenger

•	class_id – ID of travel class

•	travel_date – Travel date of each passenger

•	flight_num – Specific flight number for each route

-----------------------------------------------------------------------------------------------------------------------------------------------------

**ticket_details: Contains information about the ticket details**


•	p_date – Ticket purchase date

•	customer_id – ID of the customer

•	aircraft_id – ID of each aircraft in a brand

•	class_id – ID of travel class

•	no_of_tickets – Number of tickets purchased

•	a_code – Code of each airport

•	price_per_ticket – Price of a ticket

•	brand – Aviation service provider for each aircraft

----------------------------------------------------------------------------------------------------------------------------------------------------------

**routes: Contains information about the route details**

•	Route_id – Route ID of from and to location

•	Flight_num – Specific fight number for each route

•	Origin_airport – Departure location

•	Destination_airport – Arrival location

•	Aircraft_id – ID of each aircraft in a brand

•	Distance_miles – Distance between departure and arrival location

----------------------------------------------------------------------------------------------------------------------------------------------------------------
**Following operations should be performed:**

1.	Write a query to create route_details table using suitable data types for the fields, such as route_id, flight_num, origin_airport, destination_airport, aircraft_id, and distance_miles. Implement the check constraint for the flight number and unique constraint for the route_id fields. Also, make sure that the distance miles field is greater than 0.


         ANS : SELECT * FROM routes where distance_miles > 0;

![image](https://github.com/user-attachments/assets/0dc49ec9-df82-40a3-8304-eb5d451ef0c2)

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

2.	Write a query to display all the passengers (customers) who have travelled in routes 01 to 25. 

        ANS : select p.customer_id,
        c.first_name, c.last_name, 
        route_id from passengers_on_flights p
        join customer c on  p.customer_id = c.customer_id
        where route_id between 1 and 25 ;

![image](https://github.com/user-attachments/assets/79020b2e-a25b-412d-9421-a60c6fb54925)

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

3.    Write a query to identify the number of passengers and total revenue in business class 

          ANS :   select count(no_of_tickets) as num_of_passenger,
          sum(Price_per_ticket)as Revenue  
          from ticket_details where class_id = 'Bussiness' ;


![image](https://github.com/user-attachments/assets/cf9c1800-1721-451c-8345-18abce569b3e)

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


4.	Write a query to display the full name of the customer by extracting the first name and last name from the customer table.

           ANS: select concat(first_name,' ', last_name) as FullName from customer;

![image](https://github.com/user-attachments/assets/d77cadfb-c4d3-42aa-9e5e-ffe11a9fc3fe)


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

5.	Write a query to extract the customers who have registered and booked a ticket. 

            ANS :       select ticket_details.customer_id , ticket_details.no_of_tickets 
            from ticket_details 
            join passengers_on_flights on ticket_details.           
            customer_id	= passengers_on_flights.customer_id;


![image](https://github.com/user-attachments/assets/0b7b3023-ec92-4ad2-9234-0994024fff37)

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


6.	Write a query to identify the customer’s first name and last name based on their customer ID and brand (Emirates) 


               ANS:  select  c.customer_id,
               c.first_name, c.last_name, 
               t.brand from customer as c 
               join ticket_details as t on c.customer_id = t.customer_id where brand = 'Emirates';

![image](https://github.com/user-attachments/assets/9a8ca5ec-39e5-4aae-af3a-35c13c068871)

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

7.	Write a query to identify the customers who have travelled by Economy Plus class 


        ANS : select  c.customer_id,
        c.first_name, c.last_name, 
        t.class_id from customer as c join ticket_details as t on c.customer_id = t.customer_id where class_id = 'Economy Plus';


![image](https://github.com/user-attachments/assets/45fca136-0f53-4866-b750-85f29dd05735)

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

8.	Write a query to identify whether the revenue has crossed 10000 

         ANS : select sum(Price_per_ticket)as Revenue from ticket_details ;

![image](https://github.com/user-attachments/assets/304b1b5e-fbfd-4700-be13-87a67c234038)

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

9.	Write a query to find the maximum ticket price for each class using window functions on the ticket_details table.

        ANS:  SELECT distinct
        class_id,
        Price_per_ticket,
        MAX(Price_per_ticket) 
        OVER (PARTITION BY class_id) AS max_ticket_price FROM ticket_details;

![image](https://github.com/user-attachments/assets/738881af-8443-467e-a1ad-63333653b188)

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

10.	Write a query to extract the passengers whose route ID is 4 by improving the speed and performance of the flights.

        ANS :  select * from passengers_on_flights where route_id = 4;

![image](https://github.com/user-attachments/assets/b6104114-5ed8-4c34-bef6-d3395580d3cc)


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


11.	Write a query to create a view with only business class customers along with the brand of airlines.

         ANS : create view flght as

        select customer_id, 
        brand,class_id 
        from ticket_details 
        where class_id = 'Bussiness' ;

![image](https://github.com/user-attachments/assets/01b2bfa4-5581-4dec-89cf-c666b8552a89)











