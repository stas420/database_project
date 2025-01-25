### structure

The *vehicleModels* table stores information about various vehicle models and their associated rental pricing details:

| Field name          | Field type               | Description |
|---------------------|--------------------------|-------------|
| *modelID*           | **CHAR(32)** PRIMARY KEY | Unique identifier for each vehicle model. |
| *brandName*         | **TEXT** NOT NULL        | The brand name of the vehicle. |
| *modelName*         | **TEXT** NOT NULL; UNIQUE | The specific model name of the vehicle, ensuring no duplicates. |
| ==*vehicleType*==       | **TEXT** NOT NULL        | The type of vehicle (e.g., sedan, SUV, truck). |
| *pricePerDay*       | **DECIMAL(5,2)** NOT NULL | The rental price for a vehicle per day. |
| *priceForNoLimits*  | **DECIMAL(6,2)** NOT NULL | The rental price for a vehicle without any limits. |
| *pricePerMinute*    | **DECIMAL(4,2)** NOT NULL | The rental price for a vehicle per minute. |
| *pricePerKilometer* | **DECIMAL(4,2)** NOT NULL | The rental price for a vehicle per kilometer. |
| *recordCreated*     | **DATE** NOT NULL        | The date when the record was created. |
| *recordUpdated*     | **DATE** NOT NULL        | The date when the record was last updated. |

### functionalities

- ***addVehicleModel*** (CHAR(32) **modelID**, TEXT **brandName**, TEXT **modelName**, ==TEXT **vehicleType**,== DECIMAL(5,2) **pricePerDay**, DECIMAL(6,2) **priceForNoLimits**, DECIMAL(4,2) **pricePerMinute**, DECIMAL(4,2) **pricePerKilometer**) $\rightarrow$ BOOLEAN:
  - Adds a new vehicle model record to the table
  - returns TRUE if the new record is successfully inserted, FALSE otherwise
  
- ***updateVehicleModel*** (CHAR(32) **modelID**, TEXT **brandName**, TEXT **modelName**, ==TEXT **vehicleType**,== DECIMAL(5,2) **pricePerDay**, DECIMAL(6,2) **priceForNoLimits**, DECIMAL(4,2) **pricePerMinute**, DECIMAL(4,2) **pricePerKilometer**) $\rightarrow$ BOOLEAN:
  - Updates an existing vehicle model's information in the table, and refreshes the *recordUpdated* field
  - returns TRUE if the operation is successful, FALSE otherwise
  
- ***deleteVehicleModel*** (CHAR(32) **modelID**) $\rightarrow$ BOOLEAN:
  - Removes a vehicle model record from the table based on the given model ID.
  - returns FALSE if provided *modelID* does not already exist in table, TRUE otherwise
  
- ***getVehicleModelInfo*** (CHAR(32) **modelID**) $\rightarrow$ BOOLEAN or TEXT:
  - Retrieves all details for a specific vehicle model as a JSON-formatted string.
  - returns FALSE if provided *modelID* does not already exist in table
  
- ***listAllVehicleModels*** ():
  - Returns a list of all vehicle models stored in the table
  - ==should this be equal to SELECT \* FROM vehicle_models;?==