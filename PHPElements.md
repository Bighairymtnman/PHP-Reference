# PHP Elements Quick Reference

## Table of Contents
- [Variables & Data Types](#variables--data-types)
- [Operators](#operators)
- [Control Structures](#control-structures)
- [Functions](#functions)
- [Arrays](#arrays)
- [Superglobals](#superglobals)

## Variables & Data Types

### Variable Declaration
```php
// PHP variables start with $ symbol
$variableName = value;

// Multiple declarations
$a = 1;
$b = 2;
$c = 3;
```

### Basic Data Types
```php
// String
$text = "Hello World";    // Text enclosed in quotes
$template = "Hello $name"; // Variable interpolation

// Number
$integer = 42;            // Whole numbers
$float = 3.14;           // Decimal numbers

// Boolean
$isTrue = true;          // true or false
$isFalse = false;

// Null
$empty = null;           // No value assigned

// Array
$array = [1, 2, 3];      // Collection of values

// Object
$obj = new stdClass();   // Instance of a class
```

## Operators

### Arithmetic Operators
```php
// Basic Math
$sum = 5 + 3;      // Addition
$diff = 10 - 4;    // Subtraction
$product = 3 * 6;  // Multiplication
$quotient = 15 / 3;// Division
$remainder = 17 % 5;// Modulus
$power = 2 ** 3;   // Exponentiation
```

### Assignment Operators
```php
$x = 5;            // Basic assignment
$x += 3;           // Same as: $x = $x + 3
$x -= 2;           // Same as: $x = $x - 2
$x *= 4;           // Same as: $x = $x * 4
$x /= 2;           // Same as: $x = $x / 2
$x %= 3;           // Same as: $x = $x % 3
$x **= 2;          // Same as: $x = $x ** 2
```

### Comparison Operators
```php
// Regular comparison
5 > 3              // Greater than
5 < 3              // Less than
5 >= 3             // Greater than or equal
5 <= 3             // Less than or equal

// Equality
5 == "5"           // Equal (with type coercion)
5 === "5"          // Strictly equal (no type coercion)
5 != "5"           // Not equal
5 !== "5"          // Strictly not equal
```

### Logical Operators
```php
// AND, OR, NOT
$a && $b           // Logical AND
$a || $b           // Logical OR
!$a                // Logical NOT

// Alternative syntax
$a and $b          // Alternative AND
$a or $b           // Alternative OR
$a xor $b          // Exclusive OR
```

## Control Structures

### If Statements
```php
// Basic if
if (condition) {
    // code
}

// If-else
if (condition) {
    // code
} else {
    // code
}

// If-else if-else
if (condition1) {
    // code
} elseif (condition2) {
    // code
} else {
    // code
}
```

### Switch Statement
```php
switch ($variable) {
    case value1:
        // code
        break;
    case value2:
        // code
        break;
    default:
        // code
}
```

### Loops
```php
// For loop
for ($i = 0; $i < 5; $i++) {
    // code
}

// While loop
while (condition) {
    // code
}

// Do-while loop
do {
    // code
} while (condition);

// Foreach loop
foreach ($array as $value) {
    // code
}

// Foreach with key
foreach ($array as $key => $value) {
    // code
}
```

## Functions

### Function Declarations
```php
// Basic function
function greet($name) {
    return "Hello, $name!";
}

// Function with default parameters
function greet($name = "User") {
    return "Hello, $name!";
}

// Type declarations (PHP 7+)
function add(int $a, int $b): int {
    return $a + $b;
}

// Anonymous function
$multiply = function($a, $b) {
    return $a * $b;
};

// Arrow function (PHP 7.4+)
$multiply = fn($a, $b) => $a * $b;
```

### Built-in Functions
```php
// String Functions
strlen($str);              // Get string length
str_replace($search, $replace, $subject);
substr($string, $start, $length);

// Array Functions
count($array);            // Count elements
array_push($array, $value);
array_pop($array);
sort($array);

// Math Functions
round($number);           // Round number
rand($min, $max);         // Random number
max($value1, $value2);    // Highest value
min($value1, $value2);    // Lowest value
```

## Arrays

### Array Types
```php
// Indexed Arrays
$fruits = ["apple", "banana", "orange"];
$numbers = [1, 2, 3, 4, 5];

// Associative Arrays
$age = [
    "Peter" => 35,
    "Ben" => 37,
    "Joe" => 43
];

// Multidimensional Arrays
$matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];
```

### Array Operations
```php
// Adding Elements
$array[] = $value;              // Add to end
array_push($array, $value);     // Add to end
array_unshift($array, $value);  // Add to beginning

// Removing Elements
array_pop($array);             // Remove from end
array_shift($array);           // Remove from beginning
unset($array[$index]);         // Remove specific element
```

### Array Functions
```php
// Common Array Functions
count($array);                 // Count elements
array_merge($array1, $array2); // Merge arrays
array_slice($array, $offset);  // Extract portion
array_splice($array, $offset); // Remove/replace portion
array_search($needle, $array); // Search array
in_array($needle, $array);     // Check if exists
array_key_exists($key, $array);// Check key exists
```

## Superglobals

### Key Superglobal Variables
```php
// GET and POST
$_GET['param'];     // URL parameters
$_POST['field'];    // Form data

// Session and Cookies
session_start();
$_SESSION['user'];  // Session data
$_COOKIE['name'];   // Cookie data

// Server Information
$_SERVER['PHP_SELF'];       // Script name
$_SERVER['SERVER_NAME'];    // Server name
$_SERVER['REQUEST_METHOD']; // GET or POST

// File Uploads
$_FILES['file']['name'];    // Uploaded filename
$_FILES['file']['type'];    // File type
$_FILES['file']['size'];    // File size

// Environment and Globals
$_ENV['PATH'];             // Environment variable
$GLOBALS['variable'];      // Global scope access
```
