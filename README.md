
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DownloadGusta</title>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #080d1b, #101d3a);
      color: white;
      min-height: 100vh;
    }

    header {
      padding: 25px 8%;
      border-bottom: 1px solid #26375c;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .logo {
      font-size: 26px;
      font-weight: bold;
      color: #38a5ff;
    }

    .logo span {
      color: white;
    }

    nav a {
      color: #cbd5e1;
      text-decoration: none;
      margin-left: 18px;
    }

    main {
      width: 90%;
      max-width: 720px;
      margin: 90px auto;
      text-align: center;
    }

    h1 {
      font-size: clamp(32px, 7vw, 52px);
      margin-bottom: 15px;
    }

    h1 span {
      color: #38a5ff;
    }

    .subtitle {
      color: #b6c2d8;
      line-height: 1.7;
      margin-bottom: 35px;
    }

    .panel {
      background: #111b31;
      border: 1px solid #263b60;
      border-radius: 18px;
      padding: 28px;
      box-shadow: 0 15px 45px #0005;
    }

    input {
      width: 100%;
      padding: 16px;
      border-radius: 10px;
      border: 1px solid #344969;
      background: #080f20;
      color: white;
      font-size: 15px;
      outline: none;
    }

    input:focus {
      border-color: #38a5ff;
    }

    .formats {
      display: flex;
      gap: 12px;
      margin: 20px 0;
    }

    .formats label {
      flex: 1;
      background: #1a2944;
      border: 1px solid #344969;
      border-radius: 10px;
      padding: 15px;
      cursor: pointer;
    }

    .formats input {
      width: auto;
      margin-right: 7px;
      accent-color: #38a5ff;
    }

    button {
      width: 100%;
      padding: 16px;
      border: none;
      border-radius: 10px;
      color: white;
      font-size: 16px;
      font-weight: bold;
      background: linear-gradient(90deg, #087cf0, #35b5ff);
      cursor: pointer;
      transition: .2s;
    }

    button:hover {
      transform: translateY(-2px);
      filter: brightness(1.1);
    }

    #status {
      margin-top: 18px;
      color: #8fcaff;
      line-height: 1.6;
      overflow-wrap: anywhere;
    }

    .info {
      margin-top: 28px;
      color: #91a2bf;
      font-size: 13px;
      line-height: 1.7;
    }

    footer {
      text-align: center;
      padding: 25px;
      color: #8192ad;
      border-top: 1px solid #26375c;
    }

    @media (max-width: 480px) {
      header {
        padding: 20px 5%;
      }

      nav a {
        margin-left: 8px;
        font-size: 13px;
      }

      main {
        margin: 55px auto;
      }

      .panel {
        padding: 18px;
      }
    }
  </style>
</head>

<body>

  <header>
    <div class="logo">Download<span>Gusta</span></div>
    <nav>
      <a href="#inicio">Início</a>
      <a href="#sobre">Sobre</a>
    </nav>
  </header>

  <main id="inicio">
    <h1>Seus downloads, <span>do seu jeito.</span></h1>

    <p class="subtitle">
      Cole o link do conteúdo autorizado, escolha o formato
      e prepare seu download.
    </p>

    <section class="panel">
      <form id="downloadForm">
        <input
          type="url"
          id="videoUrl"
          placeholder="Cole aqui o link do YouTube..."
          required
        >

        <div class="formats">
          <label>
            <input type="radio" name="format" value="mp3" checked>
            🎵 MP3
          </label>

          <label>
            <input type="radio" name="format" value="mp4">
            🎬 MP4
          </label>
        </div>

        <button type="submit">
          Preparar download
        </button>
      </form>

      <p id="status" role="status">
        Aguardando um link...
      </p>

      <p class="info">
        O download real precisa de um servidor conectado.
        Baixe apenas conteúdo que você possui ou tem autorização
        para baixar.
      </p>
    </section>

    <section id="sobre" class="info">
      <h2>Sobre o DownloadGusta</h2>
      <p>
        Um projeto para organizar downloads de áudio e vídeo
        em uma interface simples e moderna.
      </p>
    </section>
  </main>

  <footer>
    © 2026 DownloadGusta — Feito com tecnologia.
  </footer>

  <script>
    const form = document.getElementById("downloadForm");
    const input = document.getElementById("videoUrl");
    const status = document.getElementById("status");

    form.addEventListener("submit", function(event) {
      event.preventDefault();

      const url = input.value.trim();
      const format = document.querySelector(
        'input[name="format"]:checked'
      ).value;

      let parsedUrl;

      try {
        parsedUrl = new URL(url);
      } catch {
        status.textContent = "Digite um link válido.";
        return;
      }

      const allowedHosts = [
        "youtube.com",
        "www.youtube.com",
        "m.youtube.com",
        "youtu.be",
        "www.youtube-nocookie.com"
      ];

      if (!allowedHosts.includes(parsedUrl.hostname)) {
        status.textContent =
          "Por favor, insira um link válido do YouTube.";
        return;
      }

      status.textContent =
        "Link validado! Formato escolhido: " +
        format.toUpperCase() +
        ". Para iniciar o download, conecte este site a um " +
        "servidor de processamento autorizado.";
    });
  </script>

</body>
</html>
