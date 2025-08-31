# Hellooo
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>Love Quiz</title>
  <style>
    body{
      margin:0;display:flex;align-items:center;justify-content:center;
      height:100vh;text-align:center;
      font-family:"Comic Sans MS",cursive,sans-serif;
      background:linear-gradient(135deg,#ffe6f0,#e6f0ff);
      overflow:hidden;position:relative;
    }
    /* Cute teddy with rose in background */
    .teddy-bg{
      position:absolute;
      bottom:0;right:0;
      width:160px;
      opacity:0.7;
      pointer-events:none;
      animation:float 6s ease-in-out infinite alternate;
    }
    @keyframes float{
      from{transform:translateY(0px);}
      to{transform:translateY(-20px);}
    }

    .card{
      background:rgba(255,255,255,0.9);
      border-radius:20px;padding:24px;max-width:420px;width:100%;
      box-shadow:0 12px 28px rgba(0,0,0,0.12);
      position:relative;z-index:2;
    }
    h1{font-size:24px;color:#444;margin:16px 0;}
    .buttons{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin-top:16px;position:relative;}
    .btn{
      flex:1;min-width:100px;padding:12px;border:none;border-radius:14px;cursor:pointer;
      font-size:16px;font-weight:bold;transition:transform .15s, left .2s, top .2s;
      position:relative;
    }
    .btn:active{transform:scale(.95);}
    .yes{background:linear-gradient(90deg,#ff7eb3,#ffb2d9);color:white;}
    .no{background:linear-gradient(90deg,#f5f5f5,#ebebff);color:#555;position:absolute;}
    .result{font-size:22px;margin-top:20px;color:#e75480;display:none;}
    .heart,.bear{
      position:fixed;pointer-events:none;z-index:9999;font-size:24px;
      animation:floatUp 2.5s ease-out forwards;
    }
    @keyframes floatUp{
      from{transform:translateY(0) scale(.9);opacity:1;}
      to{transform:translateY(-400px) scale(1.4);opacity:0;}
    }
    .music-toggle{position:fixed;bottom:16px;left:16px;
      background:white;border:none;border-radius:12px;padding:8px 12px;
      box-shadow:0 6px 16px rgba(0,0,0,0.1);cursor:pointer;z-index:5;}
  </style>
</head>
<body>
  <div class="card">
    <h1 id="question">Do you love me?</h1>
    <div class="buttons">
      <button class="btn yes" id="yesBtn">Yes 💖</button>
      <button class="btn no" id="noBtn" style="left:0;top:0;">No 🙈</button>
    </div>
    <div class="result" id="result"></div>
  </div>

  <!-- Cute Teddy Rose Background -->
  <img src="https://i.ibb.co/6gmzFzN/teddy-rose.png" class="teddy-bg" alt="teddy rose"/>

  <audio id="bg" loop preload="auto">
    <source src="https://cdn.pixabay.com/download/audio/2021/09/23/audio_8974f0b8a1.mp3?filename=kawaii-happiness-2-10911.mp3" type="audio/mpeg">
  </audio>
  <button class="music-toggle" id="musicToggle">🔈</button>

<script>
  const questions=["Do you love me?","Think again 💭","You sure? 🤔"];
  let step=0;
  const qEl=document.getElementById("question");
  const result=document.getElementById("result");
  const yesBtn=document.getElementById("yesBtn");
  const noBtn=document.getElementById("noBtn");
  const bg=document.getElementById("bg");
  const musicToggle=document.getElementById("musicToggle");

  // Floating hearts & bears
  function playHearts(){
    for(let i=0;i<14;i++){
      const el=document.createElement("div");
      el.textContent=Math.random()<0.5?"💖":"✨";
      el.className="heart";
      el.style.left=(Math.random()*window.innerWidth)+"px";
      el.style.top=(window.innerHeight-50)+"px";
      el.style.fontSize=(20+Math.random()*28)+"px";
      document.body.appendChild(el);
      setTimeout(()=>el.remove(),2500);
    }
  }

  // Progress questions
  function nextQuestion(){
    step++;
    if(step<questions.length){
      qEl.textContent=questions[step];
    }else{
      qEl.style.display="none";
      yesBtn.style.display="none";
      noBtn.style.display="none";
      result.style.display="block";
      result.innerHTML="Love you too ❤️<br>Now buy me a brownie 🍫🧸🌹";
      playHearts();
    }
  }

  yesBtn.onclick=()=>{
    tryPlayAudio();
    nextQuestion();
  };

  // No button runs away
  noBtn.onmouseover=()=>{
    const x=Math.floor(Math.random()*(window.innerWidth-200)-100);
    const y=Math.floor(Math.random()*(window.innerHeight-300)-150);
    noBtn.style.left=x+"px";
    noBtn.style.top=y+"px";
  };

  // Music control
  let started=false;
  function tryPlayAudio(){
    if(!started){
      bg.play().catch(()=>{});
      musicToggle.textContent="🔊";
      started=true;
    }
  }
  musicToggle.onclick=()=>{
    if(bg.paused){bg.play();musicToggle.textContent="🔊";}
    else{bg.pause();musicToggle.textContent="🔈";}
  };
</script>
</body>
</html>
