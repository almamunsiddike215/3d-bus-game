let scene = new THREE.Scene();
let camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
let renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// light
const light = new THREE.DirectionalLight(0xffffff, 1);
light.position.set(0, 20, 10);
scene.add(light);

// field 
const groundGeometry = new THREE.PlaneGeometry(100, 100);
const groundMaterial = new THREE.MeshStandardMaterial({ color: 0x808080 });
const ground = new THREE.Mesh(groundGeometry, groundMaterial);
ground.rotation.x = - Math.PI / 2;
scene.add(ground);

// bus stand 
const busGeometry = new THREE.BoxGeometry(2, 1, 4);
const busMaterial = new THREE.MeshStandardMaterial({ color: 0xff0000 });
const bus = new THREE.Mesh(busGeometry, busMaterial);
bus.position.y = 0.5;
scene.add(bus);

camera.position.set(0, 5, 10);
camera.lookAt(bus.position);

// keyboard control 
let keys = {};
document.addEventListener("keydown", e => keys[e.key] = true);
document.addEventListener("keyup", e => keys[e.key] = false);

// animate loop
function animate() {
  requestAnimationFrame(animate);

  if (keys["ArrowUp"]) bus.position.z -= 0.1;
  if (keys["ArrowDown"]) bus.position.z += 0.1;
  if (keys["ArrowLeft"]) bus.rotation.y += 0.05;
  if (keys["ArrowRight"]) bus.rotation.y -= 0.05;

  camera.position.x = bus.position.x + Math.sin(bus.rotation.y) * 10;
  camera.position.z = bus.position.z + Math.cos(bus.rotation.y) * 10;
  camera.lookAt(bus.position);

  renderer.render(scene, camera);
}
animate();# 3d-bus-game
hi five 
