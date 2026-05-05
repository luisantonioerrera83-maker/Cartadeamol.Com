<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para Celeste</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body, html {
            height: 100%;
            background-color: #121212;
            color: #ffffff;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }
        .contenedor {
            width: 100%;
            max-width: 450px;
            height: 100%;
            max-height: 800px;
            background: #1a1a24;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            display: flex;
            flex-direction: column;
            position: relative;
        }
        /* Pantalla de inicio */
        #pantalla-inicio {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100%;
            text-align: center;
            padding: 20px;
            background: linear-gradient(145deg, #1f1d2c 0%, #121018 100%);
        }
        .icono-sobre {
            font-size: 64px;
            color: #ff7b92;
            margin-bottom: 20px;
            animation: latido 1.5s infinite alternate;
        }
        .btn-abrir {
            margin-top: 30px;
            padding: 12px 30px;
            background: linear-gradient(90deg, #ff7b92, #e57373);
            border: none;
            border-radius: 25px;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(255, 123, 146, 0.4);
            transition: transform 0.2s;
        }
        .btn-abrir:hover {
            transform: scale(1.05);
        }
        /* Pantalla de recuerdos */
        #pantalla-carrusel {
            display: none;
            flex-direction: column;
            height: 100%;
            padding: 20px;
        }
        .cabecera {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .titulo-seccion {
            font-size: 18px;
            color: #ff7b92;
        }
        .contador {
            background: rgba(255, 255, 255, 0.1);
            padding: 4px 10px;
            border-radius: 10px;
            font-size: 14px;
        }
        .caja-foto {
            flex: 1;
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
        }
        .caja-foto img {
            max-width: 100%;
            max-height: 300px;
            border-radius: 8px;
            object-fit: cover;
            margin-bottom: 15px;
        }
        .texto-recuerdo {
            font-size: 14px;
            line-height: 1.5;
            color: #d1d1e0;
            font-style: italic;
        }
        .botones-navegacion {
            display: flex;
            justify-content: space-between;
        }
        .btn-nav {
            padding: 10px 20px;
            background: rgba(255, 255, 255, 0.1);
            border: none;
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
        }
        .btn-nav:hover {
            background: rgba(255, 255, 255, 0.2);
        }
        @keyframes latido {
            0% { transform: scale(1); }
            100% { transform: scale(1.1); }
        }
    </style>
</head>
<body>

<div class="contenedor">
    <div id="pantalla-inicio">
        <div class="icono-sobre">💌</div>
        <h2 style="margin-bottom: 10px;">Para: Celeste</h2>
        <p style="color: #888;">"Pequeña" - Con todo mi cariño</p>
        <button class="btn-abrir" onclick="abrirCarta()">💌 Abrir mis Tarjetas</button>
    </div>

    <div id="pantalla-carrusel">
        <div class="cabecera">
            <span class="titulo-seccion">Nuestros Recuerdos</span>
            <span id="contador-paginas" class="contador">1 / 7</span>
        </div>
        
        <div class="caja-foto">
            <img id="imagen-recuerdo" src="foto1.jpg" alt="Recuerdo">
            <p id="texto-recuerdo" class="texto-recuerdo">
                Cargando...
            </p>
        </div>

        <div class="botones-navegacion">
            <button class="btn-nav" onclick="cambiarPagina(-1)">← Atrás</button>
            <button class="btn-nav" onclick="cambiarPagina(1)">Siguiente →</button>
        </div>
    </div>
</div>

<script>
    const recuerdos = [
        {
            texto: '"Quería decirte que, a pesar de todo y del tiempo, mis sentimientos por ti siguen intactos. Para mí, nada ha cambiado. Sigues siendo la persona más especial que he conocido."',
            imagen: 'foto1.jpg'
        },
        {
            texto: '"No dejo de pensar en los buenos momentos que compartimos, y cada uno de ellos me recuerda por qué estoy convencido de que lo nuestro vale la pena."',
            imagen: 'foto2.jpg'
        },
        {
            texto: '"Sabes que mi intención es recuperar lo que teníamos y construir algo real, porque quiero todo contigo."',
            imagen: 'foto3.jpg'
        },
        {
            texto: '"No quiero que esto se quede en un recuerdo, sino que sea el comienzo de una etapa mucho mejor, aprendiendo de lo vivido para no soltarnos esta vez."',
            imagen: 'foto4.jpg'
        },
        {
            texto: '"Valoro cada detalle de lo que somos cuando estamos juntos y no encuentro a nadie que se compare con lo que me haces sentir."',
            imagen: 'foto5.jpg'
        },
        {
            texto: '"Eres de esas personas que llegan a la vida para quedarse, y yo estoy dispuesto a poner todo de mi parte para que lo nuestro funcione de verdad."',
            imagen: 'foto6.jpg'
        },
        {
            texto: '"Sé que tenemos mucho por delante y me visualizo cumpliendo metas a tu lado, porque no me imagino este camino con nadie más que no seas tú. Pase lo que pase, siempre serás tú."',
            imagen: 'foto7.jpg'
        }
    ];

    let paginaActual = 0;

    function abrirCarta() {
        document.getElementById('pantalla-inicio').style.display = 'none';
        document.getElementById('pantalla-carrusel').style.display = 'flex';
        actualizarContenido();
    }

    function cambiarPagina(direccion) {
        paginaActual += direccion;
        if (paginaActual < 0) paginaActual = 0;
        if (paginaActual >= recuerdos.length) paginaActual = recuerdos.length - 1;
        actualizarContenido();
    }

    function actualizarContenido() {
        document.getElementById('contador-paginas').innerText = `${paginaActual + 1} / ${recuerdos.length}`;
        document.getElementById('texto-recuerdo').innerText = recuerdos[paginaActual].texto;
        document.getElementById('imagen-recuerdo').src = recuerdos[paginaActual].imagen;
    }
</script>

</body>
</html>
