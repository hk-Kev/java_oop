BUS TRANSPORT COMPANY intends to develop a Bus Transport Management System to improve the management of buses, routes, passengers, drivers, travel schedules, ticket reservations and payments.

The company currently experiences challenges related to manual ticket booking, incorrect passenger information, duplicate reservations, poor bus scheduling, limited seat availability, incorrect payment records and difficulties retrieving transport information.

To address these challenges, the company has decided to develop a console-based application that allows users to register buses, register drivers, manage transport routes, schedule bus trips, register passengers, book tickets, cancel reservations, process payments and retrieve transport information.

As a Java programmer, you are required to design and implement this application using Object-Oriented Programming principles and Java control statements.

SECTION A: CREATE THE REQUIRED CLASSES

Develop the following eight Java classes. Each of the seven domain classes must contain exactly five attributes as specified below.

Class 1: Bus

| Attribute | Data Type |
|---|---|
| busId | int |
| plateNumber | String |
| busName | String |
| seatCapacity | int |
| busStatus | String |

Class 2: Driver

| Attribute | Data Type |
|---|---|
| driverId | int |
| driverName | String |
| driverPhone | String |
| licenseNumber | String |
| driverAge | int |

Class 3: Route

| Attribute | Data Type |
|---|---|
| routeId | int |
| departureLocation | String |
| destinationLocation | String |
| distance | double |
| ticketPrice | double |

Class 4: Passenger

| Attribute | Data Type |
|---|---|
| passengerId | int |
| passengerName | String |
| passengerEmail | String |
| passengerAge | int |
| passengerPhone | String |

Class 5: Trip

| Attribute | Data Type |
|---|---|
| tripId | int |
| bus | Bus |
| driver | Driver |
| route | Route |
| departureTime | String |

Class 6: Booking

| Attribute | Data Type |
|---|---|
| bookingId | int |
| passenger | Passenger |
| trip | Trip |
| seatNumber | int |
| bookingStatus | String |

Class 7: Payment

| Attribute | Data Type |
|---|---|
| paymentId | int |
| booking | Booking |
| amountPaid | double |
| paymentMethod | String |
| paymentStatus | String |

Class 8: Main

The Main class must manage the execution of the application and allow users to interact with the system.

OBJECT-ORIENTED PROGRAMMING REQUIREMENTS

All seven domain classes must demonstrate the following:

1. Proper encapsulation of attributes.
2. Parameterized constructors to initialize objects.
3. Getter and setter methods for accessing and modifying attributes.
4. Overriding of the toString() method to display object information.
5. Validation of object information before accepting it.
6. Prevention of invalid object states.
7. Appropriate relationships between the different classes.
8. Use of objects to reference information registered in other classes.

SECTION B: MENU-DRIVEN APPLICATION

The application must display the following menu:

BUS TRANSPORT MANAGEMENT SYSTEM

1. Register Bus
2. Register Driver
3. Register Route
4. Register Passenger
5. Schedule Trip
6. Book Ticket
7. Cancel Booking
8. Process Payment
9. View All Buses
10. View All Drivers
11. View All Routes
12. View All Passengers
13. View All Scheduled Trips
14. View All Bookings
15. View All Payments
16. Search Bus by Plate Number
17. Search Driver by License Number
18. Search Passenger by Phone Number
19. Search Trip by Trip ID
20. Search Booking by Booking ID
21. Check Available Seats
22. Exit

The application must use a switch-case statement to execute the selected operation.

A while loop must keep the application running until the user chooses to exit.

A for loop must be used to process multiple registered records, including listing, searching and checking available seats.

The system must support multiple buses, drivers, routes, passengers, trips, bookings and payments.

Registration Requirements

1. Buses must be registered before they can be assigned to trips.
2. Drivers must be registered before they can be assigned to buses for scheduled trips.
3. Routes must be registered before trips can be scheduled.
4. Passengers must be registered before booking tickets.
5. Each trip must reference an existing bus, driver and route.
6. Each booking must reference an existing passenger and scheduled trip.
7. Each payment must reference an existing booking.
8. Duplicate identifiers must not be accepted.
9. Duplicate bus plate numbers and driver license numbers must not be accepted.
10. All registration information must be received from the user using the Scanner class.

Bus and Trip Management Requirements

1. A bus must have a valid registration number and positive seating capacity.
2. A bus must have an appropriate status indicating whether it is available or unavailable.
3. Only available buses may be assigned to trips.
4. A driver must have a valid driving license number.
5. Departure and destination locations must be different.
6. Route distance and ticket price must be greater than zero.
7. A scheduled trip must reference a registered bus, driver and route.
8. A bus must not be assigned to two trips with the same departure time.
9. A driver must not be assigned to two trips with the same departure time.
10. The application must allow users to view all scheduled trips.

Ticket Booking Requirements

1. A passenger must be registered before making a booking.
2. A booking must be associated with an existing scheduled trip.
3. A passenger must not have multiple active bookings for the same trip.
4. Each booking must have a unique identifier.
5. The selected seat number must be between 1 and the seating capacity of the assigned bus.
6. A seat already reserved by an active booking on the same trip must not be booked again.
7. The number of active bookings for a trip must not exceed the bus seating capacity.
8. A successful booking must reserve the selected seat.
9. An unsuccessful booking must not affect seat availability.
10. A newly created booking must have the status ACTIVE.
11. A cancelled booking must have the status CANCELLED.
12. Cancelling an active booking must release the reserved seat.
13. A booking that has already been cancelled must not be cancelled again.

Payment Processing Requirements

1. A payment must reference an existing booking.
2. Payment must only be processed for an active booking.
3. The payment amount must be equal to the ticket price of the route associated with the booked trip.
4. Payment amounts must be greater than zero.
5. The application must support CASH, MOBILE MONEY and CARD payment methods.
6. A booking must not receive more than one successful payment.
7. Successful payments must have the status PAID.
8. Failed payments must have the status FAILED.
9. An unsuccessful payment must not be recorded as successful.
10. The application must allow users to retrieve payment information using the associated booking.

SECTION C: VALIDATION, RETRY AND EXCEPTION HANDLING

The application must satisfy the following conditions:

1. All identifiers must be positive integers.
2. All required input values must not be null or empty.
3. Bus plate numbers must be unique and non-empty.
4. Bus seating capacity must be greater than zero.
5. Driver names must not contain numeric characters.
6. Driver ages must be between 21 and 65 years.
7. Driver license numbers must be unique and non-empty.
8. Passenger names must not contain numeric characters.
9. Passenger ages must be between 0 and 120 years.
10. Passenger email addresses must have a valid basic format.
11. Passenger phone numbers must contain exactly 10 digits.
12. Route departure and destination locations must not be identical.
13. Route distance must be greater than zero.
14. Ticket prices must be greater than zero.
15. A trip must not be scheduled using an unregistered bus, driver or route.
16. Booking identifiers must be unique.
17. Seat numbers must be valid for the assigned bus.
18. Duplicate active seat reservations for the same trip must not be accepted.
19. Payment identifiers must be unique.
20. Payment amounts must be valid and match the required ticket price.
21. Invalid menu selections must be handled appropriately.
22. Invalid numeric input must not terminate the application.
23. The user must be allowed to retry after entering invalid information.
24. The application must display meaningful error messages whenever validation fails.
25. Invalid operations must not modify previously registered information.

SECTION D: APPLICATION EXECUTION AND OUTPUT

The application must demonstrate the following operations:

1. Successful registration of multiple buses, drivers, routes and passengers.
2. Successful scheduling of trips using registered buses, drivers and routes.
3. Successful ticket booking for registered passengers.
4. Prevention of duplicate seat reservations.
5. Verification of available seats before accepting a booking.
6. Successful booking cancellation and restoration of seat availability.
7. Successful payment processing for an active booking.
8. Prevention of duplicate successful payments for the same booking.
9. Display of registered objects using their overridden toString() methods.
10. Searching for buses, drivers, passengers, trips and bookings.
11. Handling invalid input through validation and retry operations.
12. Continuous execution of the application until the user selects Exit.



