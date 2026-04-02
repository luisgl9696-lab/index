<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¡Feliz Cumpleaños!</title>
    <style>
        :root {
            --color-sobre: #ff6b6b;
            --color-carta: #ffffff;
            --color-fondo: #f7d794;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: var(--color-fondo);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
        }

        /* Contenedor del sobre */
        .envelope-wrapper {
            position: relative;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .envelope-wrapper:hover {
            transform: translateY(-10px);
        }

        .envelope {
            position: relative;
            width: 300px;
            height: 200px;
            background-color: var(--color-sobre);
            border-bottom-left-radius: 10px;
            border-bottom-right-radius: 10px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
        }

        /* Triángulo superior (Tapa) */
        .envelope::before {
            content: "";
            position: absolute;
            top: 0;
            z-index: 2;
            border-top: 130px solid var(--color-sobre);
            border-left: 150px solid transparent;
            border-right: 150px solid transparent;
            transform-origin: top;
            transition: all 0.5s ease-in-out;
        }

        /* Lados del sobre */
        .envelope::after {
            content: "";
            position: absolute;
            z-index: 3;
            width: 0;
            height: 0;
            border-top: 100px solid transparent;
            border-right: 150px solid #ff5252;
            border-bottom: 100px solid #ff5252;
            border-left: 150px solid #ff5252;
            border-radius: 0 0 10px 10px;
        }

        /* La Carta */
        .card {
            position: absolute;
            bottom: 10px;
            left: 10px;
            width: 280px;
            height: 180px;
            background-color: var(--color-carta);
            text-align: center;
            padding: 20px;
            box-sizing: border-box;
            z-index: 1;
            transition: all 0.5s ease-in-out;
            border-radius: 5px;
        }

        .card h2 {
            color: #ff6b6b;
            margin: 0;
            font-size: 20px;
        }

        .card p {
            color: #444;
            font-size: 14px;
            line-height: 1.4;
        }

        /* Animación al abrir */
        .envelope-wrapper.open .envelope::before {
            transform: rotateX(180deg);
            z-index: 0;
        }

        .envelope-wrapper.open .card {
            transform: translateY(-150px);
            z-index: 5;
            height: auto;
            min-height: 220px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }

        /* Confeti simple con CSS */
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f00;
            opacity: 0;
        }
    </style>
</head>
<body>

    <div class="envelope-wrapper" id="envelope">
        <div class="envelope">
            <div class="card">
                <h2>🎂 ¡Feliz Cumpleaños, Hermana! 🎈</h2>
                <p id="mensaje">
                    Eres la mejor hermana del mundo. <br>
                    Que este día esté lleno de risas, <br>
                    pasteles y mucha felicidad. <br>
                    <strong>¡Te quiero mucho!</strong>
                </p>
            </div>
        </div>
    </div>

    <script>
        const envelope = document.getElementById('envelope');
        
        envelope.addEventListener('click', () => {
            envelope.classList.toggle('open');
            if(envelope.classList.contains('open')) {
                crearConfeti();
            }
        });

        function crearConfeti() {
            for(let i=0; i<50; i++) {
                const confeti = document.createElement('div');
                confeti.classList.add('confetti');
                confeti.style.left = Math.random() * 100 + 'vw';
                confeti.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
                confeti.style.top = '-10px';
                confeti.style.opacity = '1';
                confeti.style.transform = `rotate(${Math.random() * 360}deg)`;
                document.body.appendChild(confeti);

                const anim = confeti.animate([
                    { transform: `translateY(0) rotate(0)`, opacity: 1 },
                    { transform: `translateY(100vh) rotate(720deg)`, opacity: 0 }
                ], {
                    duration: Math.random() * 3000 + 2000,
                    easing: 'ease-out'
                });

                anim.onfinish = () => confeti.remove();
            }
        }
    </script>
</body>
</html>
