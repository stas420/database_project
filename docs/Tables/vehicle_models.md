### structure

The *vehicleModels* table stores information about various vehicle models and their associated rental pricing details:

| Field name            | Field type                | Description                                                     |
| --------------------- | ------------------------- | --------------------------------------------------------------- |
| *model_id*            | **CHAR(32)** PRIMARY KEY  | Unique identifier for each vehicle model.                       |
| *brand_name*          | **TEXT** NOT NULL         | The brand name of the vehicle.                                  |
| *model_name*          | **TEXT** NOT NULL; UNIQUE | The specific model name of the vehicle, ensuring no duplicates. |
| *vehicle_type*        | **TEXT** NOT NULL         | The type of vehicle (e.g., sedan, SUV, truck).                  |
| *price_per_day*       | **DECIMAL(5,2)** NOT NULL | The rental price for a vehicle per day.                         |
| *price_for_no_limits* | **DECIMAL(6,2)** NOT NULL | The rental price for a vehicle without any limits.              |
| *price_per_minute*    | **DECIMAL(4,2)** NOT NULL | The rental price for a vehicle per minute.                      |
| *price_per_kilometer* | **DECIMAL(4,2)** NOT NULL | The rental price for a vehicle per kilometer.                   |
| *record_created*      | **DATE** NOT NULL         | The date when the record was created.                           |
| *record_updated*      | **DATE** NOT NULL         | The date when the record was last updated.                      |

### functionalities

- ***add_vehicle_model*** (CHAR(32) **model_id**, TEXT **brand_name**, TEXT **model_name**, TEXT **vehicle_type**, DECIMAL(5,2) **price_per_day**, DECIMAL(6,2) **price_for_no_limits**, DECIMAL(4,2) **price_per_minute**, DECIMAL(4,2) **price_per_kilometer**) $\rightarrow$ BOOLEAN:
  - Adds a new vehicle model record to the table
  - returns TRUE if the new record is successfully inserted, FALSE otherwise
  
- ***updateVehicleModel*** (CHAR(32) **model_id**, TEXT **brand_name**, TEXT model_name, TEXT **vehicle_type**, DECIMAL(5,2) **price_per_day**, DECIMAL(6,2) **price_for_no_limits**, DECIMAL(4,2) **price_per_minute**, DECIMAL(4,2) **price_per_kilometer**) $\rightarrow$ BOOLEAN:
  - Updates an existing vehicle model's information in the table, and refreshes the *record_updated* field
  - returns TRUE if the operation is successful, FALSE otherwise
  
- ***deleteVehicleModel*** (CHAR(32) **model_id**) $\rightarrow$ BOOLEAN:
  - Removes a vehicle model record from the table based on the given model ID.
  - returns FALSE if provided *model_id* does not already exist in table, TRUE otherwise
  
- ***getVehicleModelInfo*** (CHAR(32) **model_id**) $\rightarrow$ BOOLEAN or TEXT:
  - Retrieves all details for a specific vehicle model as a JSON-formatted string.
  - returns FALSE if provided *model_id* does not already exist in table
  
- ***listAllVehicleModels*** ():
  - Returns a list of all vehicle models stored in the table