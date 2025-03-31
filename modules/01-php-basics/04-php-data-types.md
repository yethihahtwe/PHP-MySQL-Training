## PHP Data Types
PHP is a loosely typed language. It means you don't need to mention the data type of a variable when you declare it. Based on the value you assign to the variable, PHP automatically converts the appropriate data type. But it is crucial to understand the data types before working with variables.

### Basic PHP data types
#### 1. String
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

#### 2. Integer
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

#### 3. Float (or Double)
Floats or Doubles are numbers with decimal places or in exponential form.

```php
<?php
$price = 19.99;
$scientific = 1.5e3; // 1500

// Check if a variable is a float
var_dump(is_float($price)); // return true
?>
```

#### 4. Boolean
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

#### 5. Array
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

#### 6. Object
Objects can store an entire PHP class. Objects can access a class's data as well as methods.

```php
<?php
// A class
class Person {
    // properties
    public $name;
    public $age;

    // methods
    function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
    }

    function introduce() {
        return "Hi, I am " . $this->name . " and I am " . $this->age . " years old.";
    }
}

// Create an object variable and assign properties at the same time
// This variable can now have access to the above class and its properties
$person1 = new Person("Mary", 30);

// Access properties
echo $person1->name; // Mary

// Access method. Since we are accessing methods, we need brackets ()
echo $person1->introduce(); // Hi, I am Mary and I am 30 years old.
?>
```

#### 7. NULL
A NULL variable does not have a value.

```php
<?php
$test = NULL;

// Check if the variable is NULL
var_dump(is_null($test)); // returns true

// Variables assigned NULL and unset variables behave similarly
$another_test = NULL;
unset($another_test);
?>
```

#### 8. Resources
Resources are special variables which reference external resources such as database connections or file handling.

```php
<?php
// A resource variable is created by opening a file
$file = fopen("example.txt", "r");

// Check if the variable is a resource
var_dump(is_resource($file)); // returns true

// Close the resource when the job is done
fclose($file);
?>
```

### Type Checking
Data type of a variable can be checked using the following PHP functions.

```php
<?php
$greeting = "Hello";

// Type checking functions
var_dump(is_string($greeting)); // returns true
var_dump(is_int($greeting)); // returns false
var_dump(is_float($greeting)); // returns false
var_dump(is_bool($greeting)); // returns false
var_dump(is_array($greeting)); // returns false
var_dump(is_object($greeting)); // returns false
var_dump(is_null($greeting)); // returns false
var_dump(is_resource($greeting)); // returns false

// Get the type of a variable
echo gettype($greeting); // string

// Display a detailed variable information
var_dump($greeting); // string(5) "Hello"
?>
```

### Type Casting
A variable's data type can be converted to another using type casting.

```php
<?php
// STRING TO INTEGER
$original = "123"; // string
$converted = (int)$original; // converted to integer
// alternative method
$converted = intval($original);

// INTEGER TO STRING
$original = 456;
$converted = (string)$original; // converted to string
// alternative method
$converted = strval($original);

// STRING TO FLOAT
$original = "3.14"; // string
$converted = (float)$original; // converted to float
// alternative method
$converted = floatval($original);

// OTHER TYPE CASTS
$test = 5; // integer
$float_test = (float)$test; // 5.0
$string_test = (string)$test; // "5"
$bool_test = (bool)$test; // true (any number other than 0 will return true)

$test = 0;
$bool_test = (bool)$test; // false

$greeting = "Hello"; // string
$bool_greeting = (bool)$greeting; // true (non-empty string values will return true)

$greeting = "";
$bool_greeting = (bool)$greeting; // false
?>
```

### Special Type Behaviour
#### Automatic type conversion
PHP automatically converts types accordingly.

```php
<?php
// Mathematical addition to string and number
$result = "10" + 20; // 30 (string 10 is converted to integer)

// String concatenation
$total = "Price: " . 199.99; // Price: 199.99

// A number can be used in conditions
$number = 42;
if ($number) {
    echo "This will execute because any non-zero numbers will return true";
}
?>
```

#### Loose comparison Versus Strict comparison
PHP has two types of comparison operators, loose comparison and strict comparison.

```php
<?php
$a = 42; // integer
$b = "42"; // string

// LOOSE COMPARISON - compares values after type conversion
var_dump($a == $b); // returns true

// STRICT COMPARISON - compares both value and type
var_dump($a === $b); // returns false because types are not the same
?>
```

## Best practices for working with data types
1. **Use strict comparison (`===`, `!==`) whenever possible.** This prevents unexpected issues resulting from automatic type conversion.

2. **Validate user input.** When working with user input values, always validate and sanitize data.

3. **Use type declaration in functions.**
```php
<?php
function add(int $a, int $b): int {
    return $a + $b;
}
?>
```

> While PHP's loose data typing may seem flexible, it can also lead to unexpected results if different data types interact each other.
