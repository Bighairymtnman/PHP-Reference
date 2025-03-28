# Advanced PHP Guide

## Table of Contents
- [Object-Oriented Programming](#object-oriented-programming)
- [Database Operations](#database-operations)
- [Sessions & Cookies](#sessions--cookies)
- [Security Best Practices](#security-best-practices)
- [API Development](#api-development)
- [Advanced Functions](#advanced-functions)
- [Namespaces & Autoloading](#namespaces--autoloading)
- [Error Handling & Debugging](#error-handling--debugging)


## Object-Oriented Programming

### Classes and Objects
```php
// Basic Class Structure
class User {
    // Properties
    private $name;
    private $email;
    
    // Constructor
    public function __construct($name, $email) {
        $this->name = $name;
        $this->email = $email;
    }
    
    // Methods
    public function getName() {
        return $this->name;
    }
    
    public function setName($name) {
        $this->name = $name;
    }
}

// Creating Objects
$user = new User("John", "john@example.com");
```

### Inheritance
```php
// Parent Class
class Vehicle {
    protected $brand;
    
    public function __construct($brand) {
        $this->brand = $brand;
    }
}

// Child Class
class Car extends Vehicle {
    private $model;
    
    public function __construct($brand, $model) {
        parent::__construct($brand);
        $this->model = $model;
    }
}
```

### Access Modifiers
```php
class Example {
    public $public = "Public access";      // Accessible everywhere
    protected $protected = "Class/Child";   // Class and inherited only
    private $private = "Class only";        // Only within this class
}
```




## Database Operations

### PDO Connection
```php
// Database connection using PDO
try {
    $pdo = new PDO(
        "mysql:host=localhost;dbname=testdb",
        "username",
        "password",
        [PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION]
    );
} catch(PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
```

### CRUD Operations with PDO
```php
// Create (Insert)
$stmt = $pdo->prepare("INSERT INTO users (name, email) VALUES (:name, :email)");
$stmt->execute(['name' => 'John', 'email' => 'john@example.com']);

// Read (Select)
$stmt = $pdo->query("SELECT * FROM users");
$users = $stmt->fetchAll(PDO::FETCH_ASSOC);

// Update
$stmt = $pdo->prepare("UPDATE users SET name = :name WHERE id = :id");
$stmt->execute(['name' => 'Jane', 'id' => 1]);

// Delete
$stmt = $pdo->prepare("DELETE FROM users WHERE id = :id");
$stmt->execute(['id' => 1]);
```

### Prepared Statements
```php
// Safe query with parameters
$stmt = $pdo->prepare("SELECT * FROM users WHERE age > ? AND city = ?");
$stmt->execute([18, 'New York']);

// Named parameters
$stmt = $pdo->prepare("SELECT * FROM users WHERE age > :age AND city = :city");
$stmt->execute



## Sessions & Cookies

### Working with Sessions
```php
// Starting a session
session_start();

// Setting session variables
$_SESSION['user_id'] = 123;
$_SESSION['username'] = "john_doe";
$_SESSION['is_admin'] = true;

// Reading session data
if (isset($_SESSION['user_id'])) {
    $userId = $_SESSION['user_id'];
}

// Destroying sessions
session_unset();     // Remove all session variables
session_destroy();   // Destroy the session
```

### Managing Cookies
```php
// Setting cookies
setcookie("user", "John Doe", time() + 3600);  // Expires in 1 hour
setcookie("theme", "dark", time() + (86400 * 30), "/");  // 30 days

// Reading cookies
if (isset($_COOKIE["user"])) {
    echo $_COOKIE["user"];
}

// Deleting cookies
setcookie("user", "", time() - 3600);  // Set expiration in past
```

### Session Security
```php
// Regenerate session ID
session_regenerate_id(true);

// Session configuration
ini_set('session.cookie_httponly', 1);  // Prevent JavaScript access
ini_set('session.use_only_cookies', 1); // Force cookies only
ini_set('session.cookie_secure', 1);    // HTTPS only
```






## Security Best Practices

### Input Validation & Sanitization
```php
// Sanitizing User Input
$email = filter_var($_POST['email'], FILTER_SANITIZE_EMAIL);
$url = filter_var($_POST['url'], FILTER_SANITIZE_URL);

// Validating Data
if (filter_var($email, FILTER_VALIDATE_EMAIL)) {
    // Valid email
}

// Escaping Output
$userInput = htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');
```

### Password Security
```php
// Hashing Passwords
$password = "user_password";
$hash = password_hash($password, PASSWORD_DEFAULT);

// Verifying Passwords
if (password_verify($password, $hash)) {
    // Password is correct
}
```

### SQL Injection Prevention
```php
// Using Prepared Statements (PDO)
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = :username");
$stmt->execute(['username' => $username]);

// Using Prepared Statements (MySQLi)
$stmt = $mysqli->prepare("SELECT * FROM users WHERE username = ?");
$stmt->bind_param("s", $username);
```

### Cross-Site Scripting (XSS) Prevention
```php
// Output Encoding
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');

// Content Security Policy
header("Content-Security-Policy: default-src 'self'");
```



## API Development

### RESTful API Basics
```php
// Setting JSON headers
header('Content-Type: application/json');
header('Access-Control-Allow-Origin: *');

// Basic API endpoint
switch($_SERVER['REQUEST_METHOD']) {
    case 'GET':
        // Handle GET request
        $data = ['status' => 'success', 'data' => $results];
        echo json_encode($data);
        break;
        
    case 'POST':
        // Handle POST request
        $input = json_decode(file_get_contents('php://input'), true);
        break;
}
```

### API Authentication
```php
// API Key Authentication
function validateApiKey($apiKey) {
    return $apiKey === 'your_secure_api_key';
}

// JWT Implementation
require_once 'vendor/autoload.php';
use \Firebase\JWT\JWT;

$token = JWT::encode($payload, $secret_key, 'HS256');
```

### API Response Handling
```php
// Standard Response Format
function sendResponse($status, $message, $data = null) {
    $response = [
        'status' => $status,
        'message' => $message,
        'data' => $data,
        'timestamp' => time()
    ];
    
    echo json_encode($response);
    exit;
}

// Error Handling
function sendError($code, $message) {
    http_response_code($code);
    sendResponse('error', $message);
}
```






## Advanced Functions

### Anonymous Functions & Closures
```php
// Anonymous Function
$greet = function($name) {
    return "Hello, $name!";
};

// Closure with 'use'
$multiplier = 3;
$multiply = function($number) use ($multiplier) {
    return $number * $multiplier;
};

// Arrow Functions (PHP 7.4+)
$add = fn($a, $b) => $a + $b;
```

### Callback Functions
```php
// Array mapping with callback
$numbers = [1, 2, 3, 4, 5];
$doubled = array_map(fn($n) => $n * 2, $numbers);

// Custom callback implementation
function processItems($items, $callback) {
    $result = [];
    foreach ($items as $item) {
        $result[] = $callback($item);
    }
    return $result;
}
```

### Generator Functions
```php
// Simple Generator
function numberGenerator($start, $end) {
    for ($i = $start; $i <= $end; $i++) {
        yield $i;
    }
}

// Using Generators
foreach (numberGenerator(1, 1000000) as $number) {
    // Memory efficient iteration
    echo $number;
}
```




## Namespaces & Autoloading

### Namespace Basics
```php
// Defining a namespace
namespace App\Controllers;

class UserController {
    public function index() {
        // Controller logic
    }
}

// Using namespaced classes
use App\Models\User;
use App\Services\Auth;
```

### Composer Autoloading
```php
// composer.json
{
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}

// Usage with autoloading
require 'vendor/autoload.php';

use App\Services\PaymentService;
$payment = new PaymentService();
```

### Custom Autoloader
```php
spl_autoload_register(function ($className) {
    $path = str_replace('\\', '/', $className);
    require_once __DIR__ . '/src/' . $path . '.php';
});
```



## Error Handling & Debugging

### Advanced Exception Handling
```php
// Custom Exception Classes
class DatabaseException extends Exception {
    public function __construct($message, $code = 0) {
        parent::__construct("Database Error: " . $message, $code);
    }
}

// Try-Catch with Multiple Catches
try {
    // Risky code here
    throw new DatabaseException("Connection failed");
} catch (DatabaseException $e) {
    // Handle database errors
    error_log($e->getMessage());
} catch (Exception $e) {
    // Handle other exceptions
} finally {
    // Always executed
}
```

### Debugging Techniques
```php
// Var Dump with Formatting
echo "<pre>";
var_dump($variable);
echo "</pre>";

// Debug Backtrace
debug_print_backtrace();

// Custom Debug Function
function debug($data) {
    echo "<pre>";
    print_r($data);
    echo "</pre>";
    die();  // Stop execution
}
```

### Error Logging
```php
// Custom Error Handler
set_error_handler(function($errno, $errstr, $errfile, $errline) {
    $message = date('Y-m-d H:i:s') . ": $errstr in $errfile on line $errline";
    error_log($message, 3, "app.log");
});

// Different Logging Methods
error_log("Critical error", 1, "admin@example.com");  // Email
error_log("Debug info", 3, "debug.log");             // File
```





