### structure

The *rentals* table records details about vehicle rentals, including the renter, the vehicle, and the rental duration and cost:

| Field name        | Field type                                          | Description                                                                 |
| ----------------- | --------------------------------------------------- | --------------------------------------------------------------------------- |
| *rental_id*       | **CHAR(32)** PRIMARY KEY                            | Unique identifier for each rental record.                                   |
| *client_id*       | **CHAR(32)** NOT NULL (FK)                          | Foreign key linking to the *clients* table. Identifies the renter.          |
| *vehicle_id*      | **CHAR(32)** NOT NULL (FK)                          | Foreign key linking to the *vehicles* table. Identifies the rented vehicle. |
| *start_time*      | **TIMESTAMP** NOT NULL                              | The timestamp when the rental started.                                      |
| *start_latitude*  | **DECIMAL(9,6)** NOT NULL                           | The latitude of the vehicle's location at the start of the rental.          |
| *start_longitude* | **DECIMAL(9,6)** NOT NULL                           | The longitude of the vehicle's location at the start of the rental.         |
| *end_time*        | **TIMESTAMP**                                       | The timestamp when the rental ended.                                        |
| *end_latitude*    | **DECIMAL(9,6)**                                    | The latitude of the vehicle's location at the end of the rental.            |
| *end_longitude*   | **DECIMAL(9,6)**                                    | The longitude of the vehicle's location at the end of the rental.           |
| *rental_type*     | **TEXT** NOT NULL                                   | The type of rental pricing used.                                            |
| *charge*          | **DECIMAL(7,2)** NOT NULL CHECK (rentalCharge >= 0) | The total charge for the rental, ensuring a non-negative value.             |
| *is_paid*         | **BOOLEAN** NOT NULL                                | Indicates whether the rental charge has been paid.                          |

### functionalities

- ***create_rental*** (CHAR(32) **rental_id**, CHAR(32) **client_id**, CHAR(32) **vehicleID**, TIMESTAMP **start_time**, DECIMAL(9,6) **start_latitude**, DECIMAL(9,6) **start_longitude**, TEXT **rental_type**) $\rightarrow$  BOOLEAN:
  - Creates a new rental record in the table with the specified details.
  
- ***end_rental*** (CHAR(32) **rental_id**, TIMESTAMP **end_time**, DECIMAL(9,6) **end_latitude**, DECIMAL(9,6) **end_longitude**, DECIMAL(7,2) **charge**) $\rightarrow$  BOOLEAN:
  - Updates the rental record with the end time, end location, and calculated rental charge.
  
- ***mark_rental_as_paid*** (CHAR(32) **rental_id**)  $\rightarrow$  BOOLEAN:
  - Marks the rental as paid by setting the *is_paid* field to `true`.
  
- ***get_rental_details*** (CHAR(32) **rental_id**) $\rightarrow$  TEXT:
  - Retrieves all details for a specific rental as a JSON-formatted string.
  
- ***list_active_rentals*** () $\rightarrow$  TABLE:
  - Returns a list of all ongoing rentals (i.e., rentals where *end_time* is `NULL`).
  
- ***list_rentals_by_client*** (CHAR(32) **client_id**) SETOF rentals:
  - Returns a list of all rentals associated with a specific renter.
