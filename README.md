# live-tv-Al-Mahmud-
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Live TV</title>

<script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}

body{
background:#0f0f0f;
color:#fff;
}

header{
background:#111;
padding:15px;
display:flex;
justify-content:space-between;
align-items:center;
position:sticky;
top:0;
z-index:999;
}

.logo{
font-size:28px;
font-weight:bold;
color:red;
}

#search{
padding:10px;
width:250px;
border:none;
border-radius:5px;
}

.player-section{
padding:15px;
}

.player-wrapper{
position:relative;
}

.live-badge{
position:absolute;
top:10px;
left:10px;
background:red;
padding:5px 10px;
border-radius:5px;
font-weight:bold;
z-index:2;
}

video{
width:100%;
height:500px;
background:black;
border-radius:10px;
}

.categories{
padding:15px;
display:flex;
gap:10px;
flex-wrap:wrap;
}

.categories button{
padding:10px 15px;
background:#222;
color:white;
border:none;
cursor:pointer;
border-radius:5px;
}

.categories button:hover{
background:red;
}

#channelGrid{
display:grid;
grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
gap:15px;
padding:15px;
}

.channel-card{
background:#1e1e1e;
border-radius:10px;
overflow:hidden;
cursor:pointer;
transition:0.3s;
text-align:center;
}

.channel-card:hover{
transform:scale(1.05);
}

.channel-card img{
width:100%;
height:120px;
object-fit:cover;
}

.channel-card h3{
padding:10px;
font-size:16px;
}

footer{
text-align:center;
padding:20px;
background:#111;
margin-top:20px;
}

@media(max-width:768px){

video{
height:220px;
}

#search{
width:150px;
}

#channelGrid{
grid-template-columns:repeat(2,1fr);
}

}

</style>
</head>
<body>

<header>
<div class="logo">LIVE TV</div>

<input
type="text"
id="search"
placeholder="Search Channel">
</header>

<div class="player-section">

<div class="player-wrapper">

<div class="live-badge">
LIVE
</div>

<video
id="videoPlayer"
controls
autoplay>
</video>

</div>

</div>

<div class="categories">

<button onclick="filterCategory('All')">
All
</button>

<button onclick="filterCategory('News')">
News
</button>

<button onclick="filterCategory('Sports')">
Sports
</button>

<button onclick="filterCategory('Movies')">
Movies
</button>

<button onclick="filterCategory('Entertainment')">
Entertainment
</button>

</div>

<div id="channelGrid"></div>

<footer>
© 2026 Live TV
</footer>

<script>

const channels = [

{
name:"News Channel",
category:"News",
logo:"https://via.placeholder.com/300x150?text=News",
stream:"https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},

{
name:"Sports Channel",
category:"Sports",
logo:"https://via.placeholder.com/300x150?text=Sports",
stream:"https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},

{
name:"Movie Channel",
category:"Movies",
logo:"https://via.placeholder.com/300x150?text=Movies",
stream:"https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},

{
name:"Entertainment",
category:"Entertainment",
logo:"https://via.placeholder.com/300x150?text=Entertainment",
stream:"https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
}

];

const grid =
document.getElementById("channelGrid");

const video =
document.getElementById("videoPlayer");

function renderChannels(data){

grid.innerHTML = "";

data.forEach(channel=>{

const card =
document.createElement("div");

card.className =
"channel-card";

card.setAttribute(
"data-category",
channel.category
);

card.innerHTML = `
<img src="${channel.logo}">
<h3>${channel.name}</h3>
`;

card.onclick = ()=>{

playChannel(channel.stream);

};

grid.appendChild(card);

});

}

function playChannel(url){

if(Hls.isSupported()){

const hls = new Hls();

hls.loadSource(url);

hls.attachMedia(video);

}else{

video.src = url;

}

}

function filterCategory(category){

if(category==="All"){

renderChannels(channels);

return;

}

const filtered =
channels.filter(
c=>c.category===category
);

renderChannels(filtered);

}

document
.getElementById("search")
.addEventListener(
"keyup",
function(){

const value =
this.value.toLowerCase();

const filtered =
channels.filter(c=>
c.name
.toLowerCase()
.includes(value)
);

renderChannels(filtered);

}
);

renderChannels(channels);

playChannel(
channels[0].stream
);

</script>

</body>
</html>
