<html><meta charset='UTF-8'/><meta content='width=device-width, initial-scale=1, user-scalable=1, minimum-scale=1, maximum-scale=5' name='viewport'/><meta content='IE=edge' http-equiv='X-UA-Compatible'/>

  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11.0.19/dist/sweetalert2.all.min.js"></script>
  <script src="https://unpkg.com/typeit@8.7.0/dist/index.umd.js"></script>
  <link href="https://htmlku.com/kamumau/style.css" rel="stylesheet" type="text/css" />

<head>
  <title>Script HTML buat Kamu</title>
  <meta name="description" content="@feelthisray - Script HTML by feeldream.id">
</head>
<body>
	
   <div id="bodyblur">
     <!-- Wallpaper / Background --><img src="https://feeldreams.github.io/pics/awan/2.jpg" id="wallpaper"/>
   </div>
  
  <div class="kumpulanstiker">
         <!-- Stiker untuk Konten -->
         <img src="https://feeldreams.github.io/pandapanah.gif" id="stiker1"/>
         <img src="https://feeldreams.github.io/cilukba.gif" id="stiker2"/>
         <img src="https://feeldreams.github.io/smprt.gif" id="stiker3"/>
         <img src="https://feeldreams.github.io/gumush.gif" id="stiker4"/>
         <img src="https://feeldreams.github.io/" id="stiker5"/>
  </div>

   <div id='Content'>
   	
     <div id="suratin" onClick="memulai();audio.play();">
       <!-- Surat --><img src="https://rayyscoding.github.io/envelope.png"/>
     </div>
     <p id="ket">Klik Suratnya!</p>
   
     <div>
      <!-- Foto Akhir -->
      <img src="https://feeldreams.github.io/pusn.gif" id="fotoakhir" />
      <img src="https://feeldreams.github.io/emawh.gif" id="fotoakhir2" />
    </div>
     <div><blockquote id='bq'>
       <p id="kalimat"></p>
       <p id="kalimatc"></p>
     </blockquote></div>
   
     <!-- Tombol -->
     <div id="Tombol">
      <a id="By" onClick="fungsimau()">Mau</a>
      <a id="Bn" onClick="btn='Bn';fungsibaru(btn)">Gamau!</a>
    </div>

    <!-- Pesan Ditolak -->
    <div class="sembunyi">
      <img id="stikerditolak" src="https://feeldreams.github.io/weee.gif"/>
      <span id="kataditolak">Harus Mau yaa 😝</span>
    </div>
     
   </div>

<script src="https://htmlku.com/kamumau/script.js"></script>

<script type="text/javascript">
       async function pertama(){
         audio = new Audio('https://feeldreams.github.io/almostday.mp3');setTimeout(showDiv,100);
       } pertama();
	
       
       async function pesan(){
             	await swalst.fire({
                  title: 'Assalamualaikum mba dilaa! 😍', 
                  imageUrl: '' + stiker1.src,
                  });   	
                 await swalst.fire({
                  title: 'Gimana Kabarnya? Baik<br>Sekali, kan? 🫣',
                  imageUrl: '' + stiker2.src,
                  });
                 await swalst.fire({
                  title: 'Eh Aku Mau Ngomong,<br>Sesuatu Nihh.. 😋',
                  imageUrl: '' + stiker3.src,
                  });
                  await swalst.fire({
                  title: 'Oh ya, Aku Mau Ngajak<br>Kamu 🫣',
                  imageUrl: '' + stiker4.src,
                  });
                  
                  katangetik = "<b class='usefont2'>Kamu Mau Gak<br>Nikah Sama Aku? 😆</b>";
                  katangetik2 = "<b class='usefont'>Makasii udah <br>udah mau jadi calon aku 😆🙏<br><br>Ditunggu yaa kabar surat lamarannya yaa wkwk 🫣😋😝</b>";
                  ktbwh2 = "Tetap Sama Aku Terus yaa ❤️";
                  ktbwh3 = "Aku Sayang Kamu 💐🤍🫶";

                  kataditerima = "<b class='usefont2'>Yeaayy! 😍</b>";
                  
                  pesanwhatsapp = "ilvyou too 💞🤍💝❣️";
                 setTimeout(kpemb,200);
            }
</script>
</body>
</html>
