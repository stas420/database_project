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

- ***addVehicle*** (CHAR(32) **vehicleID**, CHAR(32) **modelID**, TEXT **vehicleColor**, TEXT **licensePlate**, TEXT **condition**, DECIMAL(9,6) **latitude**, DECIMAL(9,6) **longitude**, INT **mileage**) $\rightarrow$ BOOLEAN:
  - Adds a new vehicle record to the table
  - returns FALSE if provided vehicle ID already exists in the table, if provided model ID does not already exist in *vehicle_models*, or if any other argument is invalid/ill-formed; performs insert and returns TRUE otherwise
  
- ***updateVehicleStatus*** (CHAR(32) **vehicleID**, DECIMAL(9,6) **latitude**, DECIMAL(9,6) **longitude**, TEXT **condition**, INT **mileage**) $\rightarrow$ BOOLEAN:
  - Updates the location, condition, and mileage of a vehicle
  - returns FALSE if any argument is malformed or if vehicle ID does not exist, TRUE otherwise and if UPDATE is successful
  
- ***assignRenter*** (CHAR(32) **vehicleID**, CHAR(32) **currentRenterID**) $\rightarrow$ BOOLEAN:
  - Assigns a renter to a vehicle, marking it as currently rented, updates *lastRented* field
  - returns FALSE if both vehicle ID and current renter ID are either malformed or non-existent, TRUE otherwise
- ***removeRenter*** (CHAR(32) **vehicleID**) $\rightarrow$ BOOLEAN:
  - Clears the current renter field, marking the vehicle as available
  - assigns current renter ID to last renter ID, then assigns NULL to current renter ID, finally refreshes the *lastRented* timestamp
  
- ***getVehicleInfo*** (CHAR(32) **vehicleID**):
  - Retrieves all details for a specific vehicle as a JSON-formatted string.
  
- ***listAvailableVehicles*** ():
  - Returns a list of all vehicles that are not currently rented.
