<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Happy Bday</title>
    <style>
      :root {
        --background-color: linear-gradient(#87ceeb, #eee);
        --primary-color: #112434;
        --secondary-color: #fff;
        --stars-display: none;
        --text-color: #000;
      }

      .dark-theme {
        --background-color: linear-gradient(#000, #2b1055);
        --primary-color: #fff;
        --secondary-color: #112434;
        --stars-display: none;
        --fireflies-display: none;
        --text-color: #fff;
      }

      .dark-theme.star {
        --background-color: linear-gradient(#000, #2b1055);
        --primary-color: #fff;
        --secondary-color: #112434;
        --stars-display: block;
        --fireflies-display: none;
        --text-color: #fff;
      }

      .dark-theme.star.fireflies {
        --background-color: linear-gradient(#000, #2b1055);
        --primary-color: #fff;
        --secondary-color: #112434;
        --stars-display: block;
        --fireflies-display: block;
        --text-color: #fff;
      }

      body {
        margin: 0;
        padding: 0;
        min-height: 100vh;
        width: 100vw;
        height: 100vh;
        overflow: hidden;
      }

      section {
        width: 100%;
        height: 100%;
        overflow: hidden;
      }

      section#content #bg {
        height: 100%;
        width: 100%;
        background: var(--background-color);
        background-size: cover;
        position: absolute;
        z-index: -99;
        opacity: 100%;
      }

      @keyframes bgcolor {
        0% {
          opacity: 0;
        }

        100% {
          opacity: 100%;
        }
      }

      section#content #cover {
        height: 100%;
        width: 100%;
        background: #bbb;
        background-size: cover;
        position: absolute;
        z-index: 98;
        opacity: 100%;
      }

      @keyframes fadeout {
        0% {
          opacity: 100%;
        }

        100% {
          opacity: 0%;
        }
      }

      img {
        position: absolute;
        width: 100%;
      }

      #tree {
        z-index: 1;
      }

      #leaves {
        z-index: 2;
        animation: leavesA 5s ease-in-out infinite;
      }

      @keyframes leavesA {
        0% {
          transform: rotate(-0.7deg);
        }

        50% {
          transform: rotate(0.7deg);
        }

        100% {
          transform: rotate(-0.7deg);
        }
      }

      #grass {
        animation: grassA 5s ease-in-out infinite;
        width: 105%;
        left: -2.5%;
        top: -4%;
        z-index: 2;
      }

      @keyframes grassA {
        0% {
          transform: translateX(-3px);
        }

        50% {
          transform: translateX(3px);
        }

        100% {
          transform: translateX(-3px);
        }
      }

      img#flowerR {
        transform-origin: bottom right;
        z-index: 3;
        animation: flowerA 5s ease-in-out infinite;
      }

      img#flowerL {
        transform-origin: bottom left;
        z-index: 3;
        animation: flowerA 5s ease-in-out infinite;
      }

      @keyframes flowerA {
        0% {
          transform: rotate(-3deg);
        }

        50% {
          transform: rotate(3deg);
        }

        100% {
          transform: rotate(-3deg);
        }
      }

      .content star {
        display: var(--stars-display);
        position: absolute;
        background: #fff;
        border-radius: 50%;
        animation: twinkle linear infinite;
      }

      @keyframes twinkle {
        0% {
          opacity: 0;
          transform: translateY(0);
        }

        10%,
        90% {
          opacity: 1;
        }

        100% {
          opacity: 0;
          transform: translateY(-100px);
        }
      }

      #fireflies {
        width: 100%;
        height: 40%;
        position: absolute;
        bottom: 0;
        z-index: 99;
        opacity: 0%;
      }

      #fireflies fireflies {
        display: var(--stars-display);
        position: absolute;
        background: yellow;
        border-radius: 50%;
        animation: fly linear infinite;
      }

      @keyframes fly {
        0% {
          opacity: 0;
          transform: translateX(0);
        }

        10%,
        90% {
          opacity: 1;
        }

        100% {
          opacity: 0;
          transform: translateX(100px);
        }
      }

      #wrapDayNight {
        position: absolute;
        display: flex;
        width: 100%;
        height: 100%;
        z-index: 9;
        top: 5vh;
        left: 5vh;
      }

      .wrapper .daynight {
        width: 50px;
        height: 150vh;
        position: relative;
        transition: 1s;
        z-index: 4;
      }

      .daynight #sun {
        width: 50px;
        height: 50px;
        background-color: yellow;
        border-radius: 50%;
        box-shadow: 0px 0px 25px 25px rgba(255, 255, 0, 0.5);
        position: absolute;
        top: 0;
        cursor: pointer;
      }

      .daynight #moon {
        width: 50px;
        height: 50px;
        background-color: #fff;
        border-radius: 50%;
        box-shadow: 0px 0px 25px 25px rgba(86, 96, 190, 0.5);
        position: absolute;
        bottom: -0px;
        cursor: pointer;
      }

      .shootingStar {
        display: none;
      }

      .shootingStar span {
        position: absolute;
        top: 50%;
        left: 50%;
        width: 4px;
        height: 4px;
        background: #fff;
        border-radius: 50%;
        box-shadow: 0 0 0 4px rgba(255, 255, 255, 0.1),
          0 0 0 8px rgba(255, 255, 255, 0.1) 0 0 20px rgba(255, 255, 255, 1);
        animation: shoot 3s linear infinite;
      }

      #shootingStar.one span {
        animation: shoot 3s linear;
      }

      #shootingStar.none span {
        animation: none;
      }

      .shootingStar span::before {
        content: "";
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 300px;
        height: 1px;
        background: linear-gradient(90deg, #fff, transparent);
      }

      @keyframes shoot {
        0% {
          transform: rotate(315deg) translateX(0);
          opacity: 1;
        }

        70% {
          opacity: 1;
        }

        100% {
          transform: rotate(315deg) translateX(-1000px);
          opacity: 0;
        }
      }

      .shootingStar span:nth-child(1) {
        top: 0;
        right: -10px;
        left: initial;
        animation-delay: 0;
        animation-duration: 1s;
      }

      .shootingStar span:nth-child(2) {
        top: 0;
        right: -80px;
        left: initial;
        animation-delay: -0.2;
        animation-duration: 3s;
      }

      .shootingStar span:nth-child(3) {
        top: -10px;
        right: 100px;
        left: initial;
        animation-delay: -0.4;
        animation-duration: 2s;
      }

      .shootingStar span:nth-child(4) {
        bottom: 100px;
        right: -60px;
        left: initial;
        animation-delay: -0.7;
        animation-duration: 4s;
      }

      span#text {
        position: absolute;
        top: 23%;
        left: 50%;
        transform: translateX(-50%);
        font-size: 18px;
        z-index: 99;
        color: var(--text-color);
        text-align: center;
        /* font-family: cursive; */
      }

      @keyframes fade {
        0% {
          opacity: 0;
        }

        100% {
          opacity: 100%;
        }
      }

      span#magic {
        position: absolute;
        top: 35%;
        left: 50%;
        transform: translateX(-50%);
        font-size: 30px;
        z-index: 99;
        color: var(--text-color);
        text-align: center;
        font-family: cursive;
        display: none;
      }

      #btnWrap {
        width: 100%;
        height: 100%;
        justify-content: center;
        top: 35%;
        gap: 10px;
        position: absolute;
        z-index: 99;
        display: none;
      }

      #btnWrap button {
        width: fit-content;
        height: fit-content;
        border-radius: 5px;
        box-shadow: none;
      }

      .gam {
        position: absolute;
        z-index: 100;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        width: 40vw;
        border: #fff 5px solid;
        display: none;
      }

      #cloud-wrap {
        bottom: 0;
        left: 0;
        padding-top: 85px;
        position: fixed;
        right: 0;
        top: 0;
        z-index: -1;
      }

      @-webkit-keyframes animateCloud {
        0% {
          margin-left: -1000px;
        }

        100% {
          margin-left: 100%;
        }
      }

      @-moz-keyframes animateCloud {
        0% {
          margin-left: -1000px;
        }

        100% {
          margin-left: 100%;
        }
      }

      @keyframes animateCloud {
        0% {
          margin-left: -1000px;
        }

        100% {
          margin-left: 100%;
        }
      }

      .x1 {
        -webkit-animation: animateCloud 35s linear infinite;
        -moz-animation: animateCloud 35s linear infinite;
        animation: animateCloud 35s linear infinite;

        -webkit-transform: scale(0.65);
        -moz-transform: scale(0.65);
        transform: scale(0.65);
      }

      .x2 {
        -webkit-animation: animateCloud 20s linear infinite;
        -moz-animation: animateCloud 20s linear infinite;
        animation: animateCloud 20s linear infinite;

        -webkit-transform: scale(0.3);
        -moz-transform: scale(0.3);
        transform: scale(0.3);
      }

      .x3 {
        -webkit-animation: animateCloud 30s linear infinite;
        -moz-animation: animateCloud 30s linear infinite;
        animation: animateCloud 30s linear infinite;

        -webkit-transform: scale(0.5);
        -moz-transform: scale(0.5);
        transform: scale(0.5);
      }

      .x4 {
        -webkit-animation: animateCloud 18s linear infinite;
        -moz-animation: animateCloud 18s linear infinite;
        animation: animateCloud 18s linear infinite;

        -webkit-transform: scale(0.4);
        -moz-transform: scale(0.4);
        transform: scale(0.4);
      }

      .x5 {
        -webkit-animation: animateCloud 25s linear infinite;
        -moz-animation: animateCloud 25s linear infinite;
        animation: animateCloud 25s linear infinite;

        -webkit-transform: scale(0.55);
        -moz-transform: scale(0.55);
        transform: scale(0.55);
      }

      .cloud {
        background: #fff;
        background: -moz-linear-gradient(top, #fff 5%, #f1f1f1 100%);
        background: -webkit-gradient(
          linear,
          left top,
          left bottom,
          color-stop(5%, #fff),
          color-stop(100%, #f1f1f1)
        );
        background: -webkit-linear-gradient(top, #fff 5%, #f1f1f1 100%);
        background: -o-linear-gradient(top, #fff 5%, #f1f1f1 100%);
        background: -ms-linear-gradient(top, #fff 5%, #f1f1f1 100%);
        background: linear-gradient(top, #fff 5%, #f1f1f1 100%);
        filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#fff', endColorstr='#f1f1f1', GradientType=0);

        -webkit-border-radius: 100px;
        -moz-border-radius: 100px;
        border-radius: 100px;

        -webkit-box-shadow: 0 8px 5px rgba(0, 0, 0, 0.1);
        -moz-box-shadow: 0 8px 5px rgba(0, 0, 0, 0.1);
        box-shadow: 0 8px 5px rgba(0, 0, 0, 0.1);

        height: 120px;
        position: relative;
        width: 350px;
        transform: scale(0.5);
      }

      .cloud:after,
      .cloud:before {
        background: #fff;
        content: "";
        position: absolute;
        z-index: -1;
      }

      .cloud:after {
        -webkit-border-radius: 100px;
        -moz-border-radius: 100px;
        border-radius: 100px;

        height: 100px;
        left: 50px;
        top: -50px;
        width: 100px;
      }

      .cloud:before {
        -webkit-border-radius: 200px;
        -moz-border-radius: 200px;
        border-radius: 200px;

        width: 180px;
        height: 180px;
        right: 50px;
        top: -90px;
      }

      #giftbig,
      #giftsmall {
        display: flex;
        opacity: 100%;
        transition: opacity 2s ease-in;
        z-index: 3;
      }

      #giftbig.hide {
        opacity: 0%;
      }
    </style>
  </head>

  <body>
    <section class="content" id="content">
      <div id="bg"></div>
      <span id="text">Halooooo👋</span>
      <div id="cover"></div>
      <span id="magic">-rafii gantengnya oii</span>
      <div id="btnWrap">
        <button id="yes">sempet kok</button>
        <button id="no">GAK SEMPET!</button>
      </div>

      <!-- bg -->
      <img src="kue.png" alt="" id="tree" />
      <img src="gift-big.png" alt="" id="giftbig" />
      <!-- <img src="gift-small.png" alt="" id="giftsmall" /> -->

      <div class="shootingStar" id="shootingStar"></div>

      <div class="wrapper" id="wrapDayNight">
        <div class="daynight" id="daynight">
          <div id="sun"></div>
          <div id="moon"></div>
        </div>
      </div>

      <section class="fireworks" id="fireworks"></section>

      <section id="fireflies"></section>

      <div id="cloud-wrap">
        <div class="x1">
          <div class="cloud" id="cloud"></div>
        </div>

        <div class="x2">
          <div class="cloud" id="cloud"></div>
        </div>

        <div class="x3">
          <div class="cloud" id="cloud"></div>
        </div>

        <div class="x4">
          <div class="cloud" id="cloud"></div>
        </div>

        <div class="x5">
          <div class="cloud" id="cloud"></div>
        </div>
      </div>
    </section>

    <script>
      const audio = ["backsound.mp3"]; //Just change this source to change the song
      const audioNames = [(audioEnchanted = new Audio())];
      for (let i = 0; i < audio.length; i++) {
        audioNames[i].src = audio[i];
      }
      function audioPlay(name) {
        // play audio
        if (name === "Enchanted") {
          audioNames[0].play();
        }
      }
      function play() {
        audioPlay("Enchanted");
      }

      const isMobile = {
        Android: function () {
          return navigator.userAgent.match(/Android/i);
        },
        BlackBerry: function () {
          return navigator.userAgent.match(/BlackBerry/i);
        },
        iOS: function () {
          return navigator.userAgent.match(/iPhone|iPad|iPod/i);
        },
        Opera: function () {
          return navigator.userAgent.match(/Opera Mini/i);
        },
        Windows: function () {
          return navigator.userAgent.match(/IEMobile/i);
        },
        any: function () {
          return (
            isMobile.Android() ||
            isMobile.BlackBerry() ||
            isMobile.iOS() ||
            isMobile.Opera() ||
            isMobile.Windows()
          );
        },
      };

      if (isMobile.any()) {
        alert("Hi, pastikan udah hidupin volume suara ya dan ga budek");
      }

      let daynight = document.getElementById("daynight");
      let sun = document.querySelector("#sun");
      let moon = document.querySelector("#moon");
      let bg = document.getElementById("bg");
      var rotation = 0;
      let day = "day";
      let cloud = document.getElementById("cloud-wrap");

      sun.addEventListener("click", rotate);
      moon.addEventListener("click", rotate);

      function rotate() {
        if (
          text.innerHTML == "udahh? sekarang pencet mataharinya" ||
          scene >= 45
        ) {
          rotation = rotation + 0.5;
          daynight.style.transform = "rotate(" + rotation + "turn)";
          document.body.classList.toggle("dark-theme");
        }
        if (rotation % 1 == 0) {
          day = "day";
          cloud.style.display = "block";
        } else {
          day = "night";
          cloud.style.display = "none";
        }
      }

      function stars() {
        let count = 500;
        let scene = document.querySelector(".content");
        let i = 0;
        while (i < count) {
          let star = document.createElement("star");
          let x = Math.floor(Math.random() * window.innerWidth);
          let y = Math.floor(Math.random() * window.innerHeight);
          let duration = Math.random() * 10;
          let size = Math.random() * 1;

          star.style.left = x + "px";
          star.style.top = y + "px";
          star.style.width = 1 + size + "px";
          star.style.height = 1 + size + "px";
          star.style.animationDuration = 15 + duration + "s";
          star.style.animationDelay = duration + "s";

          scene.appendChild(star);
          i++;
        }
      }

      function firefliesF() {
        let scene = document.querySelector("#fireflies");
        let count = 300;
        let i = 0;
        while (i < count) {
          let fireflies = document.createElement("fireflies");
          let x = Math.floor(Math.random() * window.innerWidth);
          let y = Math.floor(Math.random() * window.innerHeight);
          let duration = Math.random() * 10;
          let size = Math.random() * 1;

          fireflies.style.left = x + "px";
          fireflies.style.top = y + "px";
          fireflies.style.width = 1 + size + "px";
          fireflies.style.height = 1 + size + "px";
          fireflies.style.animationDuration = 15 + duration + "s";
          fireflies.style.animationDelay = duration + "s";

          scene.appendChild(fireflies);
          i++;
        }
      }

      let content = document.getElementById("content");
      let text = document.getElementById("text");
      let magic = document.getElementById("magic");
      let shoots = document.getElementById("shootingStar");
      let btn = document.getElementById("btnWrap");
      let cover = document.getElementById("cover");
      let yes = document.getElementById("yes");
      let no = document.getElementById("no");
      let scene = -1;
      let count = 0;
      let giftBig = document.getElementById("giftbig");
      let arrow = document.getElementById("arrow");
      // let g1 = document.getElementById('g1');
      content.addEventListener("click", function () {
        scene++;
        if (scene == 0) {
          cover.style.animation = "fadeout 1s alternate forwards";
          play();
          console.log("Created by: MR90");
        } else if (scene == 1) {
          text.innerHTML =
            "harusnya ini ngasihnya pas di hari ulang tahunmu, tapi jangankan baca ini, buka hp aja gaboleh wkwk";
          cover.style.zIndex = "-98";
          play();
        } else if (scene == 2) {
          text.innerHTML = "ciee selesaii.. dapat gelar apanih?";
          play();
        } else if (scene == 3) {
          text.innerHTML = "ustadzah? bu nyai? atau humaira?";
          play();
        } else if (scene == 4) {
          text.innerHTML = "oiya dus, I wanna got something for you";
          play();
        } else if (scene == 5) {
          text.innerHTML = "semoga suka yaaa";
          play();
        } else if (scene == 6) {
          text.innerHTML = "kalo gasuka, nuwemenn bangett kamuu";
          play();
        } else if (scene == 7) {
          text.innerHTML = "coba tebak isinya apa!?";
          play();
        } else if (scene == 8) {
          text.innerHTML = "udah?";
          play();
        } else if (scene == 9) {
          text.innerHTML = "awas kagett yaa";
          play();
        } else if (scene == 10) {
          text.innerHTML = "penasaran gak apa isi nya?";
          play();
        } else if (scene == 11) {
          text.innerHTML = "mau dibuka sekarang ga?";
          play();
        } else if (scene == 12) {
          text.innerHTML = "jangan dulu deh, nanti aja hehehe";
          play();
        } else if (scene == 13) {
          text.innerHTML =
            "I wanna tell you something.. tapi nanti, tunggu malam dulu";
          play();
        } else if (scene == 14) {
          text.innerHTML = "lama ga sih kalo harus nunggu malam beneran?";
          play();
        } else if (scene == 15) {
          text.innerHTML =
            "sini, aku mau ngasih kamu kekuatan, biar kamu bisa ngerubah siang jadi malam";
          play();
        } else if (scene == 16) {
          text.innerHTML =
            "coba merem, terus ucapin mantra (rafi ganteng 3x) nnti kalo udah kamu buka mata nya";
          play();
        } else if (scene == 17) {
          text.innerHTML = "udahh? sekarang pencet mataharinya";
          play();
        } else if (scene == 18 && day == "night") {
          play();
          bg.style.background = "#000";
          let count = 0;
          text.innerHTML = "";
          const actionInterval = setInterval(function () {
            if (count == 3) {
              clearInterval(actionInterval);
              text.innerHTML = "gimana? keren gak?";
            }
            count++;
          }, 500);
        } else if (scene >= 18 && scene <= 43 && day != "night") {
          scene = 17;
          text.innerHTML = "udahh? sekarang pencet mataharinya";
          play();
        } else if (scene == 19) {
          text.innerHTML =
            "eh.. tapi sepi gak sih langitnya? pengen yang lebih keren lagi gak?";
          text.style.transitionDelay = "0s";
          play();
        } else if (scene == 20) {
          text.innerHTML = "sekalian kita buka kado nya oke?";
          play();
        } else if (scene == 21) {
          text.innerHTML = "siap siap dinduss";
          play();
        } else if (scene == 22) {
          text.innerHTML = "ready?";
          play();
        } else if (scene == 23) {
          play();
          $(".fireworks").fireworks({
            sound: false,
            opacity: 1,
            width: "100%",
            height: "100%",
          });
          count = 3;
          const actionInterval = setInterval(function () {
            text.style.fontSize = "30px";
            if (count > 0) text.innerHTML = count;
            else if (count == 0) {
              text.innerHTML = "";
              text.style.fontSize = "18px";
              scene = 23;
              stars();
            } else if (count == -3) {
              $(".fireworks").remove();
              bg.style.background = "var(--background-color)";
              bg.style.animation = "bgcolor 1.5s linear";
              document.body.classList.add("star");
              text.style.top = "20%";
              scene = 23;
            } else if (count == -4) {
              text.style.animation = "fade 2s linear";
              text.style.fontSize = "30px";
              text.innerHTML = "Happy Birthday Dinda Khusnia Amaliah";
              giftBig.classList.add("hide");
              clearInterval(actionInterval);
              scene = 23;
            }
            count--;
            scene = 23;
          }, 1000);
          scene = 23;
        } else if (scene == 24 && count == -5) {
          text.style.fontSize = "18px";
          text.style.top = "23%";
          text.innerHTML = "kado nya kue palsu sama 19.705 bintang yaa";
          play();
        } else if (scene == 25 && count == -5) {
          text.style.fontSize = "18px";
          text.style.top = "23%";
          text.innerHTML = "kalo gapercaya itung aja sendiri itu bintangnya";
          play();
        } else if (scene == 26 && count == -5) {
          text.style.fontSize = "18px";
          text.style.top = "23%";
          text.innerHTML = "sekarang kamu wish yaa";
          play();
        } else if (scene == 27 && count == -5) {
          text.style.fontSize = "18px";
          text.style.top = "23%";
          text.innerHTML = "tuhh, tak kasih bintang jatuh satu";
          shoots.style.display = "block";
          shoots.innerHTML = "<span></span>";
          shoots.classList = "shootingStar one";
          play();
        } else if (scene == 28 && count == -5) {
          text.innerHTML = "kecepetan ya? wkwk";
          shoots.classList = "shootingStar none";
          play();
        } else if (scene == 29) {
          text.innerHTML = "maaf deh, mau lagi gakk?";
          play();
        } else if (scene == 30) {
          text.innerHTML = "udah tuhh, cepetan make a wish";
          shoots.classList = "shootingStar one";
          play();
        } else if (scene == 31) {
          text.innerHTML = "sempet gak? kalo ga sempet mau aku kasih lagi";
          play();
        } else if (scene == 32) {
          text.innerHTML = "mau gak?";
          yes.innerHTML = "mauuu dong";
          no.innerHTML = "mau bangettt";
          btn.style.display = "flex";
          play();
        } else if (scene == 33) {
          text.innerHTML = "tuh aku kasih kamu buwanyakkk bintang jatuh";
          btn.style.display = "none";
          shoots.classList = "shootingStar";
          shoots.innerHTML =
            "<span></span><span></span><span></span><span></span><span></span>";
          play();
        } else if (scene == 34) {
          text.innerHTML = "biar kamu bisa make a wish sepuasnya";
          play();
        } else if (scene == 35) {
          text.innerHTML =
            "oiya tadi aku bilang, mau ngomong sesuatu sama kamu";
          play();
        } else if (scene == 36) {
          text.innerHTML = "bukan ngomong sih, soalnya ini ngetik hehe";
          play();
        } else if (scene == 37) {
          text.innerHTML = "aku cuma mau bilang";
          play();
        } else if (scene == 38) {
          text.innerHTML =
            "tahun ini umur kamu bertambah satu tahun dan jatah hidup kamu berkurang satu tahun juga";
          play();
        } else if (scene == 39) {
          text.innerHTML =
            "makasih ya udah mau terus berjuang sampai sekarang ini";
          play();
        } else if (scene == 40) {
          text.innerHTML =
            "banyak hal yang sudah kamu laluin.. tapi perlu kamu ingat, masih banyaakk lagi hal yang belum dan akan kamu laluin nantii";
          play();
        } else if (scene == 41) {
          text.innerHTML =
            "semakin kamu dewasa, semakin banyak juga rintangannya. but it's okayyy";
          play();
        } else if (scene == 42) {
          text.innerHTML = "kalo kamu butuh akuu.. I'm here";
          play();
        } else if (scene == 43) {
          text.innerHTML =
            "juga jangan lupa kalo Allah selalu ada untuk hambanya yang membutuhkan";
          play();
        } else if (scene == 44) {
          text.innerHTML =
            "apapun susahnya, apapun sedihnya, apapun senangnya harus kamu nikmatin, dan jangan lupa bersyukur";
          play();
        } else if (scene == 45) {
          text.innerHTML =
            "buktikan pada semua orang kalo kamu itu dindus bukan sembarang dindus. you're awesome!";
          play();
        } else if (scene == 46) {
          text.innerHTML = "pesanku...";
          play();
        } else if (scene == 47) {
          text.innerHTML =
            "jadilah dirimu sendiri, jangan jadi orang lain hanya untuk menyenangkan orang lain";
          play();
        } else if (scene == 48) {
          text.innerHTML =
            "kamu juga punya hati yang perlu kamu dengarkan juga";
          play();
        } else if (scene == 49) {
          text.innerHTML =
            "May this year bring you happiness, health, and everything you've always dreamed of";
          play();
        } else if (scene == 50) {
          text.innerHTML =
            "And may you always be surrounded by the people you love.";
          play();
        } else if (scene == 51) {
          text.innerHTML = "I LOVE YOU";
          firefliesF();
        } else if (scene == 52) {
          document.body.classList.add("fireflies");
          magic.style.display = "block";
          magic.style.animation = "fade 2s linear";
          document.querySelector("#fireflies").style.animation =
            "fade 1s alternate forwards";
          text.style.animation = "fade 1s linear";
          text.innerHTML = "";
          play();
        } else if (scene >= 53) {
          text.innerHTML = "";
          play();
        }
      });
    </script>

    <!-- Fireworks -->
    <script src="http://code.jquery.com/jquery-3.3.1.js"></script>
    <script type="text/javascript">
      (function ($) {
        $.fn.fireworks = function (options) {
          // set the defaults
          options = options || {};

          options.sound = options.sound || false;
          options.opacity = options.opacity || 1;
          options.width = options.width || $(this).width();
          options.height = options.height || $(this).height();

          var fireworksField = this,
            particles = [],
            rockets = [],
            MAX_PARTICLES = 400,
            SCREEN_WIDTH = options.width,
            SCREEN_HEIGHT = options.height;

          // cache the sounds if the plugin has been configured to use soudns
          var sounds = [],
            audio;
          if (options.sound) {
            sounds.push({
              prefix: "data:audio/wav;base64,",
              data: "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",
            });
            sounds.push({
              prefix: "data:audio/wav;base64,",
              data: "UklGRqStAABXQVZFZm10IBAAAAABAAIARKwAABCxAgAEABAAZGF0YYCtAAB7AHIAdABtAHsAawCaAGsAxgB4ANcAhgCvAGkAegBiAJAAfACVAJwAogCvAJsAuQCNALEAewCfAGwAjQBrAIQAeACIAHcAiABuAIIAeACMAHIAjQBcAHgAYACDAHcAjAB6AJMAfwCaAHEAlgBSAIMAUAB6AGEAcwB1AGkAkQBoAI0AWAB/AFMAgQBcAIoAeQCNAIkAlACdAIcAlACVAJUAoACQAIgAdQBxAFoAdQBcAIQAaQCXAHkAkgB/AJAAfwCfAIwAtwCaAJEAfwCNAH4AigCFAHgAggBmAG8AggCDAMAAmgDUAJwAwwCFAJsAYwCsAHMAsQB7AKAAfACCAHsAdAB6AHMAfwCQAI4AlgCLAKUAigC9AJ4AsQCXAJcAlACHAJUAlgCnAJsArgCeALUAhQCqAGQAlQBiAJ0AdwCmAIUAswCCAKwAWwCNAEIAcQBRAGkAYgBlAG4AYgBdAFsAQwBRAEsAZABUAHIAUQBtAFIAZgBVAF0AVQBGAGEARwB0AEoAbABHAGwAVAB+AGUAjwB/AJAAgQCWAIgAjwCHAIUAhABuAHYAYQB0AIQAiACXAJcAnQCWAIgAiwBxAHgAcgB1AIkAiACVAI8AegCOAGUAiQBpAJMAeQCfAKEArwCTAKEAfACHAGoAeQB+AIEAlQCNAJkAlQCNAJIAiwCaAJIApQCfAKsAqgCxALkAuACwALYApQCsAJcArACUAKsAogCxAKgAugC1ALsAwwDGAMEAyQChALcAgwCpAH4AqQCXALEAsADAAMMAxAC7AL4AoACtAJUAqACVAKsArQCzANEAzQD9AOoA8wDuAL4A0wC6ANQA8AD5AB0BFAEOAQkB5wDzAM8A5wDTAOsA2wDoAOIA8QDfAOUAzwDgAMoA3QDHANkAzADfANcA4ADlAO0A7QDzAPIA9AD6AP4ACgH/ACABEAEvARYBJwEYARQBDQEVARIBKwEjAUwBOwFVAUIBRgFDATUBNQEiATUBEwEnAQwBJAEUASkBFgEvAQgBJgH7ACoBGAE2AQsBPAHrABoB3QAZARIBMgFHAVUBTgFVATEBRQETAS8BCQEnARoBHgE1ASQBMwEaARkBBQH1APcA8AD2AO8A+wABAQUBEwESASwBIQExASwB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",
            });
            sounds.push({
              prefix: "data:audio/wav;base64,",
              data: "UklGRnivAABXQVZFZm10IBAAAAABAAIARKwAABCxAgAEABAAZGF0YVSvAACf/7f/pf+7/6//xP+p/7v/kv+t/5X/qP+e/63/n/+r/4f/m/93/5D/if+l/4n/nv96/5L/eP+G/3j/hf97/3z/fv+B/3v/gf+N/43/q/+s/73/tv+3/7T/uP/A/7f/xv+s/8//sP/X/7X/5v++/+T/u//d/8r/1f/k/9v/AwDp/wgA4f/y/9j/2f/D/7n/u/+4/8D/v//O/8T/3P+q/8z/lv+6/4n/s/+Z/6n/rv+x/8T/rv/F/6L/wf+h/8D/oP+x/6X/uv+x/8H/wP+x/7v/iv+f/3//nv+s/7j/4//m//H/6f/Y/9n/yv/G/9f/xf/j/8v/9f/d//v/+v8CABcAEwA+ACwAWgATAEoA+P80AP3/JQAiAD4AUABLAHcAZgCDAGoAXwBRADIAMQA9AD0AXgBeAGIAZgBNAGEAOABSADQASAAwADkALgAjADgAHABJAB8AWgAqAGsAPABxAFAAaABVAGcAXgBbAFQARwBAAD4ALgBsAEQAkABZAK4AawCdAGkAogBnAMEAggDJAIQAwAB/ALYAgQDOAJkA0ACeAMwApQC8AJYAoQCGAJ4AggCsAIMAtACJAMAAkQCqAIsAhQB7AJQAhwDLALIA4AC9ALkAoACdAIcAqQCPAMAAlACvAJIAggBtAG8AawCJAIUAwgCsAN4A0QDsANoAygDTAK0AwQCdALYAvwDJAMYAyACzAK8AiACSAH0AigB/AJEAjACgAKAAtQCnALgAkACoAI4AlgCrAKkAyQC1AMcAqgDJAKwA1ACuANEAnwDPAJ4A8wCrAPcAvADvALsA0wC3ANEAwwD2ANQAAwHeAO4AtQDFAI8AvwB4ANQAhADVAIsAuAB8AIQAawCDAGoAiQB8AJcAhQCRAJUAhQCLAHgAiQB9AIQAlACPAK8ApAC9AKIAtACZALoAkADSAKgAywCpALgAqwC7AK8AzADHAOwA0QDyAOMA4QDHALcAqACqAIwArACJAL0AkQC2AJEAqgB/AKMAfQC2AJQAtgCnAKsArgCgALUAnQC1AK0AuwC/AMYAwQDAAMcAuQDiAMMABwHZADQBAwFJARUBOQELASYB+QAnAQMBNwEiATcBLAEmASkBGAEbARYBFwEQAQ0BCwH9APwA9wDzAOkA6wDoANgA3gC7AMsAmQCzAJIAtgCTALcAiACwAIYAogCFAKcAlgCgAJwAnwC+AKkA2QC8ANkAqwDPAJAA1wCZAPQArgAHAcYAEgHNABAB1gD5ALwA5QCtAO8AuwD7AMwA7AC4ANkAogDgAKMAAQHIACoB7QA4AQMBFQHdANoApQDVAKAA9gDPAP4A1QDwAL8A5AC4APQAvADWAKQAzAB7ANgAkQARAbQAIwHNACYBuwAMAaoA/QCYAPgAngD/AK4A/AC2AAcByQALAdsAGAHtABEB7AAWAfAAMgEPAU8BKQFQAS0BOAERASAB+gAUAfgAHAEEARYBDQH3APUAzwDRAK0AtwCqAK0AuwC6ANEAxwDOALkApwCLAI0AZgCKAGMAnQB3AI0AbgB3AGUAagBsAH8AigB3AJUAUABuADEAWAAxAFcAMwBaACsARgAlADkAIAAxACAANAAgACsAJgA5ADUARgA1AEwALwA9ADMAPQA5ADoAQgA1AFEAKgBkADAAYwAnAGIAHwB5ACcAkQA7ALAAWACrAGEAeABCAGUANwBrAEcAeABNAHYATQCCAEwAmwBdAKYAYACtAF4ArwBhALoAcQCyAHMAoQBvAJ4AfwCpAIcAnACLAKMAgwCrAI4ApwCNALoAkQDCAJIAsgCEAIQAagCLAHkApQCSAM8AugDLAMMAuwDFALAAuQC8AMQAzQDEAOEA1AD3ANsA8QDXAN8AxAC+AK4AnACUAI8AlQCXAJ0AhACaAHEAiwBtAIoAZwB4AFYAawBlAGQAcQBmAIQAZQCGAF4AhABXAHwATQCDAFEAcQBGAHAATQB9AF4AkQBvAIQAbwB6AGUAYQBUAHIAXQCVAGkApgB1ALUAdgDkAJEABwGrABEBrwAFAbMA8wCuANUApQDLALAAwQCwAJsAngBnAH4ARwBpAFQAcQB3AIcAfACMAHQAggB4AIcAZAB3AEwAagBVAHcAjgCeAKAAtACfAK0AZQCFACwAVAAUAEAAHwBEAC0AUwAcAD0A8f8jANP/CgDX/xEA8P8gAOj/DwDV//z/uf/W/6X/zf+v/8z/r//R/4r/tv9c/5T/Sv9//zr/dv83/3D/K/9m/zf/aP9o/4L/h/+W/5z/of+h/6L/rP+c/6L/jf+z/47/2f+m//H/tf/r/7D/3/+r/9//tf/+/9//EgD9/wAAAgDw/+3/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",
            });

            audio = document.createElement("audio");
          }

          // create canvas and get the context
          var canvas = document.createElement("canvas");
          canvas.id = "fireworksField";
          canvas.width = SCREEN_WIDTH;
          canvas.height = SCREEN_HEIGHT;
          canvas.style.width = SCREEN_WIDTH + "px";
          canvas.style.height = SCREEN_HEIGHT + "px";
          canvas.style.position = "absolute";
          canvas.style.top = "0px";
          canvas.style.left = "0px";
          canvas.style.opacity = options.opacity;
          var context = canvas.getContext("2d");

          // The Particles Object
          function Particle(pos) {
            this.pos = {
              x: pos ? pos.x : 0,
              y: pos ? pos.y : 0,
            };
            this.vel = {
              x: 0,
              y: 0,
            };
            this.shrink = 0.97;
            this.size = 2;

            this.resistance = 1;
            this.gravity = 0;

            this.flick = false;

            this.alpha = 1;
            this.fade = 0;
            this.color = 0;
          }

          Particle.prototype.update = function () {
            // apply resistance
            this.vel.x *= this.resistance;
            this.vel.y *= this.resistance;

            // gravity down
            this.vel.y += this.gravity;

            // update position based on speed
            this.pos.x += this.vel.x;
            this.pos.y += this.vel.y;

            // shrink
            this.size *= this.shrink;

            // fade out
            this.alpha -= this.fade;
          };

          Particle.prototype.render = function (c) {
            if (!this.exists()) {
              return;
            }

            c.save();

            c.globalCompositeOperation = "lighter";

            var x = this.pos.x,
              y = this.pos.y,
              r = this.size / 2;

            var gradient = c.createRadialGradient(x, y, 0.1, x, y, r);
            gradient.addColorStop(0.1, "rgba(255,255,255," + this.alpha + ")");
            gradient.addColorStop(
              0.8,
              "hsla(" + this.color + ", 100%, 50%, " + this.alpha + ")"
            );
            gradient.addColorStop(
              1,
              "hsla(" + this.color + ", 100%, 50%, 0.1)"
            );

            c.fillStyle = gradient;

            c.beginPath();
            c.arc(
              this.pos.x,
              this.pos.y,
              this.flick ? Math.random() * this.size : this.size,
              0,
              Math.PI * 2,
              true
            );
            c.closePath();
            c.fill();

            c.restore();
          };

          Particle.prototype.exists = function () {
            return this.alpha >= 0.1 && this.size >= 1;
          };

          // The Rocket Object
          function Rocket(x) {
            Particle.apply(this, [
              {
                x: x,
                y: SCREEN_HEIGHT,
              },
            ]);

            this.explosionColor = 0;
          }

          Rocket.prototype = new Particle();
          Rocket.prototype.constructor = Rocket;

          Rocket.prototype.explode = function () {
            if (options.sound) {
              var randomNumber = (function (min, max) {
                min = Math.ceil(min);
                max = Math.floor(max);
                return Math.floor(Math.random() * (max - min + 1)) + min;
              })(0, 2);
              audio.src =
                sounds[randomNumber].prefix + sounds[randomNumber].data;
              // audio.play();
            }

            var count = Math.random() * 10 + 80;

            for (var i = 0; i < count; i++) {
              var particle = new Particle(this.pos);
              var angle = Math.random() * Math.PI * 2;

              // emulate 3D effect by using cosine and put more particles in the middle
              var speed = Math.cos((Math.random() * Math.PI) / 2) * 15;

              particle.vel.x = Math.cos(angle) * speed;
              particle.vel.y = Math.sin(angle) * speed;

              particle.size = 10;

              particle.gravity = 0.2;
              particle.resistance = 0.92;
              particle.shrink = Math.random() * 0.05 + 0.93;

              particle.flick = true;
              particle.color = this.explosionColor;

              particles.push(particle);
            }
          };

          Rocket.prototype.render = function (c) {
            if (!this.exists()) {
              return;
            }

            c.save();

            c.globalCompositeOperation = "lighter";

            var x = this.pos.x,
              y = this.pos.y,
              r = this.size / 2;

            var gradient = c.createRadialGradient(x, y, 0.1, x, y, r);
            gradient.addColorStop(
              0.1,
              "rgba(255, 255, 255 ," + this.alpha + ")"
            );
            gradient.addColorStop(1, "rgba(0, 0, 0, " + this.alpha + ")");

            c.fillStyle = gradient;

            c.beginPath();
            c.arc(
              this.pos.x,
              this.pos.y,
              this.flick
                ? (Math.random() * this.size) / 2 + this.size / 2
                : this.size,
              0,
              Math.PI * 2,
              true
            );
            c.closePath();
            c.fill();

            c.restore();
          };

          var loop = function () {
            // update screen size
            if (SCREEN_WIDTH != window.innerWidth) {
              canvas.width = SCREEN_WIDTH = window.innerWidth;
            }
            if (SCREEN_HEIGHT != window.innerHeight) {
              canvas.height = SCREEN_HEIGHT = window.innerHeight;
            }

            // clear canvas
            context.fillStyle = "rgba(0,0,0,0.1)";
            context.fillRect(0, 0, SCREEN_WIDTH, SCREEN_HEIGHT);
            // context.clearRect(0,0,SCREEN_WIDTH, SCREEN_HEIGHT);

            var existingRockets = [];

            for (var i = 0; i < rockets.length; i++) {
              // update and render
              rockets[i].update();
              rockets[i].render(context);

              // calculate distance with Pythagoras
              var distance = Math.sqrt(
                Math.pow(SCREEN_WIDTH - rockets[i].pos.x, 2) +
                  Math.pow(SCREEN_HEIGHT - rockets[i].pos.y, 2)
              );

              // random chance of 1% if rockets is above the middle
              var randomChance =
                rockets[i].pos.y < (SCREEN_HEIGHT * 2) / 3
                  ? Math.random() * 100 <= 1
                  : false;

              /* Explosion rules
			- 80% of screen
			- going down
			- close to the mouse
			- 1% chance of random explosion
		*/
              if (rockets[i].pos.y < SCREEN_HEIGHT / 6) {
                rockets[i].explode();
              } else {
                existingRockets.push(rockets[i]);
              }
            }

            rockets = existingRockets;

            var existingParticles = [];

            for (i = 0; i < particles.length; i++) {
              particles[i].update();

              // render and save particles that can be rendered
              if (particles[i].exists()) {
                particles[i].render(context);
                existingParticles.push(particles[i]);
              }
            }

            // update array with existing particles - old particles should be garbage collected
            particles = existingParticles;

            while (particles.length > MAX_PARTICLES) {
              particles.shift();
            }
          };

          var launchFrom = function (x) {
            if (rockets.length < 10) {
              var rocket = new Rocket(x);
              rocket.explosionColor =
                Math.floor((Math.random() * 360) / 10) * 10;
              rocket.vel.y = -7;
              rocket.vel.x = 0;
              // rocket.vel.y = Math.random() * -3 - 4;
              // rocket.vel.x = Math.random() * 6 - 3;
              rocket.size = 8;
              rocket.shrink = 0.999;
              rocket.gravity = 0.01;
              rockets.push(rocket);
            }
          };

          var launch = function () {
            launchFrom(SCREEN_WIDTH / 2);
          };

          // Append the canvas and start the loops
          $(fireworksField).append(canvas);
          setInterval(launch, 4000);
          setInterval(loop, 20);

          return fireworksField;
        };
      })(jQuery);
    </script>
  </body>
</html>
