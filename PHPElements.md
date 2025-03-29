# PHP Elements Quick Reference

## Table of Contents
- [Variables & Data Types](#variables--data-types)
- [Operators](#operators)
- [Control Structures](#control-structures)
- [Functions](#functions)
- [Arrays](#arrays)
- [Superglobals](#superglobals)


## Variables & Data Types

// Variables in PHP start with $ symbol
$variableName = value;

### Basic Data Types
- String: `$text = "Hello World";`    // Text enclosed in quotes
  
- Integer: `$number = 42;`            // Whole numbers
  
- Float: `$decimal = 3.14;`           // Decimal numbers
  
- Boolean: `$isTrue = true;`          // true or false
  
- Null: `$empty = null;`              // No value assigned
  
- Array: `$array = [1, 2, 3];`        // Collection of values
  
- Object: `$obj = new stdClass();`    // Instance of a class



## Operators

### Arithmetic Operators
// Used for performing mathematical operations
+ Addition:         `$a + $b`    // Adds values
- Subtraction:      `$a - $b`    // Subtracts values
* Multiplication:   `$a * $b`    // Multiplies values
/ Division:         `$a / $b`    // Divides values
% Modulus:          `$a % $b`    // Returns division remainder
** Exponentiation:  `$a ** $b`   // Raises to power (PHP 5.6+)

### Assignment Operators
// Used to assign values to variables
=   Basic:          `$x = 5`     // Assigns value
+=  Addition:       `$x += 5`    // Same as: $x = $x + 5
-=  Subtraction:    `$x -= 5`    // Same as: $x = $x - 5
*=  Multiplication: `$x *= 5`    // Same as: $x = $x * 5
/=  Division:       `$x /= 5`    // Same as: $x = $x / 5
%=  Modulus:        `$x %= 5`    // Same as: $x = $x % 5

### Comparison Operators
// Used to compare two values
==  Equal:          `$a == $b`   // True if values are equal
=== Identical:      `$a === $b`  // True if values AND types are equal
!=  Not equal:      `$a != $b`   // True if values are not equal
<>  Not equal:      `$a <> $b`   // Alternative notation
!== Not identical:  `$a !== $b`  // True if values OR types are not equal
>   Greater than:   `$a > $b`    // True if $a is greater than $b
<   Less than:      `$a < $b`    // True if $a is less than $b
>=  Greater/equal:  `$a >= $b`   // True if $a is greater than or equal to $b
<=  Less/equal:     `$a <= $b`   // True if $a is less than or equal to $b

### Logical Operators
// Used to combine conditional statements
&&  AND:   `$a && $b`   // True if both $a AND $b are true
||  OR:    `$a || $b`   // True if either $a OR $b is true
!   NOT:   `!$a`        // True if $a is not true
and  AND:  `$a and $b`  // Alternative AND syntax
or   OR:   `$a or $b`   // Alternative OR syntax
xor  XOR:  `$a xor $b`  // True if either $a or $b is true, but not both






## Control Structures

### If Statements
// Basic decision making
```php
if (condition) {
    // code
} elseif (condition) {
    // code
} else {
    // code
}
```

### Switch Statement
// Alternative to multiple if statements
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
// While Loop - Executes while condition is true
```php
while (condition) {
    // code
}
```

// Do-While Loop - Always executes at least once
```php
do {
    // code
} while (condition);
```

// For Loop - Used when you know number of iterations
```php
for ($i = 0; $i < 10; $i++) {
    // code
}
```

// Foreach Loop - Specifically for arrays
```php
foreach ($array as $value) {
    // code
}
// With key
foreach ($array as $key => $value) {
    // code
}
```





## Functions

### Basic Function Structure
// Simple function definition
```php
function functionName($parameter1, $parameter2) {
    // code
    return $value;
}
```

### Function Types
// Function with default parameters
```php
function greet($name = "User") {
    return "Hello, $name!";
}
```

// Function with type declarations (PHP 7+)
```php
function add(int $a, int $b): int {
    return $a + $b;
}
```

// Anonymous/Lambda Functions
```php
$multiply = function($a, $b) {
    return $a * $b;
};
```

// Arrow Functions (PHP 7.4+)
```php
$multiply = fn($a, $b) => $a * $b;
```

### Built-in Functions
// String Functions
strlen()    // Get string length
str_replace() // Replace text within string
substr()    // Get part of string

// Array Functions
count()     // Count elements in array
array_push() // Add element to array
array_pop() // Remove last element
sort()      // Sort arrays

// Math Functions
round()     // Rounds number
rand()      // Generate random number
max()       // Find highest value
min()       // Find lowest value



## Arrays

### Array Types
// Indexed Arrays (Numeric keys)
```php
$fruits = ["apple", "banana", "orange"];
$numbers = [1, 2, 3, 4, 5];
```

// Associative Arrays (Named keys)
```php
$age = [
    "Peter" => 35,
    "Ben" => 37,
    "Joe" => 43
];
```

// Multidimensional Arrays
```php
$matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];
```

### Array Operations
// Adding Elements
$array[] = value;              // Add to end
array_push($array, value);     // Add to end
array_unshift($array, value);  // Add to beginning

// Removing Elements
array_pop($array);            // Remove from end
array_shift($array);          // Remove from beginning
unset($array[index]);         // Remove specific element

### Array Functions
count()          // Count elements
array_merge()    // Merge arrays
array_slice()    // Extract portion of array
array_splice()   // Remove/replace portion
array_search()   // Search array
in_array()       // Check if value exists
array_key_exists() // Check if key exists


## Superglobals

### Key Superglobal Variables
// Available in all scopes throughout a PHP script

$_GET       // Contains form data sent via HTTP GET
```php
// URL: page.php?name=John
echo $_GET['name'];  // Outputs: John
```

$_POST      // Contains form data sent via HTTP POST
```php
// From HTML form with POST method
echo $_POST['username'];  // Access posted form data
```

$_SESSION   // Contains session variables
```php
session_start();
$_SESSION['user'] = 'John';  // Store session data
```

$_COOKIE    // Contains HTTP cookie data
```php
// Set and access cookies
setcookie("user", "John", time() + 3600);
echo $_COOKIE['user'];
```

$_SERVER    // Contains server and execution environment info
```php
echo $_SERVER['PHP_SELF'];      // Current script name
echo $_SERVER['SERVER_NAME'];    // Server name
echo $_SERVER['HTTP_HOST'];      // Host header
echo $_SERVER['REQUEST_METHOD']; // GET or POST
```

$_FILES     // Contains uploaded file information
```php
// Accessing uploaded files
$_FILES['file']['name']      // Original filename
$_FILES['file']['type']      // File type
$_FILES['file']['size']      // File size
$_FILES['file']['tmp_name']  // Temporary file location
```

$_ENV       // Contains environment variables
```php
echo $_ENV['PATH'];  // System path variable
```

$GLOBALS    // References all variables in global scope
```php
$x = 10;
echo $GLOBALS['x'];  // Access global variable
```

