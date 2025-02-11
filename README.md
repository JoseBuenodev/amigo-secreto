# amigo-secreto
amigo secreto
Estructura HTML
Primero, creamos una página sencilla con un formulario donde los participantes pueden introducir sus nombres:

html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amigo Secreto</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Amigo Secreto</h1>
        <form id="amigo-secreto-form">
            <label for="nombre">Nombre:</label>
            <input type="text" id="nombre" required>
            <button type="submit">Agregar Participante</button>
        </form>
        <ul id="lista-participantes"></ul>
        <button id="asignar">Asignar Amigos Secretos</button>
        <div id="resultados"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
Estilos CSS
Ahora agregamos algunos estilos para mejorar la apariencia:

css
/* styles.css */
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 300px;
    text-align: center;
}

h1 {
    margin-bottom: 20px;
}

form {
    margin-bottom: 20px;
}

input {
    width: calc(100% - 22px);
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: #fff;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    margin: 5px 0;
}

#resultados {
    margin-top: 20px;
}
Lógica JavaScript
Finalmente, agregamos la lógica para manejar las asignaciones:

javascript
/* script.js */
document.getElementById('amigo-secreto-form').addEventListener('submit', function (e) {
    e.preventDefault();
    const nombre = document.getElementById('nombre').value;
    if (nombre) {
        const li = document.createElement('li');
        li.textContent = nombre;
        document.getElementById('lista-participantes').appendChild(li);
        document.getElementById('nombre').value = '';
    }
});

document.getElementById('asignar').addEventListener('click', function () {
    const participantes = Array.from(document.querySelectorAll('#lista-participantes li')).map(li => li.textContent);
    const asignaciones = asignarAmigosSecretos(participantes);
    mostrarResultados(asignaciones);
});

function asignarAmigosSecretos(participantes) {
    let amigos_secretos = participantes.slice();
    amigos_secretos = shuffleArray(amigos_secretos);
    const asignaciones = {};

    for (let i = 0; i < participantes.length; i++) {
        while (participantes[i] === amigos_secretos[i]) {
            amigos_secretos = shuffleArray(amigos_secretos);
        }
        asignaciones[participantes[i]] = amigos_secretos[i];
    }

    return asignaciones;
}

function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
    return array;
}

function mostrarResultados(asignaciones) {
    const resultadosDiv = document.getElementById('resultados');
    resultadosDiv.innerHTML = '';
    for (const participante in asignaciones) {
        const p = document.createElement('p');
        p.textContent = `${participante} regalará a ${asignaciones[participante]}`;
        resultadosDiv.appendChild(p);
    }
}
Este código crea una interfaz sencilla en la que los participantes pueden agregar sus nombres, y luego se asignan los amigos secretos de manera aleatoria.
