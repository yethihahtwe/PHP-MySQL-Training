## Variables in PHP
Variables are containers which can store data values. PHP variables don't need to be declared before they are used. A PHP variable can be declared at the time when a value is going to be assigned to it.

All PHP variables must start with a dollar sign `$`. Variable names are case-sensitive which means `$name` and `$Name` are different variables.

### Naming rules
* A PHP variable must start with a dollar sign `$`.
* After the dollar sign, only letters and an underscore `_` can be followed. Not numbers and a hyphen `-`.
* Can only include alphanumeric characters and underscore (a to z, 0 to 9 and _).
* Cannot contain spaces
* Case-sensitive

```php
<?php
// valid variable names
$name = "Harry";
$age = 25;
$_user = "admin";
$firstName = "Harry";
$last_name = "Potter";
$friend1 = "Ron";

// invalid variable names
// $1friend = "Ron";
// $user-name = "Tom";
// $user name = "Voldermort";
?>
```

### Assigning values
Values can be assigned to the variables using assignment operator `=`. For the very beginners, we read it ***assign***, we don't read it equal.

```php
<?php
$username = "admin";
$age = 30;
$price = 20.00;
$is_active = true;
?>
```
Notice that we have a value in double quotes while others don't? We'll talk about that in the next topic.

#### String interpolation
When you assign a value to a variable using double quotes `"`, PHP treats it as a string variable. This is called string interpolation.

```php
<?php
$name = "Harry";
echo "Hello, $name!"; // Hello Harry

// can also use curly braces
$product = "database";
echo "This {$product}_system is working"; // This database system is working
?>
```
A pair of single quotes `'` can also be used instead of double quotes `"`. But variable names written in single quotes are treated as text, not as variables.

```php
<?php
$name = "Harry";
echo 'Hello, $name!'; // Hello $name
?>
```

### Variable variables
PHP has variable variables. It allows a value of one variable to be a name for another variable.

```php
<?php
$client = "patient";
$$client = "Hermione"; // creating a variable $patient with a value "Hermione"

echo $client; // patient
echo $$client; // Hermione
echo $patient; // Hermione
?>
```

This feature is less commonly used in everyday programming but it is good to know.

### Best practices for using variables
1. **Give variable names meaningful**
Variable names should be given to represent the value they store.

```php
<?php
// Good variable name
$client_age = 25;

// Not quite good
$ca = 25;
?>
```

2. **Consistent naming convention**
variable names and functions should be given in consistent manner. The following naming conventions are commonly used in PHP.

* `$snake_case` - recommended for PHP
* `$camelCase` - common in PHP
* `$PascalCase` - usually given to class names rather than variables

3. **Initialize variables before using**
```php
<?php
$total = 0;
// Now you can safely use $total in subsequent calculations
?>
```

4. **Avoid global variables whenever possible**
Global variables are variables than can be accessed from anywhere of your PHP script. They are not commonly used in professional projects as they can make the code harder to understand, test and maintain.
