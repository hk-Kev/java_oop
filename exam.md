
import java.util.Scanner;

class Airport {
    private int airportId;
    private String airportName;
    private String airportCode;
    private String airportCity;
    private String airportCountry;

    public Airport(int airportId, String airportName, String airportCode,
                   String airportCity, String airportCountry) {
        setAirportId(airportId);
        setAirportName(airportName);
        setAirportCode(airportCode);
        setAirportCity(airportCity);
        setAirportCountry(airportCountry);
    }

    public int getAirportId() { return airportId; }
    public String getAirportName() { return airportName; }
    public String getAirportCode() { return airportCode; }
    public String getAirportCity() { return airportCity; }
    public String getAirportCountry() { return airportCountry; }

    public void setAirportId(int airportId) {
        if (airportId <= 0)
            throw new IllegalArgumentException("Airport ID must be positive.");
        this.airportId = airportId;
    }

    public void setAirportName(String airportName) {
        if (airportName == null || airportName.trim().isEmpty())
            throw new IllegalArgumentException("Airport name cannot be empty.");
        this.airportName = airportName.trim();
    }

    public void setAirportCode(String airportCode) {
        if (airportCode == null || airportCode.trim().isEmpty())
            throw new IllegalArgumentException("Airport code cannot be empty.");
        this.airportCode = airportCode.trim();
    }

    public void setAirportCity(String airportCity) {
        if (airportCity == null || airportCity.trim().isEmpty())
            throw new IllegalArgumentException("Airport city cannot be empty.");
        this.airportCity = airportCity.trim();
    }

    public void setAirportCountry(String airportCountry) {
        if (airportCountry == null || airportCountry.trim().isEmpty())
            throw new IllegalArgumentException("Airport country cannot be empty.");
        this.airportCountry = airportCountry.trim();
    }

    @Override
    public String toString() {
        return "Airport{id=" + airportId + ", name=" + airportName
                + ", code=" + airportCode + ", city=" + airportCity
                + ", country=" + airportCountry + "}";
    }
}

class Flight {
    private int flightId;
    private String flightNumber;
    private Airport departureAirport;
    private Airport destinationAirport;
    private int availableSeats;

    public Flight(int flightId, String flightNumber,
                  Airport departureAirport, Airport destinationAirport,
                  int availableSeats) {
        setFlightId(flightId);
        setFlightNumber(flightNumber);
        setDepartureAirport(departureAirport);
        setDestinationAirport(destinationAirport);
        setAvailableSeats(availableSeats);
    }

    public int getFlightId() { return flightId; }
    public String getFlightNumber() { return flightNumber; }
    public Airport getDepartureAirport() { return departureAirport; }
    public Airport getDestinationAirport() { return destinationAirport; }
    public int getAvailableSeats() { return availableSeats; }

    public void setFlightId(int flightId) {
        if (flightId <= 0)
            throw new IllegalArgumentException("Flight ID must be positive.");
        this.flightId = flightId;
    }

    public void setFlightNumber(String flightNumber) {
        if (flightNumber == null || flightNumber.trim().isEmpty())
            throw new IllegalArgumentException("Flight number cannot be empty.");
        this.flightNumber = flightNumber.trim();
    }

    public void setDepartureAirport(Airport departureAirport) {
        if (departureAirport == null)
            throw new IllegalArgumentException("Departure airport is required.");

        if (destinationAirport != null
                && departureAirport.getAirportId() == destinationAirport.getAirportId())
            throw new IllegalArgumentException("Airports must be different.");

        this.departureAirport = departureAirport;
    }

    public void setDestinationAirport(Airport destinationAirport) {
        if (destinationAirport == null)
            throw new IllegalArgumentException("Destination airport is required.");

        if (departureAirport != null
                && destinationAirport.getAirportId() == departureAirport.getAirportId())
            throw new IllegalArgumentException("Airports must be different.");

        this.destinationAirport = destinationAirport;
    }

    public void setAvailableSeats(int availableSeats) {
        if (availableSeats < 0)
            throw new IllegalArgumentException("Seats cannot be negative.");
        this.availableSeats = availableSeats;
    }

    @Override
    public String toString() {
        return "Flight{id=" + flightId + ", number=" + flightNumber
                + ", " + departureAirport.getAirportCode()
                + " -> " + destinationAirport.getAirportCode()
                + ", seats=" + availableSeats + "}";
    }
}

class Passenger {
    private int passengerId;
    private String passengerName;
    private String passengerEmail;
    private int passengerAge;
    private String passportNumber;

    public Passenger(int passengerId, String passengerName,
                     String passengerEmail, int passengerAge,
                     String passportNumber) {
        setPassengerId(passengerId);
        setPassengerName(passengerName);
        setPassengerEmail(passengerEmail);
        setPassengerAge(passengerAge);
        setPassportNumber(passportNumber);
    }

    public int getPassengerId() { return passengerId; }
    public String getPassengerName() { return passengerName; }
    public String getPassengerEmail() { return passengerEmail; }
    public int getPassengerAge() { return passengerAge; }
    public String getPassportNumber() { return passportNumber; }

    public void setPassengerId(int passengerId) {
        if (passengerId <= 0)
            throw new IllegalArgumentException("Passenger ID must be positive.");
        this.passengerId = passengerId;
    }

    public void setPassengerName(String passengerName) {
        if (passengerName == null || passengerName.trim().isEmpty())
            throw new IllegalArgumentException("Passenger name cannot be empty.");
        this.passengerName = passengerName.trim();
    }

    public void setPassengerEmail(String passengerEmail) {
        if (passengerEmail == null
                || !passengerEmail.contains("@")
                || !passengerEmail.contains("."))
            throw new IllegalArgumentException("Invalid email address.");
        this.passengerEmail = passengerEmail.trim();
    }

    public void setPassengerAge(int passengerAge) {
        if (passengerAge <= 0)
            throw new IllegalArgumentException("Age must be positive.");
        this.passengerAge = passengerAge;
    }

    public void setPassportNumber(String passportNumber) {
        if (passportNumber == null || passportNumber.trim().isEmpty())
            throw new IllegalArgumentException("Passport number cannot be empty.");
        this.passportNumber = passportNumber.trim();
    }

    @Override
    public String toString() {
        return "Passenger{id=" + passengerId + ", name=" + passengerName
                + ", email=" + passengerEmail + ", age=" + passengerAge
                + ", passport=" + passportNumber + "}";
    }
}

class AirlineEmployee {
    private int employeeId;
    private String employeeName;
    private String employeeEmail;
    private String employeePosition;
    private Airport airport;

    public AirlineEmployee(int employeeId, String employeeName,
                           String employeeEmail, String employeePosition,
                           Airport airport) {
        setEmployeeId(employeeId);
        setEmployeeName(employeeName);
        setEmployeeEmail(employeeEmail);
        setEmployeePosition(employeePosition);
        setAirport(airport);
    }

    public int getEmployeeId() { return employeeId; }
    public String getEmployeeName() { return employeeName; }
    public String getEmployeeEmail() { return employeeEmail; }
    public String getEmployeePosition() { return employeePosition; }
    public Airport getAirport() { return airport; }

    public void setEmployeeId(int employeeId) {
        if (employeeId <= 0)
            throw new IllegalArgumentException("Employee ID must be positive.");
        this.employeeId = employeeId;
    }

    public void setEmployeeName(String employeeName) {
        if (employeeName == null || employeeName.trim().isEmpty())
            throw new IllegalArgumentException("Employee name cannot be empty.");
        this.employeeName = employeeName.trim();
    }

    public void setEmployeeEmail(String employeeEmail) {
        if (employeeEmail == null
                || !employeeEmail.contains("@")
                || !employeeEmail.contains("."))
            throw new IllegalArgumentException("Invalid employee email.");
        this.employeeEmail = employeeEmail.trim();
    }

    public void setEmployeePosition(String employeePosition) {
        if (employeePosition == null || employeePosition.trim().isEmpty())
            throw new IllegalArgumentException("Employee position cannot be empty.");
        this.employeePosition = employeePosition.trim();
    }

    public void setAirport(Airport airport) {
        if (airport == null)
            throw new IllegalArgumentException("Employee airport is required.");
        this.airport = airport;
    }

    @Override
    public String toString() {
        return "Employee{id=" + employeeId + ", name=" + employeeName
                + ", email=" + employeeEmail + ", position=" + employeePosition
                + ", airport=" + airport.getAirportCode() + "}";
    }
}

class Booking {
    private int bookingId;
    private Passenger passenger;
    private Flight flight;
    private AirlineEmployee employee;
    private String bookingStatus;

    public Booking(int bookingId, Passenger passenger, Flight flight,
                   AirlineEmployee employee, String bookingStatus) {
        setBookingId(bookingId);
        setPassenger(passenger);
        setFlight(flight);
        setAirlineEmployee(employee);
        setBookingStatus(bookingStatus);
    }

    public int getBookingId() { return bookingId; }
    public Passenger getPassenger() { return passenger; }
    public Flight getFlight() { return flight; }
    public AirlineEmployee getAirlineEmployee() { return employee; }
    public String getBookingStatus() { return bookingStatus; }

    public void setBookingId(int bookingId) {
        if (bookingId <= 0)
            throw new IllegalArgumentException("Booking ID must be positive.");
        this.bookingId = bookingId;
    }

    public void setPassenger(Passenger passenger) {
        if (passenger == null)
            throw new IllegalArgumentException("Passenger is required.");
        this.passenger = passenger;
    }

    public void setFlight(Flight flight) {
        if (flight == null)
            throw new IllegalArgumentException("Flight is required.");
        this.flight = flight;
    }

    public void setAirlineEmployee(AirlineEmployee employee) {
        if (employee == null)
            throw new IllegalArgumentException("Employee is required.");
        this.employee = employee;
    }

    public void setBookingStatus(String bookingStatus) {
        if (bookingStatus == null
                || (!bookingStatus.equalsIgnoreCase("CONFIRMED")
                && !bookingStatus.equalsIgnoreCase("CANCELLED")))
            throw new IllegalArgumentException("Invalid booking status.");

        this.bookingStatus = bookingStatus.toUpperCase();
    }

    @Override
    public String toString() {
        return "Booking{id=" + bookingId + ", status=" + bookingStatus
                + "\n   " + passenger
                + "\n   " + flight
                + "\n   handledBy=" + employee.getEmployeeName() + "}";
    }
}

public class Main {
    static Scanner input = new Scanner(System.in);

    static Airport[] airports = new Airport[100];
    static Flight[] flights = new Flight[100];
    static Passenger[] passengers = new Passenger[100];
    static AirlineEmployee[] employees = new AirlineEmployee[100];
    static Booking[] bookings = new Booking[100];

    static int airportCount = 0;
    static int flightCount = 0;
    static int passengerCount = 0;
    static int employeeCount = 0;
    static int bookingCount = 0;

    public static void main(String[] args) {
        int choice;

        do {
            System.out.println("\n===== FLIGHT BOOKING MANAGEMENT SYSTEM =====");
            System.out.println("1. Register Airport");
            System.out.println("2. Register Flight");
            System.out.println("3. Register Passenger");
            System.out.println("4. Register Airline Employee");
            System.out.println("5. Book a Flight");
            System.out.println("6. Cancel a Booking");
            System.out.println("7. View All Airports");
            System.out.println("8. View All Flights");
            System.out.println("9. View All Passengers");
            System.out.println("10. View All Airline Employees");
            System.out.println("11. View All Bookings");
            System.out.println("12. Search Flight by Flight Number");
            System.out.println("13. Search Passenger by Passport Number");
            System.out.println("14. Search Booking by Booking ID");
            System.out.println("15. Check Available Seats");
            System.out.println("16. Exit");

            choice = readInt("Choose an option: ");

            switch (choice) {
                case 1: registerAirport(); break;
                case 2: registerFlight(); break;
                case 3: registerPassenger(); break;
                case 4: registerEmployee(); break;
                case 5: bookFlight(); break;
                case 6: cancelBooking(); break;
                case 7: viewAirports(); break;
                case 8: viewFlights(); break;
                case 9: viewPassengers(); break;
                case 10: viewEmployees(); break;
                case 11: viewBookings(); break;
                case 12: searchFlight(); break;
                case 13: searchPassenger(); break;
                case 14: searchBooking(); break;
                case 15: checkAvailableSeats(); break;
                case 16: System.out.println("Exiting system."); break;
                default: System.out.println("Invalid option. Try again.");
            }
        } while (choice != 16);

        input.close();
    }

    // Input methods

    static int readInt(String message) {
        while (true) {
            System.out.print(message);
            try {
                return Integer.parseInt(input.nextLine().trim());
            } catch (NumberFormatException e) {
                System.out.println("Enter a valid whole number.");
            }
        }
    }

    static int readPositiveInt(String message) {
        int value;
        do {
            value = readInt(message);
            if (value <= 0)
                System.out.println("Value must be positive.");
        } while (value <= 0);
        return value;
    }

    static int readNonNegativeInt(String message) {
        int value;
        do {
            value = readInt(message);
            if (value < 0)
                System.out.println("Value cannot be negative.");
        } while (value < 0);
        return value;
    }

    static String readText(String message) {
        String value;
        do {
            System.out.print(message);
            value = input.nextLine().trim();
            if (value.isEmpty())
                System.out.println("This field cannot be empty.");
        } while (value.isEmpty());
        return value;
    }

    static String readEmail(String message) {
        String email;
        do {
            email = readText(message);
            if (!email.contains("@") || !email.contains("."))
                System.out.println("Enter an email containing @ and a dot.");
        } while (!email.contains("@") || !email.contains("."));
        return email;
    }

    // Search methods

    static Airport findAirportById(int id) {
        for (int i = 0; i < airportCount; i++) {
            if (airports[i].getAirportId() == id)
                return airports[i];
        }
        return null;
    }

    static Flight findFlightById(int id) {
        for (int i = 0; i < flightCount; i++) {
            if (flights[i].getFlightId() == id)
                return flights[i];
        }
        return null;
    }

    static Flight findFlightByNumber(String number) {
        for (int i = 0; i < flightCount; i++) {
            if (flights[i].getFlightNumber().equalsIgnoreCase(number))
                return flights[i];
        }
        return null;
    }

    static Passenger findPassengerById(int id) {
        for (int i = 0; i < passengerCount; i++) {
            if (passengers[i].getPassengerId() == id)
                return passengers[i];
        }
        return null;
    }

    static Passenger findPassengerByPassport(String passport) {
        for (int i = 0; i < passengerCount; i++) {
            if (passengers[i].getPassportNumber().equalsIgnoreCase(passport))
                return passengers[i];
        }
        return null;
    }

    static AirlineEmployee findEmployeeById(int id) {
        for (int i = 0; i < employeeCount; i++) {
            if (employees[i].getEmployeeId() == id)
                return employees[i];
        }
        return null;
    }

    static Booking findBookingById(int id) {
        for (int i = 0; i < bookingCount; i++) {
            if (bookings[i].getBookingId() == id)
                return bookings[i];
        }
        return null;
    }

    // Registration operations

    static void registerAirport() {
        if (airportCount == airports.length) {
            System.out.println("Airport storage is full.");
            return;
        }

        int id = readPositiveInt("Airport ID: ");
        if (findAirportById(id) != null) {
            System.out.println("Airport ID already exists.");
            return;
        }

        String name = readText("Airport name: ");
        String code = readText("Airport code: ");
        String city = readText("City: ");
        String country = readText("Country: ");

        airports[airportCount] =
                new Airport(id, name, code, city, country);
        airportCount++;

        System.out.println("Airport registered successfully.");
    }

    static void registerFlight() {
        if (flightCount == flights.length) {
            System.out.println("Flight storage is full.");
            return;
        }

        if (airportCount < 2) {
            System.out.println("Register at least two airports first.");
            return;
        }

        int id = readPositiveInt("Flight ID: ");
        if (findFlightById(id) != null) {
            System.out.println("Flight ID already exists.");
            return;
        }

        String number = readText("Flight number: ");
        if (findFlightByNumber(number) != null) {
            System.out.println("Flight number already exists.");
            return;
        }

        int departureId = readPositiveInt("Departure airport ID: ");
        Airport departure = findAirportById(departureId);
        if (departure == null) {
            System.out.println("Departure airport is not registered.");
            return;
        }

        int destinationId = readPositiveInt("Destination airport ID: ");
        Airport destination = findAirportById(destinationId);
        if (destination == null) {
            System.out.println("Destination airport is not registered.");
            return;
        }

        if (departure.getAirportId() == destination.getAirportId()) {
            System.out.println("Departure and destination must differ.");
            return;
        }

        int seats = readNonNegativeInt("Available seats: ");

        flights[flightCount] =
                new Flight(id, number, departure, destination, seats);
        flightCount++;

        System.out.println("Flight registered successfully.");
    }

    static void registerPassenger() {
        if (passengerCount == passengers.length) {
            System.out.println("Passenger storage is full.");
            return;
        }

        int id = readPositiveInt("Passenger ID: ");
        if (findPassengerById(id) != null) {
            System.out.println("Passenger ID already exists.");
            return;
        }

        String name = readText("Passenger name: ");
        String email = readEmail("Passenger email: ");
        int age = readPositiveInt("Passenger age: ");
        String passport = readText("Passport number: ");

        if (findPassengerByPassport(passport) != null) {
            System.out.println("Passport number already exists.");
            return;
        }

        passengers[passengerCount] =
                new Passenger(id, name, email, age, passport);
        passengerCount++;

        System.out.println("Passenger registered successfully.");
    }

    static void registerEmployee() {
        if (employeeCount == employees.length) {
            System.out.println("Employee storage is full.");
            return;
        }

        if (airportCount == 0) {
            System.out.println("Register an airport first.");
            return;
        }

        int id = readPositiveInt("Employee ID: ");
        if (findEmployeeById(id) != null) {
            System.out.println("Employee ID already exists.");
            return;
        }

        String name = readText("Employee name: ");
        String email = readEmail("Employee email: ");
        String position = readText("Employee position: ");

        int airportId = readPositiveInt("Employee airport ID: ");
        Airport airport = findAirportById(airportId);

        if (airport == null) {
            System.out.println("Airport is not registered.");
            return;
        }

        employees[employeeCount] =
                new AirlineEmployee(id, name, email, position, airport);
        employeeCount++;

        System.out.println("Employee registered successfully.");
    }

    // Booking operations

    static void bookFlight() {
        if (bookingCount == bookings.length) {
            System.out.println("Booking storage is full.");
            return;
        }

        if (passengerCount == 0 || flightCount == 0 || employeeCount == 0) {
            System.out.println("Register a passenger, flight, and employee first.");
            return;
        }

        int id = readPositiveInt("Booking ID: ");
        if (findBookingById(id) != null) {
            System.out.println("Booking ID already exists.");
            return;
        }

        int passengerId = readPositiveInt("Passenger ID: ");
        Passenger passenger = findPassengerById(passengerId);
        if (passenger == null) {
            System.out.println("Passenger is not registered.");
            return;
        }

        int flightId = readPositiveInt("Flight ID: ");
        Flight flight = findFlightById(flightId);
        if (flight == null) {
            System.out.println("Flight is not registered.");
            return;
        }

        int employeeId = readPositiveInt("Employee ID: ");
        AirlineEmployee employee = findEmployeeById(employeeId);
        if (employee == null) {
            System.out.println("Employee is not registered.");
            return;
        }

        if (flight.getAvailableSeats() < 1) {
            System.out.println("Booking failed. No available seats.");
            return;
        }

        for (int i = 0; i < bookingCount; i++) {
            if (bookings[i].getPassenger().getPassengerId() == passengerId
                    && bookings[i].getFlight().getFlightId() == flightId
                    && bookings[i].getBookingStatus().equals("CONFIRMED")) {
                System.out.println("Passenger already has an active booking for this flight.");
                return;
            }
        }

        bookings[bookingCount] =
                new Booking(id, passenger, flight, employee, "CONFIRMED");
        bookingCount++;

        flight.setAvailableSeats(flight.getAvailableSeats() - 1);

        System.out.println("Booking successful.");
        System.out.println(bookings[bookingCount - 1]);
    }

    static void cancelBooking() {
        int id = readPositiveInt("Booking ID to cancel: ");
        Booking booking = findBookingById(id);

        if (booking == null) {
            System.out.println("Booking not found.");
            return;
        }

        if (booking.getBookingStatus().equals("CANCELLED")) {
            System.out.println("This booking is already cancelled.");
            return;
        }

        booking.setBookingStatus("CANCELLED");

        Flight flight = booking.getFlight();
        flight.setAvailableSeats(flight.getAvailableSeats() + 1);

        System.out.println("Booking cancelled successfully.");
    }

    // Listing operations

    static void viewAirports() {
        if (airportCount == 0) {
            System.out.println("No airports registered.");
            return;
        }

        for (int i = 0; i < airportCount; i++)
            System.out.println(airports[i]);
    }

    static void viewFlights() {
        if (flightCount == 0) {
            System.out.println("No flights registered.");
            return;
        }

        for (int i = 0; i < flightCount; i++)
            System.out.println(flights[i]);
    }

    static void viewPassengers() {
        if (passengerCount == 0) {
            System.out.println("No passengers registered.");
            return;
        }

        for (int i = 0; i < passengerCount; i++)
            System.out.println(passengers[i]);
    }

    static void viewEmployees() {
        if (employeeCount == 0) {
            System.out.println("No employees registered.");
            return;
        }

        for (int i = 0; i < employeeCount; i++)
            System.out.println(employees[i]);
    }

    static void viewBookings() {
        if (bookingCount == 0) {
            System.out.println("No bookings registered.");
            return;
        }

        for (int i = 0; i < bookingCount; i++)
            System.out.println(bookings[i]);
    }

    // Search operations

    static void searchFlight() {
        String number = readText("Enter flight number: ");
        Flight flight = findFlightByNumber(number);

        if (flight == null)
            System.out.println("Flight not found.");
        else
            System.out.println(flight);
    }

    static void searchPassenger() {
        String passport = readText("Enter passport number: ");
        Passenger passenger = findPassengerByPassport(passport);

        if (passenger == null)
            System.out.println("Passenger not found.");
        else
            System.out.println(passenger);
    }

    static void searchBooking() {
        int id = readPositiveInt("Enter booking ID: ");
        Booking booking = findBookingById(id);

        if (booking == null)
            System.out.println("Booking not found.");
        else
            System.out.println(booking);
    }

    static void checkAvailableSeats() {
        String number = readText("Enter flight number: ");
        Flight flight = findFlightByNumber(number);

        if (flight == null) {
            System.out.println("Flight not found.");
        } else {
            System.out.println("Flight: " + flight.getFlightNumber());
            System.out.println("Available seats: " + flight.getAvailableSeats());
        }
    }
}
