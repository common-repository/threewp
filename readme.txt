=== ThreeWP ===
Contributors: rondevs
Tags: Three.js, 3D graphics, WordPress 3D, WebGL, visualization
Requires at least: 5.4
Tested up to: 6.6
Requires PHP: 7.4
Stable tag: 2.0.2
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Easily integrate Three.js with WordPress to create and display 3D models and animations.

== Description ==
ThreeWP is a WordPress plugin that integrates the Three.js library and its addons into your WordPress site using a custom bundle file. This setup allows you to create and manage custom 3D models, animations, and interactive graphics directly within your WordPress theme or custom JavaScript code.

== Features ==

- Custom Bundle Integration: Enqueues the Three.js library and essential addons using a custom bundle file, avoiding reliance on a CDN.
- Easy Setup: Straightforward installation and activation process.
- Custom Integration: No built-in shortcodes or settings; users add their own Three.js code for full customization.

== Source Code ==
The source code for the minified JavaScript bundle file used in this plugin is publicly available at the following URL: https://github.com/rondevs/threejs-custom-bundler


== Installation ==

1. From WordPress Dashboard:
- Go to your WordPress dashboard.
- Navigate to **Plugins** > **Add New**.
- In the search bar, type **ThreeWP**.
- Locate the **ThreeWP** plugin and click **Install Now**.
- After installation, click **Activate**.

2. Manual Installation:
- Download the plugin zip file from the [WordPress.org plugin repository](https://wordpress.org/plugins/threewp).
- Go to your WordPress dashboard.
- Navigate to **Plugins** > **Add New**.
- Click on **Upload Plugin** and select the downloaded zip file.
- Click **Install Now** and then **Activate** the plugin.

== Usage ==

After activating the plugin, Use the `[use_threewp]` shortcode to enable Three.js for specific pages. Three.js and its addons will be available for use in your theme or custom JavaScript files. You need to manually add your Three.js code to create and manage 3D content.

=== Example Usage ===

Add Custom JavaScript:
- Add your Three.js initialization and rendering code to your theme’s JavaScript file or use a custom script. Here’s a basic example:

``
	document.addEventListener('DOMContentLoaded', function () {
		if (typeof ThreeWP !== 'undefined') {
			// Destructure THREE and THREE_ADDONS from ThreeWP
			const { THREE, OrbitControls } = ThreeWP;
			// Create a scene
			const scene = new THREE.Scene();
			// Setup a camera
			const camera = new THREE.PerspectiveCamera(
				75,
				window.innerWidth / window.innerHeight,
				0.1,
				1000,
			);
			// Setup a renderer
			const renderer = new THREE.WebGLRenderer();
			// Give the renderer a width and height
			renderer.setSize(window.innerWidth, window.innerHeight);
			// Append the renderer into the html body
			document.body.appendChild(renderer.domElement);
			// Set camera position
			camera.position.z = 2;
			// Load a texture
			const textureLoader = new THREE.TextureLoader();
			const texture = textureLoader.load(
				'https://threejsfundamentals.org/threejs/resources/images/wall.jpg',
			); // Replace with your image URL
			// Create geometry
			const geometry = new THREE.BoxGeometry(1, 1, 1);
			// Create material
			const material = new THREE.MeshStandardMaterial({ map: texture });
			// Combine into mesh
			const sphere = new THREE.Mesh(geometry, material);
			scene.add(sphere);
			const light = new THREE.AmbientLight(0xffffff);
			scene.add(light);
			// Set up OrbitControls
			const controls = new OrbitControls(
				camera,
				renderer.domElement,
			);
			// Optional: Adjust controls settings (e.g., damping, auto-rotation)
			controls.enableDamping = true; // Adds smoothness when dragging
			controls.dampingFactor = 0.03;
			controls.autoRotate = true;
			controls.autoRotateSpeed = 2;
			function animate(t = 0) {
				requestAnimationFrame(animate);
				controls.update();
				renderer.render(scene, camera);
			}
			animate();
			// Responsive
			window.addEventListener('resize', () => {
				camera.aspect = window.innerWidth / window.innerHeight;
				camera.updateProjectionMatrix();
				renderer.setSize(window.innerWidth, window.innerHeight);
			});
		} else {
			console.error('Three.js could not be loaded.');
		}
	});
``

NOTE: Destructure THREE and the addons to access from ThreeWP bundle.

== Tips ==

Responsive Design: Adjust the size of the Three.js container or renderer according to your design requirements. Handle window resizing events to keep the 3D content responsive.
Documentation: Refer to the Three.js documentation for detailed information on creating more complex scenes, objects, and animations.

== Available Tools in This Plugin ==

-   **THREE**
-   **Addons:**
    -   ArcballControls
    -   BufferGeometryUtils
    -   CameraUtils
    -   CCDIKSolver
    -   ConvexGeometry
    -   ConvexH
    -   CSS2DRenderer
    -   CSS3DRenderer
    -   DecalGeometry
    -   DRACOLoader
    -   DragControls
    -   EdgeSplitModifier
    -   EffectComposer
    -   FirstPersonControls
    -   FlyControls
    -   FontLoader
    -   GLTFLoader
    -   KTX2Loader
    -   LDrawLoader
    -   Lensflare
    -   LensflareElement
    -   LightProbeGenerator
    -   LightProbeHelper
    -   Lut
    -   LUT3dlLoader
    -   LUTCubeLoader
    -   MapControls
    -   MeshSurfaceSampler
    -   MMDAnimationHelper
    -   MMDLoader
    -   MMDPhysics
    -   MTLLoader
    -   OBB
    -   OBJLoader
    -   OrbitControls
    -   ParametricGeometry
    -   PCDLoader
    -   PDBLoader
    -   PointerLockControls
    -   PositionalAudioHelper
    -   RectAreaLightHelper
    -   Rhino3dmLoader
    -   SceneUtils
    -   SDFGeometryGenerator
    -   SkeletonUtils
    -   Sky
    -   SVGLoader
    -   SVGRenderer
    -   TeapotGeometry
    -   TextGeometry
    -   TGALoader
    -   Timer
    -   TrackballControls
    -   TransformControls
    -   VertexNormalsHelper
    -   VertexTangentsHelper
    -   XREstimatedLight

== Changelog ==

== v2.0.2 ==
* Updated custom bundle file.
* Removed external dependencies from the bundle.
* Introduced shortcode [use_threewp] to load the Three.js bundle script only on pages that contain the shortcode.

= 2.0.1 =
* Added `defer` attribute to the Three.js script for improved performance and load times.
* Updated plugin code for better compatibility with modern browsers.

= 2.0.0 = 
*Introduced custom bundle file integration for Three.js and essential addons like OrbitControls, GLTFLoader, EffectComposer, and BloomPass etc. 
*This version enhances the plugin's capabilities and provides a more comprehensive setup for integrating Three.js with WordPress.

= 1.1.0 =
* Added Three.js Addons Support with CDN

= 1.0.0 =
* Initial release of the Three.js CDN Integration plugin.

== Frequently Asked Questions ==
= How do I use Three.js with this plugin?
= After activating the plugin, you can include Three.js code in your theme, html element or custom plugin to create and manage 3D models.

== Contributing ==

We welcome contributions to improve this plugin. If you have suggestions, bug reports, or feature requests, please open an issue on https://github.com/rondevs/threewp/issues.

== License ==

This plugin is licensed under the GPLv2 or later. See the LICENSE file for details.

== Support ==

If you encounter any issues or need assistance, please reach out via https://github.com/rondevs/threewp/issues.

Thank you for using ThreeWP! We hope it enhances your WordPress site with exciting 3D content.