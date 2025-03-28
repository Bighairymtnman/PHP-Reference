# PHP Basics Guide

## Table of Contents
- [Introduction to PHP](#introduction-to-php)
- [Setting Up PHP](#setting-up-php)
- [Basic Syntax](#basic-syntax)
- [Variables & Echo](#variables--echo)
- [Data Types In-Depth](#data-types-in-depth)
- [Working with Forms](#working-with-forms)
- [Basic Error Handling](#basic-error-handling)
- [Including Files](#including-files)


# PHP Basics Guide

## Table of Contents
- [Introduction to PHP](#introduction-to-php)
- [Setting Up PHP](#setting-up-php)
- [Basic Syntax](#basic-syntax)
- [Variables & Echo](#variables--echo)
- [Data Types In-Depth](#data-types-in-depth)
- [Working with Forms](#working-with-forms)
- [Basic Error Handling](#basic-error-handling)
- [Including Files](#including-files)

## Introduction to PHP

### What is PHP?
PHP (Hypertext Preprocessor) is a server-side scripting language designed specifically for web development. It runs on the web server, generating HTML that is then sent to the client.

### Why Use PHP?
- Easy to learn and use
- Large community support
- Extensive framework ecosystem
- Free and open source
- Works on various platforms
- Supports multiple databases
- Built-in security features

### How PHP Works
1. Browser sends request to server
2. Server runs PHP interpreter
3. PHP code executes and generates HTML
4. Server sends HTML back to browser
5. Browser displays the page





## Setting Up PHP

### Local Development Environment
1. **XAMPP Installation**
   - Download XAMPP from Apache Friends website
   - Includes PHP, Apache, MySQL, and more
   - Easy to set up and configure

2. **Directory Structure**
   ```
   xampp/
   └── htdocs/
       └── your-project/
           └── index.php
   ```

3. **Testing PHP Installation**
   Create a file named `info.php`:
   ```php
   <?php
   phpinfo();
   ?>
   ```
   Access via: `http://localhost/info.php`

### Basic Configuration
1. **php.ini Settings**
   - Error reporting
   - Memory limits
   - Upload sizes
   - Time zones

2. **Apache Configuration**
   - Document root
   - Virtual hosts
   - URL rewriting

### Development Tools
- Visual Studio Code with PHP extensions
- PHP Debug tools
- Code formatters
- Composer (Package Manager)






## Basic Syntax

### PHP Tags
// PHP code must be enclosed within PHP tags
```php
<?php
    // Your PHP code here
?>

// Short echo tag (if enabled)
<?= "Hello World" ?>
```

### Comments
```php
// Single line comment

# Alternative single line comment

/*
   Multi-line
   comment block
*/
```

### Statement Termination
```php
$name = "John";    // Statements end with semicolon
echo $name;        // Each statement on new line
```

### Code Blocks
```php
if (condition) {
    // Code block enclosed in curly braces
    statement1;
    statement2;
}
```

### Case Sensitivity
- Keywords (if, else, null, true) are NOT case-sensitive
- Variables ARE case-sensitive
- Functions are NOT case-sensitive (but use consistent casing)
```php
$color = "red";    // Different from $Color
$COLOR = "blue";   // Different from $color
echo strtoupper("hello");  // Same as STRTOUPPER()
```





## Variables & Echo

### Variable Basics
```php
// Variable naming rules
$validName    = "Starts with $, then letters/numbers/_";
$valid_name   = "Underscores are fine";
$validName2   = "Numbers okay, but not at start";
$this_is_long = "Descriptive names are good";

// Invalid names (don't do these)
$2invalid  = "Can't start with number";
$my-var    = "No hyphens allowed";
$my var    = "No spaces allowed";
```

### Echo and Print
```php
// Different ways to output text
echo "Hello World";              // Basic output
echo "Hello", " ", "World";      // Multiple parameters
print "Hello World";             // Alternative (single parameter)

// String concatenation
$first = "Hello";
$second = "World";
echo $first . " " . $second;     // Using dot operator

// Variable interpolation
$name = "John";
echo "Hello $name";              // Variables in double quotes
echo 'Hello $name';              // Single quotes don't interpolate
```

### Variable Scope
```php
// Global scope
$globalVar = "I'm global";

function testScope() {
    global $globalVar;           // Access global variable
    $localVar = "I'm local";     // Local scope
    
    echo $globalVar;             // Works with 'global'
    echo $GLOBALS['globalVar'];  // Alternative way
}
```



## Data Types In-Depth

### Strings
```php
// String Creation
$single = 'Single quoted';
$double = "Double quoted";
$heredoc = <<<EOD
Multiple lines
of text can go
here
EOD;

// String Functions
$str = "Hello World";
strlen($str);                // Length: 11
strtoupper($str);           // HELLO WORLD
strtolower($str);           // hello world
substr($str, 0, 5);         // Hello
str_replace("World", "PHP", $str); // Hello PHP
```

### Numbers
```php
// Integers
$int = 42;
$negative = -42;
$octal = 0755;             // Octal (starts with 0)
$hex = 0xFF;               // Hexadecimal
$binary = 0b1010;          // Binary

// Floats
$float = 3.14;
$scientific = 2.5e3;       // 2500
$scientific2 = 1E-10;      // 0.0000000001

// Number Functions
is_int($int);              // Check if integer
is_float($float);          // Check if float
round($float);             // Round number
ceil($float);              // Round up
floor($float);             // Round down
```

### Booleans
```php
$isTrue = true;
$isFalse = false;

// Type Casting to Boolean
$zero = 0;                 // false
$one = 1;                  // true
$emptyString = "";         // false
$nullValue = null;         // false
```






## Working with Forms

### HTML Form Basics
```php
<!-- Basic Form Structure -->
<form action="process.php" method="POST">
    <input type="text" name="username">
    <input type="password" name="password">
    <input type="submit" value="Submit">
</form>
```

### Processing Form Data
```php
// POST Method
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST['username'];
    $password = $_POST['password'];
    
    // Form validation
    if (empty($username)) {
        echo "Username is required";
    }
}

// GET Method
if (isset($_GET['search'])) {
    $searchTerm = $_GET['search'];
    // Process search
}
```

### Form Security
```php
// Sanitizing Input
$username = htmlspecialchars($_POST['username']);
$email = filter_var($_POST['email'], FILTER_SANITIZE_EMAIL);

// Validating Input
if (filter_var($email, FILTER_VALIDATE_EMAIL)) {
    echo "Valid email";
}

// Preventing XSS
$safeData = strip_tags($_POST['userInput']);
```




## Basic Error Handling

### Error Types
```php
// Common PHP Errors
Parse Error    // Syntax error in code
Fatal Error    // Serious error like undefined function
Warning        // Non-fatal error, script continues
Notice         // Runtime notice, script continues
```

### Try-Catch Blocks
```php
try {
    // Code that might throw an exception
    $result = divide(10, 0);
} catch (Exception $e) {
    // Handle the error
    echo "Error: " . $e->getMessage();
} finally {
    // Always executes
    echo "Process completed";
}
```

### Custom Error Handling
```php
// Set custom error handler
function customErrorHandler($errno, $errstr, $errfile, $errline) {
    echo "Error [$errno]: $errstr\n";
    echo "Line $errline in $errfile\n";
}

set_error_handler("customErrorHandler");

// Error logging
error_log("Database connection failed", 0);
```




## Including Files

### Include vs Require
```php
// Include - Warning on failure
include 'header.php';          // Warning if file not found
include_once 'config.php';     // Checks if already included

// Require - Fatal error on failure
require 'database.php';        // Fatal error if file not found
require_once 'functions.php';  // Checks if already required
```

### File Organization
```php
// Common file structure
project/
├── includes/
│   ├── header.php
│   ├── footer.php
│   └── nav.php
├── config/
│   └── database.php
└── index.php
```

### Practical Examples
```php
// Config file (config.php)
<?php
define('DB_HOST', 'localhost');
define('DB_USER', 'root');
define('DB_PASS', 'password');

// Using included files
<?php
require_once 'config/database.php';
include 'includes/header.php';
// Main content here
include 'includes/footer.php';
```

