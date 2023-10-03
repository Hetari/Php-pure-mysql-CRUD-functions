# Php-CRUD-functions
Add :heavy_plus_sign:, delete ➖, update :recycle:, and select 🗒️

## array_flatten:
This function takes **an associative array** as input and returns a flattened array. Each key-value pair from the input array is transformed into two elements in the resulting array, where the key comes first followed by the value. The function iterates over each element in the input array and appends the key and value to the resulting array.

#### Parameters:
1. `$array` (array): The input associative array to be flattened.

#### Returns:
`Array`: an array containing the flattened key-value pairs from the input array.


## add:
This function is used to insert data into a specified database table. It takes a variable number of arguments, where each pair of arguments represents a column and its corresponding value. The function constructs an `SQL INSERT` statement dynamically based on the provided table name and arguments. It then prepares and executes the SQL statement using a PDO connection.
**Note The `$data` is an array that its keys the column name, and its value is the real data that we want to add it into our DB** 
```php
$data = [
  "name" => $name
]
```

#### Parameters:
1. `$table` (string): The name of the table where the data will be inserted.

2. `...$args` (mixed): Variable number of arguments representing column-value pairs.

#### Returns:
If the data insertion is successful, the function returns true. Otherwise, it returns false.



## select:
This function is used to retrieve data from a specified database table based on the provided conditions. It takes three parameters.

#### parameters:
1. `$table (string)`: The name of the table from which to select data.
2. `$conditions (array)`: Optional. An array of conditions to filter the data. Each condition is represented as an associative array with the column name as the key and the condition value as the value. The condition value can be a single value or an array containing the comparison operator and the value.
3. `$columns` (string): Optional. The columns to select from the table. By default, it selects all columns (*).

#### Returns:
If the SELECT query returns any rows, the function returns **an array of associative arrays representing the selected rows**. Each associative array represents a row, where the keys are the column names and the values are the corresponding values.

If no rows match the conditions, **an empty array is returned**.


## update:
This function is used to update data in a specified database table. It takes three 

#### parameters:
1. `$tableName` (string): The name of the table to update.
2. `$data` (array): An associative array where the keys represent the column names to be updated, and the values represent the new values for the corresponding columns.
3. `$conditions` (array): The value that identifies the row(s) to be updated. It can be a single value (like an ID) or an array of values.


#### Returns:
If the update operation is successful, the function returns **true**. Otherwise, it returns conditions.


## Delete:
This function is used to delete a record from a specified database table.


#### parameters:
1. `$tableName` (string): The name of the table from which to delete the record.
1. `$conditions` (like ID): The value that identifies the record to be deleted.

#### Returns
If the deletion is successful, the function returns **true**. Otherwise, it returns **false**.

 
# Usage Examples
## Call add function
```php
$data = [
  "name" => $name,
  "username" => $username,
  "email" => $email,
  "phone" => $phone,
  "password" => $password,
  "gender" => $gender
];

$results = add("users", ...array_flatten($data));
```
The add function is used to insert data into the "users" table. The $data array contains the column-value pairs for the data to be inserted. The array_flatten function is used to flatten the $data array and pass it as arguments to the add function. The return value of add is stored in the $results variable.

## Call select function
```php
$conditions = array(
    array("email" => ["=", $email]),
);
$results = select("users", $conditions, "*");
```
The select function is used to retrieve data from the "users" table based on the provided conditions. The $conditions array contains a single condition to match the "email" column with the provided value. 

## Call update function
```php
$data = [
  "Name" => $name,
  "Username" => $username,
  "Email" => $email,
  "Phone" => $phone,
  "Gender" => $gender,
  "Is_active" => $active,
  "Role_id" => $role,
  "Gender" => $gender
];
$results = update("users", $data, $id);
```

The update function is used to update data in the "users" table with the values specified in the $data array. The rows to be updated are identified by the value of $id.

## Call delete function
```php
$id = 123;
$result = deleteRecord("users", $id);

if ($result) {
  // Deletion was successful
  echo "Record deleted.";
} else {
  // Deletion failed
  echo "Error deleting record.";
}
```
