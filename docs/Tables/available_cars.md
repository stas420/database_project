### structure

The *available_cars* table consists of cars that are currently available for rent, allowing clients to view what is rentable at a given time:

| Field name          | Field type                               | Description |
| :-------------------| :--------------------------------------- | :---------- |
| *CarID*             | **int(11)** NOT NULL, FOREIGN KEY        | Unique identifier for the car, linked to the *CarID* in the *all_cars* table. |
| *AvailabilityStatus*| **boolean** NOT NULL                     | Whether the car is available for rent (true = available, false = rented). |
| *AvailableFrom*     | **date(DD-MM-YYYY)** NOT NULL            | The date when the car becomes available for rent. |
| *AvailableUntil*    | **date(DD-MM-YYYY)** NOT NULL            | The date until the car is available for rent. |

### functionalities

- ***addAvailableCar*** (int(11) **carID**, date(DD-MM-YYYY) **availableFrom**, date(DD-MM-YYYY) **availableUntil**):
  - Adds an entry to the *available_cars* table to specify a car’s rental availability.
  - The database sets *AvailabilityStatus = true*, marking the car as available for rent within the given date range.

- ***removeAvailableCar*** (int(11) **carID**):
  - Removes an entry from the *available_cars* table, marking the car as unavailable.

- ***updateAvailabilityStatus*** (int(11) **carID**, boolean **newStatus**):
  - Updates the availability status of a car to either available (true) or unavailable (false).

- ***getAvailableCars*** ():
  - Returns a list of cars that are currently available for rent, as a *string in JSON format*.

- ***getCarAvailability*** (int(11) **carID**):
  - Retrieves the availability information for a specific car by its ID.
