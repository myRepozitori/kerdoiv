# kerdoiv
Kérdőív alap

<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <meta charset="UTF-8">
        <link rel="stylesheet" type="text/css" href="css/bootstrap-3.3.5-dist/css/bootstrap.min.css?%rand%">
        <link rel="stylesheet" type="text/css" href="css/base.css?%rand%">
        <link rel="stylesheet" type="text/css" href="css/bootstrap-3.3.5-dist/css/bootstrap_overwrite.css?%rand%">
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
        <script src="/js/base.js?%rand%"></script>
        <link href='https://fonts.googleapis.com/css?family=Open+Sans:400,300,300italic,400italic,600,600italic,700,700italic,800italic,800' rel='stylesheet' type='text/css'>
        <link href='https://fonts.googleapis.com/css?family=Montserrat:400,700' rel='stylesheet' type='text/css'>
        <meta charset="UTF-8">
        <title> %title% </title>
    </head>

    <body style="margin-top:200px">
        <div class="container">
            <span> %thanks% </span>
            <h1 class="bold"> Vitamonok és fogyasztásuk általános felmérője </h1> <br>
            <form class="formcontainer" action="index.php" method="POST">

                <h3> 1. Neme: </h3> <br>
                <div class="boxcontain1">
                    <span> Férfi </span>
                    <input style="margin-left:34px;" onClick="uncheckFirst()" id="genderFirst" type="checkbox" name="genderFirst" value="genderFirst"> <br>
                    <span> Nő </span> 
                    <input style="margin-left:47px;" onclick="uncheckSecond()" id="genderSecond" type="checkbox" name="genderSecond" value="genderSecond"> <br>
                    <span class="martop warningmessage"> %genderwarning% </span>
                </div>


                <h3> 2. Kora: </h3> <br>
                <div class="boxcontain2">
                    <span> 14 </span>
                    <input type="checkbox" onclick="uncheckAgeFirst()" id="age1" name="age1" value="14"> <br>
                    <span> 15 </span>
                    <input type="checkbox" onclick="uncheckAgeSecond()" id="age2" name="age2" value="15"> <br>
                    <span> 16 </span>
                    <input type="checkbox" onclick="uncheckAgeThird()" id="age3" name="age3" value="16"> <br>
                    <span> 17 </span>
                    <input type="checkbox" onclick="uncheckAgeFourth()" id="age4" name="age4" value="17"> <br>
                    <span> 18 </span>
                    <input type="checkbox" onclick="uncheckAgeFifth()" id="age5" name="age5" value="18"> <br>
                    <span class="martop warningmessage"> %agewarning% </span>
                </div>


                <h3> 3. Szokott vitamin tablettákat fogyasztani? </h3> <br>
                <div class="boxcontain3">
                    <span> Igen </span>
                    <input style="margin-left:35px;" onclick="uncheckYes()" id="yes" type="checkbox" name="yes" value="yes"> <br>
                    <span> Nem </span>
                    <input style="margin-left:30px;" onclick="uncheckNo()" id="no" type="checkbox" name="no" value="no"> <br>
                    <span class="martop warningmessage"> %thirdwarning% </span>
                </div>
                <input type="hidden" name="posted" id="hidden" value="1">
                <input type="submit" value="Küld" class="btn btn-default alining">

            </form>
        </div>
    </body>
</html>

//index
<?php

include (__DIR__ . '/../lib/header.php');

//error_reporting(E_ALL);
//ini_set('display_errors', 1);

$content = loadFile('index.html');
$title = "Teszt";
$_POST = array_map("htmlspecialchars", $_POST);
$_GET = array_map("htmlspecialchars", $_GET);

$cb1 = empty($_POST["genderFirst"]) ? false : true;
$cb2 = empty($_POST["genderSecond"]) ? false : true;
$cb3 = empty($_POST["age1"]) ? false : true;
$cb4 = empty($_POST["age2"]) ? false : true;
$cb5 = empty($_POST["age3"]) ? false : true;
$cb6 = empty($_POST["age4"]) ? false : true;
$cb7 = empty($_POST["age5"]) ? false : true;
$cb8 = empty($_POST["yes"]) ? false : true;
$cb9 = empty($_POST["no"]) ? false : true;
$cb10 = empty($_POST["posted"]) ? false : true;

if (isset($_POST["posted"])) {
    if (!empty($cb10)) {
        $thanks = "Köszönjük, hogy kitöltötte a kérdőívet! ";
    }
    if (empty($cb1) && empty($cb2)) {
        $genderwarning .= "Kérjük adja meg a nemét! ";
    }
    $cb1 = $_SESSION["genderFirst"];
    $cb2 = $_SESSION["genderSecond"];

    if (empty($cb3) && empty($cb4) && empty($cb5) && empty($cb6) && empty($cb7)) {
        $agewarning .= "Kérjük adja meg a korát! ";
    }
    $cb3 = $_SESSION["age1"];
    $cb4 = $_SESSION["age2"];
    $cb5 = $_SESSION["age3"];
    $cb6 = $_SESSION["age4"];
    $cb7 = $_SESSION["age5"];

    if (empty($cb8) && empty($cb9)) {
        $thirdwarning .= "Kérjük válaszoljon a harmadik kérdésre ";
    }
    $cb8 = $_SESSION["yes"];
    $cb9 = $_SESSION["no"];
    
} else {
    
}

include (__DIR__ . '/../lib/footer.php');

//footer
<?php

if(empty($redirect)){
    $output = str_replace('%content%', $content, $output);
    $output = str_replace('%title%', $title, $output);
    $output = str_replace('%rand%', mt_rand(1, 9999999999), $output);
    $output = str_replace('%genderwarning%', $genderwarning, $output);
    $output = str_replace('%agewarning%', $agewarning, $output);
    $output = str_replace('%thirdwarning%', $thirdwarning, $output);
    $output = str_replace('%thanks%', $thanks, $output);
    //$output = str_replace('%horse%', $generated, $output);
    //$output = str_replace('%teglalapkerulete%', $teglalapkerulete, $output);
    //$output = str_replace('%teglalapterulete%', $teglalapterulete, $output);
    //$output = str_replace('%teglatestfelszine%', $teglatestfelszine, $output);
    //$output = str_replace('%teglatestterfogata%', $teglatestterfogata, $output);
    echo $output;
} else {
    header('location:' . $redirect);
}

exit;

//header
<?php

include (__DIR__ . '/lib.php');
$content = "";
$output = loadFile('base.html');

//lib
<?php

function loadFile($file){
    return file_get_contents(__DIR__.'/../templates/'.$file);
}

//basejs

function uncheckFirst() {
    document.getElementById("genderFirst").checked = true;
    document.getElementById("genderSecond").checked = false;
}
function uncheckSecond() {
    document.getElementById("genderFirst").checked = false;
    document.getElementById("genderSecond").checked = true;
}
function uncheckAgeFirst() {
    document.getElementById("age1").checked = true;
    document.getElementById("age2").checked = false;
    document.getElementById("age3").checked = false;
    document.getElementById("age4").checked = false;
    document.getElementById("age5").checked = false;
}
function uncheckAgeSecond() {
    document.getElementById("age1").checked = false;
    document.getElementById("age2").checked = true;
    document.getElementById("age3").checked = false;
    document.getElementById("age4").checked = false;
    document.getElementById("age5").checked = false;
}
function uncheckAgeThird() {
    document.getElementById("age1").checked = false;
    document.getElementById("age2").checked = false;
    document.getElementById("age3").checked = true;
    document.getElementById("age4").checked = false;
    document.getElementById("age5").checked = false;
}
function uncheckAgeFourth() {
    document.getElementById("age1").checked = false;
    document.getElementById("age2").checked = false;
    document.getElementById("age3").checked = false;
    document.getElementById("age4").checked = true;
    document.getElementById("age5").checked = false;
}
function uncheckAgeFifth() {
    document.getElementById("age1").checked = false;
    document.getElementById("age2").checked = false;
    document.getElementById("age3").checked = false;
    document.getElementById("age4").checked = false;
    document.getElementById("age5").checked = true;
}
function uncheckYes() {
    document.getElementById("yes").checked = true;
    document.getElementById("no").checked = false;
}
function uncheckNo() {
    document.getElementById("yes").checked = false;
    document.getElementById("no").checked = true;
}

//document.cookie = "username=John Doe; expires ";

$('input[type=text]').on('keyup', function (e) {
    if (e.which === 13) {
        e.preventDefault();
    }
});

//basecss

body {
    margin:0px auto;
    padding:0px;
}
body, html, p{
    font-family:'Open Sans', sans-serif;
    color:black;
    font-size:18px;
    line-height:24px;
    padding:0px;
    margin:0px;
}
h1,h2,h3 {
    font-family:'Montserrat', sans-serif;
    text-transform:uppercase;
    color:#21252b;
    letter-spacing:-0.04em;
}
h1 {
    font-size: 32px;
}
h2 {}
h3 {
    font-weight:700;
    font-size:20px;
}
input[type="text"] {     
    font-family:'Open Sans', sans-serif;
    padding-left:20px;
    width:250px;
}
input[type="checkbox"]{
    margin-left:50px;
    width:17px;
    height:17px;
}
.inpcust {
    padding-left:20px;
    width:450px;
    background-color:#efefef;
    height:50px;
    border:none;
    outline:none;
}
.formcontainer{
    width:100%;
    float:left;
}
.boxcontain1{
    margin-left:75px;
}
.boxcontain2{
    margin-left:75px;
}
.boxcontain3{
    margin-left:75px;
}
.martop{
    margin-top:25px;
}
.warningmessage{
    color: #CC0000;
    text-transform:uppercase;
    font-weight:700;
}
.alining{
    width:150px;
}

//
