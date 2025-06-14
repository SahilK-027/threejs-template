# Theory of some important topics

## Scene graph

In Three.js, a scene graph is a hierarchical data structure used to organize and manage all the objects in a 3D scene.

At its core, s scene graph is like a tree structure, where:

- The root is the `Scene` object.
- Each node is an `Object3D` (or a subclass like `Mesh`, `Group`, `Camera`, `Light`, etc.).
- You add things as child using `.add()` method.

```
Ex. scene.add(camera);
Ex. carGeometry.add(playerGeometry)
```

- Each node can have children, forming a parent-child relationship.

### Why it's important:

The scene graph lets you:

- Organize complex scenes easily.
- Apply transformations (position, rotation, scale) to parent objects and have them affect all children.
- Efficiently render scenes by traversing the graph and drawing each object.

## Lights

### Ambient light

- A global light that illuminates all objects equally, no matter where they are or how they're oriented.
- Has no direction, no shadows, and no falloff.
- Usage: Used as a base fill light to ensure that all parts of your scene are at least slightly visible, especially in shadowy areas.

### Hemisphere light

- Similar to ambient light, that simulates the sky and ground.
- Illuminates objects from above (sky color) and below (ground color).
- Directionless like ambient, but gives a soft gradient feel, more natural than plain ambient light. No shadows.
- Usage: Good for outdoor scenes where you want a soft, diffuse light feel from the environment.

### React area light

- Emits light from a rectangular surface.
- Usage: More physically accurate for things like windows, soft boxes, or ceiling panels.
- Only works with `MeshStandardMaterial` and `MeshPhysicalMaterial`.
- No shadow.
- Needs to be manually added to the scene and oriented correctly.
- Requires `RectAreaLightUniformsLib` to be initialized.

### Directional light

- Simulates light from a faraway source, like the sun.
- All rays are parallel, creating strong, uniform shadows.
- Casts shadows and can be targeted to a specific object.
- Usage: Ideal for simulating sunlight or moonlight in outdoor scenes.

### Point light

- Emits light in all directions from a single point (like a light bulb).
- Has distance-based falloff and can cast shadows.
- Usage: Great for simulating bulbs, torches, or small light sources.

### Spotlight

- Emits a cone-shaped beam of light (like a flashlight or stage light).
- Has an angle, decay, distance, and can cast shadows.
- Can be aimed at a specific point using .target.
- Usage: Used when you need focused lighting, e.g., on characters, objects, or stages.

## Textures in 3D Graphics

In 3D graphics, a texture is not just a decorative image, it's data applied to the surface of a 3D object to control specific properties of the material. Textures act as inputs that drive how a material behaves visually.

### Types of Textures & What They Control

Here’s what different types of texture maps do:
| Texture Type | Role / Purpose |
| -------------------------- | -------------------------------------------------------------- |
| **Color / Diffuse** | Defines the **base color** of a surface |
| **Normal Map** | Simulates **fine surface detail** by altering lighting normals |
| **Bump Map** | Similar to normal maps, but simpler, using grayscale height |
| **Displacement Map** | Actually modifies **geometry vertices** (expensive) |
| **Roughness Map** | Controls how **rough or smooth** a surface appears |
| **Metalness Map** | Defines which parts behave like **metal** |
| **AO (Ambient Occlusion)** | Simulates shadows in crevices for **realism** |
| **Alpha Map** | Controls **transparency** |
| **Emissive Map** | Makes parts of a model **glow** |
| **Specular Map** | (older model) Defines **highlight strength** |
| **Environment Map** | Simulates **reflections** (skybox, cubemap, etc.) |

### Normal Map vs Bump Map vs Height Map vs Displacement Map

| Type                 | Alters Geometry? | Alters Lighting?  | Affects Silhouette? | Realism                           | Performance |
| -------------------- | ---------------- | ----------------- | ------------------- | --------------------------------- | ----------- |
| **Bump Map**         | ❌ No            | ✅ Yes (simple)   | ❌ No               | Low                               | Fast        |
| **Normal Map**       | ❌ No            | ✅ Yes (accurate) | ❌ No               | Medium                            | Medium      |
| **Height Map**       | 🔸 Used as input | ❌ By itself      | ❌ No               | Used for Displacement or Parallax |             |
| **Displacement Map** | ✅ Yes           | ✅ Yes (indirect) | ✅ Yes              | High                              | Slowest     |

### All Mesh Materials in Three.js

1. `MeshBasicMaterial`

- Lighting: ❌ No lighting, no shadows.
- Use: Simple unlit color, UI, wireframes, always fully bright.
- Realism: ❌ None.
- Performance: ✅ Very fast.

2. `MeshDepthMaterial`

- Lighting: ❌ No direct lighting.
- Use: Renders depth from camera — black = near, white = far.
- Realism: ❌ Not for direct use, but useful for shadows, post-processing, fog.
- Performance: ✅ Fast.

3. `MeshDistanceMaterial`

- Lighting: ❌ No direct lighting.
- Use: Encodes distance to a reference point/light (used in shadow computations like RectAreaLightShadow).
- Realism: ❌ Not visible directly in scenes.
- Performance: ✅ Fast.

4. `MeshLambertMaterial`

- Lighting: ✅ Yes (Lambertian shading – diffuse only).
- Use: Basic lit material. No specular highlights.
- Realism: 🟠 Low-medium.
- Performance: ✅ Fast.
- Limitations: No specular (shiny) reflections.

5. `MeshMatcapMaterial`

- Lighting: ❌ No real lighting. Uses a baked lighting image (matcap).
- Use: Stylized rendering (e.g., sculpting preview, clay material).
- Realism: 🟡 Depends on the matcap.
- Performance: ✅ Very fast.
- Note: Lighting baked into texture; rotates with camera.

6. `MeshNormalMaterial`

- Lighting: ❌ No lights, shows surface normals.
- Use: Debug surface orientation. Color = normal vector.
- Realism: ❌ None.
- Performance: ✅ Very fast.

7. `MeshPhongMaterial`

- Lighting: ✅ Yes (Phong model – diffuse + specular).
- Use: Glossy surfaces, shininess, metal, glass.
- Realism: 🟡 Moderate.
- Performance: 🟡 Medium.
- Note: Legacy, not PBR (Physically Based Rendering). Still good for simple shiny objects.

> **NOTE**
>
> What is physically based rendering?
> Physically based rendering (PBR) is a method of shading in computer graphics that aims to simulate the physical behavior of a light beam and its interaction with materials to achieve photoreal visuals. It employs algorithms based on physically accurate formulas to replicate real-world materials, resulting in cohesive and photorealistic environments.

8. `MeshStandardMaterial`

- Lighting: ✅ Full PBR (Physically Based Rendering).
- Use: Real-world surfaces (wood, metal, stone, etc.).
- Realism: ✅ High.
- Performance: 🔵 Slower than Phong.
- Supports: Roughness, metalness, environment maps, AO, etc.

9. `MeshPhysicalMaterial`

- Lighting: ✅ Full PBR + extended physical features.
- Use: Advanced materials like glass, clearcoat, fabric.
- Realism: ✅✅ Highest.
- Performance: 🔴 Heaviest (most computations).
- Supports Extra: clearcoat, transmission, ior, sheen, etc.

10. `MeshToonMaterial`

- Lighting: ✅ Yes, uses cel-shading style.
- Use: Cartoon, stylized look. Requires gradientMap.
- Realism: ❌ Stylized.
- Performance: 🟢 Efficient.
- Note: Great for anime/comic-style rendering.

(^ `MeshToonMaterial` is my favourite one)

### Summary table

| Material               | Lighting   | Shadows | Realism     | Style         | Performance | Use Case                     |
| ---------------------- | ---------- | ------- | ----------- | ------------- | ----------- | ---------------------------- |
| `MeshBasicMaterial`    | ❌ No      | ❌ No   | ❌ None     | Flat/Unlit    | ✅ Fastest  | UI, colors, always visible   |
| `MeshDepthMaterial`    | ❌ No      | N/A     | ❌ None     | Depth Debug   | ✅ Fast     | Shadow mapping, fog, effects |
| `MeshDistanceMaterial` | ❌ No      | N/A     | ❌ None     | Distance Calc | ✅ Fast     | Shadow distance computation  |
| `MeshLambertMaterial`  | ✅ Diffuse | ✅ Yes  | 🟠 Basic    | Matte         | ✅ Fast     | Simple lighting              |
| `MeshMatcapMaterial`   | ❌ Baked   | ❌ No   | Stylized    | Sculpting     | ✅ Fast     | Clay/anime/matcap style      |
| `MeshNormalMaterial`   | ❌ No      | ❌ No   | ❌ None     | Debug         | ✅ Fast     | Visualize normals            |
| `MeshPhongMaterial`    | ✅ Yes     | ✅ Yes  | 🟡 Moderate | Glossy        | 🟡 Medium   | Old-school shiny objects     |
| `MeshStandardMaterial` | ✅ PBR     | ✅ Yes  | ✅ High     | Realistic     | 🔵 Slower   | Modern realism               |
| `MeshPhysicalMaterial` | ✅ PBR++   | ✅ Yes  | ✅✅ Ultra  | Glass, fabric | 🔴 Slowest  | Advanced realism             |
| `MeshToonMaterial`     | ✅ Yes     | ✅ Yes  | ❌ Stylized | Cartoon       | 🟢 Good     | Toon/anime effects           |

## The Two RGB Worlds: Linear vs. sRGB

### sRGB: Perceptual, Non‑Linear Space

- **Designed for our eyes**: Humans are more sensitive to dark tones than bright ones, so sRGB applies a gamma curve that allocates more precision where we notice it most.
- **Great for display**: Images and textures saved in sRGB “look right” on monitors, TVs, phones.
- **Bad for math**: Because the relationship between stored values and actual intensity is non‑linear, blending or lighting computations on sRGB data produce incorrect results—shading that’s too bright or too dark.

### Linear: The Math‑Friendly Space

- **True proportionality**: A value of 0.5 is exactly half the light of 1.0.
- **Essential for lighting**: All physically based rendering (PBR) lighting, shadowing, and material math assume linear arithmetic to model energy conservation and realistic falloff.

---

## Mixing Spaces: The Root of Many Rendering Bugs

Since textures, colors, and light intensities all start as simple RGB numbers, it’s easy to forget which space you’re in. Accidentally lighting in sRGB space leads to:

- **Gamma artifacts**—unexpected banding, blow‑outs, or muddy shadows
- **Inaccurate color shifts**—your bright highlights won’t “feel” physically correct

---

## Why HDR? Capturing Real‑World Brightness

Standard (LDR) renders clamp values into [0…1], so a blazing sun and a candle flame both end up somewhere in that tiny range. HDR (High Dynamic Range) lets you:

1. **Use floating‑point buffers** (e.g. `RGBE`, `RGBA16F`) so intensities ost.
2. **Drive PBR shaders**—materials like `MeshStandardMaterial` or `MeshPhysicalMaterial` expect HDR input to simulate metallic reflections, bloom, etc.
3. **Preserve contrast**—from the deepest shadows (0.01) to the brightest speculars (1000.0+).

---

## Tone Mapping: From HDR to Your Monitor

Monitors still only accept [0…1] in sRGB, so you need a “compressor”:

- **Linear**: Straight scale of all values; often too flat or washed‑out.
- **Reinhard**: A filmic classic:
  ```jsx
  result = color / (color + 1);
  ```
  → rolls off bright areas into soft white.
- **Cineon**: Designed to mimic film scan response.
- **ACES**: Academies’ standard: more gamut, more contrast, filmic but controlled.
- **AcesNeutral (AgX/Neutral)**: A newer, subtler “balanced” look—minimal hue shifts, realistic preserves.

Tone‑mapping operators each have trade‑offs in contrast, saturation, and highlight roll‑off; choosing one depends on your artistic needs.

---

## Putting It All Together in Three.js

1. **Textures & Color Spaces**

   - **Color textures** (diffus, emissive):
     ```jsx
     texture.colorSpace = THREE.SRGBColorSpace;
     ```
   - **Data textures** (normal, height, roughness, metalness):
     ```jsx
     texture.colorSpace = THREE.LinearColorSpace;
     ```

   Data maps do not represent “color” but raw values, so they must stay linear.

2. **Scene Colors**

   When you write `new THREE.Color(0xffeecc)`, assume sRGB. Three.js will convert to linear under-the-hood before lighting.

3. **Renderer Setup**

   ```jsx
   const renderer = new THREE.WebGLRenderer({ antialias: true });
   renderer.outputColorSpace = THREE.SRGBColorSpace;
   renderer.toneMapping = THREE.ACESFilmicToneMapping; // or Reinhard, Cineon, rtc.
   renderer.toneMappingExposure = 1.0; // tweak for scene brightnes
   ```

4. **Lighting Calculations**

   Three.js does all lighting in linear space automatically, so long as your inputs are tagged correctly.

5. **Custom Shaders**

   If you write GLSL:

   ```glsl
   vec3 linearColor = pow(texel.rgb, vec3(2.2));   // sRGB → linear
   // … lighting math in linear …
   vec3 finalSRGB = pow(linearColor, vec3(1.0/2.2)); // linear → sRGB
   gl_FragColor = vec4(finalSRGB, texel.a);
   ```

---

## Best Practices & Gotchas

- **Always label your textures** with the correct `colorSpace`.
- **Keep lighting math linear**—never blend or add raw sRGB values.
- **Pick a tone‑mapper** early, then adjust exposures as you light your scene.
- **Check your final look** on an sRGB‑calibrated display; HDR previews in some browsers/OSs can deceive you.

---

By respecting the separation between perceptual (sRGB) and arithmetic (linear) spaces, leveraging HDR buffers, and choosing an appropriate tone‑mapping curve, you unlock true-to-life lighting from the soft glow of a candle to the blinding radiance of the sun.
