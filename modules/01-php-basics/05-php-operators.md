## PHP Operators
PHP operators are symbols to create mathematical, relational or logical operations.

### Arithmetic Operators
Arithmetic operators perform mathematical operations.

| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| + | Addition | $x + $y | Summation of $x and $y |
| - | Substraction | $x - $y | Difference of $x and $y |
| * | Multiplication | $x * $y | Product of $x and $y |
| / | Division | $x / $y | Quotient of $x and $y |
| % | Modulus | $x % $y | Remainder of $x divided by $y |
| ** | Exponentiation | $x ** $y | Raising $x to the power of $y |

```php
<?php
$a = 10;
$b = 3;

echo $a + $b; // 13
echo $a - $b; // 7
echo $a * $b; // 30
echo $a / $b; // 3.3333...
echo $a % $b; // 1
echo $a ** $b; // 1000
?>
```

### Assignment operators
Assignment operators assign values to a variable.

| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| = | Assign | $x = 5 | $x = 5 |
| += | Addition | $x += 5 | $x = $x + 5 |
| -= | Substraction | $x -= 5 | $x = $x - 5 |
| *= | Multiplication | $x *= 5 | $x = $x * 5 |
| /= | Division | $x /= 5 | $x = $x / 5 |
| %= | Modulus | $x %= 5 | $x = $x % 5 |
| .= | Concatenation | $x .= "text" | $x = $x . "text" |

```php
<?php
$x = 10;
$x += 5; // $x is now 15
$x -= 3; // $x is now 12
$x *= 2; // $x is now 24
$x /= 4; // $x is now 6
$x %= 4; // $x is now 2

$name = "David";
$name .= " Beckham"; // $name is now "David Beckham"
?>
```

### Comparison operators
Comparison operators compare two values and return a boolean (true or false).

| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| == | Equal | $x == $y | If $x is equal to $y, returns `true` |
| === | Identical | $x === $y | If $x is equal to $y and have the same type, returns `true` |
| != | Not equal | $x != $y | If $x is not equal to $y, returns `true` |
| <> | Not equal | $x <> $y | If $x is not equal to $y, returns `true` |
| !== | Not identical | $x !== $y | If $x is not equal to $y or they are just not having the same type, returns `true` |
| > | Greater than | $x > $y | If $x is greater than $y, returns `true` |
| < | Less than | $x < $y | If $x is less than $y, returns `true` |
| >= | Greater than or equal | $x >= $y | If $x is greater than or equal to $y, returns `true` |
| <= | Less than or equal | $x <= $y | If $x is less than or equal to $y, returns `true` |
| <=> | Spaceship | $x <=> $y | If $x < $y, returns `-1`, If $x == $y, returns `0`, if $x > $y, returns `1` |

```php
<?php
$a = 10;
$b = "10";
$c = 5;

var_dump($a == $b); // true
var_dump($a === $b); // false
var_dump($a != $c); // true
var_dump($a !== $c); // true
var_dump($a > $c); // true
var_dump($a < $c); // false
var_dump($a >= $b); // true
var_dump($a <=> $c); // 1
?>
```

### Logical Operators
Logical operators are used to combine conditional statements.

| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| and | And | $x and $y | True if both $x and $y are true |
| or | Or | $x or $y | True if either of $x or $y is true |
| xor | Exclusive or | $x xor $y | True if either $x or $y is true, but not both |
| ! | Not | !$x | True if $x is not true |
| && | And | $x && $y | True if both $x and $y are true |
| &#124;&#124; | Or | $x &#124;&#124; $y | True if either $x or $y is true |

```php
<?php
$a = true;
$b = false;

var_dump($a && $b); // false
var_dump($a || $b); // true
var_dump($a and $b); // false
var_dump($a or $b); // true
var_dump($a xor $b); // true
var_dump(!$a); // false

// Example
$user_is_logged_in = true;
$is_admin = false;

if ($user_is_logged_in && $is_admin) {
    echo "Welcome, Admin!";
} elseif ($user_is_logged_in) {
    echo "Welcome, User!";
} else {
    echo "Please log in.";
}
// Output - "Welcome User!"
?>
```
> **Note:** The `and` and `or` operators have lower priority than `&&` and `||`.
> It is safer to use `&&` and `||` to avoid unexpected behavior.

```php
<?php
// user input validation
$username = $_POST['username']; // get data from a form field
$password = $_POST['password']; // get data from a form field

// && is used here
$isValid = !empty($username) && strlen($password) >= 8;
if ($isValid) {
    // continue with login
}

// "and" is used here
$isValid = !empty($username) and strlen($password) >= 8;
// This will only be interpreted as ($isValid = !empty($username)) and strlen($password) >= 8
// So $isValid only takes care of !empty($username)
?>
```

### Increment/Decrement operators
Increment and decrement operators are used to increase or decrease the values of a variable.

| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| ++$x | Pre-increment | Increments $x by one, then returns $x |
| $x++ | Post-increment | Returns $x, then increment by one |
| --$x | Pre-decrement | Decrements $x by one, then returns $x |
| $x-- | Post-decrement | Returns $x, then decrements by one |

```php
<?php
$x = 5;
echo ++$x; // $x is incremented then returned as 6
echo $x; // 6

$y = 5;
echo $y++; // $y is returned as 5 then incremented
echo $y; // 6

$a = 5;
echo --$a; // $a is decremented and returned as 4
echo $a; // 4

$b = 5;
echo $b--; // $b is returned as 5 an decremented
echo $b; // 4
?>
```
