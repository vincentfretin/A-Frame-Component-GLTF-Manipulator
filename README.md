# A-Frame-Component-GLTF-Manipulator
<img src="img/screenshot.gif" title="Video screen capture" alt="Video screen capture" height="300">



### **Description / Rationale**
This is a A-Frame component which allows to manipulate GLTF/GLB file. In particular it demonstrates the possibility editing position, rotation, scale, visibility, material color and texture of individual nodes.   

### **Instructions**

In order to use the component one attach "gltf-manipulator" to an entity. The component has the following attributes: 
* <b>nodeNumber: { type: 'int', default: 1 }</b> - the number of nodes of a GLTF/GLB file to be edited. All other attributes are dependent on it, i.e. if 2 is indicated, then the rest of attributes should have by 2 values.   
* <b>nodeName: { type: 'array', default: [] }</b> - the name of individual node(s) in a GLTF/GLB file. It is different from node material name. Accepts array of strings. They could be seen in Blender before exporting GLTF file (or alternatively they can be console.logged).    
* <b>nodePosition: { type: 'array', default: [] }</b> - position of individual node(s) in a GLTF/GLB file. Accepts array of x y z values.
* <b>nodeRotation: { type: 'array', default: [] }</b> - rotation of individual node(s) in a GLTF/GLB file. Accepts array of x y z values.
* <b>nodeScale: { type: 'array', default: [] }</b> - scale of individual node(s) in a GLTF/GLB file. Accepts array of x y z values.
* <b>nodeVisibility: { type: 'array', default: [] }</b> - visibility of individual node(s) in a GLTF/GLB file. Accepts array of boolean values
* <b>nodeMaterialName: { type: 'array', default: [] }</b> - the name(s) of individual node material(s) in a GLTF/GLB file. It is different from node name. Accepts array of strings. They could be seen in Blender before exporting GLTF file (or alternatively they can be console.logged).
* <b>nodeTextureURL: { type: 'array', default: [] }</b> - the URL(s) to individual node texture(s) to be added to a GLTF/GLB file. Accepts array of strings.
* <b>nodeColor: { type: 'array', default: [] }</b> - color(s) of individual node(s). Accepts array of HEX values.

If attributes are indicated inline, they will be loaded as soon as a-frame is loaded. To make more precise changes it is possible to combine it with the following function:
```
updateNodeFunction(nodeName, textureURL, position, rotation, scale, color, visibility);
```
The code below shows the sample implementation of the compoent. Initially major edits are done inline to GLTF file, then individual changes are done through button click event:
```
<html>
<head>
    <title>A-Frame Component: GLTF Manipulator</title>
    <script src="https://aframe.io/releases/1.4.2/aframe.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/donmccurdy/aframe-extras@v6.1.1/dist/aframe-extras.min.js"></script>
    <script src="js/gltf-manipulator-component.js"></script>
</head>
<body>
    <a-scene>
        <a-entity gltf-manipulator="
        nodeNumber: 2;
        nodeName: Circle003_drum_paint_0, Cube004_drum_defaultCol_0; 
        nodePosition: 0 0 0, 0 0 0;
        nodeRotation: 90 0 0, 0 0 0;
        nodeScale: 1 1 1, 1 1 1;
        nodeVisibility: true, true;
        nodeMaterialName: drum_paint, raccoon_paint; 
        nodeTextureURL: ;
        nodeColor: " 
        id="model" 
        position="0 1 -3" 
        scale="0.2 0.2 0.2" 
        gltf-model="url(model/raccoon.glb)"
        animation-mixer>
        </a-entity>
        <a-sky color="#ECECEC"></a-sky>
    </a-scene>
    <script>
        // Update individual nodes
        document.querySelector('a-scene').addEventListener('loaded', function () {
            document.querySelector('#myButton').addEventListener('click', () => {
                updateNodeFunction(
                    'drum_paint',       // node name
                    'model/drum.png',   // textureURL
                    '0 -4 1',            // position
                    '0 0 0',            // rotation
                    '1 1 1',            // scale
                    '#ffffff',          // color
                    true                // visibility
                );
                updateNodeFunction(
                    'raccoon_paint',       // node name
                    'model/raccoon.png',   // textureURL
                    '0 1 1',            // position
                    '0 0 0',            // rotation
                    '1 1 1',            // scale
                    '#ffffff',          // color
                    true                // visibility
                );            
            });
        })

    </script>
</body>

</html>
```

### **Tech Stack**
The project is powered by AFrame and Three.js. 3D model of raccoon was created by Hiu Kim and was taken from <a href="https://github.com/hiukim/mind-ar-js/tree/master/examples/image-tracking/assets/band-example/raccoon">MindAr.js repository</a>. 

### **Demo**
See demo of the component here: [Demo](https://gltf-manipulator.glitch.me/)
