					/////////////////////////////
					//  	Lightning Talk
					/////////////////////////////

	1. What problem does this technology solve?

		Three.js allows front-end developers to take the UX/UI of their apps and projects to a whole new level of creativity. 

							-Features-

			Anaglyph, cross-eyed and parallax barrier.

			Scenes: add and remove objects at run-time; fog

			Cameras: perspective and orthographic; 

			Controllers: trackball, FPS, path and more

			Animation: armatures, forward kinematics, inverse kinematics, morph and keyframe

			Lights: ambient, direction, point and spot lights; shadows: cast and receive

			Materials: Lambert, Phong, smooth shading, textures and more

			Shaders: access to full OpenGL Shading Language (GLSL) 

			Capabilities: lens flare, depth pass and extensive post-processing library

			Objects: meshes, particles, sprites, lines, ribbons, bones and more - all with Level of detail

			Geometry: plane, cube, sphere, torus, 3D text and more; modifiers: lathe, extrude and tube

			Data loaders: binary, image, JSON and scene

			Utilities: full set of time and 3D math functions including frustum, matrix, quaternion, UVs and more

			Export and import: utilities to create Three.js-compatible JSON 

			Files from within: Blender, openCTM, FBX, Max, and OBJ

			Support: API documentation is under construction, public forum and wiki in full operation

			Examples: Over 150 files of coding examples plus fonts, models, textures, sounds and other support files

			Debugging: Stats.js, WebGL Inspector, Three.js Inspector

			Runs in all browsers supported by WebGL.

		Physijs plugin brings an easy-to use interface to three.js.
		Easy for graphics newbies to get into 3D programming. 
		Makes physics simulations easy to run. 

									-Features-

				Support for multiple object shapes, including convex objects and heightfields.
				
				Material system provides simple control over friction and restitution ("bounciness")
				
				Integrated collision detection and events
				
				Compound objects using three.js's hierarchy system 
			
				Full constraint system including Point, Hinge, Degree of Freedom, and more
				
				Vehicle systems
				
				Rotations using either euler or quaternion systems - your preference
				
				Built on top of three.js to keep same convention and coding style


		The Three.js library is being used for a wide variety of applications and purposes including:

			Mixed Media

			Model Visualization and Scene Creation Applications

			Game and Simulation Authoring Tools

			Education


	2. How do you use it? 
	  
	  About: https://github.com/mrdoob/three.js/wiki

	  Three.js is a cross-browser JavaScript library/API used to create and display animated 3D computer graphics in a web browser.Three.js uses WebGL. 

	  Physijs is built on top of ammo.js and runs the physics simulation in a separate thread (via web worker) to avoid impacting the application's performance and taking up 3D rendering time. Apart from updating an object's position, all of the normal three.js conventions remain the same.
	

										Getting Started

			Download three.js

				 Download link on left side of screen at http://threejs.org/. 
				 Once zip downloads, open it.
				 Go to the build folder, find file three.min.js.
				 Copy this file into your local development directory.

				For this tutorial, you’ll need a file called OrbitControls.js, included in three.js download. 
				File path: threejs folder > examples > js > controls > OrbitControls.js

				If you’d rather grab the files, they’rein example code for this tutorial.

			Setup the Local Environment

				JavaScript has a security feature 'the same-origin policy', meaning you cannot load externally hosted files inside your JavaScript code. Three.js needs to load geometry, textures, and other files. 
				You’ll need a local http server so that your files come from the same origin. Simply opening the index.html file directly in the browser isn’t going to work.

				There’s a three.js FAQ with a guide on how to run three.js locally using either Python, Ruby, or adjusting your browser settings. 

			Create 3D Assets

				Use 3D version of the Treehouse logo (you can find the mesh inside the code download), but if you’d like to create your own meshes, use Blender. It’s a 3D modeling and rendering package that’s free, open source, and cross-platform.
				To export a mesh from Blender for use in three.js, open the utility folder in three.js and install the exporter.

			The HTML

				You’ve got files in place and local environment setup
				You need a basic template. This assumes your JavaScript is stored in a folder called js, so check your file paths.

				index.html

				!doctype html<script src="js/three.min.js"></script><script src="js OrbitControls.js"></script>

				<script>// <![CDATA[// Our 3D code will go here... // ]]></script>

			Create 3D Scenes

				We could write JavaScript externally, but since there aren’t any HTML elements inside of body, inline script tags are used.

			Global Variables and Functions

				Inside script tags, set up some global variables and call some functions, all of which will be defined later on:

				 	 // Set up the scene, camera, and renderer as global variables.
			 		 var scene, camera, renderer;
			 
			  			init();
						animate();

			Create the Scene

				Three.js uses the concept of a scene to define an area where you can place geometry, lights, cameras, etc. 
				In the following code, we start writing our initialization function by creating a scene. 
				Then, we store the width and height of the browser window in the variables WIDTH and HEIGHT. 
				We’ll need them in more than once place later on, so it’s good to just grab them once and store them.

					// Globals from the previous step go here...
			 
			  		// Sets up the scene.
			  			function init() {
			 
			    	// Create the scene and set the scene size.
			    		scene = new THREE.Scene();
			   			var WIDTH = window.innerWidth,
			      		HEIGHT = window.innerHeight;
			 
			  		// More code goes here next...
			 
						  }
			Create the Renderer

				Set up a three.js renderer. We could use the SVG or canvas renderers, but we want to use the WebGL renderer because it’s able to take advantage of the GPU, which makes it several orders of magnitude more performant. After creating the renderer, we append it to the DOM via the body element. This will make three.js create a canvas inside the body element that will be used to render our scene.

			  // Sets up the scene.
			  function init() {
			 
			    // Code from previous steps goes here...
			 
			    // Create a renderer and add it to the DOM.
			    renderer = new THREE.WebGLRenderer({antialias:true});
			    renderer.setSize(WIDTH, HEIGHT);
			    document.body.appendChild(renderer.domElement);
			 
			    // More code goes here next...
			 
			  }
			Create a Camera

			Once our scene and renderer are in place, we can create a camera. The PerspectiveCamera takes a few parameters. They are:

			FOV – We’re using 45 degrees for our field of view.
			Apsect – We’re simply dividing the browser width and height to get an aspect ratio.
			Near – This is the distance at which the camera will start rendering scene objects.
			Far – Anything beyond this distance will not be rendered. Perhaps more commonly known as the draw distance.
			After our camera is created, we set the position by using some simply XYZ coordinates. The default is 0,0,0 but I’ve set the Y value to 6 just to get some distance between our view and the mesh.

			Finally, we need to add the camera to the scene.

			  // Sets up the scene.
			  function init() {
			 
			    // Code from previous steps goes here...
			 
			    // Create a camera, zoom it out from the model a bit, and add it to the scene.
			    camera = new THREE.PerspectiveCamera(45, WIDTH / HEIGHT, 0.1, 20000);
			    camera.position.set(0,6,0);
			    scene.add(camera);
			 
			    // More code goes here next...
			 
			  }
			Update the Viewport on Resize

			This is all well and good, but what happens when the site visitor resizes the browser window? For that, we’ll need to add an event listener. When the browser is resized, a couple of things happen. First, we resample the new width and height of the browser and store it in a variable that’s scoped to the function. Then, we use those values to set the new size of our renderer as well as recalculate the aspect ratio of the camera. In addition, we need to call updateProjectionMatrix() on the camera object so that our scene will actually update with the new parameters. This is computationally expensive in the context of real-time 3D rendering, but once the browser is resized, things click back to their normal frame rates.

			  // Sets up the scene.
			  function init() {
			 
			    // Code from previous steps goes here...
			 
			    // Create an event listener that resizes the renderer with the browser window.
			    window.addEventListener('resize', function() {
			      var WIDTH = window.innerWidth,
			          HEIGHT = window.innerHeight;
			      renderer.setSize(WIDTH, HEIGHT);
			      camera.aspect = WIDTH / HEIGHT;
			      camera.updateProjectionMatrix();
			    });
			 
			    // More code goes here next...
			 
			  }
			Add Lighting

			Now it’s time to start crafting our scene a bit. By calling the setClearColorHex function on our WebGLRenderer object, we’re able to set the background color of our scene to the Treehouse grey hex color with an opacity of 1.

			Next, we’ll need a light in order to see our 3D objects, so we’ll add a PointLight to the scene and set its position. There are several other kinds of lights you can add to a scene, so be sure to check out the linked documentation.

			  // Sets up the scene.
			  function init() {
			 
			    // Code from previous steps goes here...
			 
			    // Set the background color of the scene.
			    renderer.setClearColorHex(0x333F47, 1);
			 
			    // Create a light, set its position, and add it to the scene.
			    var light = new THREE.PointLight(0xffffff);
			    light.position.set(-100,200,100);
			    scene.add(light);
			 
			    // More code goes here next...
			 
			  }
			Load Geometry

			Our mesh has been exported from Blender using the three.js JSON exporter, so we need to use the JSONLoader to get the geometry into the scene. A callback is used inside the loader to set the material on the mesh. In this case, we’re using a basic LambertMaterial to set the mesh to Treehouse’s green color. For completeness, I should note here that the green you’re seeing in the final render isn’t quite the same as Treehouse’s logo green. That’s because the point light is skewing the brightness slightly, but we won’t worry about it for this demo.

			Before leaving the callback function, we create a new mesh with our geometry and the material as parameters, then we add the mesh to the scene.

			  // Sets up the scene.
			  function init() {
			 
			    // Code from previous steps goes here...
			 
			    // Load in the mesh and add it to the scene.
			    var loader = new THREE.JSONLoader();
			    loader.load( "models/treehouse_logo.js", function(geometry){
			      var material = new THREE.MeshLambertMaterial({color: 0x55B663});
			      mesh = new THREE.Mesh(geometry, material);
			      scene.add(mesh);
			    });
			 
			    // More code goes here next...
			 
			  }
			Add Controls

			The last thing in our initialization function is the orbit controls we included earlier. These aren’t totally necessary, but they do allow us to drag the mouse across the mesh and orbit around it. It also allows the mousewheel to be used to zoom in and out of the mesh.

			  // Sets up the scene.
			  function init() {
			 
			    // Code from previous steps goes here...
			 
			    // Add OrbitControls so that we can pan around with the mouse.
			    controls = new THREE.OrbitControls(camera, renderer.domElement);
			 
			  }
			 
			  // More code goes here next...
			Render the Scene

			After our initialization function, we need to finish up with our animation function. It may not seem like anything is really “animated” here in the traditional sense, but we do need to redraw when the camera orbits around the mesh.

			The requestAnimationFrame() function uses a newer browser API that delegates redraws to the browser. This has some pretty cool benefits, but primarily it makes sure the browser isn’t drawing your animation unnecessarily if that tab isn’t currently selected. Paul Irish wrote an excellent blog post on requestAnimationFrame that explains this in more detail.

			After that, we need to render our scene through the camera we added earlier and then update the orbit controls.

			  // Sets up the scene.
			  function init() {
			    // Code from previous steps goes here...
			  }
			 
			  // Renders the scene and updates the render as needed.
			  function animate() {
			 
			    // Read more about requestAnimationFrame at http://www.paulirish.com/2011/requestanimationframe-for-smart-animating/
			    requestAnimationFrame(animate);
			 
			    // Render the scene.
			    renderer.render(scene, camera);
			    controls.update();
			 
			  }
			To see what the final result looks like, be sure to download the code. Try changing some of the parameters around and see what happens!



	3. Is there a "cheatsheet" you found or made that others can reference?
		
	

			Documentation: 
				
				Physijs 	


	4. What did you build with this technology?

http://chandlerprall.github.io/Physijs/examples/jenga.html


What are the differences between WebGL, ThreeJS, CSS 3D and D3.JS?

WebGL: is the Javascript API that allows you to create 3D graphics in the browser.

Three.js: A framework build on top of WebGL which makes it easier to create 3D graphics in the browser, it uses a canvas + WebGL to display the 3D scene.

CSS 3D: CSS only has some 3D transforms which make it possible to achieve  3D effects with regular DOM nodes.

D3.js: D3 is a data visualisation library. It makes it easy to generate and modify graphics based on data. This is nothing about 3D though.
Use cases

If you want to do simple 3D effects on your website try CSS3 transformations, check out this nice introduction: Intro to CSS 3D transforms
If you want to do 3D models/textures/render scenes, more like "real" 3D, use Three.js. It's a nice and simple layer on top of WebGL, it is well documented, and has a lot of documentation. Start with the Three.js intro docs: three.js / documentation or check out this introduction tutorial: https://aerotwist.com/tutorials/...
For data driven 2D graphics, use D3. This library has a lot of power to build your own custom graphs, update them, and make them interactive.  Nice introduction: Overview
Just for fun: It is possible to combine all above, a very cool demo: delimited | CrunchBase Top Investors and the article that goes along with the demo: D3.js, Three.js and CSS 3D Transforms




GOOGLE SLIDE:
https://docs.google.com/presentation/d/1UcJn7UfPIg0UR24mJ7BExJ4dPQtPu1oXDbqUeza8joM/edit#slide=id.gd9c453428_0_16

