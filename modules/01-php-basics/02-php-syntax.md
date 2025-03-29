# Basic PHP Syntax
Let's take a look at the basic PHP syntax

## PHP tags
PHP codes are written inside `<?php` and `?>`. These are called opening (`<?php`) and close (`?>`) tags.

```php
<?php
    // php code
?>
```

PHP can be directly embedded inside HTML.

```php
<!DOCTYPE html>
<html>
<head>
    <title>PHP page</title>
</head>
<body>
        <h1>Welcome to PHP</h1>
        <?php
        echo "This is PHP code."
        ?>
</body>
</html>
```

## Showing Output
### 1. echo
It is the most commonly used method to output content.

```php
<?php
    echo "Hello World!";
    echo "<h1>Welcome to my page</h1>";
    echo "You can ", "concatenate ", "these ", "words.";
?>
```

### 2. print
The same as `echo` but it can only output one string and returns a value of (1).

```php
<?php
    print "Hello World!";
?>
```

## Comments in PHP
Like we give comments in Microsoft Word or Google docs, our code can also be commented to explain or take notes. Comments are skipped by the PHP interpreter.

### Single-line comments

```php
<?php
// This is a single line comment
echo "Hi"; // Single line comment can also be written at the end of the code
?>
```

### Multi-line comments
```php
<?php
/* This is a multi-line comment
   Can be written in more than 1 line
 */
echo "Hi";
?>
```

### Doc-style comments
PHP has a special comment format called PHPDoc. It helps in automatic documentation generation and modern IDE integration.

PHPDoc comments start with `/**` and end with `*/`.

```php
<?php
/**
 * This is a doc-style comment
 * @param string $name - it accepts a string parameter
 * @return string - it returns a string result
 */
function greet($name) {
    return "Hello, " . $name;
}
?>
```

Writing doc-style comments helps the devlopers easier to understand and modern IDEs like VSCode and PHPStorm provide autocomplete and hints based on the the PHPDoc comments.

PHP lacks type checking by default but writing PHPDoc comments helps in type checking.

## First PHP example
Let's create a simple "Hello World" PHP script.

1. Create a new file `hello.php` in your project folder which is `C:/xampp/htdocs`.
> If you use simple text editor like notpad, you can write your code and save the file as `hello.php` inside your project folder.

> We're going to use Visual Studio Code from now on. Open the project folder in VSCode. In the VSCode Explorer, click "New File" button to quickly create a new file and name it `hello.php`.

2. Write the following code.
> Please try to type the code yourself instead of copying to help you develop a muscle memory and better understand the context.

```php
<!DOCTYPE html>
<html>
<head>
    <title>My PHP page</title>
</head>
<body>
    <h1>Hello</h1>

    <?php
        // Output a simple message
        echo "<p>The current date and time is " . date('m-d-Y H:i:s') . "</p>";

        // Output the server info
        echo "<p>Your current PHP version is ". phpversion() . "</p>";
    ?>
</body>
</html>
```

Save this file and open this url from your browser `http://localhost/hello.php`.

## Summary
In this basic introduction, we have covered
* What is PHP
* Why PHP is suitable for web development and database applications
* The basic setup for PHP development
* Fundamental PHP syntax elements
* Creating a simple PHP script

In the next lesson, we will go deeper into PHP varaibles, data types and operators.

## Resources
[Official PHP documentation](https://www.php.net/docs.php)

[PHP The Right Way](https://phptherightway.com/)

[W3 School PHP tutorial](https://www.w3schools.com/php/)

## Exercises
1. Setup XAMPP on your computer and check it is working as expected.
2. Create simple PHP page that displays your name and current date.
3. Modify this page to include some information about yourself including HTML elements.
