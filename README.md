<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sistem Administrasi</title>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Inter',sans-serif;transition:.3s}
:root{
--bg:#0f172a;--card:#1e293b;--text:#ffffff;
--soft:#39475a;--primary:#4346fa;
}
body.light{
--bg:#f1f5f9;--card:#ffffff;
--text:#0f172a;--soft:#e2e8f0;
}
body{
background:var(--bg);
color:var(--text);
min-height:100vh;
display:flex;
flex-direction:column;
}

/* LOGIN */
#loginBox{
position:fixed;inset:0;display:flex;
justify-content:center;align-items:center;
background:var(--bg);z-index:2000;
}
.login-card{
background:var(--card);
padding:40px;border-radius:20px;
width:360px;text-align:center;
box-shadow:0 15px 40px rgba(0,0,0,0.3);
}
.login-card input{
width:100%;padding:12px;margin:8px 0;
border-radius:10px;border:none;
background:var(--soft);color:var(--text);
}
.login-card button{
width:100%;padding:12px;margin-top:10px;
border:none;border-radius:10px;
background:var(--primary);color:#fff;
font-weight:600;cursor:pointer;
}

/* APP */
#app{display:none;flex:1}

/* HEADER */
header{
display:flex;justify-content:space-between;
align-items:center;padding:20px 40px;
background:var(--card);
box-shadow:0 5px 20px rgba(0,0,0,0.1);
position:relative;z-index:1000;
}
.theme-toggle{
cursor:pointer;padding:8px 15px;
border-radius:30px;background:var(--soft);
}

/* ACCOUNT */
.account-box{position:relative;z-index:1100;}
.account-btn{
display:flex;align-items:center;gap:10px;
background:var(--soft);
padding:8px 15px;border-radius:30px;
cursor:pointer;
}
.avatar{
width:32px;height:32px;border-radius:50%;
background:var(--primary);
display:flex;align-items:center;
justify-content:center;font-weight:600;color:#fff;
}
.account-menu{
position:absolute;right:0;top:60px;
background:var(--card);
padding:20px;border-radius:15px;
box-shadow:0 15px 40px rgba(0,0,0,0.3);
display:none;flex-direction:column;gap:12px;
min-width:200px;z-index:1200;
opacity:0;transform:translateY(-10px);
transition:all .3s ease;
}
.account-menu input{
background:var(--soft);border:none;
padding:10px;border-radius:10px;
color:var(--text);
}
.account-menu button{
width:100%;padding:10px;border-radius:10px;
border:none;background:var(--primary);
color:#fff;cursor:pointer;
}

/* SIDEBAR */
aside{
width:230px;position:fixed;
top:80px;left:0;
height:calc(100vh - 80px);
padding:25px;background:var(--card);
z-index:500;
}
aside button{
display:block;width:100%;margin-bottom:12px;
padding:12px;border:none;border-radius:12px;
background:var(--soft);color:var(--text);
cursor:pointer;
}
aside button:hover{
background:var(--primary);color:#fff;
}

main{margin-left:250px;padding:40px;flex:1;}

.card{
background:var(--card);
padding:25px;border-radius:20px;
box-shadow:0 10px 30px rgba(0,0,0,0.1);
margin-bottom:25px;
}

main section{
opacity:0;transform:translateY(10px);
transition:all 0.4s ease;
}
main section.active{
opacity:1;transform:translateY(0);
}

input{
width:100%;padding:12px;margin-top:8px;
border-radius:10px;border:none;
background:var(--soft);color:var(--text);
}

button{
margin-top:10px;padding:10px 15px;
border:none;border-radius:10px;
cursor:pointer;background:var(--primary);
color:#fff;
}

table{width:100%;border-collapse:collapse;margin-top:15px;}
th,td{padding:10px;border-bottom:1px solid var(--soft);}

.stats{
display:flex;gap:20px;flex-wrap:wrap;margin-top:20px;
}
.stat{
flex:1;min-width:180px;
padding:20px;border-radius:15px;
background:var(--primary);color:#fff;
}

/* FOOTER */
.main-footer{
margin-left:250px;
background:var(--card);
border-top:1px solid var(--soft);
padding:20px;
text-align:center;
box-shadow:0 -5px 20px rgba(0,0,0,0.08);
animation:fadeFooter .6s ease;
}
.footer-content{
display:flex;justify-content:center;
align-items:center;gap:8px;
font-size:14px;opacity:.85;flex-wrap:wrap;
}
.footer-logo{
font-size:16px;font-weight:600;color:var(--primary);
}
@keyframes fadeFooter{
from{opacity:0;transform:translateY(10px);}
to{opacity:1;transform:translateY(0);}
}
.hidden{display:none}
</style>
</head>

<body>

<div id="loginBox">
<div class="login-card">
<h2>Login</h2>
<input type="text" id="user" placeholder="Username">
<input type="password" id="pass" placeholder="Password">
<button onclick="login()">Masuk</button>
</div>
</div>

<div id="app">

<header>
<h3>Sistem Administrasi</h3>
<div style="display:flex;align-items:center;gap:15px;">
<span class="theme-toggle" onclick="toggleTheme()">🌙 / ☀</span>

<div class="account-box">
<div class="account-btn" onclick="toggleAccountMenu()">
<div class="avatar" id="avatarInitial">A</div>
<span id="accountName">Admin</span> ⌄
</div>

<div class="account-menu" id="accountMenu">
<input type="text" id="newName" placeholder="Ganti Nama">
<button onclick="saveName()">Simpan Nama</button>
<button onclick="logout()">Logout</button>
</div>
</div>
</div>
</header>

<aside>
<button onclick="showPage('dashboard')">Dashboard</button>
<button onclick="showPage('masuk')">Surat Masuk</button>
<button onclick="showPage('keluar')">Surat Keluar</button>
<button onclick="showPage('arsip')">Arsip Surat</button>
<button onclick="showPage('privasi')">Ketentuan Privasi</button>
</aside>

<main>

<section id="dashboard" class="card active">
<h3>Dashboard</h3>
<div class="stats">
<div class="stat"><h4>Surat Masuk</h4><p id="totalMasuk">0</p></div>
<div class="stat"><h4>Surat Keluar</h4><p id="totalKeluar">0</p></div>
<div class="stat"><h4>Total Arsip</h4><p id="totalArsip">0</p></div>
</div>
<canvas id="chartStat" height="100"></canvas>
</section>

<section id="masuk" class="card hidden">
<h3>Surat Masuk</h3>
<input type="text" id="m_perihal" placeholder="Perihal">
<input type="date" id="m_tanggal">
<input type="text" id="m_pengirim" placeholder="Pengirim">
<input type="file" id="m_file">
<button onclick="tambahSurat('masuk')">Tambah</button>
<table>
<thead><tr><th>Perihal</th><th>Tanggal</th><th>Pengirim</th><th>Dokumen</th><th>Aksi</th></tr></thead>
<tbody id="tableMasuk"></tbody>
</table>
</section>

<section id="keluar" class="card hidden">
<h3>Surat Keluar</h3>
<input type="text" id="k_perihal" placeholder="Perihal">
<input type="date" id="k_tanggal">
<input type="text" id="k_tujuan" placeholder="Tujuan">
<input type="file" id="k_file">
<button onclick="tambahSurat('keluar')">Tambah</button>
<table>
<thead><tr><th>Perihal</th><th>Tanggal</th><th>Tujuan</th><th>Dokumen</th><th>Aksi</th></tr></thead>
<tbody id="tableKeluar"></tbody>
</table>
</section>

<section id="arsip" class="card hidden">
<h3>Arsip Surat</h3>
<table>
<thead><tr><th>Jenis</th><th>Perihal</th><th>Tanggal</th><th>Pengirim/Tujuan</th><th>Dokumen</th></tr></thead>
<tbody id="tableArsip"></tbody>
</table>
</section>

<section id="privasi" class="card hidden">
<h3>Ketentuan Privasi</h3>
<p>Sistem Administrasi berkomitmen melindungi kerahasiaan dan keamanan data pengguna. Setiap informasi yang dimasukkan ke dalam sistem hanya digunakan untuk kepentingan pengelolaan administrasi dan peningkatan layanan.

Pengelola tidak membagikan atau memperjualbelikan data kepada pihak lain tanpa persetujuan pengguna, kecuali diwajibkan oleh ketentuan peraturan perundang-undangan yang berlaku.

Pengguna bertanggung jawab menjaga keamanan akun masing-masing serta menggunakan layanan sesuai ketentuan yang berlaku.

Dengan mengakses dan menggunakan Sistem Administrasi, pengguna dianggap telah membaca, memahami, dan menyetujui Ketentuan Privasi ini..</p>
<div style="margin-top:20px;padding:20px;border-radius:15px;background:var(--soft);">
<p>📱 WhatsApp :
<a href="https://wa.me/6282312362580" target="_blank" style="color:var(--primary);font-weight:600;text-decoration:none;">
Chat WhatsApp
</a></p>
<p style="margin-top:10px;">📧 Email :
<a href="mailto:dimzzz867@gmail.com" style="color:var(--primary);font-weight:600;text-decoration:none;">
dimzzz867@gmail.com
</a></p>
</div>
</section>

</main>
</div>

<footer class="main-footer">
<div class="footer-content">
<span class="footer-logo">©</span>
<span>Sistem Administrasi By <strong>@dimaspermana</strong></span>
<span id="footerYear"></span>
</div>
</footer>

<script>
document.getElementById("footerYear").textContent=new Date().getFullYear();

window.onload=function(){
if(localStorage.getItem("isLogin")==="true"){
loginBox.style.display="none";
app.style.display="block";
}
if(localStorage.getItem("theme")==="light"){
document.body.classList.add("light");
}
loadAccount();
loadData();
};

function login(){
if(user.value==="admin" && pass.value==="1234"){
localStorage.setItem("isLogin","true");
location.reload();
}else alert("Login salah");
}
function logout(){
localStorage.removeItem("isLogin");
location.reload();
}

function saveName(){
const name=newName.value.trim();
if(name.length<2){alert("Minimal 2 karakter");return;}
localStorage.setItem("accountName",name);
updateAccountUI(name);
newName.value="";
}
function loadAccount(){
updateAccountUI(localStorage.getItem("accountName")||"Admin");
}
function updateAccountUI(name){
accountName.textContent=name;
avatarInitial.textContent=name.charAt(0).toUpperCase();
}
function toggleAccountMenu(){
accountMenu.style.display="flex";
setTimeout(()=>{
accountMenu.style.opacity="1";
accountMenu.style.transform="translateY(0)";
},10);
}
window.addEventListener("click",e=>{
if(!e.target.closest(".account-box")){
accountMenu.style.display="none";
}
});

function toggleTheme(){
document.body.classList.toggle("light");
localStorage.setItem("theme",
document.body.classList.contains("light")?"light":"dark");
}

function showPage(id){
document.querySelectorAll("main section").forEach(s=>{
s.classList.remove("active");
s.classList.add("hidden");
});
let t=document.getElementById(id);
t.classList.remove("hidden");
setTimeout(()=>t.classList.add("active"),10);
}

function tambahSurat(jenis){
let data=JSON.parse(localStorage.getItem(jenis)||"[]");
let fileInput = jenis==="masuk"?m_file:k_file;
let file=fileInput.files[0];
if(!file){alert("Pilih file");return;}
let reader=new FileReader();
reader.onload=function(e){
let obj={
perihal:jenis==="masuk"?m_perihal.value:k_perihal.value,
tanggal:jenis==="masuk"?m_tanggal.value:k_tanggal.value,
pengirim:jenis==="masuk"?m_pengirim.value:undefined,
tujuan:jenis==="keluar"?k_tujuan.value:undefined,
fileName:file.name,
fileData:e.target.result
};
data.push(obj);
localStorage.setItem(jenis,JSON.stringify(data));
loadData();
};
reader.readAsDataURL(file);
}

function hapus(jenis,i){
let data=JSON.parse(localStorage.getItem(jenis)||"[]");
data.splice(i,1);
localStorage.setItem(jenis,JSON.stringify(data));
loadData();
}

function renderTable(jenis){
let table=document.getElementById(jenis==="masuk"?"tableMasuk":"tableKeluar");
let data=JSON.parse(localStorage.getItem(jenis)||"[]");
table.innerHTML="";
data.forEach((d,i)=>{
table.innerHTML+=`
<tr>
<td>${d.perihal}</td>
<td>${d.tanggal}</td>
<td>${d.pengirim||d.tujuan}</td>
<td><a href="${d.fileData}" target="_blank">${d.fileName}</a></td>
<td><button onclick="hapus('${jenis}',${i})">Hapus</button></td>
</tr>`;
});
}

function renderArsip(){
tableArsip.innerHTML="";
["masuk","keluar"].forEach(j=>{
let data=JSON.parse(localStorage.getItem(j)||"[]");
data.forEach(d=>{
tableArsip.innerHTML+=`
<tr>
<td>${j}</td>
<td>${d.perihal}</td>
<td>${d.tanggal}</td>
<td>${d.pengirim||d.tujuan}</td>
<td><a href="${d.fileData}" target="_blank">${d.fileName}</a></td>
</tr>`;
});
});
}

let chart;
function updateChart(masuk,keluar){
const ctx=document.getElementById("chartStat");
if(chart) chart.destroy();
chart=new Chart(ctx,{
type:'bar',
data:{
labels:['Surat Masuk','Surat Keluar'],
datasets:[{
data:[masuk,keluar],
backgroundColor:['#6366f1','#8b5cf6']
}]
},
options:{plugins:{legend:{display:false}}}
});
}

function loadData(){
renderTable("masuk");
renderTable("keluar");
renderArsip();
let m=JSON.parse(localStorage.getItem("masuk")||"[]");
let k=JSON.parse(localStorage.getItem("keluar")||"[]");
totalMasuk.innerText=m.length;
totalKeluar.innerText=k.length;
totalArsip.innerText=m.length+k.length;
updateChart(m.length,k.length);
}
</script>

</body>
</html>
