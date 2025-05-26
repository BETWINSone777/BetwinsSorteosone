<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Bet Wins - Sorteo Diario</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <img src="img/logo.png" class="logo" alt="Logo Bet Wins">
    <form id="formulario">
      <h2>Participá del sorteo diario</h2>
      <input type="text" id="nombre" name="nombre" placeholder="Tu nombre" required>
      <input type="tel" id="telefono" name="telefono" placeholder="Tu teléfono" required>
      <button type="submit">Anotarme</button>
      <p id="mensaje"></p>
    </form>
  </div>
  <script src="script.js"></script>
</body>
</html>
body {
  margin: 0;
  font-family: sans-serif;
  background: url('img/fondo.jpg') no-repeat center center fixed;
  background-size: cover;
}

.container {
  backdrop-filter: blur(8px);
  background-color: rgba(0,0,0,0.6);
  max-width: 400px;
  margin: 80px auto;
  padding: 30px;
  border-radius: 12px;
  color: white;
  text-align: center;
  box-shadow: 0 0 10px #000;
  position: relative;
}

.logo {
  width: 100px;
  opacity: 0.2;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
}

input {
  width: 90%;
  padding: 10px;
  margin: 10px 0;
  border-radius: 5px;
  border: none;
}

button {
  width: 95%;
  padding: 12px;
  background-color: gold;
  color: black;
  font-weight: bold;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

#mensaje {
  margin-top: 15px;
  font-weight: bold;
}
const form = document.getElementById('formulario');
const mensaje = document.getElementById('mensaje');

form.addEventListener('submit', async (e) => {
  e.preventDefault();

  const nombre = document.getElementById('nombre').value.trim();
  const telefono = document.getElementById('telefono').value.trim();

  if (!nombre || !telefono) {
    mensaje.textContent = 'Por favor completá todos los campos.';
    mensaje.style.color = 'red';
    return;
  }

  const url = 'AQUÍ_TU_ENDPOINT_BACKEND'; // ← Debes reemplazar esto con la URL real a la que enviarás los datos

  const formData = new FormData();
  formData.append('nombre', nombre);
  formData.append('telefono', telefono);

  try {
    const res = await fetch(url, {
      method: 'POST',
      body: formData
    });

    const texto = await res.text();

    if (texto.includes('ya está registrado')) {
      mensaje.textContent = 'Este número ya fue registrado.';
      mensaje.style.color = 'red';
    } else {
      mensaje.textContent = '¡Te anotaste con éxito!';
      mensaje.style.color = 'green';
      form.reset();
    }
  } catch (err) {
    mensaje.textContent = 'Error al enviar. Intentá de nuevo.';
    mensaje.style.color = 'red';
  }
});
