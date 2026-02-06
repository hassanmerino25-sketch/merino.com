# merino.com
☑️
<!DOCTYPE html>
<html lang="mg">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Archive Raza'adratovo</title>
  <style>
    body{font-family:Arial;background:#0f172a;color:#e5e7eb;margin:0}
    header{padding:15px;background:#020617;text-align:center}
    .container{padding:15px}
    input,button{padding:10px;border-radius:8px;border:none;margin:5px 0}
    .box{background:#020617;padding:15px;border-radius:12px;margin-bottom:12px}
    .files img, .files video{max-width:100%;border-radius:10px;margin-top:8px}
    .file-card{background:#020617;border:1px solid #1e293b;border-radius:10px;padding:10px;margin-top:10px}
    .download{display:inline-block;margin-top:6px;color:#38bdf8;text-decoration:none}
    .hidden{display:none}
    .tabs button{margin-right:5px}
  </style>
</head>
<body>

  <!-- LOGIN -->
  <div id="login" class="container">
    <div class="box">
      <h2>🔐 Archive Privé</h2>
      <p>Midira amin'ny mot de passe</p>
      <input type="password" id="password" placeholder="Mot de passe">
      <button onclick="login()">Entrer</button>
      <p id="error" style="color:#f87171"></p>
    </div>
  </div>

  <!-- APP -->
  <div id="app" class="hidden">
    <header>
      <h2>Razanadratovo 31240</h2>
      <p>Photos • Vidéos • PDF</p>
    </header>

    <div class="container">
      <div class="box">
        <h3>➕ Ampidiro fichier</h3>
        <input type="file" id="fileInput" multiple accept="image/*,video/*,application/pdf">
        <button onclick="addFiles()">Ajouter</button>
      </div>

      <div class="box tabs">
        <button onclick="showTab('images')">🖼️ Sary</button>
        <button onclick="showTab('videos')">🎥 Vidéo</button>
        <button onclick="showTab('pdfs')">📄 PDF</button>
      </div>

      <div class="box files" id="images"><h3>🖼️ Sary</h3></div>
      <div class="box files hidden" id="videos"><h3>🎥 Vidéo</h3></div>
      <div class="box files hidden" id="pdfs"><h3>📄 PDF</h3></div>
    </div>
  </div>

  <script>
    const PASSWORD = "merino1998";

    function login(){
      const input = document.getElementById("password").value;
      if(input === PASSWORD){
        document.getElementById("login").style.display = "none";
        document.getElementById("app").classList.remove("hidden");
      } else {
        document.getElementById("error").textContent = "❌ Mot de passe diso";
      }
    }

    function showTab(tab){
      document.getElementById("images").classList.add("hidden");
      document.getElementById("videos").classList.add("hidden");
      document.getElementById("pdfs").classList.add("hidden");
      document.getElementById(tab).classList.remove("hidden");
    }

    function addFiles(){
      const input = document.getElementById("fileInput");

      for(let file of input.files){
        const card = document.createElement("div");
        card.className = "file-card";
        const url = URL.createObjectURL(file);
        let preview, target;

        if(file.type.startsWith("image/")){
          preview = document.createElement("img");
          preview.src = url;
          target = document.getElementById("images");

        } else if(file.type.startsWith("video/")){
          preview = document.createElement("video");
          preview.src = url;
          preview.controls = true;
          target = document.getElementById("videos");

        } else {
          preview = document.createElement("a");
          preview.href = url;
          preview.textContent = "📄 " + file.name;
          preview.target = "_blank";
          target = document.getElementById("pdfs");
        }

        const download = document.createElement("a");
        download.href = url;
        download.download = file.name;
        download.textContent = "⬇️ Télécharger";
        download.className = "download";

        card.appendChild(preview);
        card.appendChild(download);
        target.appendChild(card);
      }
    }
  </script>
</body>
</html>
