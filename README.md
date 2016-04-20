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
*Controls:
  + [Device Orientation Controls](https://github.com/mrdoob/three.js/blob/master/examples/js/controls/DeviceOrientationControls.js)
  + [Orbit Controls](https://github.com/mrdoob/three.js/blob/master/examples/js/controls/OrbitControls.js)

1. Firstly, set up the variables you will need to set up the camera, animations, particle systems, etc.
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
```
