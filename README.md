# anp412-ar-lab
repository for ANP 412 (Method &amp; Practice in Digital Heritage) augmented reality lab (using A-Frame and ar.js)
## ANP 412 Augmented Reality Lab

In this tutorial, we're going to walk through how you create an augmented reality (AR) experience via your phone's mobile browser, by creating a webpage that uses your phone's camera to display a 3D model when pointed at a paper target. We'll be using [AR.js](https://ar-js-org.github.io/AR.js-Docs/) and one of the Javascript frameworks it can rely upon, [A-Frame](https://aframe.io/).

To start off with, open the `basic_html_template.html` file in your code editor of choice (There are lots of options, but we recommend either [Pulsar](https://pulsar-edit.dev/) or [VSCode](https://code.visualstudio.com/). There are other options for both Mac and PC, many of which are listed on the [Resources](https://anthropology.msu.edu/anp412-fs24/resources/) page on the course website. The important thing is that you can't use a text editor like Word - doing so will completely screw your project up.

> How do you download the files that this tutorial is working with? The easiest way (if you aren't already familiar with Github) is just to click the big green download Code button above and choose the Download Zip option. This will download the file you'll be working with (as well as all of the other supplementary examples files). After you download it, unzip the folder and stick it somewhere safe and obvious on your computer - your desktop is probably the best.
>
Make sure you save the `basic_html_template.html` after every step (just in case). You might also resave the file using a different filename - `basic_html_template_lastname.html` for example.

### Linking to the AR.js Javascript Library Files

The first thing we need to do is point to the AR.js Javascript file. This is basically telling the webpage where it will need to look for the Javascript it will be executing.

1\. In the `<head>` section of the `basic_html_template.html` document (below the `<title>`, enter:

`<script src="https://aframe.io/releases/1.3.0/aframe.min.js"></script>`

This file contains code that AR.js relies upon for displaying the 3D files.

2\. Next is the AR.js code itself, which you will place below the code added in the previous step. Enter:

`<script src="https://raw.githack.com/AR-js-org/AR.js/dev/aframe/build/aframe-ar.js"></script>`

This file is what the webpage uses to track the location where the model will display. In the case of this tutorial it will be tracking a paper target.

### Building the Camera Viewer Webpage

1\. Now it's time to build the webpage itself. Begin by defining the style of the page's body. In the `<style>` section of the `basic_html_template.html` document, enter the following code:

    ` body{
        margin:0px;
        overflow:hidden;
    }`

This snippet of CSS code tells the webpage to load the camera viewer without any unused space around the edges of the screen and without showing a scrollbar. This means the webpage, when loaded, will take up the entire view of the browser.

2\. Next, you will tell the webpage what parameters to rely upon when calling the AR.js and A-Frame code libraries you added earlier. Begin by telling it what kind of scene to create. To the `<body>` section of the document, add the following:

    `<a-scene
        embedded
        arjs
        renderer="logarithmicDepthBuffer: true;"
        vr-mode-ui="enabled: false"
        id="scene"
    >

    </a-scene>`

This block of code is referred to in HTML as an element, which is styled in a way that is meaningful to the A-Frame library. It has a number of attributes to tell the webpage how this scene should be loaded, including that it is embedded on a webpaged, that it's an AR.js scene, that it is using a specific model renderer when it displays the 3D model, and that its AV mode is disabled. Later in this tutorial we will add an addtional attribute, but for now these will get the model working.

3\. Within the `<a-scene>` element (so, at the blank line, between `>` and `</a-scene>`), add this additional block of code:

`<a-marker preset="hiro">

</a-marker>
<a-entity camera></a-entity>
`

The first of these elements tells the scene to rely upon the "hiro" tracking code, for when it analyzes the view from the camera, for where to place the 3D model in the display. The second element tells the scene to use the camera to create the webpage's view.

4\. Now, within the `<a-marker>` element (again, on the blank line), place this block of code:

`<a-entity

>
</a-entity>`

This element will define all of the aspects of the 3D model to be displayed, when the view through the camera detects the specified target.

At this point, your entire body section should look like this:

`    <body>
        <a-scene
            embedded
            arjs
            renderer="logarithmicDepthBuffer: true;"
            vr-mode-ui="enabled: false"
            gesture-detector
            id="scene"
        >
            <a-marker preset="hiro">
                <a-entity

                >
                </a-entity>
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
`
### Defining the 3D model's display parameters

1\. Using an `<a-entity>` element inside of an `<a-marker>` element to set the display parameters for a given 3D model relies on several customizable attributes. For the purposes of this tutorial, we will only cover a few of the available options, but more can be found by looking through the [A-Frame 1.3.0 knowledge base](https://aframe.io/docs/1.3.0/).

Find this section of your code:
`<a-marker preset="hiro">
    <a-entity

    >
    </a-entity>
</a-marker>
`

2\. On this blank line, put in the following block of code:

`position="0 0 0"
rotation="0 0 0"
scale="1 1 1"
gltf-model="assets/3d/toy-ambulance-gltf/scene.gltf"
`

This block of attributes controls the eventually-displayed 3D model, including which model is loaded. The `position` attribute specifies the X, Y, and Z coordinates of the model, referenced to the target; `rotation` controls the model's rotation along its X, Y, and Z axes (in degrees), again relative to the model's saved state and the referenced target; and `scale` controls the size of the model along its X, Y, and Z axes, based once again upon the model's saved state. In the example values provided here, the model will load exactly at the target, without any rotation, and at its default size. If, for instance, you wanted to lay the model on one side and double its size, you could change it to `rotation="90 0 0"` and `scale="2 2 2"`.

The final attribute defines the type of 3D file being used, and its pathway relative to this webpage's code. In this example, the 3D model is in the `gltf` format, which is an open-source 3D file format gaining popularity. The 3D model is saved inside of some folders contained within the same project, so this pathway is relative. That is, the `.gltf` file is inside of a folder called `toy-ambulance-gltf`, which itself is inside a folder called `3d`, which itself is inside `assets`.

### Adding Pinch-Zoom and Rotation Functionality



### Next Steps and Going Further

Want to go a little further? Fom here, you can try:

* Placing more than one marker on the map. Have a look at `basic_leaflet_multiple_pins.html` for an example.
* Bind pop ups to multiple markers. Have a look at `basic_leaflet_multiple_pins_and_popups.html` for an example.
* Make the map fullscreen. Have a look at `fullscreen_leaflet.html` for an example.
* Make the fullscreen map edge to edge in the browser. Have a look at `edge_to_edge_leaflet.html` for an example.

### Some Helpful Resources

There are lots of grest resources out there for learning Leaflet (or doing more than we've covered in this lab):

* Leflet itself ahs some pretty good tutorials: [https://leafletjs.com/examples.html](https://leafletjs.com/examples.html)
* Joshua Frazier's Leaflet tutorial (covers some of the same things we looked at, but goes a little further): [https://joshuafrazier.info/leaflet-basics/](https://joshuafrazier.info/leaflet-basics/)
* [Leaflet Tutorial](https://maptimeboston.github.io/leaflet-intro/), written for Maptime Boston by Andy Woodruff and Ryan Mullins that gets into some more advanced techniques such as incorporating jQuery, external geojson files and the Leaflet.markercluster plugin into a project.
* [Leaflet.JS Introduction](https://luxembourgjs.github.io/leaflet-demo/#/), by Thierry Nicola for JS Luxembourg.
* [Leaflet provider map](https://leaflet-extras.github.io/leaflet-providers/preview/index.html), an open source Leaflet extension that contains configurations for various free tile providers.
* [Mapbox Guides](https://docs.mapbox.com/help/) and [examples](hhttps://docs.mapbox.com/mapbox-gl-js/example/) are great for learning about web maps in general in addition to Mapbox.js, which is built on top of Leaflet.
