# Martina-te-amo
Eres y siempre serás la mejor mujer que he conocido te amo más que a nada en este mundo y quiero q todo el mundo sepa que eres la mejor😿❤️‍🩹💗

index.html 
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Martina 💗 Te Amo</title>

<style>
html, body {
    margin: 0;
    padding: 0;
    overflow: hidden;
    background: black;
    height: 100%;
    font-family: Arial, sans-serif;
}

canvas {
    display: block;
}

#hint {
    position: fixed;
    bottom: 30px;
    width: 100%;
    text-align: center;
    color: #ffb6c1;
    font-size: 18px;
    opacity: 0.9;
    z-index: 10;
}
</style>
</head>

<body>

<div id="hint">Toca la pantalla para escuchar nuestra canción 💗</div>

<audio id="bg-music" loop playsinline>
    <source src="https://cdn.pixabay.com/download/audio/2022/03/24/audio_4e5c5d1c66.mp3?filename=perfect-112662.mp3" type="audio/mpeg">
</audio>

<script src="https://cdn.jsdelivr.net/npm/three@0.128.0/build/three.min.js"></script>

<script>
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

camera.position.z = 5;

// Corazones flotando
const hearts = [];
const heartShape = new THREE.Shape();
heartShape.moveTo(0, 0);
heartShape.bezierCurveTo(0, 0, -0.5, -0.5, -1, 0);
heartShape.bezierCurveTo(-1.5, 1, 0, 2, 0, 3);
heartShape.bezierCurveTo(0, 2, 1.5, 1, 1, 0);
heartShape.bezierCurveTo(0.5, -0.5, 0, 0, 0, 0);

const geometry = new THREE.ShapeGeometry(heartShape);

for (let i = 0; i < 60; i++) {
    const color = new THREE.Color().setHSL(Math.random() * 0.1 + 0.9, 0.8, 0.6); // Tonos rosa/rojo
    const material = new THREE.MeshBasicMaterial({ color: color });
    const heart = new THREE.Mesh(geometry, material);
    heart.position.set(
        (Math.random() - 0.5) * 12,
        (Math.random() - 0.5) * 12,
        (Math.random() - 0.5) * 8
    );
    heart.scale.set(0.4, 0.4, 0.4);
    scene.add(heart);
    hearts.push(heart);
}

// Texto central personalizado
const canvasText = document.createElement("canvas");
canvasText.width = 800;
canvasText.height = 400;
const ctx = canvasText.getContext("2d");

ctx.fillStyle = "#ff69b4";
ctx.font = "bold 80px Arial";
ctx.textAlign = "center";
ctx.textBaseline = "middle";
ctx.fillText("👑 Martina 👑", 400, 120);

ctx.fillStyle = "white";
ctx.font = "bold 48px Arial";
ctx.fillText("Te amo más que a nada", 400, 200);
ctx.fillText("en este mundo", 400, 260);
ctx.fillText("Eres mi todo 💕", 400, 320);

const texture = new THREE.CanvasTexture(canvasText);
const textMaterial = new THREE.SpriteMaterial({ map: texture });
const textSprite = new THREE.Sprite(textMaterial);
textSprite.scale.set(8, 4, 1);
scene.add(textSprite);

// Animación
function animate() {
    requestAnimationFrame(animate);
    hearts.forEach(h => {
        h.rotation.y += 0.008;
        h.rotation.x += 0.008;
        h.position.y += 0.002;
        if (h.position.y > 8) h.position.y = -8;
    });
    renderer.render(scene, camera);
}
animate();

// Música + ocultar hint
const audio = document.getElementById("bg-music");

function startMusic() {
    audio.volume = 0.5;
    audio.play().catch(() => {});
    document.getElementById("hint").style.display = "none";
    document.removeEventListener("touchstart", startMusic);
    document.removeEventListener("click", startMusic);
}

document.addEventListener("touchstart", startMusic, { once: true });
document.addEventListener("click", startMusic, { once: true });

// Resize
window.addEventListener("resize", () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
});
</script>

</body>
</html>