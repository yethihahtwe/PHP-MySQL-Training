# Introduction to PHP

## What is PHP?
PHP (Hypertext Preprocessor) is a commonly used scripting language specifically for web development. PHP scripts run on the web server and can generate HTML content delivered to the client's web browser.

## Key properties of PHP
PHP is a **server side language**. It means PHP codes run on the **web server**, not in the user's browser. PHP can generate **HTML output** which is rendered in client web browser. While PHP can generate HTML, it can be **written inside HTML** as well.  
PHP is free and open-source and has a large community of developers. It can eaily integrate with most databases especially **MySQL**.

## How PHP works

![PHP processing flow](../../resources/images/php-flow.png)

When a user opens a PHP page in their browser (or) when a php file is served to the user
1. The browser sends a request to the web server that I want to see this result.
2. The web server check the file being served to the user whether it contains php code.
3. If it contains PHP code, the PHP interpreter starts processing the file
4. The server sends the HTML output to the user's browser
5. The browser displays the HTML to the user

## Why learn PHP?
While PHP is one of the older web programming languages, it occupies the majority of websites on the internet and still adopted by OpenAI, Facebook and Wikipedia. The use of PHP is trending again after the emergence of frameworks such as Laravel and Symphony. Popular Content Management Systems such as Wordpress, Joomla and Learning Management Systems such as Moodle are developed with PHP.

PHP has a gentle learning curve compared to other languages. A new PHP learner can start with simple scripts followed by progressive development of advanced applications.

Since it can integrates with relational dababase management systems like MySQL, MariaDB and PostgreSQL, PHP is ideal for creating data-driven web-applications.

It is best suited for lean institutions which are required to launch the result fast and efficient without taking up the majority of the institution's resources due to the following reasons -
* It can handle user authentication and authorization
* Processes form submission and validates data
* Generate reports and data exports
* Create web interfaces for Create, Read, Update, Delete (CRUD) operations

## Setting up Development Environment
Since PHP is a server side language that runs on the web server, we need to turn our computer to work like a web server. We need to create a local development server to implement this. For this course, we will be using XAMPP.

XAMPP is a free and open-source local development server package including **X** - Cross platform which can be installed on Windows, Mac and Linux, **A** - Apache HTTP server, **M** - MySQL/MariaDB database, **P** - PHP, **P** - Perl.

Download XAMPP for Windows from this link: https://www.apachefriends.org/download.html

* Download XAMPP 8.2.12 (which is the current latest version)
* Double click to open the downloaded file. If you have a User Account Control (UAC) activated on your computer, you'll need to click OK when UAC warning appears.
* Click Next. Check default XAMPP components as it is. You might want to leave the installation location as the default `C:/xampp` but it is up to you to switch locations.
* After you click Finish, the XAMPP control panel will open. Close the XAMPP control panel for now as we're going to open it as administrator
* Click or press the Windows start button
* Type ***xampp***
* Click **Run as administrator**
* Click Yes when prompted

In the XAMPP control panel, make sure Apache and MySQL each has a green check mark next to them. If any of Apache and MySQL shows a red (x), check it to install first. Select Yes when prompted.

In order to develop PHP and MySQL database, you need these servers running. When you first open XAMPP control panel, Apache and MySQL might show a "Start" button on the right side. It means the servers are not running. Click "Start" buttons next to Apache and MySQL. When the text on the button is switched to "Stop", that means the servers are running.

Click "Admin" next to Apache. A browser tab will be opened and redirected to http://localhost/dashboard . Alternatively, you can directly visit this url on your browser.

Now, click "Admin" next to MySQL. The browser will open http://localhost/phpmyadmin . phpMyAdmin is where you can create or manage local databases.

### Troubleshooting
On some computers, apache will not start running due to a block port.
* Click "Config" on the right of Apache. 
* Click "Apache (httpd.conf)".
* Press Ctrl + F from your keyboard and type `listen 80`
* Replace 80 with other open port such as `81` or `9080`.
* Save and exit the text editor
* Restart XAMPP by clicking "Quit" button and run it again as Administrator
