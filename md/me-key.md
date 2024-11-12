## Q1: HTML & CSS

### Q1.1:
```html
<!DOCTYPE html>
<html>
<head>
    <title>CONTACT US</title>
</head>
<body>
    <footer class="bottom">
        <address id="contact-info">
        </address>
    </footer>
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
            width: 350px;
            border: 3px double black;
        }
        th, td {
            padding: 10px;
            border: 1px dotted gray;
        }
        th {
            background-color: #000;
            color: white;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>Section</th>
            <th>Time</th>
        </tr>
        <tr>
            <td>01</td>
            <td>8:00 PM</td>
        </tr>
    </table>
</body>
</html>
```

### Q1.3:
"Products": a) color: yellow

"Services": a) color: red

\newpage

## Q2: PHP

### Q2.1:
```php
$cars = [
    [
        'model' => 'Model 3',
        'brand' => 'Tesla',
        'year' => 2022
    ],
    [
        'model' => 'Camry',
        'brand' => 'Toyota',
        'year' => 2019
    ],
    [
        'model' => 'Mustang',
        'brand' => 'Ford',
        'year' => 2021
    ]
];
```

### Q2.2:
```php
if ($cars[0]['year'] > 2020) {
    echo $cars[0]['model'];
}
```

### Q2.3:
```php
foreach ($cars as $car) {
    if (preg_match('/^[MBA]/i', $car['model'])) {
        echo $car['model'] . "\n";
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