<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Pagamento PIX</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      margin: 0;
      padding: 0;
    }

    .container {
      max-width: 420px;
      margin: 40px auto;
      background: #fff;
      padding: 24px;
      border-radius: 12px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.1);
      text-align: center;
    }

    h1 {
      margin: 0;
      font-size: 22px;
    }

    .subtitle {
      margin: 10px 0 20px;
      color: #555;
    }

    .qr {
      margin: 20px 0;
    }

    .qr img {
      width: 220px;
      height: 220px;
    }

    .pix-key {
      margin-top: 10px;
      font-size: 14px;
      color: #333;
      word-break: break-all;
    }

    .banks {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      margin: 20px 0;
    }

    .bank {
      padding: 8px 12px;
      border: 1px solid #ddd;
      border-radius: 8px;
      font-size: 13px;
      background: #fafafa;
    }

    .open-bank-btn {
      margin-top: 20px;
      width: 100%;
      padding: 14px;
      font-size: 16px;
      font-weight: bold;
      color: #fff;
      background: #00b894;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }

    .open-bank-btn:active {
      opacity: 0.9;
    }

    .hint {
      margin-top: 12px;
      font-size: 12px;
      color: #666;
    }
  </style>
</head>

<body>
  <div class="container">
    <h1>Pagamento PIX</h1>
    <div class="subtitle">Escolha como pagar</div>

    <div class="qr">
      <!-- TROQUE pelo nome correto da imagem do QR -->
      <img src="qr-pix.png" alt="QR Code PIX">
    </div>

    <div class="pix-key">
      Chave PIX (CNPJ): <strong>07.836.612/0001-68</strong>
    </div>

    <div class="banks">
      <div class="bank">Nubank</div>
      <div class="bank">Inter</div>
      <div class="bank">Itaú</div>
      <div class="bank">Bradesco</div>
      <div class="bank">Banco do Brasil</div>
      <div class="bank">Santander</div>
    </div>

    <button class="open-bank-btn" onclick="openBankApp()">
      Abrir aplicativo do banco
    </button>

    <div class="hint">
      Caso não abra automaticamente, use o app do seu banco e escaneie o QR Code.
    </div>
  </div>

  <script>
    function openBankApp() {
      const links = [
        "nubank://",
        "itau://",
        "bradesco://",
        "bb://",
        "santander://",
        "inter://"
      ];

      let opened = false;

      links.forEach((link, index) => {
        setTimeout(() => {
          if (!opened) {
            window.location.href = link;
            opened = true;
          }
        }, index * 300);
      });

      setTimeout(() => {
        alert(
          "Não foi possível abrir automaticamente.\n" +
          "Abra o app do seu banco e escaneie o QR Code PIX."
        );
      }, 2500);
    }
  </script>
</body>
</html>
