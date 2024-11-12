## Q1: HTML & CSS

### Q1.1:
```html
<!DOCTYPE html>
<html>
<head>
    <title>SERVICES</title>
</head>
<body>
    <form class="contact-form">
        <fieldset id="user-info">
        </fieldset>
    </form>
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
            width: 400px;
            border: 2px solid purple;
        }
        th, td {
            padding: 15px;
            border-bottom: 1px solid purple;
        }
        th {
            background-color: #E6E6FA;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>Name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>Ahmed</td>
            <td>a@email.com</td>
        </tr>
    </table>
</body>
</html>
```

### Q1.3:
Text input: a) border: 1px solid

Password input: a) border: 1px solid

\newpage

## Q2: PHP

### Q2.1:
```php
$books = [
    [
        'title' => 'To Kill a Mockingbird',
        'author' => 'Harper Lee',
        'year' => 1960
    ],
    [
        'title' => 'Modern PHP',
        'author' => 'Josh Lockhart',
        'year' => 2015
    ],
    [
        'title' => 'Web Design 101',
        'author' => 'John Smith',
        'year' => 2005
    ]
];
```

### Q2.2:
```php
if ($books[2]['year'] > 2000) {
    echo $books[2]['title'];
}
```

### Q2.3:
```php
foreach ($books as $book) {
    if (preg_match('/\d$/', $book['title'])) {
        echo $book['title'] . "\n";
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