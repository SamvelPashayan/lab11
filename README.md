<p align = "center">МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ
РОССИЙСКОЙ ФЕДЕРАЦИИ
ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ
ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ
«САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»</p>
<br>
<p align = "center">Институт естественных наук и техносферной безопасности</p>
<p align = "center">Кафедра информатики</p>
<p align = "center">Пашаян Самвел Алексанович</p>
<br>
<p align = "center">Лабораторная работа №11 "Гостевая Книга"</p>
<p align = "center">01.03.02 Прикладная математика и информатика</p>
<br>
<p align = "right" >Научный руководитель</p>
<p align = "right" >Соболев Евгений Игоревич</p>
<p align = "center" >Южно-Сахалинск</p>
<p align = "center" >2022 г.</p>
<p align = "center" ><b>ВВЕДЕНИЕ</b></p>
<p> <b> PHP  </b> (рекурсивный акроним словосочетания PHP: Hypertext Preprocessor) - это распространённый язык программирования общего назначения с открытым исходным кодом.</p>
<p> Вместо рутинного вывода HTML-кода командами языка (как это происходит, например, в Perl или C), скрипт PHP содержит HTML с встроенным кодом (в нашем случае, это вывод текста "Привет, я - скрипт PHP!"). Код PHP отделяется специальными начальным и конечным тегами <?php и ?>, которые позволяют "переключаться" в "PHP-режим" и выходить из него.
Код PHP отделяется специальными начальным и конечным тегами <?php и ?>, которые позволяют "переключаться" в "PHP-режим" и выходить из него.</p>
<p align = "center" > РЕШЕНИЕ ЗАДАЧ (ОСНОВНАЯ ЧАСТЬ) </p>
- - -
## Начальная страница
 <!DOCTYPE html>
 <html>

<head>
    <meta charset='utf-8'>
    <meta http-equiv='X-UA-Compatible' content='IE=edge'>
    <title>Page Title</title>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" />
    <script src='script.js'></script>
</head>

<body>
    <h1 style="margin-top:15%; margin-left: 40%; margin-right: auto;  width: 20em">Гостевая книга</h1>
    <button style="margin-left: 40%; font-size: medium;   width: 16em" type="submit" class="btn btn-sm btn-primary" onClick="location.href='http://lab11.book/send.php'">Оставить отзыв</button>
    <br>
    <br>
    <button style="margin-left: 40%; font-size: medium;   width: 16em" type="submit" class="btn btn-sm btn-primary" onClick="location.href='http://lab11.book/show.php'">Просмотреть отзывы</button><br>
</body>
</html>

## Страница с Формой
    <!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>Оставьте отзыв</title>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" />
    <script src="https://www.google.com/recaptcha/api.js" async defer></script>
</head>
<body>
    <h2>Оставьте отзыв</h2>
    <form class="my-form" action="sender.php" method="post" enctype="multipart/form-data" style="margin-left:10px; margin-right:10px">    
        <label for="name">Username:</label>
        <input class="form-control" name="username" />
           
        <label for="email">Email:</label>
        <input id="emailinput" class="form-control" name="email" />
    
        <label for="homepage">HomePage:</label>
        <input class="form-control" name="homepage" />
     
        <label for="message">Message:</label><br>

        <button type="button" onclick="code()" class="btn btn-info">code</button>
        <button type="button" onclick="italic()" class="btn btn-info">italic</button>
        <button type="button" onclick="strike()" class="btn btn-info">strike</button>
        <button type="button" onclick="strong()" class="btn btn-info">strong</button>
        <div style="color:red;" id="valid"></div>

        <textarea id="textarea" style="margin-top:5px" class="form-control" name="message"></textarea>
        
        <input style="margin-top:5px;"  type="file"  name="file">

        <div style="margin-top:5px" class="g-recaptcha" data-sitekey="6LdFCU4jAAAAAIZ3j4Gc1bq_KYtQHbIHN7cED3IK"></div>

        <button style="margin-top:5px; " class="btn btn-sm btn-primary" type="submit" name="submit" >Отправить</button> 
    </form>
    <script src="http://code.jquery.com/jquery-3.1.1.min.js"></script>
    <script type="text/javascript">
        var $textarea = $('#textarea');
        var $emailinput=$('#emailinput')
        //Валидация textarea
        $textarea.on('input', function() {
            if(valid()){
                $('#valid').empty();
            }else{
                document.getElementById('valid').innerHTML="Некорректно введенные данные";
            }
            
        });
        //Валидация email
        function validateEmail(email) {
        var re = /[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?/;
        return re.test(String(email).toLowerCase());
        }

        $emailinput.on('input', function() {
            if(validemail()){
                emailinput.style.borderColor = 'green';
            }else{
                emailinput.style.borderColor = 'red';
            }
            
        });

        function code(){
            document.getElementById('textarea').value +="<code> </code>";
        }
        function italic(){
            document.getElementById('textarea').value +="<i> </i>";
        }
        function strike(){
            document.getElementById('textarea').value +="<strike> </strike>";
        }
        function strong(){
            document.getElementById('textarea').value +="<strong> </strong>";
        }
        function isValid(s) {
            s = s.replace(/\s/g, '');
            s = s.replace(/[a-zа-яё]/gi, '');
            let open=0;
            let close=0;
            for (let i = 0; i < s.length; i++) {
                if(s[i]=="<"){
                    open++;
                }
                if(s[i]==">"){
                    close++;
                }
            } 
            return open%2==0 && open==close;
        }
        function valid(){
            let string=document.getElementById('textarea').value;
            return isValid(string);
        }
        function validemail(){
            let string=document.getElementById('emailinput').value;
            return validateEmail(string);
        }
    </script>
</body>
</html>
## Обработка форма на сервере
<?php
$conn = new mysqli("localhost", "root", "root","messages");
if($conn->connect_error){
    die("Ошибка: " . $conn->connect_error);
}
$UserName = strip_tags($_POST["username"]);
$Email = strip_tags($_POST["email"]);
$Homepage = strip_tags($_POST["homepage"]);
$Text = $_POST["message"];

//ip
$ip = $_SERVER['REMOTE_ADDR'];
function getIp() {
  $keys = [
    'HTTP_CLIENT_IP',
    'HTTP_X_FORWARDED_FOR',
    'REMOTE_ADDR'
  ];
  foreach ($keys as $key) {
    if (!empty($_SERVER[$key])) {
      $ip = trim(end(explode(',', $_SERVER[$key])));
      if (filter_var($ip, FILTER_VALIDATE_IP)) {
        return $ip;
      }
    }
  }
}

$ip = getIp();
//Browser
$user_agent = $_SERVER["HTTP_USER_AGENT"];
  if (strpos($user_agent, "Firefox") !== false) $browser = "Firefox";
  elseif (strpos($user_agent, "Opera") !== false) $browser = "Opera";
  elseif (strpos($user_agent, "Chrome") !== false) $browser = "Chrome";
  elseif (strpos($user_agent, "MSIE") !== false) $browser = "Internet Explorer";
  elseif (strpos($user_agent, "Safari") !== false) $browser = "Safari";
  else $browser = "Неизвестный";
//Дата
$date = date("Y-m-d");
//Файл
if($_FILES["file"]["type"]=='image/png' || $_FILES["file"]["type"]=='image/jpeg' || $_FILES["file"]["type"]=='image/gif'){
  require_once  'thumbs.php';

  $image = new Thumbs($_FILES["file"]['tmp_name']);
  $image->reduce(320, 240);
  $image->save();
  
  $filename=time().$_FILES["file"]['name'];
  move_uploaded_file($_FILES["file"]['tmp_name'],'data/'.$filename);
}
else if($_FILES["file"]["type"]=='text/plain' && $_FILES["file"]["size"]<105000){
  $filename=time().$_FILES["file"]['name'];
  move_uploaded_file($_FILES["file"]['tmp_name'],'data/'.$filename);
}
echo($Text);
//Отправляем в таблицу
$result = $conn->query("INSERT INTO `allmess` (`username`, `email`, `homepage`, `text`, `ip`, `browser`, `date`, `filename`) VALUES ('$UserName', '$Email', '$Homepage', '$Text','$ip','$browser','$date','$filename');");
?>
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" />
<h2 style="margin-top:15%; margin-left: 40%; margin-right: auto;  width: 20em">Сообщение отправлено</h2>
<button style="margin-left: 40%; font-size: medium;   width: 21em" type="submit" class="btn btn-sm btn-primary" onClick="location.href='http://lab11.book'">На главную</button>

## Просмотр Информации

    <!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>Все сообщения</title>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" />
</head>
<body>
    <h2>Все сообщения</h2>
    <?php
    $conn = new mysqli("localhost", "root", "root", "messages");
    if($conn->connect_error){
    die("Ошибка: " . $conn->connect_error);
    }
    $sql = "SELECT * FROM allmess";
    if($result = $conn->query($sql)){
    $rowsCount = $result->num_rows; // количество полученных строк
    echo "<p>Получено объектов: $rowsCount</p>";
    echo "<table class='table table-condensed table-striped table-bordered'>
    <tr><th>UserName</th><th>Email</th><th>Homepage</th><th>Message</th><th>Ip</th><th>Browser</th><th>Date</th><th>File</th></tr>";
    foreach($result as $row){
        $filename=$row["filename"];
        $pattern_name = '/\*\.txt/';
        echo "<tr>";
            echo "<td>" . $row["username"] . "</td>";
            echo "<td>" . $row["email"] . "</td>";
            echo "<td>" . $row["homepage"] . "</td>";
            echo "<td>" . $row["text"] . "</td>";
            echo "<td>" . $row["ip"] . "</td>";
            echo "<td>" . $row["browser"] . "</td>";
            echo "<td>" . $row["date"] . "</td>";
            if($filename!=null && end(explode(".", $filename))=="txt"){
                echo "<td >" . $filename . "</td>";
            }
            else if($filename!=null ){
            echo "<td width=\"250\">" . "<img src=\"data/".$filename."\" alt=\"\" width=\"320\" height=\"240\">". "</td>";
            }
            
        echo "</tr>";
    }
    echo "</table>";
    $result->free();
    } else{
    echo "Ошибка: " . $conn->error;
    }
    $conn->close();
    ?>
    </body>

     