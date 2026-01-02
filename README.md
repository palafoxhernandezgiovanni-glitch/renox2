<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>RENOX</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family: Arial, Helvetica, sans-serif;
}

body{ background:#fafafa; }

/* HEADER */
header{
    background:#1877f2;
    padding:12px 0;
}

.navbar{
    width:90%;
    max-width:1000px;
    margin:auto;
    background:white;
    padding:10px 20px;
    border-radius:10px;
    display:flex;
    justify-content:space-between;
    align-items:center;
}

.logo{
    font-size:24px;
    font-weight:bold;
    color:#1877f2;
}

/* LOGIN */
.login-container{
    margin-top:60px;
    display:flex;
    justify-content:center;
}

.login-box{
    background:white;
    border:1px solid #ddd;
    border-radius:10px;
    padding:30px;
    width:320px;
    text-align:center;
}

.btn{
    width:100%;
    padding:10px;
    margin:8px 0;
    border-radius:6px;
    border:1px solid #ddd;
    cursor:pointer;
    font-size:14px;
}

.google{ background:white; }
.apple{ background:black; color:white; }
.email{ background:#1877f2; color:white; }
.phone{ background:#34a853; color:white; }

/* APP */
.app{ display:none; }

/* BUSCADOR */
.search-box{
    padding:10px;
    width:90%;
    max-width:500px;
    margin:15px auto;
    border-radius:20px;
    border:1px solid #ddd;
}

/* MENU */
.menu{
    background:white;
    border-bottom:1px solid #ddd;
    padding:10px 0;
}

.menu ul{
    list-style:none;
    display:flex;
    justify-content:space-around;
    max-width:600px;
    margin:auto;
    font-weight:bold;
}

/* SUBIR */
.upload{
    background:white;
    padding:15px;
    margin:15px auto;
    max-width:500px;
    border-radius:10px;
    border:1px solid #ddd;
}

/* FEED */
.feed{
    width:90%;
    max-width:500px;
    margin:auto;
}

.post{
    background:white;
    border:1px solid #ddd;
    border-radius:8px;
    margin-bottom:20px;
}

.post-header{
    padding:10px;
    font-weight:bold;
}

.post-media img,
.post-media audio{
    width:100%;
}

.post-footer{
    padding:10px;
}
</style>
</head>

<body>

<header>
    <div class="navbar">
        <div class="logo">RENOX</div>
        <div id="user">Invitado</div>
    </div>
</header>

<!-- LOGIN -->
<div class="login-container" id="login">
    <div class="login-box">
        <h2>Inicia sesión en RENOX</h2>

        <button class="btn google" onclick="login('Google')">Continuar con Google</button>
        <button class="btn apple" onclick="login('Apple')">Continuar con Apple</button>
        <button class="btn email" onclick="login('Correo')">Correo electrónico</button>
        <button class="btn phone" onclick="login('Teléfono')">Número telefónico</button>
    </div>
</div>

<!-- APP -->
<div class="app" id="app">

    <input class="search-box" placeholder="Buscar amigas, publicaciones, videos, música">

    <nav class="menu">
        <ul>
            <li>Inicio</li>
            <li>Historias</li>
            <li>Publicar</li>
            <li>Música</li>
            <li>Perfil</li>
        </ul>
    </nav>

    <!-- SUBIR -->
    <div class="upload">
        <h3>Crear publicación</h3><br>

        <input type="file" id="imageInput" accept="image/*"><br><br>
        <input type="file" id="audioInput" accept="audio/*"><br><br>
        <input type="text" id="textInput" placeholder="Escribe algo..." style="width:100%;padding:8px;"><br><br>

        <button class="btn email" onclick="createPost()">Publicar</button>
    </div>

    <!-- FEED -->
    <div class="feed" id="feed">

        <!-- PUBLICACIÓN ÚNICA SOLICITADA -->
        <div class="post">
            <div class="post-header">renox_seguridad</div>
            <div class="post-footer">
                🔐 Esto es una prueba de la seguridad de la página web y su funcionalidad.
            </div>
        </div>

    </div>

</div>

<script>
function login(type){
    document.getElementById("login").style.display="none";
    document.getElementById("app").style.display="block";
    document.getElementById("user").innerText="Sesión con " + type + " ✔️";
}

function createPost(){
    const feed = document.getElementById("feed");
    const text = document.getElementById("textInput").value;
    const image = document.getElementById("imageInput").files[0];
    const audio = document.getElementById("audioInput").files[0];

    const post = document.createElement("div");
    post.className = "post";

    let mediaHTML = "";

    if(image){
        const imgURL = URL.createObjectURL(image);
        mediaHTML += `<div class="post-media"><img src="${imgURL}"></div>`;
    }

    if(audio){
        const audioURL = URL.createObjectURL(audio);
        mediaHTML += `<div class="post-media"><audio controls src="${audioURL}"></audio></div>`;
    }

    post.innerHTML = `
        <div class="post-header">tu_usuario</div>
        ${mediaHTML}
        <div class="post-footer">${text}</div>
    `;

    feed.prepend(post);

    document.getElementById("textInput").value="";
    document.getElementById("imageInput").value="";
    document.getElementById("audioInput").value="";
}
</script>

</body>
</html>
