### structure

The *rentals* table records details about vehicle rentals, including the renter, the vehicle, and the rental duration and cost:

| Field name         | Field type                                         | Description |
|--------------------|----------------------------------------------------|-------------|
| *rentalID*         | **CHAR(32)** PRIMARY KEY                          | Unique identifier for each rental record. |
| *renterID*         | **CHAR(32)** NOT NULL (FK)                        | Foreign key linking to the *clients* table. Identifies the renter. |
| *vehicleID*        | **CHAR(32)** NOT NULL (FK)                        | Foreign key linking to the *vehicles* table. Identifies the rented vehicle. |
| *startTime*        | **TIMESTAMP** NOT NULL                            | The timestamp when the rental started. |
| *startLatitude*    | **DECIMAL(9,6)** NOT NULL                         | The latitude of the vehicle's location at the start of the rental. |
| *startLongitude*   | **DECIMAL(9,6)** NOT NULL                         | The longitude of the vehicle's location at the start of the rental. |
| *endTime*          | **TIMESTAMP**                                     | The timestamp when the rental ended. |
| *endLatitude*      | **DECIMAL(9,6)**                                  | The latitude of the vehicle's location at the end of the rental. |
| *endLongitude*     | **DECIMAL(9,6)**                                  | The longitude of the vehicle's location at the end of the rental. |
| *rentalType*       | **ENUM('perDay', 'perMinute', 'perKilometer', 'noLimits')** NOT NULL | The type of rental pricing used. |
| *rentalCharge*     | **DECIMAL(7,2)** NOT NULL CHECK (rentalCharge >= 0) | The total charge for the rental, ensuring a non-negative value. |
| *isPaid*           | **BOOLEAN** NOT NULL                              | Indicates whether the rental charge has been paid. |

### functionalities

- ***createRental*** (CHAR(32) **rentalID**, CHAR(32) **renterID**, CHAR(32) **vehicleID**, TIMESTAMP **startTime**, DECIMAL(9,6) **startLatitude**, DECIMAL(9,6) **startLongitude**, ENUM **rentalType**):
  - Creates a new rental record in the table with the specified details.
  
- ***endRental*** (CHAR(32) **rentalID**, TIMESTAMP **endTime**, DECIMAL(9,6) **endLatitude**, DECIMAL(9,6) **endLongitude**, DECIMAL(7,2) **rentalCharge**):
  - Updates the rental record with the end time, end location, and calculated rental charge.
  
- ***markAsPaid*** (CHAR(32) **rentalID**):
  - Marks the rental as paid by setting the *isPaid* field to `true`.
  
- ***getRentalDetails*** (CHAR(32) **rentalID**):
  - Retrieves all details for a specific rental as a JSON-formatted string.
  
- ***listActiveRentals*** ():
  - Returns a list of all ongoing rentals (i.e., rentals where *endTime* is `NULL`).
  
- ***listRentalsByRenter*** (CHAR(32) **renterID**):
  - Returns a list of all rentals associated with a specific renter.
