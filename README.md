
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Selamat malam dan selamat lepas lelah sayang 🫶🏻💞</title>
  <meta name="description" content="HTML Pesan Teruntuk Kamuuu!">
    <meta name="keywords" content="html, pesan, kata kata, good night">
    <meta name="author" content="Feeldream">
    <meta name="robots" content="index, follow">
    <!-- Open Graph -->
    <meta property="og:title" content="Feeldream - HTML Night for You">
    <meta property="og:description" content="Script HTML Feeldream">
    <meta property="og:image" content="https://feeldreams.github.io/main-icon.png">
    <meta property="og:url" content="https://htmlku.my.id/">
    <meta property="og:site_name" content="Feeldream">
    <meta property="og:type" content="website">
    <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;600;700&family=Handlee&family=Sriracha&display=swap" rel="stylesheet"><link href="https://fonts.googleapis.com/css2?family=Varela+Round&display=swap" rel="stylesheet"><link href="https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Varela+Round&display=swap" rel="stylesheet"><script src="https://unpkg.com/typeit@8.7.0/dist/index.umd.js"></script><link rel="stylesheet" href="https://htmlku.com/lepaslelah/style.css">
</head>
<body>
  
  <!-- Audio -->
  <audio src="https://feeldreams.github.io/audio/wedont.mp3" id="linkmp3"></audio>
  
  <!-- Background / Wallpaper -->
  <div class="background-overlay" data-src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjuwbO_NyQeozwcybDF1OaPMzQy0t8AYv718sFc_lFl6LqHdyZG9HgQ-Tp4rusKtixlYVKBP-ORlbn30Q1pdMa3SOZ4osL8Cvg100Uh6FeD639gn6h0WwAQr_nAeUPJE8GKNk9eqN1YgMln2VMKTQUcFlB1Th93N_QodkeMSiqw8K5OXMUd5Bv2yHAJSnch/s1600/81495.jpg"></div>

  <!-- Gambar di atas finalGreeting -->
  <img id="finalGreetingImage" src="https://htmlku.com/0/panda/hearthappy.gif" alt="Night Pacarku!">
  
  <!-- Animasi Teks Happy Mother's Day -->
  <div id="finalGreeting">
    Good Night Pacarkuu ♡.ᐟ
  </div>

  <!-- Halaman 1: Envelope -->
  <div id="hal1">
    <div class="envlope-wrapper">
      <div id="envelope" class="close">
        <div class="front flap"></div>
        <div class="front pocket"></div>
        <!-- Emoji Hati di Tengah Amplop -->
        <div class="envelope-heart">🤍</div>
        <div class="letter">
          <div class="letter-corner corner-tl"></div>
          <div class="letter-corner corner-br"></div>
          <div class="message">
            <p>For You 🎉</p>
          </div>
        </div>
        <div class="hearts">
          <div class="heart a1"></div>
          <div class="heart a2"></div>
          <div class="heart a3"></div>
        </div>
        <div class="sparkles">
          <div class="sparkle s1"></div>
          <div class="sparkle s2"></div>
          <div class="sparkle s3"></div>
        </div>
      </div>
    </div>
    <div class="reset">
      <button onclick="bukaEnvelope()">💭 Tap Me</button>
    </div>
  </div>

  <!-- Halaman 2: Memory Game (TIDAK LAGI DIGUNAKAN)-->
  <div id="hal2" class="kotak sembunyi"><canvas id="game-canvas"></canvas><h2></h2><p></p><div id="kotakPesan"></div><div id="papanGame" class="papanGame"></div><p id="statusGame"></p><button id="lanjut" onclick="pindahHal(3)" class="sembunyi">Lihat Pesan Cinta!</button><button id="ulang" onclick="mulaiHal2()" class="tombolCadangan sembunyi">Coba Lagi!</button></div>

  <!-- Halaman 3: Pesan Akhir -->
  <div id="hal3" class="kotak sembunyi">
    <div class="decor decor-tl"></div>
    <div class="decor decor-br"></div>
    <!-- Stiker Gif -->
    <div id="stiker3" class="stiker">
        <img id="stiker3a" src="https://htmlku.com/0/panda/ciumin.gif" />
        <img id="stiker3b" class="sembunyi" src="https://htmlku.com/0/panda/tidur.gif" />
    </div>
    <div id="containerPesan">
	    <p id="teksCinta"></p>
	    <p id="pesanAkhir"></p>
	    <p id="teksLucu"></p>
    </div>
  </div>
  <div class="tombol">
    <button onclick="balasWa()">💌 Balas</button>
  </div>
  
  <!-- Circle Animation -->
  <div><div><div class="circ"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div></div></div>

  <script>
    // Edit Kata-kata di Sini
    const txtDoa = "Selamat malam dan selamat lepas lelah sayang 🫶🏻💞 Aku bener-bener beruntung punya kamu, aku suka semua tentang kamu—perhatianmu, suaramu, caramu peduli sama aku. Kamu ga perlu ragu lagi sama aku karena aku sayang banget sama kamu dan kamu selalu jadi orang yang aku butuhin setiap hari 💞";
    const txtPesanAkhir = "Maafin aku ya kalau aku sering bikin salah dan belum selalu bisa ngertiin kamu. Aku takut kehilangan kamu dan ga mau kamu pergi atau menjauh dari aku. Semua ini karena aku sesayang itu sama kamu 🥺💗";
    const txtLucu = "── ᯓᡣ𐭩<br>Makasih udah selalu ada dan bikin aku bahagia. Jangan pernah ngerasa sendirian, ada aku di sini buat kamu. Good night, sweet dreams—I’m so grateful for you, you mean everything to me, <b>iloveu everything about you 💖</b>";
  </script>
  <script src="https://htmlku.com/lepaslelah/script.js"></script>
  <script>
    // Balas pesan ke WhatsApp
    function balasWa() {
      const url = window.location.href;
      const text = "Night too sayaanggg";
      window.open(`https://wa.me/?text=${encodeURIComponent(text)}`, '_blank');
    }
  </script>
</body>
</html>  </script>
  <script src="https://htmlku.com/lepaslelah/script.js"></script>
  <script>
    // Balas pesan ke WhatsApp
    function balasWa() {
      const url = window.location.href;
      const text = "Night too sayaanggg";
      window.open(`https://wa.me/?text=${encodeURIComponent(text)}`, '_blank');
    }
  </script>
</body>
</html>=device-width, initial-scale=1, user-scalable=1, minimum-scale=1, maximum-scale=5' name='viewport'/><meta content='IE=edge' http-equiv='X-UA-Compatible'/><link href="https://feeldreams.github.io/hayoloh/style.css" rel="stylesheet" type="text/css" /><script src="https://feeldreams.github.io/hayoloh/script.js"></script>
<link rel="preconnect" href="https://fonts.googleapis.com"><link rel="preconnect" href="https://fonts.gstatic.com" crossorigin><link href="https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;700&display=swap" rel="stylesheet"><script src="https://cdn.jsdelivr.net/npm/sweetalert2@11.0.19/dist/sweetalert2.all.min.js"></script><script src="https://kit.fontawesome.com/4f3ce16e3e.js" crossorigin="anonymous"></script>
<head>
<title>Script HTML</title>
<!-- 
  Made with love by Rayys!
     Blog: https://PalingIT.com
     Instagram: @rayyarrr
     TikTok: @rayy4r
     Email: rayyar0703@gmail.com
  Thanks to all <3
  
  DM ke IG: @rayyarrr apabila masih bingung
  untuk cara edit scriptnya!
-->
</head>
<style>
:root {
--warna-bg: rgba(0, 0, 0, .5); 
--warna-teks: #fff;
--warna-bingkai: #fff;
--bingkai: 8px;
--bingkai-kiri: 2px solid var(--warna-bingkai);
--bingkai-kanan: 2px solid var(--warna-bingkai);
--gaya-font: 'Josefin Sans', sans-serif;
}
</style>
<body>
	
   <!-- Ganti Audio di sini --><audio id="linkmp3">https://feeldreams.github.io/papapa.mp3</audio>
   
   <div id="bodyblur">
     <!-- Wallpaper --><img src="https://feeldreams.github.io/wp3.jpeg" id="wallpaper"/>
   </div>

   <div id='Content'>
   	
     <div id="suratin" onClick="memulai();audio.play();">
       <!-- Tombol Surat --><img src="https://rayyscoding.github.io/envelope.png"/>
     </div>
     <p id="ket">Klik Suratnya!</p>

     <div><blockquote id='bq'>
       <div>
         <!-- Stiker untuk Konten -->
         <img src="https://feeldreams.github.io/bunga.gif" id="fotoakhir"/>
         <img src="https://feeldreams.github.io/peach1.gif" id="fotoakhir2"/>
         <img src="https://feeldreams.github.io/weee.gif" id="fotoakhir3"/>
       </div>

       <!-- Konten Pertanyaan -->
       <p id="kalimat">Kamu Mau Gak Jadi Pacar Aku? 🤭❤️</p>
       <p id="kalimatb"></p>
       <p id="kalimatc"></p>

       <!-- Konten Jawaban -->
       <p id="kalimat2">Yeaayy! 😆</p>
       <p id="kalimatb2">Sekarang, Kamu adalah Pacarku ❤️</p>
       <p id="kalimatc2">Eitss.. 🏃 Tapi kita akan PUTUS dalam waktu: <b id="ctimer" style="font-size:24px">7</b></p>

       <!-- Konten Jawaban 2 -->
       <p id="kalimat3">Tapi Boong😜</p>
       <p id="kalimatb3">Kamu beneran jadi pacar aku kok, wkwk🤣❤️</p>
       <p id="kalimatc3">📅 </p>
     </blockquote></div>

     <!-- Tombol Multifungsi -->
     <div id="Tombol">
       <a id="By" onClick="multifungsi()">
         <b id="tmbl">Mau</b>
       </a>
       
       <a id="Bn" onClick="ditolak()">Gamau</a><a id="Bn2" onClick="ditolak2()"></a>
     </div>
     
   </div>

<!-- Jangan Edit Bagian Ini --><script>
  ftom=0;jikapr=1;ftganti=0;flag=1;flagg=1;fungsi=0;Bn2.innerHTML=Bn.innerHTML;function showDiv() {pesanwhatsapp = "Aku mau kok jadi pacarmu ><";Bn2.style.display="none";Content.style = "opacity:1;margin-top:15vh;";ket.style="margin-top:30px";}
  function memulai(){suratin.style="transition:all 1s ease;transform:scale(.1);opacity:0";ket.style="transition:all 1s ease;transform:scale(.1);opacity:0";setTimeout(mulaikonten,300)}
  function mulaikonten() {otomatis();suratin.style="display:none";ket.style="display:none";Content.style = "opacity:1;margin-top:4vh";bodyblur.style="opacity:.6;animation:none";wallpaper.style="transform: scale(2);opacity:1;";fotoakhir.style="display:inline-flex;";setTimeout(ftmuncul,200);bq.style = "position:relative;opacity:1;visibility:visible;transform: scale(1);border-radius:var(--bingkai);margin-top:0";fungsi=1;setTimeout(tombol,500);}
  
  function ftmuncul(){
    if(ftganti==0){fotoakhir.style="display:inline-flex;opacity:1;transform:scale(1)";}
    if(ftganti==1){fotoakhir.src = fotoakhir2.src;fotoakhir.style="display:inline-flex;opacity:1;transition:all .7s ease;transform:scale(1);";}
    if(ftganti==2){fotoakhir.src = fotoakhir3.src;fotoakhir.style="display:inline-flex;opacity:1;transition:all .7s ease;transform:scale(1);";}
  }
  function fthilang(){fotoakhir.style="display:inline-flex;opacity:1;transition:all .7s ease;transform:scale(.1)";}
  function jjfoto(){fotoakhir.style.animation="rto .8s infinite alternate";}
  
  function tombol(){Tombol.style="opacity:1;transform: scale(1);";Bn.style="margin:12px 0 12px 12px";ftom=1;}
  function multifungsi(){if(ftom==1){diterima();} if(ftom==5){menuju();}}
  async function menuju(){await swals.fire('OK!', 'Kirim pesan ke WhatsApp aku, ya!', 'success');window.location = "https://api.whatsapp.com/send?phone=&text=" + pesanwhatsapp;Tombol.style="margin-top:15px;opacity:1;transform: scale(1);";} setTimeout(showDiv,100);

  const swalst = Swal.mixin({timer: 2777, allowOutsideClick: false, showConfirmButton: false, timerProgressBar: true, imageHeight: 100,}); audio = new Audio('' + linkmp3.innerHTML);const swals = Swal.mixin({allowOutsideClick: false, cancelButtonColor: '#FF0040', imageWidth: 100, imageHeight: 100,}); const style = document.createElement('style'); var today = new Date();var dd = String(today.getDate()).padStart(2, '0');var mm = String(today.getMonth() + 1).padStart(2, '0');var yyyy = today.getFullYear();const monthNames = ["Januari", "Februari", "Maret", "April", "Mei", "Juni", "Juli", "Agustus", "September", "Oktober", "November", "Desember"];today = dd + ' ' + monthNames[today.getMonth()] + ' ' + yyyy;
   const body = document.querySelector("body");function createHeart() {const heart = document.createElement("div"); heart.className = "fas fa-heart"; heart.style.left = (Math.random() * 90)+"vw"; heart.style.animationDuration = (Math.random()*3)+2+"s"; body.appendChild(heart);} setInterval(function name(params) {var heartArr = document.querySelectorAll(".fa-heart"); if (heartArr.length > 100) {heartArr[0].remove()}},100);
</script>
<!-- Sampai Sini -->
</body>
</html>
