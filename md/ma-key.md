## Q1: HTML & CSS

### Q1.1:
```html
<!DOCTYPE html>
<html>
<head>
    <title>PORTFOLIO</title>
</head>
<body>
    <header class="navbar">
        <nav id="main-nav">
        </nav>
    </header>
</body>
</html>
```

### Q1.2:
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        table {
            width: 300px;
            box-shadow: 2px 2px 5px gray;
        }
        th, td {
            border: 2px dashed blue;
            padding: 10px;
        }
        th {
            background-color: #FFE4E1;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>Product</th>
            <th>Price</th>
        </tr>
        <tr>
            <td>Coffee</td>
            <td>1.3 BD</td>
        </tr>
    </table>
</body>
</html>
```

### Q1.3:
First paragraph: d) color: red

Second paragraph: d) color: red

\newpage

## Q2: PHP

### Q2.1:
```php
$students = [
    [
        'name' => 'John Doe',
        'grade' => 'A',
        'age' => 18
    ],
    [
        'name' => 'Emma Wilson',
        'grade' => 'B',
        'age' => 19
    ],
    [
        'name' => 'Isaac Newton',
        'grade' => 'A',
        'age' => 17
    ]
];
```

### Q2.2:
```php
if ($students[1]['grade'] === 'A') {
    echo $students[1]['name'];
}
```

### Q2.3:
```php
foreach ($students as $student) {
    if (preg_match('/^[aeiou]/i', $student['name'])) {
        echo $student['name'] . "\n";
    }
}
```

\newpage

## Q3: PHP PDO

### Q3.1:
```php
$dsn = 'mysql:host=mydb.rds.amazonaws.com;dbname=mydb';
$username = 'myuser';
$password = 'mypassword';

$pdo = new PDO($dsn, $username, $password);
```

### Q3.2:
```php
$stmt = $pdo->prepare("SELECT username, email FROM user WHERE email = :email");
$email = $_POST['email'];
$stmt->bindParam(':email', $email);
$stmt->execute();
$user = $stmt->fetch(PDO::FETCH_ASSOC);
```

### Q3.3:
```php
if ($user) {
    echo "<div class='welcome'>Welcome " . 
         htmlspecialchars($user['username']) . 
         ", your registered email is " . 
         htmlspecialchars($user['email']) . 
         "</div>";
}
```