#Google Cardboard Javascript Browser App
#### Sheridan IMM: Tech Studio Term 2 Project
#### Repo: googleCardboard_techstudio_term2

####Contributors: Caitlin Haaf, Jermain Joseph, Lucey Kim
******

JS Library: [three.js](https://github.com/mrdoob/three.js/)

All the effects/contollers etc. used were pulled from the [three.js library examples](https://github.com/mrdoob/three.js/tree/master/examples)  
* Effects and Systems: 
  + [Stero effect](https://github.com/mrdoob/three.js/blob/master/examples/webgl_effects_stereo.html) - splits the screen in half and duplicates the image.
  + [GPU Particle System](https://github.com/mrdoob/three.js/blob/master/examples/webgl_gpu_particle_system.html) - allows for the generation/manipulation/destruction of particle systems
* Renderers:
  + [Canvas Renderer](https://github.com/mrdoob/three.js/blob/master/examples/js/renderers/CanvasRenderer.js)
  + [Projector Renderer](https://github.com/mrdoob/three.js/blob/master/examples/js/renderers/Projector.js)
* Controls:
  + [Device Orientation Controls](https://github.com/mrdoob/three.js/blob/master/examples/js/controls/DeviceOrientationControls.js)
  + [Orbit Controls](https://github.com/mrdoob/three.js/blob/master/examples/js/controls/OrbitControls.js)

1. Firstly, in the body of our index.html document, create a div that will act as a container for our project.
```{r}
<div id="webglviewer"></div>
```
Then style this div so that is takes up the entire device screen/ broswer window 
```{r}
body {
        margin: 0;
        overflow: hidden;
      }
#webglviewer {
        bottom: 0;
        left: 0;
        position: absolute;
        right: 0;
        top: 0;
      }	
```
2. Be sure to link to all of the neccessary modules/libraries etc. (links above)
```r
    <!-- EFFECTS/LIBRARIES  -->
    <script src="js/three.min.js"></script>
    <script src="js/StereoEffect.js"></script>
    <script src="js/GPUParticleSystem.js" charset="utf-8"></script>

    <!-- THREE JS CONTROLS  -->
    <script src="js/controls/DeviceOrientationControls.js"></script>
    <script src="js/controls/OrbitControls.js"></script>

    <!-- RENDERERS -->
    <script src="js/renderers/Projector.js"></script>
    <script src="js/renderers/CanvasRenderer.js"></script>
```

3. Set up the variables you will need to set up the camera, animations, particle systems, etc.
```{r}
    //CAMERA/SETUP VARIABLES
    //------------------------------
    var scene,
        camera,
        renderer,
        element,
        container,
        effect,
        controls,
        clock = new THREE.Clock(true),

    //PARTICLE SYSTEM VARIABLES
    //------------------------------
    tick = 0,
    options1,
    options2,
    spawnerOptions,
		particleSystem1,
    particleSystem2,
    effect,

    //PARTICLE VARIABLES
    //------------------------------
    particles = new THREE.Object3D(),
    totalParticles = 30,
    maxParticleSize = 80,
    particleRotationSpeed = .1,
    particleRotationDeg = 5,
    lastColorRange = [0, 5],
    currentColorRange = [0, 0.3];
    
    init()
```
4. The rest of the app will be run in the init function we initiated above. You will want to create a new three.js scene, camera (to be added to/positioned within the scene), renderer (to be applied to the #webglviewer div), stereo effect (to be applied to the renderer), and control schemes (to be added to the window).
```r
function init() {
        // CAMERA SETUP
        scene = new THREE.Scene();
        camera = new THREE.PerspectiveCamera(90, window.innerWidth / window.innerHeight, 0.001, 700);
        camera.position.set(0, 15, 0);
        scene.add(camera);

        //RENDERER SETUP
        renderer = new THREE.WebGLRenderer();
        element = renderer.domElement;
        container = document.getElementById('webglviewer');
        container.appendChild(element);

// STEREO EFFECT
//------------------------------
effect = new THREE.StereoEffect(renderer);


// ORBIT CONTROLS
//------------------------------
// Our initial control fallback with mouse/touch events in case DeviceOrientation is not enabled
controls = new THREE.OrbitControls(camera, element);
controls.target.set(
  camera.position.x + 0.15,
  camera.position.y,
  camera.position.z
);
controls.noPan = true;
controls.noZoom = true;
// Our preferred controls via DeviceOrientation
function setOrientationControls(e) {
  if (!e.alpha) {
    return;
  }
  controls = new THREE.DeviceOrientationControls(camera, true);
  controls.connect();
  controls.update();

  element.addEventListener('click', fullscreen, false);

  window.removeEventListener('deviceorientation', setOrientationControls, true);
}
window.addEventListener('deviceorientation', setOrientationControls, true);
```
