## Q1: HTML & CSS

### Q1.1:
```html
<!DOCTYPE html>
<html>
<head>
    <title>PRODUCTS</title>
</head>
<body>
    <aside class="sidebar">
        <ul id="product-list">
        </ul>
    </aside>
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
            box-shadow: 0 0 10px rgba(0,0,0,0.2);
        }
        th, td {
            border: none;
            padding: 12px;
            border-bottom: 2px solid orange;
        }
        th {
            background-color: #FFF3E0;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>Title</th>
            <th>Author</th>
        </tr>
        <tr>
            <td>The Hub</td>
            <td>A. Smith</td>
        </tr>
    </table>
</body>
</html>
```

### Q1.3:
First paragraph: c) font-size: 12px (might consider 16 also)

Second paragraph: d) font-size: 18px

\newpage

## Q2: PHP

### Q2.1:
```php
$employees = [
    [
        'name' => 'John Doe',
        'position' => 'Junior Developer',
        'salary' => 750
    ],
    [
        'name' => 'Jane Smith',
        'position' => 'Senior Manager',
        'salary' => 1200
    ],
    [
        'name' => 'Mike Johnson',
        'position' => 'Lead Developer',
        'salary' => 1500
    ]
];
```

### Q2.2:
```php
if ($employees[1]['salary'] > 900) {
    echo $employees[1]['name'];
}
```

### Q2.3:
```php
foreach ($employees as $employee) {
    if (preg_match('/Senior/', $employee['position'])) {
        echo $employee['position'] . "\n";
    }
}
```

\newpage

## Q3: PHP PDO

### Q3.1:
```php
$dsn = 'mysql:host=userdb.rds.amazonaws.com;dbname=userdb';
$username = 'user';
$password = 'password';

$pdo = new PDO($dsn, $username, $password);
```

### Q3.2:
```php
$stmt = $pdo->prepare("SELECT name, email FROM user WHERE email = :email");
$email = $_GET['email'];
$stmt->bindParam(':email', $email);
$stmt->execute();
$user = $stmt->fetch(PDO::FETCH_ASSOC);
```

### Q3.3:
```php
if ($user) {
    echo "<div class='welcome'>Welcome " . 
         htmlspecialchars($user['name']) . 
         ", your registered email is " . 
         htmlspecialchars($user['email']) . 
         "</div>";
}
```