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
