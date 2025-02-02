Each table enlisted in [[Tables List]] was tested manually, using preconfigured, exemplary function calls. The order of testing *is* actually important, as *vehicles* and *rentals* tables make use of foreign keys from *clients* and *vehicle_models*. Below works on predefined data already present in database dump.

### clients

```sql
--------- clients_add_user --------- 
SELECT clients_add_user (
  '123456890abcdef',
  'jhhnydoey@example.com',
  'Jon',
  'De',
  'DL13456',
  'hahed_password',
  '1980-01-01'
); -- OK

SELECT clients_add_user (
  '123456890abcdef',
  'jhhnydoey@example.com',
  'Jon',
  'De',
  'DL13456',
  'hahed_password',
  '1980-01-01'
); -- not OK, already exists

SELECT clients_add_user (
  '',
  'Jon',
  'De',
  'DL13456',
  'hahed_password',
  '1980-01-01'
); -- not OK

SELECT clients_add_user (
  '123456890abcdef',
  'jhhnydoey@example.com',
  'Jon',
  'De',
  'DL13456',
  'hahed_password',
  ''
); -- not OK 

SELECT clients_add_user (
  '123456890abcdef',
  'jhhnyexamplecom',
  'Jon',
  'De',
  'DL13456',
  'hahed_password',
  '1980-01-01'
); -- not OK

SELECT clients_add_user (
  '123456890abcdef',
  'jhhnyexamplecom',
  '',
  '',
  'DL13456',
  'hahed_password',
  '1980-01-01'
); -- not OK

SELECT clients_add_user (
  '123456890abcdef',
  'jhhnydoey@example.com',
  'Jon',
  'De',
  '',
  'hahed_password',
  '1980-01-01'
); -- not OK


SELECT clients_add_user (
  '123456890abcdef',
  'jhhnydoey@example.com',
  'Jon',
  'De',
  'DL13456',
  '',
  '1980-01-01'
); -- not OK

SELECT clients_add_user (
  '123456890abcdef',
  '',
  'Jon',
  'De',
  'DL13456',
  'hahed_password',
  '1980-01-01'
); -- not OK

--------- clients_user_authorized --------- 
SELECT clients_user_authorized(
  'jhhnydoey@example.com'
); -- OK

SELECT clients_user_authorized(
  'jhh'
); -- not OK

SELECT clients_user_authorized(
  'jhdoey@example.com'
); -- not OK, it does not exist in database

SELECT clients_user_authorized(
  ''
); -- not OK

--------- clients_email_verified --------- 
SELECT clients_email_verified(
  'jhhnydoey@example.com'
); -- OK

SELECT clients_email_verified(
  'jhh'
); -- not OK

SELECT clients_email_verified(
  'jhdoey@example.com'
); -- not OK, it does not exist in database

SELECT clients_email_verified(
  ''
); -- not OK

--------- clients_email_not_verified --------- 
SELECT clients_email_not_verified(
  'jhhnydoey@example.com'
); -- OK

SELECT clients_email_not_verified(
  'jhh'
); -- not OK

SELECT clients_email_not_verified(
  'jhdoey@example.com'
); -- not OK, it does not exist in database

SELECT clients_email_not_verified(
  ''
); -- not OK

--------- clients_remove_user --------- 
SELECT clients_remove_user(
  'jhhnydoey@example.com'
); -- OK

SELECT clients_remove_user(
  'jhhnydoey@example.com'
); -- not OK now, just removed

SELECT clients_remove_user(
  'jhh'
); -- not OK

SELECT clients_remove_user(
  'jhdoey@example.com'
); -- not OK, it does not exist in database

SELECT clients_remove_user(
  ''
); -- not OK

--------- clients_get_user_info --------- 
SELECT clients_get_user_info(
  'jane.smith@example.com'
); -- OK

SELECT clients_get_user_info(
  'r'
); -- not OK

SELECT clients_get_user_info(
  'janemith@example.com'
); -- not OK, does not exist

SELECT clients_get_user_info(
  ''
); -- not OK
```

### vehicle_models

```sql
--------- vehicle_models_add_vehicle_model --------- 
SELECT vehicle_models_add_vehicle_model(
  '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P',
  'Toyota',
  'Corolla',
  45.50,
  65.00,
  0.15,
  0.25
); -- OK 

SELECT vehicle_models_add_vehicle_model(
  '1A2B3C4D5E6F7G8H9I0J1M4N5O6P',
  'Toyota',
  'Corolla',
  45.50,
  65.00,
  0.15,
  0.25
); -- not OK 

SELECT vehicle_models_add_vehicle_model(
  '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P',
  '',
  '',
  45.50,
  65.00,
  0.15,
  0.25
); -- not OK 

SELECT vehicle_models_add_vehicle_model(
  '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P',
  'Toyota',
  'Corolla',
  45.50,
  65.00
); -- not OK 

--------- vehicle_models_update_vehicle_model --------- 
SELECT vehicle_models_update_vehicle_model(
 '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P', 'Toyoa', 'Coolla', 45.0, 65.00, 0.15, 0.25
); -- OK

SELECT vehicle_models_update_vehicle_model(
 '', 'Toyoa', 'Coolla', 45.0, 65.00, 0.15, 0.25
); -- not OK

SELECT vehicle_models_update_vehicle_model(
 '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P', '', 'Coolla', 45.0, 65.00, 0.15, 0.25
); -- not OK

SELECT vehicle_models_update_vehicle_model(
 '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P', 'Toyoa', 'Coolla', 45.0, 0.25
); -- not OK

SELECT vehicle_models_update_vehicle_model(
 'B3C4D5E6F7G8H9I0J1K2L3M4N5O6P', 'Toyoa', 'Coolla', 45.0, 65.00, 0.15, 0.25
); -- not OK

SELECT vehicle_models_update_vehicle_model(
 '99999999999F7G8H9I0J1K2L3M4N5O6P', 'Toyoa', 'Coolla', 45.0, 65.00, 0.15, 0.25
); -- not OK, does not exist

--------- vehicle_models_get_vehicle_model_info --------- 
SELECT vehicle_models_get_vehicle_model_info(
  '123e4567e89b12d3a456426655440011'
); -- OK

SELECT vehicle_models_get_vehicle_model_info(
  'e4567e89b12d3a456426655440011'
); -- not OK

SELECT vehicle_models_get_vehicle_model_info(
  ''
); -- not OK

--------- vehicle_models_delete_vehicle_model --------- 
SELECT vehicle_models_delete_vehicle_model(
 '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P'
); -- OK

SELECT vehicle_models_delete_vehicle_model(
 '1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P'
); -- not OK, just deleted

SELECT vehicle_models_delete_vehicle_model(
 '9999999999997G8H9I0J1K2L3M4N5O6P'
); -- not OK, does not exist

SELECT vehicle_models_delete_vehicle_model(
 ''
); -- not OK

```
### vehicles 

```sql
--------- vehicles_add_vehicle --------- 
SELECT vehicles_add_vehicle(
  '123e4567e89b12d3a456426655440111',
  '123e4567e89b12d3a456426655440014',
  'szmozooo',
  'K1BOLO',
  'fine as hell',
  99.999,
  99.999,
  2137
); -- OK

SELECT vehicles_add_vehicle(
  '123e4567e89b12d3a456426655440111',
  '123e4567e89b12d3a456426655440014',
  'szmozooo',
  'K1BOLO',
  'fine as hell',
  99.999,
  99.999,
  2137
); -- not OK, just added

SELECT vehicles_add_vehicle(
  '123e4567e89b12d3a55440111',
  '123e4567e89b12d3a456426655440014',
  'szmozooo',
  'K1BOLO',
  'fine as hell',
  99.999,
  99.999,
  2137
); -- not OK

SELECT vehicles_add_vehicle(
  '123e4567e89b12d3a456426655440111',
  '123e4567e89b12d3a456426999999999',
  'szmozooo',
  'K1BOLO',
  'fine as hell',
  99.999,
  99.999,
  2137
); -- not OK, model ID invalid

SELECT vehicles_add_vehicle(
  '123e4567e89b12d3a456426655440111',
  '123e4567e89b12d3a456426655440014',
  '',
  'K1BOLO',
  'fine as hell',
  99.999,
  99.999,
  2137
); -- not OK

SELECT vehicles_add_vehicle(
  '123e4567e89b12d3a456426655440111',
  '123e4567e89b12d3a456426655440014',
  'szmozooo',
  'K1BOLO',
  'fine as hell',
  99.999,
  2137
); -- not OK

--------- vehicles_update_vehicle_status --------- 
SELECT vehicles_update_vehicle_status(
  '123e4567e89b12d3a456426655440003',
  33.3333,
  -11.1111,
  'wankin',
  999
); -- OK

SELECT vehicles_update_vehicle_status(
  '4567e89b12d3a456426655440003',
  33.3333,
  -11.1111,
  'wankin',
  999
); -- not OK

SELECT vehicles_update_vehicle_status(
  '99999999999999999999426655440003',
  33.3333,
  -11.1111,
  'wankin',
  999
); -- not OK

SELECT vehicles_update_vehicle_status(
  '123e4567e89b12d3a456426655440003',
  -11.1111,
  'wankin',
  999
); -- not OK

SELECT vehicles_update_vehicle_status(
  '123e4567e89b12d3a456426655440003',
  33.3333,
  -11.1111,
  'wankin',
  -11
); -- not OK

--------- vehicles_assign_renter --------- 
SELECT vehicles_assign_renter(
  '123e4567e89b12d3a456426655440111',
  '123e4567e89b12d3a456426655440007'
); -- OK

SELECT vehicles_assign_renter(
  '',
  '123e4567e89b12d3a456426655440007'
); -- not OK

SELECT vehicles_assign_renter(
  '123e4567e89b12d3a456426655440111',
  ''
); -- not OK

SELECT vehicles_assign_renter(
  '99999567e89b12d3a456426655440111',
  '123e4567e89b12d3a456426655440007'
); -- not OK

SELECT vehicles_assign_renter(
  '123e4567e89b12d3a456426655440111',
  '00000007e89b12d3a456426655440007'
); -- not OK

SELECT vehicles_assign_renter(
  '123e4567e89b12d3a456426655440007'
); -- not OK

--------- vehicles_remove_renter --------- 
SELECT vehicles_remove_renter(
  '123e4567e89b12d3a456426655440111'
); -- OK

SELECT vehicles_remove_renter(
  '00000067e89b12d3a456426655440111'
); -- not OK

SELECT vehicles_remove_renter(
  'ivneifd'
); -- not OK

SELECT vehicles_remove_renter(
); -- not OK

--------- vehicles_get_vehicle_info --------- 
SELECT vehicles_get_vehicle_info(
  '123e4567e89b12d3a456426655440111'
); -- OK

SELECT vehicles_get_vehicle_info(
  '00000000089b12d3a456426655440111'
); -- not OK

SELECT vehicles_get_vehicle_info(
); -- not OK

SELECT vehicles_get_vehicle_info(
  '4567e89b12d3a456426655440111'
); -- not OK
```
### rentals
```sql
--------- create_rental --------- 
SELECT create_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    '123e4567e89b12d3a456426655440006',
    '123e4567e89b12d3a456426655440001',
    '2024-02-01 08:30:00',
    40.712776,
    -74.005974,
    'electric_scooter'
); -- OK

SELECT create_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    '123e4567e89b12d3a456426655440006',
    '123e4567e89b12d3a456426655440001',
    '2024-02-01 08:30:00',
    40.712776,
    -74.005974,
    'electric_scooter'
); -- not OK, vehicle in use

SELECT create_rental(
    '000000000fgh5678ijkl9012mnop3456',
    '123e4567e89b12d3a456426655440006',
    '123e4567e89b12d3a456426655440001',
    '2024-02-01 08:30:00',
    40.712776,
    -74.005974,
    'electric_scooter'
); -- not OK

SELECT create_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    'e4567e89b12d3a456426655440006',
    '123e4567e89b12d3a456426655440001',
    '2024-02-01 08:30:00',
    40.712776,
    -74.005974,
    'electric_scooter'
); -- not OK

SELECT create_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    '123e4567e89b12d3a456426655440006',
    '123e4567e89b12d3a456426655440001',
    '2024-02-01 08:30:00',
    -74.005974,
    'electric_scooter'
); -- not OK

SELECT create_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    '123e4567e89b12d3a456426655440006',
    '123e4567e89b12d3a456426655440001',
    '2024-02-01',
    40.712776,
    -74.005974,
    'electric_scooter'
); -- not OK

--------- end_rental --------- 
SELECT end_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    '2024-02-01 09:30:00',
    43.712776,
    -77.005974,
    420.69
); -- OK

SELECT end_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    '2024-02-01 09:30:00',
    43.712776,
    -77.005974,
    420.69
); -- not OK, just ended

SELECT end_rental(
    'abcd1234efgh567l9012mnop3456',
    '2024-02-01 09:30:00',
    43.712776,
    -77.005974,
    420.69
); -- not OK

SELECT end_rental(
    'abcd1234efgh5678ijkl9012mnop3456',
    '2024-02-01 09:30:00',
    -77.005974,
    420.69
); -- not OK

--------- get_rental_details --------- 
SELECT get_rental_details(
    'abcd1234efgh5678ijkl9012mnop3456'	
); -- OK

SELECT get_rental_details(
    '000000000fgh5678ijkl9012mnop3456'	
); -- not OK

SELECT get_rental_details(
); -- not OK

--------- list_active_rentals --------- 
-- always OK --

--------- list_rentals_by_client --------- 
-- always OK --

--------- mark_rental_as_paid --------- 
SELECT mark_rental_as_paid(
    'abcd1234efgh5678ijkl9012mnop3456'	
); -- OK

SELECT mark_rental_as_paid(
    'abcd1234efgh5678ijkl9012mnop3456'	
); -- not OK, already marked

SELECT mark_rental_as_paid(
    'efgh5678ijkl9012mnop3456'	
); -- not OK

SELECT mark_rental_as_paid(
); -- not OK

```