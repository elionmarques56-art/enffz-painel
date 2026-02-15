<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>enffz painel</title>

<style>
body{
  margin:0;
  background:transparent;
  font-family:Arial;
  overflow:hidden;
}

/* BOTÃO MOSTRAR/ESCONDER */
#toggle{
  position:fixed;
  top:20px;
  right:20px;
  z-index:9999;
  background:#00ff88;
  border:none;
  padding:10px 14px;
  border-radius:10px;
  font-weight:bold;
  cursor:pointer;
  box-shadow:0 0 15px #00ff88;
}

/* PAINEL */
#painel{
  position:fixed;
  top:80px;
  right:20px;
  width:300px;
  padding:18px;
  border-radius:14px;
  background:rgba(10,10,20,0.9);
  backdrop-filter: blur(10px);
  color:#fff;
  box-shadow:0 0 30px #00ff88;
  cursor:move;
  z-index:9998;
}

h2{
  text-align:center;
  color:#00ff88;
  margin-top:0;
}

/* BOTÃO INJETAR */
#inject{
  width:100%;
  padding:12px;
  border:none;
  border-radius:10px;
  background:#00ff88;
  color:#000;
  font-weight:bold;
  cursor:pointer;
  box-shadow:0 0 15px #00ff88;
}

#status{
  text-align:center;
  height:18px;
  margin-top:6px;
  color:#00ff88;
}

/* SLIDERS */
label{font-size:13px}
.slider{
  width:100%;
  margin-bottom:10px;
}

/* BOTÕES ZONA */
.zonas button{
  width:100%;
  margin-top:6px;
  padding:10px;
  border:none;
  border-radius:8px;
  background:#1b1b2e;
  color:#fff;
  cursor:pointer;
  box-shadow:0 0 8px #00ff88;
}
</style>
</head>

<body>

<button id="toggle">Ocultar painel</button>

<div id="painel">

<h2>enffz painel</h2>

<button id="inject">Injetar</button>
<div id="status"></div>

<label>Sensibilidade geral</label>
<input type="range" class="slider" onchange="resetar()">

<label>Precisão fina</label>
<input type="range" class="slider" onchange="resetar()">

<label>Velocidade horizontal</label>
<input type="range" class="slider" onchange="resetar()">

<label>Velocidade vertical</label>
<input type="range" class="slider" onchange="resetar()">

<div class="zonas">
<label>Zonas</label>
<button onclick="resetar()">Cabeça</button>
<button onclick="resetar()">Pescoço</button>
<button onclick="resetar()">Peito</button>
</div>

</div>

<script>
const btn = document.getElementById("inject")
const status = document.getElementById("status")
const painel = document.getElementById("painel")
const toggle = document.getElementById("toggle")

let ativo = false

btn.onclick = () => {
  if(ativo) return

  ativo = true
  btn.disabled = true
  status.innerText = "Injetando códigos..."

  setTimeout(()=>{
    status.innerText = "Códigos injetados com sucesso"
    btn.disabled = false
  },5000)
}

function resetar(){
  ativo = false
  btn.disabled = false
  status.innerText = ""
}

/* MOSTRAR / ESCONDER */
toggle.onclick = ()=>{
  if(painel.style.display === "none"){
    painel.style.display = "block"
    toggle.innerText = "Ocultar painel"
  }else{
    painel.style.display = "none"
    toggle.innerText = "Mostrar painel"
  }
}

/* ARRASTAR PAINEL */
let offsetX, offsetY, dragging=false

painel.addEventListener("mousedown",e=>{
  dragging=true
  offsetX = e.clientX - painel.offsetLeft
  offsetY = e.clientY - painel.offsetTop
})

document.addEventListener("mousemove",e=>{
  if(dragging){
    painel.style.left = (e.clientX - offsetX) + "px"
    painel.style.top  = (e.clientY - offsetY) + "px"
  }
})

document.addEventListener("mouseup",()=>dragging=false)
</script>

</body>
