<!DOCTYPE html>
<html lang="en">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>QA DASHBOARD PRO</title>

<!-- FIREBASE -->
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore-compat.js"></script>

<!-- LEAFLET -->
<link rel="stylesheet"
href="https://unpkg.com/leaflet/dist/leaflet.css"/>

<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<!-- CHART -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<!-- ICONS -->
<link rel="stylesheet"
href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"/>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
}

html,
body{
width:100%;
height:100%;
overflow:hidden;
font-family:Arial,sans-serif;
background:#020617;
color:white;
}

/* ================= HEADER ================= */

.company-header{

height:145px;

position:relative;

background:
linear-gradient(
135deg,
#020617,
#071226,
#0f172a
);

padding:20px 30px;

display:flex;

justify-content:center;

align-items:center;

border-bottom:
1px solid rgba(59,130,246,.18);

overflow:hidden;

box-shadow:
0 15px 40px rgba(0,0,0,.35);

}

.header-glow{

position:absolute;

width:300px;
height:300px;

border-radius:50%;

filter:blur(100px);

opacity:.18;

}

.glow-left{
left:-120px;
top:-120px;
background:#2563eb;
}

.glow-right{
right:-120px;
bottom:-120px;
background:#06b6d4;
}

.header-center{

display:flex;

align-items:center;

gap:18px;

z-index:2;

}

.company-logo-box{

width:88px;
height:88px;

border-radius:24px;

padding:4px;

background:
linear-gradient(
135deg,
#2563eb,
#06b6d4
);

display:flex;

align-items:center;

justify-content:center;

box-shadow:
0 0 35px rgba(37,99,235,.45);

animation:
logoPulse 4s ease-in-out infinite;

}

@keyframes logoPulse{

0%{
transform:scale(1);
}

50%{
transform:scale(1.04);
}

100%{
transform:scale(1);
}

}

.company-logo{

width:100%;
height:100%;

border-radius:20px;

object-fit:cover;

background:white;

}

.company-details{
text-align:center;
}

.company-title{

font-size:38px;

font-weight:900;

background:
linear-gradient(
90deg,
#ffffff,
#93c5fd
);

-webkit-background-clip:text;

-webkit-text-fill-color:transparent;

}

.company-subtitle{

font-size:12px;

color:#94a3b8;

margin-top:4px;

}

.company-live{

margin-top:10px;

display:inline-flex;

align-items:center;

gap:8px;

padding:8px 16px;

border-radius:999px;

background:
rgba(34,197,94,.12);

border:
1px solid rgba(34,197,94,.22);

font-size:11px;

font-weight:bold;

color:#4ade80;

}

.live-dot{

width:9px;
height:9px;

border-radius:50%;

background:#22c55e;

box-shadow:
0 0 14px #22c55e;

animation:
livePulse 1.4s infinite;

}

@keyframes livePulse{

0%{
transform:scale(1);
}

50%{
transform:scale(1.5);
}

100%{
transform:scale(1);
}

}

.header-time-box{

position:absolute;

right:24px;

top:50%;

transform:translateY(-50%);

background:
linear-gradient(
135deg,
#111827,
#0f172a
);

padding:12px 16px;

border-radius:16px;

border:
1px solid rgba(59,130,246,.18);

}

.header-time-label{

font-size:10px;

color:#94a3b8;

margin-bottom:4px;

}

.header-time{

font-size:20px;

font-weight:800;

color:#38bdf8;

}

/* ================= MAIN ================= */

.main{

height:calc(100vh - 145px);

display:flex;

flex-direction:column;

gap:14px;

padding:14px;

overflow:hidden;

}

/* ================= TOP GRID ================= */

.top-grid{

display:grid;

grid-template-columns:
260px 260px 1fr;

gap:14px;

flex-shrink:0;

}

/* ================= LOWER GRID ================= */

.lower-grid{

display:grid;

grid-template-columns:
320px 1fr 320px;

gap:14px;

height:100%;

overflow:hidden;

}

/* ================= CARD ================= */

.card{

background:
linear-gradient(
180deg,
rgba(15,23,42,.98),
rgba(2,6,23,.98)
);

border:
1px solid rgba(59,130,246,.18);

border-radius:20px;

padding:14px;

display:flex;

flex-direction:column;

overflow:hidden;

backdrop-filter:blur(14px);

box-shadow:
0 0 20px rgba(37,99,235,.12);

}

.card-title{

font-size:13px;

font-weight:bold;

margin-bottom:12px;

display:flex;

align-items:center;

gap:8px;

}

/* ================= INPUT ================= */

select,
input{

width:100%;

height:42px;

padding:10px;

border:none;

border-radius:12px;

background:#0f172a;

color:white;

font-size:11px;

outline:none;

}

/* ================= WEATHER ================= */

.weather-grid{

display:grid;

grid-template-columns:
repeat(4,1fr);

gap:10px;

align-items:center;

text-align:center;

height:100%;

}

.weather-temp{
font-size:30px;
font-weight:800;
color:#fde047;
}

.weather-icon{

font-size:30px;

animation:
weatherFloat 3s ease-in-out infinite;

}

@keyframes weatherFloat{

0%{
transform:translateY(0px);
}

50%{
transform:translateY(-6px);
}

100%{
transform:translateY(0px);
}

}

/* ================= MAP ================= */

.map-card{

position:relative;

background:
linear-gradient(
180deg,
#071226,
#020617
);

}

#map{

width:100%;

height:100%;

min-height:84vh;

border-radius:22px;

overflow:hidden;

}

/* ================= SUMMARY ================= */

.summary-box{

background:#0f172a;

padding:10px 12px;

border-radius:14px;

display:flex;

justify-content:space-between;

align-items:center;

margin-bottom:10px;

}

.summary-value{
font-size:30px;
font-weight:800;
}

/* ================= CHART ================= */

.chart-wrapper{

flex:1;

min-height:520px;

}

/* ================= COORD ================= */

.coord-box{

flex:1;

background:#0f172a;

padding:12px;

border-radius:14px;

overflow:auto;

font-family:monospace;

font-size:11px;

line-height:1.8;

white-space:pre-line;

}

/* ================= BUTTON ================= */

.btn{

width:100%;

padding:13px;

border:none;

border-radius:14px;

margin-top:12px;

background:
linear-gradient(
135deg,
#2563eb,
#1d4ed8
);

color:white;

font-weight:bold;

cursor:pointer;

}

/* ================= LIVE PIN ================= */

.live-pin-wrapper{
position:relative;
width:42px;
height:42px;
transform:translate(-50%,-100%);
z-index:9999;
}

.live-pin-pulse{

position:absolute;

width:42px;
height:42px;

border-radius:50%;

background:rgba(34,197,94,.28);

animation:
liveRadar 2s infinite;

top:0;
left:0;

}

.live-pin-core{

position:absolute;

width:30px;
height:30px;

left:6px;
top:6px;

border-radius:
50% 50% 50% 0;

transform:
rotate(-45deg);

border:2px solid white;

background:#22c55e;

}

.live-pin-label{

position:absolute;

top:-62px;
left:50%;

transform:translateX(-50%);

background:
linear-gradient(
135deg,
#16a34a,
#15803d
);

padding:9px 12px;

border-radius:14px;

min-width:170px;

text-align:center;

font-size:10px;

font-weight:bold;

color:white;

}

.live-purpose{

margin-top:4px;

font-size:9px;

color:#dcfce7;

font-weight:normal;

}

@keyframes liveRadar{

0%{
transform:scale(.6);
opacity:.9;
}

70%{
transform:scale(1.8);
opacity:0;
}

100%{
opacity:0;
}

}

/* ================= NORMAL PIN ================= */

.company-pin{
position:relative;
width:28px;
height:28px;
transform:translate(-50%,-100%);
}

.pin-core{

position:absolute;

width:28px;
height:28px;

border-radius:
50% 50% 50% 0;

transform:
rotate(-45deg);

border:2px solid white;

}

/* ================= POPUP ================= */

.ultimate-popup{

width:190px;

background:
linear-gradient(180deg,#111827,#0f172a);

border-radius:14px;

padding:8px;

color:white;

}

.popup-line{

background:#1e293b;

padding:6px;

border-radius:8px;

margin-bottom:6px;

font-size:10px;

}

/* ================= MOBILE ================= */

@media(max-width:1100px){

html,
body{
overflow:auto;
}

.main{
height:auto;
overflow:visible;
}

.top-grid,
.lower-grid{
grid-template-columns:1fr;
}

#map{
height:75vh;
min-height:75vh;
}

}

</style>

</head>

<body>

<div class="company-header">

<div class="header-glow glow-left"></div>
<div class="header-glow glow-right"></div>

<div class="header-center">

<div class="company-logo-box">

<img src="https://upload.wikimedia.org/wikipedia/commons/a/ab/Logo_TV_2015.png"
class="company-logo">

</div>

<div class="company-details">

<div class="company-title">
QA DASHBOARD PRO
</div>

<div class="company-subtitle">
Realtime Company GPS Monitoring System
</div>

<div class="company-live">

<div class="live-dot"></div>

LIVE COMPANY DASHBOARD

</div>

</div>

</div>

<div class="header-time-box">

<div class="header-time-label">
🇵🇭 Philippine Time
</div>

<div class="header-time"
id="phTime">
Loading...
</div>

</div>

</div>

<div class="main">

<div class="top-grid">

<div class="card">

<div class="card-title">
<i class="fa-solid fa-user"></i>
Employee Filter
</div>

<select id="employeeFilter">
<option value="">All Employees</option>
</select>

</div>

<div class="card">

<div class="card-title">
<i class="fa-solid fa-calendar"></i>
Date Filter
</div>

<input type="date"
id="dateFilter">

</div>

<div class="card">

<div class="weather-grid">

<div>
<div class="weather-icon">☀️</div>
<div class="weather-temp">32°C</div>
<div>Sunny</div>
</div>

<div>
📍<br>Nueva Ecija
</div>

<div>
💧<br>68%
</div>

<div>
🌬<br>10 km/h
</div>

</div>

</div>

</div>

<div class="lower-grid">

<div style="display:flex;flex-direction:column;gap:14px;overflow:hidden;">

<div class="card">

<div class="card-title">
<i class="fa-solid fa-clock"></i>
Attendance Summary
</div>

<div class="summary-box">
<div>TIME IN</div>
<div class="summary-value" id="timeInCount">0</div>
</div>

<div class="summary-box">
<div>TIME OUT</div>
<div class="summary-value" id="timeOutCount">0</div>
</div>

</div>

<div class="card" style="flex:1;">

<div class="card-title">
<i class="fa-solid fa-location-dot"></i>
Coordinate List
</div>

<div style="
display:grid;
grid-template-columns:1fr 1fr;
gap:10px;
margin-bottom:12px;
">

<select id="coordEmployeeFilter">
<option value="">All Employees</option>
</select>

<input type="date"
id="coordDateFilter">

</div>

<div class="coord-box"
id="history">
Loading...
</div>

<button class="btn"
onclick="copyCoords()">
COPY COORDINATES
</button>

</div>

</div>

<div class="card map-card">

<div class="card-title">
<i class="fa-solid fa-map-location-dot"></i>
Realtime GPS Map
</div>

<div id="map"></div>

</div>

<div style="display:flex;flex-direction:column;gap:14px;overflow:hidden;">

<div class="card" style="flex:1;">

<div class="card-title">
<i class="fa-solid fa-chart-pie"></i>
Activity Summary
</div>

<div class="chart-wrapper">

<canvas id="activityChart"></canvas>

</div>

</div>

<div class="card">

<div class="card-title">
<i class="fa-solid fa-triangle-exclamation"></i>
Warnings
</div>

<div id="warningBox">
No warnings
</div>

</div>

</div>

</div>

</div>

<script>

const firebaseConfig = {

apiKey:"YOUR_API_KEY",

authDomain:"YOUR_PROJECT.firebaseapp.com",

projectId:"YOUR_PROJECT_ID"

};

firebase.initializeApp(firebaseConfig);

const db = firebase.firestore();

function updatePHTime(){

document.getElementById("phTime")
.innerText =

new Date().toLocaleString(
'en-PH',
{
timeZone:'Asia/Manila'
}
);

}

setInterval(updatePHTime,1000);

updatePHTime();

const map =
L.map('map').setView([15.4863,120.9674],10);

L.tileLayer(
'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
).addTo(map);

let markers =
L.layerGroup().addTo(map);

const ctx =
document.getElementById('activityChart');

let activityChart =
new Chart(ctx,{

type:'pie',

data:{
labels:[],
datasets:[{
data:[],
backgroundColor:[
'#22c55e',
'#3b82f6',
'#f59e0b',
'#ef4444',
'#8b5cf6',
'#06b6d4'
]
}]
},

options:{
responsive:true,
maintainAspectRatio:false
}

});

function loadData(){

markers.clearLayers();

let historyText="";
let purposeCount={};

let timeIn=0;
let timeOut=0;

db.collection("attendance")
.get()
.then(snapshot=>{

snapshot.forEach(doc=>{

let d = doc.data();

if(d.type=="IN"){
timeIn++;
}

if(d.type=="OUT"){
timeOut++;
}

if(!purposeCount[d.purpose]){
purposeCount[d.purpose]=0;
}

purposeCount[d.purpose]++;

historyText +=
`${Number(d.lat).toFixed(6)}, ${Number(d.lon).toFixed(6)}\n`;

let isLive =
d.type == "IN";

const customIcon = L.divIcon({

html:isLive

?

`

<div class="live-pin-wrapper">

<div class="live-pin-pulse"></div>

<div class="live-pin-label">

👤 ${d.name}

<div class="live-purpose">
📌 ${d.purpose}
</div>

</div>

<div class="live-pin-core"></div>

</div>

`

:

`

<div class="company-pin">

<div class="pin-core"
style="
background:#ef4444;
">
</div>

</div>

`,

className:"",
iconSize:[42,42],
iconAnchor:[21,42]

});

L.marker(
[d.lat,d.lon],
{
icon:customIcon
}
)

.bindPopup(`

<div class="ultimate-popup">

<div class="popup-line">
👤 ${d.name}
</div>

<div class="popup-line">
🕒 ${d.date} ${d.time}
</div>

<div class="popup-line">
📌 ${d.purpose}
</div>

<div class="popup-line">
📍 ${Number(d.lat).toFixed(6)},
${Number(d.lon).toFixed(6)}
</div>

</div>

`)

.addTo(markers);

});

document.getElementById("history")
.innerText =
historyText;

document.getElementById("timeInCount")
.innerText =
timeIn;

document.getElementById("timeOutCount")
.innerText =
timeOut;

activityChart.data.labels =
Object.keys(purposeCount);

activityChart.data.datasets[0].data =
Object.values(purposeCount);

activityChart.update();

});

}

function copyCoords(){

navigator.clipboard.writeText(
document.getElementById("history").innerText
);

alert("COPIED");

}

setInterval(loadData,5000);

loadData();

</script>

</body>
</html>
