--- 
layout: docs 
title: Core
categories: [Documentation]
---

Script: Core {#Core}
===========================

Provides the global `PhiloGL` function to create WebGL applications, the static `PhiloGL.hasWebGL()` method to detect if the browser is WebGL capable 
and the static `PhiloGL.unpack()` method for unpacking modules into the global namespace.


PhiloGL Static Method: hasWebGL {#PhiloGL:hasWebGL}
------------------------------------------------------

Returns true or false whether the browser supports WebGL or not.

### Syntax:

	PhiloGL.hasWebGL();


PhiloGL Static Method: unpack {#PhiloGL:unpack}
-------------------------------------------------

Unpacks [Vec3](math.html), [Mat4](math.html), [Camera](camera.html), [Program](program.html), [WebGL](webgl.html), [O3D](o3d.html), 
[Scene](scene.html), [Shaders](shaders.html), [IO](io.html), [Events](event.html), [WorkerGroup](workers.html), [Fx](fx.html) 
modules and classes so they can be accessed by the global scope and not through PhiloGL.*moduleName*.

### Syntax:

	PhiloGL.unpack();


PhiloGL Method: constructor {#PhiloGL:constructor}
----------------------------------------------------

Creates a PhiloGL application. The PhiloGL application provides a [WebGL](webgl.html) context, a [Program](program.html), a [Camera](camera.html), a [Scene](scene.html), 
and also options for handling [Events](event.html), loading textures via [IO](io.html) and more.

### Syntax:

	PhiloGL(canvasId, options);

### Arguments:

1. canvasId  - (*string*) The *id* of the canvas element.
5. options - (*object*) An object containing the following options:

### Options:

* context - (*object*, optional) An object to pass in options for when the [WebGL context]() is created. For now the only option supported is `debug: true`.
* program - (*object*, optional) An object that contains options for creating a [Program](program.html). The options for program are:
  * from - (*string*) Possible options are `defaults`, `ids`, `sources`, `uris`.
  * path - (*string*, optional) Sets a link path appended as prefix to the `vs` and `fs` string properties.
  * vs - (*string*) The name, id, source or path to the Vertex Shader.
  * fs - (*string*) The name, id, source or path to the Fragment Shader.
* camera - (*object*, optional) An object with options for creating a [Camera](camera.html). These options are:
  * fov - (*number*) Field of View. Default's `45`.
  * near - (*number*) Near distance. Default's `0.1`.
  * far - (*number*) Far distance. Default's `500`.
  * position - (*object*) The position of the camera. Default's `{ x: 0, y: 0, z: 0 }`.
  * target - (*object*) The target position to where the camera will look at. Default's `{ x: 0, y: 0, z: 0 }`.
* scene - (*object*, optional) [Scene](scene.html) creation options. These options are:

  * lights - (*object*, optional) An object for managing lights. The options for lighting are:
    * enable - (*boolean*) Set this to `true` to enable lighting.
    * ambient - (*object*, optional) A r, g, b object with values in [0, 1] to select ambient lighting.
    * directional - (*object*, optional) An object with properties:
      * direction - (*object*) An object with x, y, z coordinates to display the light direction.
      * color - (*object*) A r, g, b object with values in [0, 1] to select the color.
    * points - (*mixed*, optional) An array of point lights configuration objects containing as properties:
      * position - (*object*) A x, y, z object with the point light position.
      * color|diffuse - (*object*) A r, g, b object with values in [0, 1] that sets the (diffuse) color for the point light.
      * specular - (*object*, optional) A r, g, b object with values in [0, 1] that sets the specular light color.
    * effects - (*object*, optional) An object with scene effect options.
      
      * fog - (*object*, optional) An object with linear fog options explained below.
        * near - (*number*, optional) The near fog factor. Default's the [Camera](camera.html) near factor.
        * far - (*number*) The far fog factor. Default's the [Camera](camera.html) far factor.
        * color - (*object*) An `{ r, g, b }` object with the fog color.
* textures - (*object*, optional) An object to load textures with the [IO](io.html) module. See also [Program.setTexture](). The object has as properties:
  * src - (*array*) An array of strings containing the path of the images to be loaded.
  * textureType - (*string*, optional) The type of the texture. Default's `TEXTURE_2D`.
  * pixelStore - (*array*, optional) An array of name, value objects to define how pixels are stored into the texture. Defualt's `[ { name: 'UNPACK_FLIP_Y_WEBGL', value: true }]`.
  * parameters - (*array*, optional) Parameters to set texture filters among other things. Default's `NEAREST` for `MAG` and `MIN` filters.
  * data - (*object*) An object containing either the dimensions of the texture or the image itself. The properties for the data object are:
    * format - (*number*, optional) The color format of the image. Defaults `RGBA`.
    * value - (*ImageElement*, optional) An image element (if any) to paste into the texture.
    * width - (*number*, optional) The width of the texture. Used when no image is provided. Default's 0.
    * height - (*number*, optional) The height of the texture. Used when no image is provided. Default's 0.
    * border - (*number*, optional) The borde of the texture. Default's 0.
* events - (*object*, optional) An object with callbacks and configuration for event handling. For more information about the event callbacks check the [Event](event.html) documentation. These options are:
  * cachePosition - (*boolean*, optional) Whether to cache the current position of the canvas or calculate it each time in the event loop. Default's `true`.
  * cacheSize - (*boolean*, optional) Whether to cache the size of the canvas or calculate it each time in the event loop. Default's `true`.
  * relative - (*boolean*, optional) Whether to calculate the mouse position as relative to the canvas position or absolute. Default's `true`.
  * centerOrigin - (*boolean*, optional) Whether to set the center (0, 0) coordinate to the center of the canvas or to the top-left corner. Default's `true`.
  * disableContextMenu - (*boolean*, optional) Disable the context menu (generally shown when the canvas is right clicked). Default's `true`.
  * bind - (*mixed*, optional) bind the *thisArg* in the callbacks to the specified object.
  * pick - (*boolean*, optional) Whether to use picking. If true, the second parameter for the callback functions will be an [O3D](o3d.html) target for the event (or a falsy value otherwise). Default's false.
  * onClick - (*function*, optional) Handles the onClick event.
  * onRightClick - (*function*, optional) Handles the onRightClick event.
  * onDragStart - (*function*, optional) Handles the onDragStart event.
  * onDragMove - (*function*, optional) Handles the onDragMove event.
  * onDragEnd - (*function*, optional) Handles the onDragEnd event.
  * onDragCancel - (*function*, optional) Handles the onDragCancel event.
  * onTouchStart - (*function*, optional) Handles the onTouchStart event.
  * onTouchMove - (*function*, optional) Handles the onTouchMove event.
  * onTouchEnd - (*function*, optional) Handles the onTouchEnd event.
  * onTouchCancel - (*function*, optional) Handles the onTouchCancel event.
  * onMouseMove - (*function*, optional) Handles the onMouseMove event.
  * onMouseEnter - (*function*, optional) Handles the onMouseEnter event.
  * onMouseLeave - (*function*, optional) Handles the onMouseLeave event.
  * onMouseWheel - (*function*, optional) Handles the onMouseWheel event.
  * onKeyDown - (*function*, optional) Handles the onKeyDown event.
  * onKeyUp - (*function*, optional) Handles the onKeyUp event.
* onError - (*function*, optional) A callback for when the app creation goes wrong. The first parameter might be an object with the error description.
* onLoad - (*function*) A function called when the application is successfully created. An app is created if the context is loaded, the program is compiled 
and linked correctly, the scene object is created correctly, the events are appended correctly to the canvas element, all textures and images are correctly 
loaded and set and the camera is created. The first parameter of the callback function is an app object that has a properties:
  * gl - (*object*) The WebGL context.
  * camera - (*object*) The [Camera](camera.html) instance.
  * scene - (*object*) The [Scene](scene.html) instance.
  * program - (*object*) The [Program](program.html) instance.



### Examples:

Creates an application from two shader files, sets some camera properties and loads two images as textures. 
Taken from LearningWebGL [lesson 14](http://senchalabs.github.com/philogl/PhiloGL/examples/lessons/14/).

{% highlight js %}
  //Create application
  PhiloGL('lesson14-canvas', {
    program: {
      from: 'uris',
      path: '../../../shaders/',
      vs: 'frag-lighting.vs.glsl',
      fs: 'frag-lighting.fs.glsl'
    },
    camera: {
      position: {
        x: 0, y: 0, z: -50
      }
    },
    textures: {
      src: ['arroway.jpg', 'earth.jpg'],
      parameters: [{
        name: 'TEXTURE_MAG_FILTER',
        value: 'LINEAR'
      }, {
        name: 'TEXTURE_MIN_FILTER',
        value: 'LINEAR_MIPMAP_NEAREST',
        generateMipmap: true
      }]
    },
    onError: function() {
      alert("There was an error creating the app.");
    },
    onLoad: function(app) {
      /* Do things here */
    }
  });

{% endhighlight %}

Creates an application with a moon texture and sets events to apply drag and drop to the moon object as well as to zoom in and out. 
Taken from LearningWebGL [lesson 11](http://senchalabs.github.com/philogl/PhiloGL/examples/lessons/11/).

{% highlight js %}
  //Create application
  PhiloGL('lesson11-canvas', {
    camera: {
      position: {
        x: 0, y: 0, z: -7
      }
    },
    textures: {
      src: ['moon.gif'],
      parameters: [{
        name: 'TEXTURE_MAG_FILTER',
        value: 'LINEAR'
      }, {
        name: 'TEXTURE_MIN_FILTER',
        value: 'LINEAR_MIPMAP_NEAREST',
        generateMipmap: true
      }]
    },
    events: {
      onDragStart: function(e) {
        pos = {
          x: e.x,
          y: e.y
        };
      },
      onDragMove: function(e) {
        var z = this.camera.position.z,
            sign = Math.abs(z) / z;

        moon.rotation.y += -(pos.x - e.x) / 100;
        moon.rotation.x += sign * (pos.y - e.y) / 100;
        moon.update();
        pos.x = e.x;
        pos.y = e.y;
      },
      onMouseWheel: function(e) {
        e.stop();
        var camera = this.camera;
        camera.position.z += e.wheel;
        camera.update();
      }
    },
    onError: function() {
      alert("There was an error creating the app.");
    },
    onLoad: function(app) {
      /* Do stuff here... */
    }
  });

{% endhighlight %}


