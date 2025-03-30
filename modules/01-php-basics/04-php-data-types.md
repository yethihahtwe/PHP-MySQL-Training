## PHP Data Types
PHP is a loosely typed language. It means you don't need to mention the data type of a variable when you declare it. Based on the value you assign to the variable, PHP automatically converts the appropriate data type. But it is crucial to understand the data types before working with variables.

### Basic PHP data types
1. **String**
A string is a sequence of characters which can be enclosed with single quotes `'` or double quotes `"`.

```php
<?php
$name = "Harry Potter"; // double quoted
$address = '4 Pivet Drive'; // single quoted

// String can be concatenated with a dot (.) character
$full_text = $name . " lives at " . $address;
echo $full_text; // Harry Potter lives at 4 Pivet Drive

// String length
echo strlen($name); // 12

// Access a character on a specific index
echo $name[0]; // H
?>
```

2. **Integer**
Integers are whole numbers without a decimal point. Integers can be both positive and negative.

```php
<?php
$age = 25;
$negative_num = -10;

// var_dump checks data type of a variable
// is_int checks if the value is an integer
var_dump(is_int($age)); // return true

// Check maximum and minimum integer values that PHP can handle
echo PHP_INT_MAX; // maximum supported integer value
echo PHP_INT_MIN; // minimum support integer value
?>
```

3. **Float (or Double)**
Floats or Doubles are numbers with decimal places or in exponential form.

```php
<?php
$price = 19.99;
$scientific = 1.5e3; // 1500

// Check if a variable is a float
var_dump(is_float($price)); // return true
?>
```

4. **Boolean**
Booleans represent truth values and can be either `true` or `false`.

```php
<?php
$is_active = true;
$is_completed = false;

// Check if a variable is a boolean
var_dump(is_bool($is_active)); // return true

if ($is_active) {
    echo "The client is active.";
}
?>
```

5. **Array**
Arrays store multiple values in a single variable.

```php
<?php
$fruits = ["Apple", "Orange", "Banana"];

// Access array element with index
echo $fruits[0]; // Apple

// Associate arrays with key value pairs
$client = [
    "id" => 101,
    "name" => "Draco",
    "age" => 15
];

// Access associate array elements
echo $client["name"]; // Draco

// Multi-dimensional array
$services = [
    [
        "name" => "Primary Care",
        "provider_count" => 10
    ],
    [
        "name" => "Counselling",
        "provider_count" => 5
    ]
];

// Access multi-dimension array elements
echo $services[0]["name"]; // Primary Care
?>
```
