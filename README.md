
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<meta name="theme-color" content="#07111f">
<title>Photos - Alislamiah</title>
<link rel="icon" href="icon.png">

<style>
*{box-sizing:border-box;margin:0;padding:0;font-family:'Segoe UI',Tahoma,Arial}
body{background:#07111f;color:#f5f8ff;min-height:100vh;overflow-x:hidden}
button,input{font:inherit}
button{cursor:pointer}

/* SPLASH SCREEN */
#splash{
position:fixed;inset:0;background:#07111f;z-index:9999;
display:flex;align-items:center;justify-content:center;
}
.splash-icon{width:115px;height:115px;object-fit:contain;border-radius:25px}
.splash-brand{
position:absolute;bottom:45px;display:flex;
flex-direction:column;align-items:center;gap:9px;
}
.splash-brand img{width:57px;height:57px;object-fit:contain}
.splash-brand span{font-size:19px;font-weight:700;letter-spacing:1px}
.loader{position:absolute;bottom:155px;width:28px;height:28px;border:3px solid #ffffff20;border-top-color:#00baff;border-radius:50%;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

/* MAIN APPLICATION */
#app{display:none;min-height:100vh;padding-bottom:85px}
.topbar{
height:68px;padding:0 19px;display:flex;align-items:center;
justify-content:space-between;background:#0b1728;
border-bottom:1px solid #ffffff10;position:sticky;top:0;z-index:50;
}
.brand{display:flex;align-items:center;gap:10px}
.brand img{width:38px;height:38px;object-fit:contain;border-radius:10px}
.brand strong{font-size:20px;letter-spacing:.3px}
.brand small{display:block;color:#7189a9;font-size:10px}
.top-actions{display:flex;gap:9px}
.icon-btn{
width:40px;height:40px;border:1px solid #ffffff15;
border-radius:12px;background:#ffffff09;color:white;font-size:19px;
}
.content{max-width:1250px;margin:auto;padding:25px 19px}
.welcome{margin-bottom:22px}
.welcome h1{font-size:28px;margin-bottom:7px}
.welcome p{color:#8197b5;font-size:14px}

.searchbox{
display:flex;align-items:center;gap:10px;background:#101f33;
border:1px solid #ffffff12;border-radius:14px;padding:0 15px;
margin:20px 0 23px;height:51px;
}
.searchbox span{font-size:19px;color:#829ab9}
.searchbox input{background:none;border:0;outline:none;color:white;width:100%;font-size:14px}
.searchbox input::placeholder{color:#7187a3}

.section-head{
display:flex;justify-content:space-between;
align-items:center;margin:25px 0 15px;
}
.section-head h2{font-size:19px}
.section-head span{font-size:12px;color:#7892b2}

.tabs{display:flex;gap:9px;overflow-x:auto;padding-bottom:5px;margin:18px 0}
.tabs::-webkit-scrollbar{display:none}
.tabs button{
white-space:nowrap;padding:10px 17px;border-radius:12px;
border:1px solid #ffffff13;background:#101e31;color:#a9bad1;font-size:13px;
}
.tabs button.active{background:#0878ee;color:white;border-color:#0878ee}

.stats{
display:grid;grid-template-columns:repeat(3,1fr);gap:11px;margin:22px 0;
}
.stat{
background:linear-gradient(145deg,#10243c,#0c192b);
border:1px solid #ffffff10;border-radius:16px;padding:15px 12px;
}
.stat-icon{font-size:21px;margin-bottom:9px}
.stat strong{font-size:22px;display:block}
.stat small{color:#8198b5;font-size:12px}

.media-grid{
display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:9px;
}
.media-card{
position:relative;aspect-ratio:1/1;border-radius:12px;
overflow:hidden;background:#122238;border:1px solid #ffffff0c;
cursor:pointer;
}
.media-card img,.media-card video{
width:100%;height:100%;object-fit:cover;display:block;
}
.media-card .video-mark{
position:absolute;top:9px;right:9px;background:#0009;
width:28px;height:28px;border-radius:50%;
display:flex;align-items:center;justify-content:center;font-size:12px;
}
.media-card .favorite-mark{
position:absolute;top:9px;left:9px;font-size:16px;
text-shadow:0 2px 5px #000;
}
.media-card .media-name{
position:absolute;bottom:0;left:0;right:0;
background:linear-gradient(transparent,#000b);
padding:22px 8px 8px;font-size:11px;
white-space:nowrap;overflow:hidden;text-overflow:ellipsis;
}

.empty{
padding:55px 15px;text-align:center;
background:#0c192a;border:1px dashed #ffffff20;
border-radius:18px;color:#8197b5;
}
.empty .empty-icon{font-size:43px;margin-bottom:15px}
.empty h3{color:white;margin-bottom:8px;font-size:17px}
.empty p{font-size:13px;line-height:1.8}

.add-box{
border:1px solid #0878ee55;
background:linear-gradient(120deg,#0878ee18,#00c3ff08);
border-radius:17px;padding:18px;margin:22px 0;
display:flex;align-items:center;justify-content:space-between;gap:12px;
}
.add-box h3{font-size:15px;margin-bottom:5px}
.add-box p{font-size:12px;color:#91a7c4}
.primary-btn{
border:0;background:linear-gradient(135deg,#0878ee,#00c3ff);
color:white;padding:12px 17px;border-radius:11px;font-weight:700;
white-space:nowrap;font-size:13px;
}

/* ALBUMS */
.album-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:13px}
.album-card{
background:#101f33;border:1px solid #ffffff12;
border-radius:15px;overflow:hidden;cursor:pointer;
}
.album-cover{height:115px;background:#152942;display:grid;grid-template-columns:1fr 1fr;gap:2px;overflow:hidden}
.album-cover img{width:100%;height:100%;object-fit:cover}
.album-info{padding:12px}
.album-info strong{font-size:14px}
.album-info small{display:block;color:#8096b2;font-size:11px;margin-top:5px}

/* BOTTOM NAV */
.bottom-nav{
position:fixed;bottom:0;left:0;right:0;height:72px;
background:#0b1728f5;border-top:1px solid #ffffff13;
display:flex;justify-content:space-around;align-items:center;
z-index:60;backdrop-filter:blur(18px);
}
.nav-btn{
background:none;border:0;color:#8296b2;
display:flex;flex-direction:column;align-items:center;gap:5px;
font-size:10px;min-width:55px;
}
.nav-btn .nav-icon{font-size:21px}
.nav-btn.active{color:#20aaff}
.nav-btn.active .nav-icon{transform:translateY(-2px)}

/* VIEWER */
#viewer{
position:fixed;inset:0;background:#03070d;z-index:200;
display:none;flex-direction:column;
}
.viewer-header{
height:65px;display:flex;align-items:center;
justify-content:space-between;padding:0 17px;
background:#0a1422;
}
.viewer-header button{
background:#ffffff10;border:0;color:white;
width:39px;height:39px;border-radius:11px;font-size:19px;
}
.viewer-content{
flex:1;display:flex;align-items:center;justify-content:center;
overflow:hidden;padding:10px;
}
.viewer-content img,.viewer-content video{
max-width:100%;max-height:100%;object-fit:contain;
}
.viewer-footer{
padding:15px 20px;background:#0a1422;
display:flex;justify-content:space-between;align-items:center;
font-size:12px;color:#9db1ca;
}

/* SETTINGS */
.settings-list{display:flex;flex-direction:column;gap:10px}
.setting{
display:flex;align-items:center;justify-content:space-between;
padding:17px;background:#101f33;border:1px solid #ffffff10;
border-radius:13px;
}
.setting strong{font-size:14px}
.setting small{display:block;color:#8197b5;font-size:11px;margin-top:5px}
.setting button{background:#ffffff12;color:white;border:0;border-radius:9px;padding:9px 13px;font-size:12px}

/* MENU */
#menu{
position:fixed;inset:0;background:#0009;z-index:150;display:none;
}
.menu-panel{
position:absolute;top:0;right:0;bottom:0;width:min(300px,85%);
background:#0d192b;padding:23px;box-shadow:-15px 0 40px #0005;
}
.menu-head{display:flex;align-items:center;gap:12px;padding:10px 0 25px}
.menu-head img{width:45px;height:45px;object-fit:contain}
.menu-head strong{font-size:18px}
.menu-item{
width:100%;padding:15px;text-align:right;color:#c3d2e6;
background:#ffffff08;border:1px solid #ffffff0b;
border-radius:12px;margin-bottom:10px;font-size:14px;
}
.menu-item span{margin-left:10px}
.user-info{padding:15px;background:#ffffff08;border-radius:12px;margin:15px 0 22px;overflow-wrap:anywhere}
.user-info strong{font-size:13px}
.user-info small{display:block;color:#8197b5;font-size:12px;margin-top:6px}

/* RESPONSIVE */
@media(min-width:700px){
.media-grid{grid-template-columns:repeat(5,minmax(0,1fr));gap:13px}
.album-grid{grid-template-columns:repeat(4,minmax(0,1fr))}
.content{padding:35px 30px}
}
@media(max-width:370px){
.media-grid{grid-template-columns:repeat(2,minmax(0,1fr))}
.stats{gap:6px}
.stat{padding:12px 8px}
.stat strong{font-size:19px}
}
</style>
</head>

<body>

<!-- SPLASH -->
<div id="splash">
<img src="icon.png" class="splash-icon" alt="Photos">
<div class="loader"></div>
<div class="splash-brand">
<img src="Alislamiah.png" alt="Alislamiah">
<span>Alislamiah</span>
</div>
</div>

<!-- APP -->
<div id="app">

<header class="topbar">
<div class="brand">
<img src="icon.png" alt="Photos">
<div>
<strong>Photos</strong>
<small>by Alislamiah</small>
</div>
</div>

<div class="top-actions">
<button class="icon-btn" onclick="openSearch()" title="Search">⌕</button>
<button class="icon-btn" onclick="toggleMenu()" title="Menu">☰</button>
</div>
</header>

<main class="content">

<section id="homePage">

<div class="welcome">
<h1>صورك، في مكان واحد.</h1>
<p>مرحباً بك في Photos by Alislamiah</p>
</div>

<div class="searchbox" id="searchBox">
<span>⌕</span>
<input id="searchInput" type="search" placeholder="ابحث عن صورة أو فيديو...">
</div>

<div class="stats">
<div class="stat">
<div class="stat-icon">▧</div>
<strong id="photoCount">0</strong>
<small>الصور</small>
</div>
<div class="stat">
<div class="stat-icon">▷</div>
<strong id="videoCount">0</strong>
<small>الفيديوهات</small>
</div>
<div class="stat">
<div class="stat-icon">♡</div>
<strong id="favoriteCount">0</strong>
<small>المفضلة</small>
</div>
</div>

<div class="add-box">
<div>
<h3>أضف الصور والفيديوهات</h3>
<p>اختر الوسائط من جهازك لعرضها هنا</p>
</div>
<button class="primary-btn" onclick="document.getElementById('filePicker').click()">＋ إضافة</button>
</div>

<input type="file" id="filePicker" accept="image/*,video/*" multiple hidden>

<div class="section-head">
<h2 id="sectionTitle">أحدث الوسائط</h2>
<span id="mediaCountLabel">0 عنصر</span>
</div>

<div class="tabs">
<button class="active" data-filter="all">الكل</button>
<button data-filter="image">الصور</button>
<button data-filter="video">الفيديوهات</button>
<button data-filter="favorite">المفضلة</button>
</div>

<div id="mediaGrid" class="media-grid"></div>

</section>

<!-- ALBUMS PAGE -->
<section id="albumsPage" style="display:none">
<div class="welcome">
<h1>الألبومات</h1>
<p>اكتشف مجموعات الصور والفيديوهات الخاصة بك</p>
</div>
<div id="albumGrid" class="album-grid"></div>
</section>

<!-- FAVORITES PAGE -->
<section id="favoritesPage" style="display:none">
<div class="welcome">
<h1>المفضلة ♡</h1>
<p>الوسائط التي قمت بحفظها في المفضلة</p>
</div>
<div id="favoritesGrid" class="media-grid"></div>
</section>

<!-- SETTINGS PAGE -->
<section id="settingsPage" style="display:none">
<div class="welcome">
<h1>الإعدادات</h1>
<p>إدارة تطبيق Photos</p>
</div>

<div class="settings-list">
<div class="setting">
<div><strong>الحساب</strong><small id="accountEmail">...</small></div>
<button onclick="toggleMenu()">عرض</button>
</div>
<div class="setting">
<div><strong>التخزين المحلي</strong><small>الوسائط محفوظة على هذا الجهاز داخل التطبيق</small></div>
<span>▧</span>
</div>
<div class="setting">
<div><strong>عدد الوسائط</strong><small id="settingsCount">0 عنصر</small></div>
<span>▤</span>
</div>
<div class="setting">
<div><strong>حول Photos</strong><small>Photos by Alislamiah</small></div>
<span>ⓘ</span>
</div>
<div class="setting">
<div><strong>المطور</strong><small>Alislamiah</small></div>
<img src="Alislamiah.png" width="32" height="32" style="object-fit:contain">
</div>
<div class="setting">
<div><strong>تسجيل الخروج</strong><small>الخروج من حسابك</small></div>
<button onclick="logout()" style="background:#a52d3a">خروج</button>
</div>
</div>
</section>

</main>

<nav class="bottom-nav">
<button class="nav-btn active" data-page="homePage">
<span class="nav-icon">⌂</span><span>الرئيسية</span>
</button>
<button class="nav-btn" data-page="albumsPage">
<span class="nav-icon">▦</span><span>الألبومات</span>
</button>
<button class="nav-btn" data-page="favoritesPage">
<span class="nav-icon">♡</span><span>المفضلة</span>
</button>
<button class="nav-btn" data-page="settingsPage">
<span class="nav-icon">⚙</span><span>الإعدادات</span>
</button>
</nav>

</div>

<!-- VIEWER -->
<div id="viewer">
<div class="viewer-header">
<button onclick="closeViewer()">×</button>
<strong id="viewerTitle">Photos</strong>
<button onclick="toggleCurrentFavorite()" id="viewerFavorite">♡</button>
</div>
<div class="viewer-content" id="viewerContent"></div>
<div class="viewer-footer">
<span id="viewerDetails"></span>
<span>Photos by Alislamiah</span>
</div>
</div>

<!-- SIDE MENU -->
<div id="menu" onclick="if(event.target.id==='menu')toggleMenu()">
<div class="menu-panel">
<div class="menu-head">
<img src="icon.png" alt="">
<div><strong>Photos</strong><small style="display:block;color:#8299b6;font-size:11px">Alislamiah</small></div>
</div>
<div class="user-info">
<strong id="menuName">User</strong>
<small id="menuEmail">...</small>
</div>
<button class="menu-item" onclick="goPage('homePage');toggleMenu()"><span>⌂</span> الرئيسية</button>
<button class="menu-item" onclick="goPage('albumsPage');toggleMenu()"><span>▦</span> الألبومات</button>
<button class="menu-item" onclick="goPage('favoritesPage');toggleMenu()"><span>♡</span> المفضلة</button>
<button class="menu-item" onclick="goPage('settingsPage');toggleMenu()"><span>⚙</span> Settings</button>
<button class="menu-item" onclick="logout()" style="color:#ff8585"><span>↪</span> تسجيل الخروج</button>
</div>
</div>

<script type="module">

import {initializeApp} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-app.js";

import {
getAuth,
onAuthStateChanged,
signOut
} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-auth.js";

const firebaseConfig={
apiKey:"AIzaSyBrv1ky0Br5nLb68uvdXE3o6QdzTKpIU4g",
authDomain:"alislamiah-ai-34202.firebaseapp.com",
projectId:"alislamiah-ai-34202",
storageBucket:"alislamiah-ai-34202.firebasestorage.app",
messagingSenderId:"683051452829",
appId:"1:683051452829:web:e96e40422c7f31e563c774",
measurementId:"G-LFQLND010S"
};

const appFirebase=initializeApp(firebaseConfig);
const auth=getAuth(appFirebase);

const $=id=>document.getElementById(id);

let currentUser=null;
let media=[];
let currentFilter="all";
let currentItem=null;
let currentPage="homePage";
let db=null;
let objectUrls=[];

/* DATABASE */

function openDatabase(){
return new Promise((resolve,reject)=>{
const request=indexedDB.open("AlislamiahPhotosDB",1);

request.onupgradeneeded=e=>{
const database=e.target.result;
if(!database.objectStoreNames.contains("media")){
database.createObjectStore("media",{keyPath:"id"});
}
};

request.onsuccess=()=>resolve(request.result);
request.onerror=()=>reject(request.error);
});
}

function transaction(mode){
return db.transaction("media",mode).objectStore("media");
}

function saveMedia(item){
return new Promise((resolve,reject)=>{
const request=transaction("readwrite").put(item);
request.onsuccess=()=>resolve();
request.onerror=()=>reject(request.error);
});
}

function readAllMedia(){
return new Promise((resolve,reject)=>{
const request=transaction("readonly").getAll();
request.onsuccess=()=>resolve(request.result);
request.onerror=()=>reject(request.error);
});
}

function deleteMedia(id){
return new Promise((resolve,reject)=>{
const request=transaction("readwrite").delete(id);
request.onsuccess=()=>resolve();
request.onerror=()=>reject(request.error);
});
}

/* FAVORITES */

function favoriteKey(){
return "alislamiah_photos_favorites_"+currentUser.uid;
}

function getFavorites(){
try{
return JSON.parse(localStorage.getItem(favoriteKey())||"[]");
}catch{return []}
}

function isFavorite(id){
return getFavorites().includes(id);
}

function toggleFavorite(id){
let favorites=getFavorites();

if(favorites.includes(id)){
favorites=favorites.filter(x=>x!==id);
}else{
favorites.push(id);
}

localStorage.setItem(favoriteKey(),JSON.stringify(favorites));
renderAll();
}

/* AUTHENTICATION */

let authChecked=false;

onAuthStateChanged(auth,async user=>{

if(!user){
currentUser=null;
localStorage.removeItem("alislamiah_current_user");
window.location.replace("signin.html");
return;
}

currentUser=user;

localStorage.setItem("alislamiah_current_user",JSON.stringify({
id:user.uid,
name:user.displayName||user.email?.split("@")[0]||"User",
email:user.email
}));

$("menuName").textContent=user.displayName||"Photos User";
$("menuEmail").textContent=user.email||"";
$("accountEmail").textContent=user.email||"";

try{
db=await openDatabase();
media=await readAllMedia();

// كل مستخدم يرى وسائط حسابه فقط
media=media.filter(item=>item.uid===user.uid);

await showApplication();

}catch(error){
console.error(error);
$("splash").style.display="none";
alert("تعذر فتح مكتبة الصور. يرجى تحديث الصفحة.");
}
});

/* START APPLICATION */

async function showApplication(){
if(authChecked)return;
authChecked=true;

$("splash").style.display="none";
$("app").style.display="block";

renderAll();
}

/* IMPORT MEDIA */

$("filePicker").addEventListener("change",async event=>{

const files=Array.from(event.target.files||[]);

if(!files.length)return;

let added=0;

for(const file of files){

if(!file.type.startsWith("image/")&&!file.type.startsWith("video/"))continue;

const item={
id:crypto.randomUUID(),
uid:currentUser.uid,
name:file.name,
type:file.type.startsWith("video/")?"video":"image",
mime:file.type,
size:file.size,
date:new Date().toISOString(),
blob:file
};

try{
await saveMedia(item);
media.push(item);
added++;
}catch(error){
console.error("Save error",error);
}
}

event.target.value="";
renderAll();

if(added)alert("تمت إضافة "+added+" من الوسائط بنجاح.");
});

/* URL */

function getURL(item){
const url=URL.createObjectURL(item.blob);
objectUrls.push(url);
return url;
}

function clearOldUrls(){
objectUrls.forEach(url=>URL.revokeObjectURL(url));
objectUrls=[];
}

/* RENDER MEDIA */

function makeCard(item){

const card=document.createElement("div");
card.className="media-card";

const url=getURL(item);

if(item.type==="image"){
const img=document.createElement("img");
img.src=url;
img.loading="lazy";
img.alt=item.name;
card.appendChild(img);
}else{
const video=document.createElement("video");
video.src=url;
video.muted=true;
video.preload="metadata";
card.appendChild(video);

const mark=document.createElement("div");
mark.className="video-mark";
mark.textContent="▶";
card.appendChild(mark);
}

if(isFavorite(item.id)){
const heart=document.createElement("div");
heart.className="favorite-mark";
heart.textContent="♥";
card.appendChild(heart);
}

const name=document.createElement("div");
name.className="media-name";
name.textContent=item.name;
card.appendChild(name);

card.addEventListener("click",()=>openViewer(item.id));

return card;
}

function filteredMedia(filter,query=""){

let result=[...media];

if(filter==="image")result=result.filter(x=>x.type==="image");
if(filter==="video")result=result.filter(x=>x.type==="video");
if(filter==="favorite")result=result.filter(x=>isFavorite(x.id));

if(query){
result=result.filter(x=>x.name.toLowerCase().includes(query.toLowerCase()));
}

return result.sort((a,b)=>new Date(b.date)-new Date(a.date));
}

function renderGrid(container,items){

container.innerHTML="";

if(!items.length){
container.innerHTML=`
<div class="empty" style="grid-column:1/-1">
<div class="empty-icon">▧</div>
<h3>لا توجد وسائط هنا</h3>
<p>أضف الصور والفيديوهات من جهازك لتظهر في هذه المساحة.</p>
</div>`;
return;
}

items.forEach(item=>container.appendChild(makeCard(item)));
}

function renderHome(){

const query=$("searchInput").value.trim();
const items=filteredMedia(currentFilter,query);

$("photoCount").textContent=media.filter(x=>x.type==="image").length;
$("videoCount").textContent=media.filter(x=>x.type==="video").length;
$("favoriteCount").textContent=getFavorites().length;
$("mediaCountLabel").textContent=items.length+" عنصر";
$("settingsCount").textContent=media.length+" عنصر";

renderGrid($("mediaGrid"),items);
}

function renderFavorites(){
const i
tems=filteredMedia("favorite");
renderGrid($("favoritesGrid"),items);
}

function renderAlbums(){

const groups={};

media.forEach(item=>{
const date=new Date(item.date);
const key=date.getFullYear()+"-"+String(date.getMonth()+1).padStart(2,"0");

if(!groups[key])groups[key]=[];
groups[key].push(item);
});

const grid=$("albumGrid");
grid.innerHTML="";

const entries=Object.entries(groups).sort((a,b)=>b[0].localeCompare(a[0]));

if(!entries.length){
grid.innerHTML=`
<div class="empty" style="grid-column:1/-1">
<div class="empty-icon">▦</div>
<h3>لا توجد ألبومات بعد</h3>
<p>ستظهر ألبوماتك تلقائياً حسب تاريخ الصور والفيديوهات.</p>
</div>`;
return;
}

entries.forEach(([key,items])=>{

const card=document.createElement("div");
card.className="album-card";

const cover=document.createElement("div");
cover.className="album-cover";

items.slice(0,4).forEach(item=>{
const img=document.createElement("img");
img.src=getURL(item);
cover.appendChild(img);
});

card.appendChild(cover);

const info=document.createElement("div");
info.className="album-info";

const title=document.createElement("strong");
title.textContent=new Date(key+"-01").toLocaleDateString("ar",{year:"numeric",month:"long"});

const count=document.createElement("small");
count.textContent=items.length+" عنصر";

info.append(title,count);
card.appendChild(info);

card.onclick=()=>{
clearOldUrls();
goPage("homePage");
currentFilter="all";
document.querySelectorAll(".tabs button").forEach(b=>{
b.classList.toggle("active",b.dataset.filter==="all");
});
renderHome();
};

grid.appendChild(card);
});
}

function renderAll(){
clearOldUrls();
renderHome();
renderFavorites();
renderAlbums();
}

/* NAVIGATION */

function goPage(page){

currentPage=page;

["homePage","albumsPage","favoritesPage","settingsPage"].forEach(id=>{
$(id).style.display=id===page?"block":"none";
});

document.querySelectorAll(".nav-btn").forEach(btn=>{
btn.classList.toggle("active",btn.dataset.page===page);
});

clearOldUrls();

if(page==="homePage")renderHome();
if(page==="albumsPage")renderAlbums();
if(page==="favoritesPage")renderFavorites();
}

document.querySelectorAll(".nav-btn").forEach(btn=>{
btn.addEventListener("click",()=>goPage(btn.dataset.page));
});

/* FILTERS */

document.querySelectorAll(".tabs button").forEach(btn=>{

btn.addEventListener("click",()=>{

document.querySelectorAll(".tabs button").forEach(b=>b.classList.remove("active"));

btn.classList.add("active");
currentFilter=btn.dataset.filter;

clearOldUrls();
renderHome();
});
});

/* SEARCH */

$("searchInput").addEventListener("input",()=>{
clearOldUrls();
renderHome();
});

window.openSearch=()=>{
goPage("homePage");
$("searchInput").focus();
};

$("searchInput").addEventListener("keydown",e=>{
if(e.key==="Escape"){
$("searchInput").value="";
clearOldUrls();
renderHome();
}
});

/* VIEWER */

function openViewer(id){

const item=media.find(x=>x.id===id);
if(!item)return;

currentItem=item;
$("viewerContent").innerHTML="";
clearOldUrls();

const url=getURL(item);

if(item.type==="image"){
const img=document.createElement("img");
img.src=url;
img.alt=item.name;
$("viewerContent").appendChild(img);
}else{
const video=document.createElement("video");
video.src=url;
video.controls=true;
video.autoplay=true;
video.playsInline=true;
$("viewerContent").appendChild(video);
}

$("viewerTitle").textContent=item.name;
$("viewerDetails").textContent=
item.type==="image"?"صورة":"فيديو";

$("viewerFavorite").textContent=isFavorite(id)?"♥":"♡";
$("viewer").style.display="flex";
}

window.closeViewer=()=>{
$("viewer").style.display="none";
$("viewerContent").innerHTML="";
currentItem=null;
clearOldUrls();
};

window.toggleCurrentFavorite=()=>{
if(!currentItem)return;

const id=currentItem.id;
toggleFavorite(id);

$("viewerFavorite").textContent=isFavorite(id)?"♥":"♡";
};

/* SIDE MENU */

window.toggleMenu=()=>{
const menu=$("menu");
menu.style.display=menu.style.display==="block"?"none":"block";
};

/* LOGOUT */

window.logout=async()=>{

if(!confirm("هل تريد تسجيل الخروج من Photos؟"))return;

try{
await signOut(auth);
localStorage.removeItem("alislamiah_current_user");
window.location.replace("signin.html");
}catch(error){
alert("تعذر تسجيل الخروج: "+error.message);
}
};

/* KEYBOARD */

document.addEventListener("keydown",e=>{
if(e.key==="Escape"){
if($("viewer").style.display==="flex"){
closeViewer();
}else if($("menu").style.display==="block"){
toggleMenu();
}
}
});

/* CLEANUP */

window.addEventListener("pagehide",clearOldUrls);

</script>
</body>
</html>
