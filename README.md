# El-Secreto

<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>El Secreto - Alfajor Misterioso</title>
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      background-color: #0d0d0d;
      color: #f5f5f5;
      margin: 0;
      padding: 0;
    }

    header {
      background: linear-gradient(90deg, #1a1a1a, #3d3d3d);
      padding: 20px;
      text-align: center;
      color: gold;
      font-size: 2em;
      letter-spacing: 2px;
      box-shadow: 0 2px 10px rgba(255, 215, 0, 0.2);
    }

    section {
      padding: 40px 20px;
      text-align: center;
    }

    h2 {
      color: gold;
      margin-bottom: 10px;
    }

    p {
      max-width: 700px;
      margin: 10px auto;
      line-height: 1.6;
    }

    .product {
      display: flex;
      justify-content: center;
      margin-top: 40px;
    }

    .card {
      background-color: #1b1b1b;
      border: 1px solid #444;
      border-radius: 15px;
      width: 320px;
      padding: 25px;
      box-shadow: 0 4px 15px rgba(255, 215, 0, 0.1);
      transition: transform 0.3s, box-shadow 0.3s;
    }

    .card:hover {
      transform: scale(1.05);
      box-shadow: 0 6px 20px rgba(255, 215, 0, 0.3);
    }

    .card img {
      width: 100%;
      border-radius: 10px;
      margin-bottom: 15px;
    }

    .btn {
      display: inline-block;
      background-color: gold;
      color: black;
      padding: 10px 25px;
      border-radius: 25px;
      text-decoration: none;
      font-weight: bold;
      transition: background 0.3s;
      cursor: pointer;
    }

    .btn:hover {
      background-color: #f0c000;
    }

    footer {
      text-align: center;
      padding: 20px;
      background-color: #111;
      font-size: 0.9em;
      color: #aaa;
    }

    /* Secretos */
    #secrets {
      background-color: #111;
      padding: 50px 20px;
    }

    #secretInput {
      width: 80%;
      max-width: 500px;
      padding: 10px;
      border: 1px solid #444;
      border-radius: 10px;
      background-color: #222;
      color: white;
      margin-bottom: 15px;
      font-size: 1em;
    }

    #secretList {
      margin-top: 30px;
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
      text-align: left;
    }

    .secret-item {
      background: #1b1b1b;
      border-left: 3px solid gold;
      padding: 10px 15px;
      border-radius: 8px;
      margin-bottom: 10px;
      font-style: italic;
    }

    /* Notificación */
    #notification {
      position: fixed;
      bottom: 30px;
      right: 30px;
      background: gold;
      color: black;
      padding: 15px 25px;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(255, 215, 0, 0.4);
      display: none;
      font-weight: bold;
    }

    @media (max-width: 600px) {
      .card {
        width: 90%;
      }
    }
  </style>
</head>
<body>

  <header>✨ El Secreto ✨</header>

  <section>
    <h2>El alfajor más misterioso</h2>
    <p>
      Nadie sabe qué dulce le va a tocar...  
      Puede ser <strong>clásico</strong>, <strong>Malbec</strong> o <strong>con naranja</strong>.  
      Solo el destino (y tu mordida) lo revelarán 🍫
    </p>

    <div class="product">
      <div class="card" id="mysteryAlfajor">
        <img src="https://upload.wikimedia.org/wikipedia/commons/5/59/Alfajor.jpg" alt="El Secreto Alfajor">
        <h3>El Secreto</h3>
        <p>Un solo alfajor. Tres posibles destinos. ¿Cuál será el tuyo?</p>
        <button class="btn" onclick="revealSecret()">Descubrí tu sabor</button>
      </div>
    </div>
  </section>

  <section id="secrets">
    <h2>💬 Contá tu secreto</h2>
    <p>Dejá tu secreto anónimo y mirá los de otros. Nadie sabrá quién sos.</p>

    <input type="text" id="secretInput" placeholder="Escribí tu secreto...">
    <button class="btn" onclick="addSecret()">Enviar Secreto</button>

    <div id="secretList"></div>
  </section>

  <footer>
    © 2025 El Secreto. Todos los derechos reservados.
  </footer>

  <div id="notification"></div>

  <script>
    // Posibles sabores del alfajor
    const flavors = [
      "Dulce de leche clásico 🧁",
      "Dulce de leche Malbec 🍷",
      "Dulce de leche con naranja 🍊"
    ];

    function revealSecret() {
      const randomFlavor = flavors[Math.floor(Math.random() * flavors.length)];
      const notification = document.getElementById('notification');
      notification.innerText = `Te tocó: ${randomFlavor}`;
      notification.style.display = 'block';
      setTimeout(() => notification.style.display = 'none', 3000);
    }

    // Sección de secretos
    const secretList = document.getElementById('secretList');
    const savedSecrets = JSON.parse(localStorage.getItem('secrets')) || [];

    // Mostrar los secretos guardados
    function renderSecrets() {
      secretList.innerHTML = '';
      savedSecrets.slice().reverse().forEach(secret => {
        const div = document.createElement('div');
        div.classList.add('secret-item');
        div.textContent = `"${secret}"`;
        secretList.appendChild(div);
      });
    }
    renderSecrets();

    function addSecret() {
      const input = document.getElementById('secretInput');
      const text = input.value.trim();
      if (text === '') return;

      savedSecrets.push(text);
      localStorage.setItem('secrets', JSON.stringify(savedSecrets));

      input.value = '';
      renderSecrets();

      const notification = document.getElementById('notification');
      notification.innerText = "Tu secreto fue compartido 🔒";
      notification.style.display = 'block';
      setTimeout(() => notification.style.display = 'none', 2000);
    }
  </script>

</body>
</html>
