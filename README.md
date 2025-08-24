 select *
  from Hotel_Booking_DB..resort_hotel

  select *
  from Hotel_Booking_DB..city_hotel


  alter table Hotel_Booking_DB..Resort_Hotel
  add Date_of_Arrival date

  alter table Hotel_Booking_DB..city_hotel
  add Date_of_Arrival date

  update Hotel_Booking_DB..Resort_Hotel
  set Date_of_Arrival = convert(date, Date_OfArrival)

    update Hotel_Booking_DB..City_Hotel
  set Date_of_Arrival = convert(date, Date_OfArrival)

  alter table Hotel_Booking_DB..Resort_Hotel
  add Reservation_Status_Date_Converted date

  alter table Hotel_Booking_DB..city_hotel
  add Reservation_Status_Date_Converted date
  

  update Hotel_Booking_DB..Resort_Hotel
  set Reservation_Status_Date_Converted = convert(date,reservation_status_date)

    update Hotel_Booking_DB..City_Hotel
  set Reservation_Status_Date_Converted = convert(date,reservation_status_date)

  alter table Hotel_Booking_DB..resort_hotel
  drop column date_ofarrival, [lead time], reservation_status_date,f30

    alter table Hotel_Booking_DB..city_hotel
  drop column date_ofarrival, [lead time], reservation_status_date, f30

    alter table Hotel_Booking_DB..resort_hotel
  drop column f30

    alter table Hotel_Booking_DB..city_hotel
  drop column f30


  select distinct(Country),count(Country)
  from Hotel_Booking_DB..Resort_Hotel
  group by Country
   --having count(Country) = '9'
  order by country



  --CITY HOTEL STARTS HERE


  --this contains all data BOOKINGS for 1 YEAR (2015/2016) for CITY HOTEL
  select *
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival < '2016-07-01'
  order by Date_of_Arrival


      select  Reservation_status_date_converted, reserved_room_type, count(Reserved_Room_Type) as Count_of_Room_Count
  from Hotel_Booking_DB..City_Hotel
  where Is_Repeated_Guest = '1'
  group by Reservation_status_date_converted, Reserved_Room_Type
  
  --order by Reservation_Status_Date_Converted ASC




  --this contains all CANCELLED BOOKINGS for 1 year 2015/2016 for CITY HOTEL
    select *
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival < '2016-07-01' AND Reservation_Status = 'canceled'
  order by Date_of_Arrival 


  --this contains all customers who showed-up and checked-out for 1 year 2015/2016 for CITY HOTEL
    select *
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival < '2016-07-01' AND Reservation_Status = 'check-out'
  order by Date_of_Arrival




  --this contains all details of customers that booked succesfully but did not SHOW-UP for  1year 2015/2016  for CITY HOTEL
      select *
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival < '2016-07-01' AND Reservation_Status = 'No-show'
  order by Date_of_Arrival



  --this contains all details number of customers that CHECKED-OUT, DID NOT SHOW-UP AND CANCELLED for 1 year 2015/2016 for CITY HOTEL
     select distinct(Reservation_Status),count(reservation_status) as Sum_Of_Reservation_Status
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival < '2016-07-01'
  group by Reservation_Status
  order by Sum_Of_Reservation_Status desc


  --This contains the Count_of_Each_Distribution_Channel_Used for CITY HOTEL FOR 1 YEAR 2015/2016
    SELECT [Distribution Channel], count([Distribution Channel]) as Count_of_Each_Distribution_Channel_Used
  FROM Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival < '2016-07-01'
  group by [Distribution Channel]
  order by Count_of_Each_Distribution_Channel_Used desc


    --This is the Count per meal type for CITY HOTEL FOR 1 YEAR 2015/2016
     SELECT Meal, count(meal) as Count_Per_Meal_type
  FROM Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival < '2016-07-01'
  group by Meal
  order by Count_Per_Meal_type desc

  --This shows the Agent with the best performance based on number of clients brought to CITY HOTEL IN 1 YEAR 2015/2016
    SELECT distinct(Agent), count(agent) as Registered_Bookings_Per_Agent
  FROM Hotel_Booking_DB..City_Hotel
  where Agent is not null and Date_of_Arrival < '2016-07-01'
  group by agent
  order by 2 desc





  --CITY HOTEL 2016/2017 DATA STARTS HERE



  select *
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival >= '2016-07-01' AND Reservation_Status = 'canceled'
  order by Date_of_Arrival


  --this contains all customers who showed-up and checked-out for 1 year 2016/2017 for CITY HOTEL
    select *
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival >= '2016-07-01' AND Reservation_Status = 'check-out'
  order by Date_of_Arrival



  --this contains all details of customers that booked succesfully but did not SHOW-UP for  1year 2016/2017  for CITY HOTEL
      select *
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival >= '2016-07-01' AND Reservation_Status = 'No-show'
  order by Date_of_Arrival



  --this contains all details number of customers that CHECKED-OUT, DID NOT SHOW-UP AND CANCELLED for 1 year 2016/2017 for CITY HOTEL
     select distinct(Reservation_Status),count(reservation_status) as Sum_Of_Reservation_Status
  from Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival >= '2016-07-01'
  group by Reservation_Status
  order by Sum_Of_Reservation_Status desc


  --This contains the Count_of_Each_Distribution_Channel_Used for CITY HOTEL FOR 1 YEAR 2016/2017
    SELECT [Distribution Channel], count([Distribution Channel]) as Count_of_Each_Distribution_Channel_Used
  FROM Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival >= '2016-07-01'
  group by [Distribution Channel]
  order by Count_of_Each_Distribution_Channel_Used desc


    --This is the Count per meal type for CITY HOTEL FOR 1 YEAR 2016/2017
     SELECT Meal, count(meal) as Count_Per_Meal_type
  FROM Hotel_Booking_DB..City_Hotel
  where Date_of_Arrival >= '2016-07-01'
  group by Meal
  order by Count_Per_Meal_type desc


  --This shows the Agent with the best performance based on number of clients brought to CITY HOTEL IN 1 YEAR 2016/2017
    SELECT distinct(Agent), count(agent) as Best_Performing_Agent
  FROM Hotel_Booking_DB..City_Hotel
  where Agent is not null and Date_of_Arrival >= '2016-07-01'
  group by agent
  order by 2 desc




  --CITY HOTEL GENERAL ANALYSIS (NOT DATA BASED)

  --This shows the list of countries, the count of each country by their RESERVATION STATUS EACH for CITY HOTEL
  SELECT distinct(Country), Reservation_Status, count(country) as Count_By_Country
  FROM Hotel_Booking_DB..City_Hotel
  --WHERE COUNTRY = 'NGA'
  group by Country, Reservation_Status
  order by 1,3 desc

  --This shows the list of countries, the individual MARKET SEGEMENT AND COUNT showing how they booked for CITY HOTEL
   SELECT distinct(Country), Market_segment, count(country) as Count_By_Country
  FROM Hotel_Booking_DB..City_Hotel
  --WHERE COUNTRY = 'UKR'
  group by Country, Market_Segment
  order by 1,3 desc

   --This contains the total number of each MARKET SEGMENT and PERFORMANCE of each MARKET SEGMENT for CITY HOTEL
  SELECT distinct Market_Segment, count(market_segment) as Count_Of_Market_Segment
  FROM Hotel_Booking_DB..City_Hotel
  group by Market_Segment
  order by Count_Of_Market_Segment desc


  --This contains the Count_of_Each_Distribution_Channel_Used for CITY HOTEL
  SELECT [Distribution Channel], count([Distribution Channel]) as Count_of_Each_Distribution_Channel_Used
  FROM Hotel_Booking_DB..City_Hotel
  group by [Distribution Channel]
  order by Count_of_Each_Distribution_Channel_Used desc


  --This is the Count per meal type for CITY HOTEL
     SELECT Meal, count(meal) as Count_Per_Meal_type
  FROM Hotel_Booking_DB..City_Hotel
  group by Meal
  order by Count_Per_Meal_type desc


  --This shows the Agent with the best performance based on number of clients brought to CITY HOTEL
   SELECT distinct(Agent), count(agent) as Registered_Bookings_Per_Agent
  FROM Hotel_Booking_DB..City_Hotel
  where Agent is not null
  group by agent
  order by 2 desc

  --This is to show the details and performance of the best performing agent in CITY HOTEL
     SELECT distinct(Agent), Market_segment, count(agent) as Best_Performing_Agent
  FROM Hotel_Booking_DB..City_Hotel
  where Agent is not null and  Agent = '9'
  group by agent, Market_Segment
  order by 1,3 desc


  --This is the sum total of guests who visited the CITY HOTEL more than once AND who visited just once
  SELECT Is_Repeated_Guest, count(is_repeated_guest) as Sum_Total_Repeated_And_Once_Time_Guest
  FROM Hotel_Booking_DB..City_Hotel
  group by Is_Repeated_Guest
  order by Sum_Total_Repeated_And_Once_Time_Guest desc

  --This indicates the best performing room types for CITY HOTEL
   SELECT Assigned_Room_Type, count(assigned_room_type) as Sum_of_Each_Room_Activity
  FROM Hotel_Booking_DB..City_Hotel
  group by Assigned_Room_Type
  order by Sum_of_Each_Room_Activity desc


    SELECT Company, COUNT(company) as Company_Activity_Count
  FROM Hotel_Booking_DB..City_Hotel
  where Company  is not null
  group by Company
  order by Company_Activity_Count desc
  


  --This shows the sum total of the individual CUSTOMER-TYPE for CITY HOTEL
 SELECT Customer_Type, count(customer_type) as Sum_Of_Customer_Type
  FROM Hotel_Booking_DB..City_Hotel
  group by Customer_Type
  --having count(customer_type) > '8000'
  order by count(customer_type) desc
  


  --Select Reserved_Room_Type, count(reserved_room_type), Assigned_Room_Type, count(assigned_room_type),Booking_Changes
  --from Hotel_Booking_DB..Resort_Hotel
  --group by Reserved_Room_Type, Assigned_Room_Type, Booking_Changes
  --order by 2 desc, 4 desc


  --This shows the number of times persons RESERVED rooms but were ASSIGNED other rooms.
    Select Reserved_Room_Type, count(reserved_room_type) as Count_Of_Reserved_Room, Assigned_Room_Type, count(assigned_room_type) as Count_Of_Assigned_Room
  from Hotel_Booking_DB..Resort_Hotel
  where Reserved_Room_Type <> Assigned_Room_Type
  group by Reserved_Room_Type, Assigned_Room_Type
  order by 4 desc
  


  --This shows the number of times persons RESERVED rooms AND were ASSIGNED the same rooms IN CITY HOTEL
  
  Select Reserved_Room_Type,count(reserved_room_type) as Count_Of_Reserved_Room, Assigned_Room_Type, count(assigned_room_type) as Count_Of_Assigned_Room
  from Hotel_Booking_DB..City_Hotel
  where Reserved_Room_Type = Assigned_Room_Type
  group by Reserved_Room_Type, Assigned_Room_Type
  order by 4 DESC


  --This Shows the best performing Agent based on REPEATED GUEST COUNT BY COUNTRY FOR CITY HOTEL
   select  Is_Repeated_Guest, Agent, count(agent) as Agent_Activity,
    count(is_repeated_guest) over (partition by is_repeated_guest) as count_of_repeated_guest
  from Hotel_Booking_DB..City_Hotel
  where Is_Repeated_Guest > 0 and Agent IS NOT NULL
  group by Agent, Is_Repeated_Guest
  order by Agent_Activity desc





--JOINED BOTH TABLES FROM HERE-ON




  
    --This shows the collective data and sum of customer type for both RESORT HOTEL AND CITY HOTEL
   SELECT Resort_Hotel.Hotel as Resort_Hotel,
   resort_hotel.customer_type as Resort_Hotel_Customer_Type,
   count(Resort_Hotel.Customer_Type) as Sum_of_resort_hotel_customer_type,
   city_hotel.Hotel as City_Hotel,
   city_hotel.customer_type as City_Hotel_Customer_Type,
   count(city_hotel.Customer_Type) as Sum_of_City_hotel_Customer_Type
  FROM Hotel_Booking_DB..Resort_Hotel
  full join Hotel_Booking_DB..city_hotel
  on City_Hotel.hotel = Resort_Hotel.Hotel
  group by Resort_Hotel.Hotel, resort_hotel.customer_type, city_hotel.Hotel, city_hotel.customer_type
  order by 1,2,3 desc,4,5,6 desc
  --where Resort_Hotel.Customer_Type is not null and City_Hotel.Customer_Type is not null


   SELECT resort_hotel.Market_Segment, count(resort_hotel.Market_Segment), City_Hotel.Market_Segment, count(City_Hotel.Market_Segment)
  FROM Hotel_Booking_DB..Resort_Hotel
  full join Hotel_Booking_DB..city_hotel
  on Resort_Hotel.Hotel = City_Hotel.Hotel
  group by resort_hotel.Market_Segment, City_Hotel.Market_Segment
  order by 2 desc,4 desc






  --CITY HOTEL ENDS HERE















  --RESORT HOTEL STARTS HERE



  --this contains all data BOOKINGS for 1 YEAR (2015/2016) for RESORT HOTEL
  select *
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival < '2016-07-01'
  order by Date_of_Arrival



  --this contains all CANCELLED BOOKINGS for 1 year 2015/2016 for RESORT HOTEL
    select *
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival < '2016-07-01' AND Reservation_Status = 'canceled'
  order by Date_of_Arrival


  --this contains all customers who showed-up and checked-out for 1 year 2015/2016 for RESORT HOTEL
    select *
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival < '2016-07-01' AND Reservation_Status = 'check-out'
  order by Date_of_Arrival



  --this contains all details of customers that booked succesfully but did not SHOW-UP for  1year 2015/2016  for RESORT HOTEL
      select *
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival < '2016-07-01' AND Reservation_Status = 'No-show'
  order by Date_of_Arrival



  --this contains all details number of customers that CHECKED-OUT, DID NOT SHOW-UP AND CANCELLED for 1 year 2015/2016 for RESORT HOTEL
     select distinct(Reservation_Status),count(reservation_status) as Sum_Of_Reservation_Status
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival < '2016-07-01'
  group by Reservation_Status
  order by Sum_Of_Reservation_Status desc


  --This contains the Count_of_Each_Distribution_Channel_Used for RESORT HOTEL FOR 1 YEAR 2015/2016
    SELECT [Distribution Channel], count([Distribution Channel]) as Count_of_Each_Distribution_Channel_Used
  FROM Hotel_Booking_DB..Resort_Hotel
  where Date_of_Arrival < '2016-07-01'
  group by [Distribution Channel]
  order by Count_of_Each_Distribution_Channel_Used desc


    --This is the Count per meal type for RESORT HOTEL FOR 1 YEAR 2015/2016
     SELECT Meal, count(meal) as Count_Per_Meal_type
  FROM Hotel_Booking_DB..Resort_Hotel
  where Date_of_Arrival < '2016-07-01'
  group by Meal
  order by Count_Per_Meal_type desc

  --This shows the Agent with the best performance based on number of clients brought to RESORT HOTEL IN 1 YEAR 2015/2016
    SELECT distinct(Agent), count(agent) as Best_Performing_Agent_RESORT_HOTEL
  FROM Hotel_Booking_DB..Resort_Hotel
  where Agent is not null and Date_of_Arrival < '2016-07-01'
  group by agent
  order by 2 desc





  SELECT *
  FROM Hotel_Booking_DB..Resort_Hotel
  order by Date_of_Arrival



   --this contains all CANCELLED BOOKINGS for 1 year 2016/2017 for RESORT HOTEL
    select *
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival >= '2016-07-01' AND Reservation_Status = 'canceled'
  order by Date_of_Arrival


  --this contains all customers who showed-up and checked-out for 1 year 2016/2017 for RESORT HOTEL
    select *
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival >= '2016-07-01' AND Reservation_Status = 'check-out'
  order by Date_of_Arrival



  --this contains all details of customers that booked succesfully but did not SHOW-UP for  1year 2016/2017  for RESORT HOTEL
      select *
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival >= '2016-07-01' AND Reservation_Status = 'No-show'
  order by Date_of_Arrival



  --this contains all details number of customers that CHECKED-OUT, DID NOT SHOW-UP AND CANCELLED for 1 year 2016/2017 for RESORT HOTEL
     select distinct(Reservation_Status),count(reservation_status) as Sum_Of_Reservation_Status
  from Hotel_Booking_DB..resort_hotel
  where Date_of_Arrival >= '2016-07-01'
  group by Reservation_Status
  order by Sum_Of_Reservation_Status desc


  --This contains the Count_of_Each_Distribution_Channel_Used for RESORT HOTEL FOR 1 YEAR 2016/2017
    SELECT [Distribution Channel], count([Distribution Channel]) as Count_of_Each_Distribution_Channel_Used
  FROM Hotel_Booking_DB..Resort_Hotel
  where Date_of_Arrival >= '2016-07-01'
  group by [Distribution Channel]
  order by Count_of_Each_Distribution_Channel_Used desc


    --This is the Count per meal type for RESORT HOTEL FOR 1 YEAR 2016/2017
     SELECT Meal, count(meal) as Count_Per_Meal_type
  FROM Hotel_Booking_DB..Resort_Hotel
  where Date_of_Arrival >= '2016-07-01'
  group by Meal
  order by Count_Per_Meal_type desc

  --This shows the Agent with the best performance based on number of clients brought to RESORT HOTEL IN 1 YEAR 2016/2017
    SELECT distinct(Agent), count(agent) as Best_Performing_Agent
  FROM Hotel_Booking_DB..Resort_Hotel
  where Agent is not null and Date_of_Arrival >= '2016-07-01'
  group by agent
  order by 2 desc









  --This shows the list of countries, the count of each country by their RESERVATION STATUS EACH for RESORT HOTEL
  SELECT distinct(Country), Reservation_Status, count(country) as Count_By_Country
  FROM Hotel_Booking_DB..Resort_Hotel
  --WHERE COUNTRY = 'NGA'
  group by Country, Reservation_Status
  order by 1,3 desc

  --This shows the list of countries, the individual MARKET SEGEMENT AND COUNT showing how they booked for RESORT HOTEL
   SELECT distinct(Country), Market_segment, count(country) as Count_By_Country
  FROM Hotel_Booking_DB..Resort_Hotel
  --WHERE COUNTRY = 'UKR'
  group by Country, Market_Segment
  order by 1,3 desc

   --This contains the total number of each MARKET SEGMENT and PERFORMANCE of each MARKET SEGMENT for RESORT HOTEL
  SELECT distinct Market_Segment, count(market_segment) as Count_Of_Market_Segment
  FROM Hotel_Booking_DB..Resort_Hotel
  group by Market_Segment
  order by Count_Of_Market_Segment desc


  --This contains the Count_of_Each_Distribution_Channel_Used for RESORT HOTEL
  SELECT [Distribution Channel], count([Distribution Channel]) as Count_of_Each_Distribution_Channel_Used
  FROM Hotel_Booking_DB..Resort_Hotel
  group by [Distribution Channel]
  order by Count_of_Each_Distribution_Channel_Used desc


  --This is the Count per meal type for RESORT HOTEL
     SELECT Meal, count(meal) as Count_Per_Meal_type
  FROM Hotel_Booking_DB..Resort_Hotel
  group by Meal
  order by Count_Per_Meal_type desc


  --This shows the Agent with the best performance based on number of clients brought to RESORT HOTEL
   SELECT distinct(Agent), count(agent) as Best_Performing_Agent
  FROM Hotel_Booking_DB..Resort_Hotel
  where Agent is not null
  group by agent
  order by 2 desc

  --This is to show the details and performance of the best performing agent in RESORT HOTEL
     SELECT distinct(Agent), Market_segment, count(agent) as Best_Performing_Agent
  FROM Hotel_Booking_DB..Resort_Hotel
  where Agent is not null and  Agent = '240'
  group by agent, Market_Segment
  order by 1,3 desc


  --This is the sum total of guests who visited the RESORT HOTEL more than once AND who visited just once
  SELECT Is_Repeated_Guest, count(is_repeated_guest) as Sum_Total_Repeated_And_Once_Time_Guest
  FROM Hotel_Booking_DB..Resort_Hotel
  group by Is_Repeated_Guest
  order by Sum_Total_Repeated_And_Once_Time_Guest desc

  --This indicates the best performing room types for RESORT HOTEL
   SELECT Assigned_Room_Type, count(assigned_room_type) as Sum_of_Each_Room_Activity
  FROM Hotel_Booking_DB..Resort_Hotel
  group by Assigned_Room_Type
  order by Sum_of_Each_Room_Activity desc


    SELECT Company, COUNT(company) as Company_Activity_Count
  FROM Hotel_Booking_DB..Resort_Hotel
  where Company  is not null
  group by Company
  order by Company_Activity_Count desc
  


  --This shows the sum total of the individual CUSTOMER-TYPE for RESORT HOTEL
 SELECT Customer_Type, count(customer_type) as Sum_Of_Customer_Type
  FROM Hotel_Booking_DB..Resort_Hotel
  group by Customer_Type
  order by count(customer_type) desc
  --having count(customer_type) > '8000'


  --Select Reserved_Room_Type, count(reserved_room_type), Assigned_Room_Type, count(assigned_room_type),Booking_Changes
  --from Hotel_Booking_DB..Resort_Hotel
  --group by Reserved_Room_Type, Assigned_Room_Type, Booking_Changes
  --order by 2 desc, 4 desc

  --This shows the number of times persons RESERVED rooms but were ASSIGNED other rooms.
  
    Select Reserved_Room_Type, count(reserved_room_type) as Count_Of_Reserved_Room, Assigned_Room_Type, count(assigned_room_type) as Count_Of_Assigned_Room
  from Hotel_Booking_DB..Resort_Hotel
  where Reserved_Room_Type <> Assigned_Room_Type
  group by Reserved_Room_Type, Assigned_Room_Type
  order by 4 desc
  


  --This shows the number of times persons RESERVED rooms AND were ASSIGNED the same rooms.
  
  Select Reserved_Room_Type, count(reserved_room_type) as Count_Of_Reserved_Room, Assigned_Room_Type, count(assigned_room_type) as Count_Of_Assigned_Room
  from Hotel_Booking_DB..Resort_Hotel
  where Reserved_Room_Type = Assigned_Room_Type
  group by Reserved_Room_Type, Assigned_Room_Type
  order by 4 desc


  --This Shows the best performing Agent based on REPEATED GUEST COUNT BY COUNTRY
   select  Is_Repeated_Guest, Agent, count(agent) as Agent_Activity,
    count(is_repeated_guest) over (partition by is_repeated_guest) as count_of_repeated_guest
  from Hotel_Booking_DB..Resort_Hotel
  where Is_Repeated_Guest > 0 and Agent IS NOT NULL
  group by Agent, Is_Repeated_Guest
  order by Agent_Activity desc



  --This Shows AGENT PERFORMANCE by total of repeated guest brought to RESORT HOTEL
   select /**country,**/ Is_Repeated_Guest, Agent, count(agent) as Agent_Activity,
    count(is_repeated_guest) over (partition by is_repeated_guest) as count_of_repeated_guest
  from Hotel_Booking_DB..Resort_Hotel
  where Is_Repeated_Guest > 0 and Agent IS NOT NULL
  group by Agent, Is_Repeated_Guest
  order by Agent_Activity desc





  
  

    


    --This shows the collective data and sum of customer type for both RESORT HOTEL AND CITY HOTEL
   SELECT Resort_Hotel.Hotel, resort_hotel.customer_type, count(Resort_Hotel.Customer_Type) as Sum_of_resort_hotel_customer_type, city_hotel.Hotel, city_hotel.customer_type, count(city_hotel.Customer_Type) as Sum_of_City_hotel_Customer_Type
  FROM Hotel_Booking_DB..Resort_Hotel
  full join Hotel_Booking_DB..city_hotel
  on City_Hotel.hotel = Resort_Hotel.Hotel
  group by Resort_Hotel.Hotel, resort_hotel.customer_type, city_hotel.Hotel, city_hotel.customer_type
  order by 1,2,3 desc,4,5,6 desc
  --where Resort_Hotel.Customer_Type is not null and City_Hotel.Customer_Type is not null


   SELECT resort_hotel.Market_Segment as Resort_Market_Segment,
   count(resort_hotel.Market_Segment) as Count_Of_Resort_Market_Segment,
   City_Hotel.Market_Segment as City_Market_Segment,
   count(City_Hotel.Market_Segment) as Count_Of_City_Market_Segment

  FROM Hotel_Booking_DB..Resort_Hotel
  full join Hotel_Booking_DB..city_hotel
  on Resort_Hotel.Hotel = City_Hotel.Hotel
  group by resort_hotel.Market_Segment, City_Hotel.Market_Segment
  order by 2 desc,4 desc
  
  

  --This shows the bookings for RESORT HOTEL that were cancelled same day they booked for reservation
    select Date_of_Arrival, Reservation_Status_Date_Converted,Reservation_Status
  from Hotel_Booking_DB..Resort_Hotel
  group by Reservation_Status,Reservation_Status_Date_Converted, Date_of_Arrival
  having Date_of_Arrival = Reservation_Status_Date_Converted and Reservation_Status = 'canceled'
  order by Reservation_Status_Date_Converted

  --This shows the bookings for CITY HOTEL that were cancelled same day they booked for reservation
     select Date_of_Arrival, Reservation_Status_Date_Converted,Reservation_Status
  from Hotel_Booking_DB..City_Hotel
  group by Reservation_Status,Reservation_Status_Date_Converted, Date_of_Arrival
  having Date_of_Arrival = Reservation_Status_Date_Converted and Reservation_Status = 'canceled'
  order by Reservation_Status_Date_Converted


 --This shows the bookings for RESORT HOTEL that CHECKED-OUT same day they CHECKED-IN THE HOTEL AND HAD EXTRA DAYS LEFT TO STAY
   select Date_of_Arrival, Reservation_Status_Date_Converted,Reservation_Status,Stays_In_Week_Nights, Stays_In_Weekend_Nights
  from Hotel_Booking_DB..Resort_Hotel
  group by Reservation_Status,Reservation_Status_Date_Converted, Date_of_Arrival,Stays_In_Week_Nights, Stays_In_Weekend_Nights
  having Date_of_Arrival = Reservation_Status_Date_Converted and Reservation_Status = 'check-out'
  order by 4 DESC,5 DESC


  --THE CODE ABOVE AND BELOW SHOWS THE DATA THAT PROVES THAT GUESTS ARE MORE PROBABLY DISSATISFIED WITH RESORT HOTELS
  --DUE TO THE FACT THAT MORE PERSONS CHECK-OUT SAME DAY THEY CHECKED-IN, WHICH MIGHT BE DUE TO SERVICE DISSATISFACTION

  --This shows the bookings for CITY HOTEL that CHECKED-OUT same day they CHECKED-IN THE HOTEL AND HAD EXTRA DAYS LEFT TO STAY
   select Date_of_Arrival, Reservation_Status_Date_Converted,Reservation_Status,Stays_In_Week_Nights, Stays_In_Weekend_Nights
  from Hotel_Booking_DB..City_Hotel
  group by Reservation_Status,Reservation_Status_Date_Converted, Date_of_Arrival,Stays_In_Week_Nights, Stays_In_Weekend_Nights
  having Date_of_Arrival = Reservation_Status_Date_Converted and Reservation_Status = 'check-out'
  order by 4 DESC,5 DESC
  




   select  reservation_status, count(Reservation_Status) as No_of_Bookings_That_Checked_Out, Required_Car_Parking_Spaces
  from Hotel_Booking_DB..Resort_Hotel
  group by Required_Car_Parking_Spaces, Reservation_Status
  having Reservation_Status = 'check-out'


    select  reservation_status, count(Reservation_Status) as No_of_Bookings_That_DidNot_ShowUp, Required_Car_Parking_Spaces
  from Hotel_Booking_DB..Resort_Hotel
  group by Required_Car_Parking_Spaces, Reservation_Status
  having Reservation_Status = 'No-show'


  select  reservation_status, count(Reservation_Status) as No_of_Bookings_That_Checked_Out, Required_Car_Parking_Spaces
  from Hotel_Booking_DB..City_Hotel
  group by Required_Car_Parking_Spaces, Reservation_Status
  having Reservation_Status = 'check-out'


  select  reservation_status, count(Reservation_Status) as No_of_Bookings_That_DidNot_ShowUp, Required_Car_Parking_Spaces
  from Hotel_Booking_DB..City_Hotel
  group by Required_Car_Parking_Spaces, Reservation_Status
  having Reservation_Status = 'no-show'

  
  
  
  
  select distinct(Required_Car_Parking_Spaces)
  from Hotel_Booking_DB..Resort_Hotel
  --where Required_Car_Parking_Spaces > '0' and Reservation_Status = 'no-show'



  select *
    from Hotel_Booking_DB..City_Hotel
