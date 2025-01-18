### structure

The *vehicles* table contains information about individual vehicles available for rent, including their current status and location:

| Field name           | Field type               | Description |
|----------------------|--------------------------|-------------|
| *vehicleID*          | **CHAR(32)** PRIMARY KEY | Unique identifier for each vehicle. |
| *modelID*            | **CHAR(32)** NOT NULL; FOREIGN KEY | Foreign key linking to the *vehicleModels* table. Identifies the vehicle model. |
| *currentRenterID*    | **CHAR(32)** FOREIGN KEY         | Foreign key linking to the *clients* table. Identifies the current renter of the vehicle. |
| *vehicleColor*       | **TEXT** NOT NULL        | The color of the vehicle. |
| *licensePlate*       | **TEXT** UNIQUE NOT NULL | The vehicle's license plate, ensuring uniqueness. |
| *condition*          | **TEXT** NOT NULL        | Describes the condition of the vehicle (e.g., "new", "good", "damaged"). |
| *latitude*           | **DECIMAL(9,6)** NOT NULL | The current latitude of the vehicle's location. |
| *longitude*          | **DECIMAL(9,6)** NOT NULL | The current longitude of the vehicle's location. |
| *mileage*            | **INT** NOT NULL CHECK (mileage >= 0) | The total mileage of the vehicle, ensuring a non-negative value. |
| *recordCreated*      | **DATE** NOT NULL        | The date when the vehicle record was created. |
| *lastRented*         | **TIMESTAMP**            | The timestamp of the last rental event. |
| *lastRenterID*       | **CHAR(32)** (FK)         | Foreign key linking to the *clients* table. Identifies the last person who rented the vehicle. |

### functionalities

- ***addVehicle*** (CHAR(32) **vehicleID**, CHAR(32) **modelID**, TEXT **vehicleColor**, TEXT **licensePlate**, TEXT **condition**, DECIMAL(9,6) **latitude**, DECIMAL(9,6) **longitude**, INT **mileage**):
  - Adds a new vehicle record to the table.
  
- ***updateVehicleStatus*** (CHAR(32) **vehicleID**, DECIMAL(9,6) **latitude**, DECIMAL(9,6) **longitude**, TEXT **condition**, INT **mileage**):
  - Updates the location, condition, and mileage of a vehicle.
  
- ***assignRenter*** (CHAR(32) **vehicleID**, CHAR(32) **currentRenterID**):
  - Assigns a renter to a vehicle, marking it as currently rented.
  
- ***removeRenter*** (CHAR(32) **vehicleID**):
  - Clears the current renter field, marking the vehicle as available.
  
- ***getVehicleDetails*** (CHAR(32) **vehicleID**):
  - Retrieves all details for a specific vehicle as a JSON-formatted string.
  
- ***listAvailableVehicles*** ():
  - Returns a list of all vehicles that are not currently rented.
