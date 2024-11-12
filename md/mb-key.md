## Q1: HTML & CSS

### Q1.1:
```html
<!DOCTYPE html>
<html>
<head>
    <title>BLOG POST</title>
</head>
<body>
    <div class="container">
        <section id="post-content">
        </section>
    </div>
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
            border-radius: 10px;
            overflow: hidden;
        }
        th, td {
            border: 1px solid green;
            padding: 12px;
        }
        th {
            background-color: #E6FFE6;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>City</th>
            <th>Temp(C)</th>
        </tr>
        <tr>
            <td>Riffa</td>
            <td>31</td>
        </tr>
    </table>
</body>
</html>
```

### Q1.3:
"Current": b) background: yellow

"Next": d) background: red

\newpage

## Q2: PHP

### Q2.1:
```php
$videos = [
    [
        'title' => 'Intro to PHP',
        'likes' => 500,
        'duration' => 60
    ],
    [
        'title' => 'Advanced Web Development',
        'likes' => 750,
        'duration' => 180
    ],
    [
        'title' => 'The Web Masterclass',
        'likes' => 1000,
        'duration' => 240
    ]
];
```

### Q2.2:
```php
if ($videos[0]['duration'] < 120) {
    echo $videos[0]['title'];
}
```

### Q2.3:
```php
foreach ($videos as $video) {
    if (preg_match('/^The/', $video['title'])) {
        echo $video['title'] . "\n";
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