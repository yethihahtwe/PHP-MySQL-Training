# PHP Control Structures

Control structures help the application to make decisions and repeat tasks. Just like the traffic signals and road signs that control the traffic, PHP control structures can direct the flow of the application. They can decide which part of the code should run, when they should run and how many times to run.

## Conditional statements

We make decisions based on existing conditions in our daily lives. If it's raining, we get an umberella. Likewise, in programming, conditional statements can decide which code blocks should run based on whether a condition is true or false.

### `if` Statement

`if` statement runs a code block only if the condition is true.

```php
<?php
$age = 25;

if ($age >= 18) {
    echo "This person is an adult.";
}
?>
```

Only if the value is greater or equal to 18, the message will be displayed. Otherwise, none will return.

### `if-else` Statement

`if-else` statement enables to run a code block if a condition is true and another code block if false.

```php
<?php
$registration_status = "Pending";

if ($registration_status == 'Approved') {
    echo "Your registration has been approved.";
} else {
    echo "Your registration is still in process.";
}
?>
```

### `if-elseif-else` Statement

`if-elseif-else` statement allows to check multiple conditions and run codeblock based on their conditions.

```php
<?php
$client_age = 65;

if ($client_age < 18) {
    echo "Client is eligible for youth program.";
} elseif ($client_age >= 60) {
    echo "Client is eligible for elderly program.";
} else {
    echo "Client is eligible for adult program.";
}
?>
```

### `switch` Statement

The `switch` statement is similar to multiple `if-elseif-else` statements. It is commonly used to check a single variable value with multiple conditions.

```php
<?php
$department = "logistics";

switch ($department) {
    case "finance" :
        echo "Please dial ext. 201 for Finance department.";
        break;
    case "hr" :
        echo "Please dial ext. 202 for HR department.";
        break;
    case "logistics" :
        echo "Please dial ext. 203 for Logistics department.";
        break;
    default :
        echo "Please contact the operator for assistance.";
}
?>
```

The output is going to be "Please dial ext. 203 for Logistics department.".

It is important to add `break` statement in `switch`. If not added, PHP will continue executing the following code even though the condition does not match the cases.

The `default` is run when the value does not match any of the specified cases.

## Loops

Loops can run a code block repeatedly. Loops are commonly used to process items from an array or fetch records from a database table.

### `for` loop

If you already knew how many times you want to run a code block, a `for` loop can be used.

```php
<?php
for ($day = 1; $day <= 5; $day++) {
    echo "Day $day attendance tracking.<br />";
}
?>
```

This will display -
```
Day 1 attendance tracking.
Day 2 attendance tracking.
Day 3 attendance tracking.
Day 4 attendance tracking.
Day 5 attendance tracking.
```

A `for` loop contains 3 parts. The **initializing** (`$day = 1`) which specifies the starting point of the loop, the **condition** (`$day <= 5`) where the loop will continue till the condition is true, the **increment/decrement** (`$day++`) to update the counter after each loop iteration.


### `while` loop

The `while` loop runs a code block as long as the condition is true.

```php
<?
$remaining_clients = 5;

while ($remaining_clients > 0) {
    echo "Processing client number $remaining_clients.<br />";
    $remaining_clients--;
}
?>
```

This will display -
```
Processing client number 5.
Processing client number 4.
Processing client number 3.
Processing client number 2.
Processing client number 1.
```

In this example, the `while` loop will continue to execute as long as `$remaining_clients` is greater than `0`.

### `do while` loop

The `do while` loop is similar to `while` loop. But it runs the code block for once before checking the loop condition. The code inside `do while` loop will at least run once even if the loop condition is false.

```php
<?php
$remaining_clients = 5;

do {
    echo "Processing client number $remaining_clients.";
    $remaining_clients--;
} while ($remaining_clients > 5);
?>
```
In this example, even if the condition is false, the code block will run once and resulting in -
```
Processing client number 5.
```
