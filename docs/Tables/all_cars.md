### structure


The *all_cars* table consists of all cars available in the car rental fleet, including details about the car, its model, and condition:

| Field name          | Field type                               | Description |
| :-------------------| :--------------------------------------- | :---------- |
| *CarID*             | **int(11)** AUTO_INCREMENT PRIMARY KEY   | Unique identifier for each car in the fleet. |
| *CarModel*          | **string(128)** NOT NULL                 | The model of the car. |
| *CarBrand*          | **string(128)** NOT NULL                 | The brand/manufacturer of the car. |
| *CarYear*           | **int(4)** NOT NULL                      | The year of manufacture of the car. |
| *CarColor*          | **string(32)** NOT NULL                  | The color of the car. |
| *CarType*           | **string(64)** NOT NULL                  | Type of the car (e.g., sedan, SUV, etc.). |
| *CarRegistration*   | **string(64)** NOT NULL UNIQUE           | The unique registration number of the car. |
| *CarCondition*      | **string(64)** NOT NULL                  | Current condition of the car (e.g., "new", "used", "maintenance"). |
| *CarPricePerDay*    | **decimal(10,2)** NOT NULL               | The rental price per day for the car. |
| *CarLocation*       | **string(128)** NOT NULL                 | The current location where the car can be rented from. |
| *CreatedAt*         | **timestamp** NOT NULL                   | Timestamp when the car entry was created. |

### functionalities

- ***addCar*** (string(128) **carModel**, string(128) **carBrand**, int(4) **carYear**, string(32) **carColor**, string(64) **carType**, string(64) **carRegistration**, string(64) **carCondition**, decimal(10,2) **carPricePerDay**, string(128) **carLocation**):
  - Adds a new car record to the *all_cars* table.
  - The database sets fields as follows: 
    ```CarModel = carModel, CarBrand = carBrand, CarYear = carYear, CarColor = carColor, CarType = carType, CarRegistration = carRegistration, CarCondition = carCondition, CarPricePerDay = carPricePerDay, CarLocation = carLocation, CreatedAt = getCurrentTime()```

- ***removeCar*** (int(11) **carID**):
  - Removes a car record from the *all_cars* table, based on the car's unique ID.

- ***getAllCars*** ():
  - Returns a list of all cars in the fleet as a *string in JSON format*.

- ***updateCarCondition*** (int(11) **carID**, string(64) **newCondition**):
  - Updates the condition of a car to a new state (e.g., "maintenance" to "available").
