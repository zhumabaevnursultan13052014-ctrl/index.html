<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>QOLAI — полезные инструменты</title>

<style>
*{
  box-sizing:border-box;
}

body{
  margin:0;
  font-family:Arial, sans-serif;
  background:#f4f6f8;
  color:#202124;
}

header{
  background:#111827;
  color:white;
  padding:28px 20px;
  text-align:center;
}

header h1{
  margin:0;
  font-size:34px;
}

header p{
  margin:8px 0 0;
  color:#cbd5e1;
}

.container{
  max-width:700px;
  margin:auto;
  padding:18px;
}

.card{
  background:white;
  border-radius:18px;
  padding:20px;
  margin-bottom:18px;
  box-shadow:0 4px 15px rgba(0,0,0,0.08);
}

.card h2{
  margin-top:0;
  font-size:21px;
}

input{
  width:100%;
  padding:13px;
  margin:6px 0;
  border:1px solid #d1d5db;
  border-radius:10px;
  font-size:17px;
}

button{
  width:100%;
  padding:13px;
  margin-top:8px;
  border:none;
  border-radius:10px;
  background:#2563eb;
  color:white;
  font-size:17px;
  font-weight:bold;
}

button:active{
  transform:scale(0.98);
}

.result{
  margin-top:12px;
  padding:12px;
  background:#eff6ff;
  border-radius:10px;
  font-size:18px;
  font-weight:bold;
}

footer{
  text-align:center;
  padding:30px;
  color:#777;
  font-size:14px;
}
</style>
</head>

<body>

<header>
<h1>QOLAI</h1>
<p>Простые инструменты на каждый день</p>
</header>

<div class="container">

<!-- СКИДКА -->

<div class="card">
<h2>🏷️ Цена со скидкой</h2>

<input id="price" type="number" placeholder="Цена, например 50000">
<input id="discount" type="number" placeholder="Скидка %, например 20">

<button onclick="calcDiscount()">Посчитать</button>

<div class="result" id="discountResult">
Введите цену и скидку
</div>
</div>


<!-- РАЗДЕЛИТЬ СЧЁТ -->

<div class="card">
<h2>🍽️ Разделить счёт</h2>

<input id="bill" type="number" placeholder="Общая сумма">
<input id="people" type="number" placeholder="Количество человек">

<button onclick="splitBill()">Разделить</button>

<div class="result" id="billResult">
Сколько платит каждый?
</div>
</div>


<!-- ДО ДАТЫ -->

<div class="card">
<h2>📅 Сколько дней осталось?</h2>

<input id="futureDate" type="date">

<button onclick="daysUntil()">Посчитать</button>

<div class="result" id="dateResult">
Выберите дату
</div>
</div>


<!-- БЮДЖЕТ -->

<div class="card">
<h2>💰 Бюджет до зарплаты</h2>

<input id="money" type="number" placeholder="Сколько денег осталось">
<input id="days" type="number" placeholder="Сколько дней до зарплаты">

<button onclick="dailyBudget()">Рассчитать</button>

<div class="result" id="budgetResult">
Узнайте дневной лимит
</div>
</div>


<!-- КОНВЕРТЕР -->

<div class="card">
<h2>📏 Километры → мили</h2>

<input id="km" type="number" placeholder="Количество километров">

<button onclick="convertKm()">Перевести</button>

<div class="result" id="kmResult">
Введите расстояние
</div>
</div>


<!-- ПАРОЛЬ -->

<div class="card">
<h2>🔐 Генератор пароля</h2>

<input id="passwordLength"
       type="number"
       value="12"
       min="6"
       max="30"
       placeholder="Длина пароля">

<button onclick="generatePassword()">Создать пароль</button>

<div class="result" id="passwordResult">
Пароль появится здесь
</div>
</div>

</div>


<footer>
QOLAI • Полезные инструменты
</footer>


<script>

/* СКИДКА */

function calcDiscount(){

let price =
Number(document.getElementById("price").value);

let discount =
Number(document.getElementById("discount").value);

if(price <= 0){
document.getElementById("discountResult").innerHTML =
"Введите цену";
return;
}

let saving =
price * discount / 100;

let finalPrice =
price - saving;

document.getElementById("discountResult").innerHTML =
"Итого: " +
finalPrice.toLocaleString() +
" ₸<br>Экономия: " +
saving.toLocaleString() +
" ₸";
}


/* РАЗДЕЛЕНИЕ СЧЁТА */

function splitBill(){

let bill =
Number(document.getElementById("bill").value);

let people =
Number(document.getElementById("people").value);

if(bill <= 0 || people <= 0){
document.getElementById("billResult").innerHTML =
"Введите сумму и количество людей";
return;
}

let perPerson =
bill / people;

document.getElementById("billResult").innerHTML =
"По " +
perPerson.toLocaleString(undefined,{
maximumFractionDigits:2
}) +
" ₸ с человека";
}


/* ДНИ ДО ДАТЫ */

function daysUntil(){

let value =
document.getElementById("futureDate").value;

if(!value){
document.getElementById("dateResult").innerHTML =
"Сначала выберите дату";
return;
}

let target =
new Date(value);

let today =
new Date();

today.setHours(0,0,0,0);
target.setHours(0,0,0,0);

let difference =
target - today;

let days =
Math.ceil(
difference /
(1000 * 60 * 60 * 24)
);

if(days > 0){

document.getElementById("dateResult").innerHTML =
"Осталось " + days + " дней";

}
else if(days === 0){

document.getElementById("dateResult").innerHTML =
"Это сегодня! 🎉";

}
else{

document.getElementById("dateResult").innerHTML =
"Эта дата уже прошла";

}

}


/* БЮДЖЕТ */

function dailyBudget(){

let money =
Number(document.getElementById("money").value);

let days =
Number(document.getElementById("days").value);

if(money <= 0 || days <= 0){
document.getElementById("budgetResult").innerHTML =
"Введите деньги и количество дней";
return;
}

let daily =
money / days;

document.getElementById("budgetResult").innerHTML =
"Можно тратить примерно<br>" +
daily.toLocaleString(undefined,{
maximumFractionDigits:0
}) +
" ₸ в день";
}


/* КИЛОМЕТРЫ */

function convertKm(){

let km =
Number(document.getElementById("km").value);

let miles =
km * 0.621371;

document.getElementById("kmResult").innerHTML =
km +
" км = " +
miles.toFixed(2) +
" миль";
}


/* ПАРОЛЬ */

function generatePassword(){

let length =
Number(
document.getElementById("passwordLength").value
);

if(length < 6){
length = 6;
}

if(length > 30){
length = 30;
}

let chars =
"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%&*";

let password = "";

for(let i = 0; i < length; i++){

let random =
Math.floor(
Math.random() * chars.length
);

password += chars[random];

}

document.getElementById("passwordResult").innerHTML =
password;

}

</script>

</body>
</html>
