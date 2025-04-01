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

$name = "Severus";
$name .= " Snape"; // $name is now "Severus Snape"
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

