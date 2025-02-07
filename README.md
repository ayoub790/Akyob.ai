# Akyob.ai

html
<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>موقع ثلاثي الأبعاد</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="scene-container"></div>
    <div class="content">
        <h1>مرحبًا بك في موقع ثلاثي الأبعاد</h1>
        <p>هذا مثال بسيط لموقع تفاعلي مع رسومات ثلاثية الأبعاد.</p>
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r146/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.4/gsap.min.js"></script>
    <script src="script.js"></script>
</body>
</html>

css
body, html {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
    font-family: Arial, sans-serif;
    color: white;
}

#scene-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
}

.content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    z-index: 1;
}

h1 {
    font-size: 3rem;
    margin-bottom: 20px;
}

p {
    font-size: 1.5rem;
}

javascript
// إعداد المشهد ثلاثي الأبعاد
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.getElementById('scene-container').appendChild(renderer.domElement);

// إضافة إضاءة
const light = new THREE.DirectionalLight(0xffffff, 1);
light.position.set(5, 5, 5).normalize();
scene.add(light);

// إنشاء كائن ثلاثي الأبعاد (مكعب)
const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshPhongMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

// ضبط وضعية الكاميرا
camera.position.z = 5;

// تحريك الكائن
function animate() {
    requestAnimationFrame(animate);
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    renderer.render(scene, camera);
}
animate();

// جعل الموقع متجاوبًا مع تغيير حجم النافذة
window.addEventListener('resize', () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
});

// إضافة تحريك باستخدام GSAP
gsap.from(cube.scale, {
    duration: 2,
    x: 0,
    y: 0,
    z: 0,
    ease: "power2.out",
    repeat: -1,
    yoyo: true
});

javascript
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

const loader = new GLTFLoader();
loader.load('path/to/model.glb', (gltf) => {
    scene.add(gltf.scene);
});
