# lab5_assignment
#python file added to branch
class Flight:
    def __init__(self, flight_id, origin, destination, price):
        self.flight_id = flight_id
        self.origin = origin
        self.destination = destination
        self.price = price

class FlightDatabase:
    def __init__(self):
        self.flights = []

    def add_flight(self, flight):
        self.flights.append(flight)

    def search_flights_for_city(self, city):
        result = []
        for flight in self.flights:
            if flight.origin == city or flight.destination == city:
                result.append(flight)
        return result

    def search_flights_from_city(self, city):
        result = []
        for flight in self.flights:
            if flight.origin == city:
                result.append(flight)
        return result

    def search_flights_between_cities(self, city1, city2):
        result = []
        for flight in self.flights:
            if (flight.origin == city1 and flight.destination == city2) or \
               (flight.origin == city2 and flight.destination == city1):
                result.append(flight)
        return result

def main():
    flight_db = FlightDatabase()

    flight_data = [
        ("AI161E90", "BLR", "BOM", 5600),
        ("BR161F91", "BOM", "BBI", 6750),
        ("AI161F99", "BBI", "BLR", 8210),
        ("VS171E20", "JLR", "BBI", 5500),
        ("AS171G30", "HYD", "JLR", 4400),
        ("AI131F49", "HYD", "BOM", 3499)
    ]

    for data in flight_data:
        flight_db.add_flight(Flight(*data))

    while True:
        print("Search Options:")
        print("1. Flights for a particular City")
        print("2. Flights From a city")
        print("3. Flights between two given cities")
        print("4. Exit")

        choice = int(input("Enter your choice: "))

        if choice == 1:
            city = input("Enter the city: ")
            result = flight_db.search_flights_for_city(city)
        elif choice == 2:
            city = input("Enter the city: ")
            result = flight_db.search_flights_from_city(city)
        elif choice == 3:
            city1 = input("Enter the first city: ")
            city2 = input("Enter the second city: ")
            result = flight_db.search_flights_between_cities(city1, city2)
        elif choice == 4:
            print("Exiting the program.")
            break
        else:
            print("Invalid choice. Please choose a valid option.")
            continue

        if result:
            print("Flight ID | Origin | Destination | Price")
            print("-" * 40)
            for flight in result:
                print(f"{flight.flight_id} | {flight.origin} | {flight.destination} | {flight.price}")
        else:
            print("No flights found for the given search criteria.")

if __name__ == "__main__":
    main()
