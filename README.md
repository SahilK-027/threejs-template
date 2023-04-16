# Three.js - Template

Get started with Three.js to render 3d Web Experience.

## Setup

Download Node.js. Run this followed commands:

```bash
# Install dependencies (only the first time)
npm install

# Run the local server at localhost:8080
npm run dev

# Run the local server at locat ip
npm run host

# Build for production in the dist/ directory
npm run build
```
## Credits
- [Vite Bundler](https://vitejs.dev/)

## 🤨 What is WebGL?
WebGL is a JavaScript API that renders triangles in a canvas at a remarkable speed. It's compatible with most modern browsers, and it's fast because it uses the Graphic Processing Unit (GPU) of the visitor.

WebGL can draw more than triangles and can also be used to create 2D experiences, but we will focus on 3D experiences using triangles for the course's sake.

The GPU can do thousands of parallel calculations. Imagine that you want to render a 3D model and this model is constituted of 1000 triangles—which, come to think about it, is not that many. Each triangle includes 3 points. When we want to render our model, the GPU will have to calculate the position of these 3000 points. Because the GPU can do parallel calculations, it will handle all the triangles points in one raw.

Once the model's points are well placed, the GPU needs to draw each visible pixel of those triangles. Yet again, the GPU will handle the thousands and thousands of pixels calculations in one go.

The instructions to place the points and draw the pixels are written in what we call shaders. And let me tell you, shaders are hard to master. We also need to provide data to these shaders. For example: how to place the points according to the model transformations and the camera's properties. These are called matrices. We also need to provide data to help colorize the pixels. If there is a light and the triangle is facing that light, it should be brighter than if the triangle isn't.

And this is why native WebGL is so hard. Drawing a single triangle on the canvas would take at least 100 lines of code. Good luck if you want to add perspective, lights, models, and animate everything in that case.

But native WebGL benefits from existing at a low level, very close to the GPU. This enables excellent optimizations and more control.

## 🤨 What is three.js ?
Three.js is a cross-browser JavaScript library and application programming interface used to create and display animated 3D computer graphics in a web browser using WebGL. The source code is hosted in a [repository](https://github.com/mrdoob/three.js/) on GitHub.
### See also
- [Three.js](https://en.wikipedia.org/wiki/Three.js) on Wikipedia
- [Three.js official website](https://threejs.org/)

Three.js is the most popular JavaScript framework for displaying three-dimensional content on the web.
Three.js eliminates the need for a high-end gaming PC or console to display photorealistic 3D graphics. You don't even need to instal any software. With only a smartphone and a web browser, anyone can now experience stunning 3D applications in the palm of their hand.

This incredible library, as well as the vibrant community that surrounds it, are all you need to create games, music videos, scientific and data visualisations, and pretty much anything else you can think of, right in your browser on your laptop, tablet, or smartphone!

<a href="https://threejs.org/"><img width="1440" alt="three.js" src="https://user-images.githubusercontent.com/104154041/210220215-9f70696a-f899-4d98-ba20-3f7c77ee19e1.png"></a>

## 💖 List of my favourite Three.js projects:


<table>
<tr>
<td>(1)</td>
<td><a href="https://bruno-simon.com/"><img width="200" src = "https://user-images.githubusercontent.com/104154041/210220729-dd908da9-38dc-4d04-8f78-f752de85ba9e.png" alt = "bruno-simons"></a></td>
<td><a href="https://bruno-simon.com/">Bruno Simon's Portfolio Website</a><br/></td>

<td>(2)</td>
<td><a href="https://coastalworld.com/"><img width="200" src = "https://user-images.githubusercontent.com/104154041/210223053-e7382a16-b2f6-4502-b7d1-520c1ef6be1c.png" alt = "img"></a></td>
<td><a href="https://coastalworld.com/">Coastal World</a><br/></td>
</tr>


<tr>
<td>(3)</td>
<td><a href="https://lusion.co/"><img width="200" src = "https://user-images.githubusercontent.com/104154041/210222106-ba178df0-eb57-4f12-8dfa-c0bb6a09e55c.jpg" alt = "lusion"></a></td>
<td><a href="https://lusion.co/">lusion.co</a><br/></td>

<td>(4)</td>
<td><a href="https://www.oculus.com/medal-of-honor/"><img width="200" src = "https://user-images.githubusercontent.com/104154041/210222396-984c3a51-fd1d-4015-9b98-1cfe4cf6bf17.jpg" alt = "alt"></a></td>
<td><a href="https://www.oculus.com/medal-of-honor/">Medal of honor</a><br/></td>
</tr>

<tr>
<td>(5)</td>
<td><a href="https://heraclosgame.com/"><img width="200" src = "https://user-images.githubusercontent.com/104154041/210222576-aa50f1ee-fa82-483b-9535-77fd30c33c2b.png" alt = "img"></a></td>
<td><a href="https://heraclosgame.com/">Heraclos Game</a><br/></td>

<td>(6)</td>
<td><a href="https://midwam.com/en"><img width="200" src = "https://user-images.githubusercontent.com/104154041/210221555-f28ad8fc-6866-44ac-800e-e3a184f0e070.jpg" alt = "MIDWAM"></a></td>
<td><a href="https://midwam.com/en">MIDWAM Company</a><br/></td>
</tr>

<tr>
<td>(7)</td>
<td><a href="https://www.knguru.de/en"><img width="200" src = "https://user-images.githubusercontent.com/104154041/232286380-317e9287-554d-417d-9a60-0b6853a21959.jpg" alt = "img"></a></td>
<td><a href="https://www.knguru.de/en">Knguru</a><br/></td>

<td>(8)</td>
<td><a href="http://cabbi.bo/enough/"><img width="200" src = "https://user-images.githubusercontent.com/104154041/232286385-5c15d3f3-76fe-468f-b8ad-9ec5859edf9b.png" alt = "MIDWAM"></a></td>
<td><a href="http://cabbi.bo/enough/">Enough</a><br/></td>
</tr>

</table>

### Made with 💜 by [SahilK-027](https://github.com/SahilK-027)
