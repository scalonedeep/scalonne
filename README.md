!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Votación Jugadores U14 Sayago</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f0f4f8;
      margin: 0;
      padding: 20px;
    }
    .container {
      max-width: 600px;
      margin: auto;
      background: #fff;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      color: #333;
    }
    label {
      display: block;
      margin: 12px 0 6px;
      color: #555;
    }
    select, button {
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    button {
      background: #28a745;
      color: white;
      font-weight: bold;
      margin-top: 20px;
      cursor: pointer;
      transition: background 0.3s;
    }
    button:hover {
      background: #218838;
    }
    .footer {
      margin-top: 30px;
      text-align: center;
      font-size: 12px;
      color: #999;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Votá al Mejor Jugador</h1>
    <form action="https://formsubmit.co/santiagoscalone96@gmail.com" method="POST">
      <label for="jugador">Seleccioná un jugador:</label>
      <select name="Jugador favorito" id="jugador" required>
        <option value="Dona">Dona</option>
        <option value="Gio">Gio</option>
        <option value="Scalone">Scalone</option>
        <option value="Juani">Juani</option>
        <option value="Tacua">Tacua</option>
        <option value="Thiago L">Thiago L</option>
        <option value="Emi">Emi</option>
        <option value="Mate M">Mate M</option>
        <option value="Rodri">Rodri</option>
        <option value="Mateo A">Mateo A</option>
        <option value="Diego">Diego</option>
        <option value="Iñaki">Iñaki</option>
        <option value="Thiago chico">Thiago chico</option>
        <option value="Rama">Rama</option>
      </select>
      <input type="hidden" name="_captcha" value="false">
      <input type="hidden" name="_next" value="https://gracias-por-votar.com">
      <button type="submit">Votar</button>
    </form>
    <div class="footer">
      Resultados enviados directamente a don sexoscalone
    </div>
  </div>
</body>
</html>
