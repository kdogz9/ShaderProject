# ShaderProject
 
 ### 1. Stylized Water Material with World Position Offset  
**Technical Requirements:**  
- Implement **World Position Offset (WPO)** to create animated wave motion
- Use time-based animation for continuous wave movement
- Include parameters for wave height, speed, and frequency
- Add visual elements: foam, depth fade, refraction, or transparency
- Demonstrate vertex animation without skeletal meshes

For this material, I started with creating the parameters for the water colour and the depth. This was so I could make the water a realistic colour and adjust the parameters of the colour being darker as depth was added to the material using a scattering depth parameter. 
![ ](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image.png)

I then added WPO to the normal map of the water texture to be able to animate the wave movement and control the parameters for how fast/slow I wanted the waves to move.
![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-1.png)

 I then added in the foam to appear around the edges of the water when it touched the rocks surrounding it. This gives it more realism and emphasises the effects of the waves. 
 ![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-2.png)

 *End result*

 ![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-3.png)
 ![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-4.png)

**Guiding Questions:**
- How does WPO affect performance compared to animated meshes?

World Position Offset (WPO) runs in the vertex stage every frame. This is good for when simple maths is used i.e fewer waves and meshes arent really dense.  However, it becomes heavy when you stack wave octaves or use high density meshes. WPO is better to use for large bodies of water which is what I have used in my project since I’ve made a pool of water rather than adding in waterfalls. This makes the performance a lot cheaper and more flexible compared to animated meshes.  Animated meshes include skeletal and Vertex animation textures (VAT). Skeletal involves a high CPU and skinning cost and is more suitable for waterfalls/ smaller bodies of water. VAT reads baked motion on GPU and has a stable cost but adds texture bandwidth.These are usually used for materials which require more complex motions as they can be cleaner and more advanced than WPO. 

- How can you control wave direction and intensity?

I controlled wave direction and intensity by adding parameters to my material instance of the water material. I chose to add water tiling which when controlled it adjusts how stretched the material is to give a more controlled ripple effect of the normal material. Adjusting this changes how the ripples will look. I added wave speed to control how fast it moved, the faster the speed the more choppy look the waves give and I also added a parameter to adjust the intensity of them so they could appear more relaxed if needed. I added texture panning for both the x and y values so that the material would move both forward and backwards rather than just in one direction to make it look more realistic and have a better flow. 

![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-5.png)

- How does your water material respond to different lighting conditions?

When the directional light is adjusted using the time of day cycle I have made in my MPC, the water has highlights added on the waves where the light hits it during the dark and the foam still appears as white as well. The colour of the water goes really dark but when the light is set to during the day it goes back to normal as expected. 

![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-6.png)

### 2. Material Parameter Collection (MPC) System  
**Technical Requirements:**  
- Create an MPC with at least **4 parameters** that control a global scene effect
- Implement the MPC in **at least 2 different materials**
- Create a Blueprint that modifies MPC values at runtime
- Demonstrate a cohesive environmental effect (e.g., time of day, weather system, global color grading)

I implemented a Material Parameter Collection to dynamically control environmental changes based on the time of day. The collection includes parameters for time of day, lamp tint, sunlight tint, and rain intensity, allowing multiple materials to react in sync.

![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-20.png) 
material parameter collection 

![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-21.png)
time of day parameter set up in the level blueprint 

![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-22.png)
lamp tint material 
![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-23.png)
sky tint material 
![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-24.png)
rock material 
The time of day parameter ranges from 0 to 1, smoothly transitioning the scene from day to night while influencing the other parameters. As night falls, the lamps shift from a soft pink hue to a glowing blue, increasing their emissive intensity to simulate artificial lighting in the dark. Meanwhile, the sky transitions from a warm pink to a deep purple, creating a natural dusk effect. Additionally, the rock materials gain a subtle shine at night, using increased roughness and reflection to mimic dew forming on their surfaces.
![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-25.png)
beginning of the day 
![alt text](https://raw.githubusercontent.com/kdogz9/ShaderProject/refs/heads/main/image-26.png)
middle of the day 
![alt text](image-28.png)
end of the day 

 This setup creates a cohesive and immersive atmosphere that visually communicates the passage of time and changing environmental conditions.

**Guiding Questions:**
- Why use MPC instead of individual material parameters?

Using a Material Parameter Collection (MPC) instead of individual material parameters allowed me to efficiently synchronize visual changes across multiple materials and lighting elements in my scene.If I had relied on individual material parameters, I would have had to manually update each material or use multiple blueprints to coordinate these effects, making the process more complex and less consistent. The MPC made it possible to achieve smooth, cohesive transitions across the environment with one central controller, improving both performance and workflow efficiency.

- How does your system maintain visual consistency across materials?

My system maintains visual consistency across materials by using a Material Parameter Collection (MPC) to drive all environmental changes from a single, unified set of parameters.Since they all use the same set of parameters, the lighting, color palette, and material reactions remain perfectly synchronized. This centralized control ensures that the environment changes feel cohesive and natural, maintaining a consistent visual tone throughout the scene.

### 3. Dynamic Material Instance with Runtime Control  
**Technical Requirements:**  
- Create a material with **at least 3 exposed parameters** (scalar and/or vector)
- Implement a **Dynamic Material Instance (DMI)** in Blueprint
- Create interactive controls to modify parameters during gameplay
- Demonstrate a practical use case (e.g., damage effect, dissolve, customization, hit feedback)

I implemented a Dynamic Material Instance (DMI) to allow real-time adjustments to various material properties through user input. The DMI controls three key parameters: Water Tint, Opacity Level, and Glow Intensity. 
![ ](image-17.png)
Water tint final product 
![alt text](image-18.png)
opacity final product 
![alt text](image-19.png)
glow final product 

I set up input bindings so that pressing the 1 key changes the water’s tint to pink using a Vector Parameter, while pressing 2 modifies the Scalar Parameter controlling a ball’s opacity, making it visible in the scene. Pressing 3 adjusts another Scalar Parameter to increase the ball’s glow intensity, giving it an emissive effect. 
![ ](image-15.png)
water tint blueprint 
![alt text](image-16.png)
opacity and glow blueprint 

The DMI is linked directly to the corresponding materials in the level, enabling each parameter change to update instantly during gameplay.
![alt text](image-13.png) 
water tint material set up 
![alt text](image-14.png)
opacity and glow material set up 

 This setup demonstrates how DMIs can provide flexible, interactive control over material behaviors without the need to recompile shaders or duplicate materials, streamlining both testing and visual experimentation.

**Guiding Questions:**
- When should you use DMI versus Material Instance Constant?

In my project, I used a Dynamic Material Instance (DMI) because I needed materials that could change in real time based on player input. These interactions required the material properties to update instantly during gameplay, which is exactly what DMIs are designed for. In contrast, a Material Instance Constant (MIC) is better suited for static or pre-defined variations—values that are set in the editor and remain fixed during runtime. If I had used MICs, I would have had to create separate instances for each visual variation and could not modify them interactively without rebuilding. By using DMIs, I was able to achieve smooth, real-time visual feedback while maintaining a single, flexible material setup, making them ideal for any system that needs dynamic responsiveness.

- How do you optimize DMI creation and updates?

I optimized Dynamic Material Instance (DMI) creation and updates by carefully managing when and how they were generated and modified during gameplay. Rather than creating new DMIs every time a key was pressed, I created them once at the start of the level and stored references to reuse throughout runtime. This allowed me to efficiently update parameters—like the water tint, ball opacity, and glow intensity—without the overhead of repeatedly instantiating materials. For example, when the player pressed keys 1, 2, or 3, I simply updated the existing DMI’s vector or scalar parameters to change the tint, opacity, or emissive glow instantly. Keeping the DMI linked directly to the materials in the scene also ensured minimal performance cost while maintaining responsiveness. This approach reduces unnecessary memory usage and improves frame stability, making it a best practice for optimizing DMI performance in real-time environments. 

### 4. Parallax Occlusion Mapping (POM) Material  
**Technical Requirements:**  
- Implement **Parallax Occlusion Mapping** using UE5's POM node
- Use appropriate height map with visible depth effect
- Configure min/max steps for quality vs. performance balance
- Apply POM offset to all relevant texture samples (base color, normal, roughness)
- Demonstrate self-occlusion and depth parallax

I implemented Parallax Occlusion Mapping (POM) to create a realistic sense of depth and surface detail within my material. I began by setting up Parallax UVs that combined the base material, ambient occlusion (AO) texture, and normal map to enhance the visual complexity. I then introduced parameters for the material’s metallic and roughness values, allowing for easy adjustments to surface reflectivity. To generate the 3D illusion of depth, I created a Pixel Depth Intensity parameter and multiplied it by the Pixel Depth Offset, which shifts the texture coordinates to simulate parallax. 
![alt text](image-8.png)
The AO texture was integrated into the POM setup, and I added parameters for Height Ratio, Min Strength (32), and Max Strength (64) to fine-tune the perceived surface height. Additionally, I included a Boolean parameter to enable shadow rendering, setting its shadow strength to 32, and applied an underlay texture to add subtle detail beneath the main surface. 
![alt text](image-9.png)
This combination of parameterized controls and layered textures allowed the material to achieve a convincing, adjustable 3D effect while maintaining performance flexibility.
![alt text](image-10.png) 
![alt text](image-11.png)
**Guiding Questions:**

- What types of surfaces benefit most from POM?

I found that Parallax Occlusion Mapping (POM) works best on surfaces that need detailed depth without using extra geometry. For example, materials like rocks, brick walls, or uneven ground textures benefit greatly from POM because the technique simulates realistic height variation and surface layering through texture manipulation. In my implementation, I used Parallax UVs with a base material, AO texture, and normal map to create the illusion of depth, supported by parameters like Pixel Depth Intensity and Height Ratio. These allowed me to control how strongly the texture appeared to rise or sink, giving flat surfaces a more three-dimensional look. Since I also added shadow rendering and underlay textures, the material responded more realistically to lighting, which further enhanced the illusion of physical geometry. Overall, POM is ideal for static, detailed surfaces that viewers observe up close—where visual richness is important but additional polygons would be inefficient.


- What are the limitations at silhouette edges?

I noticed that while Parallax Occlusion Mapping (POM) effectively creates the illusion of depth on flat surfaces, it has clear limitations at silhouette edges. Since POM only manipulates texture coordinates and pixel depth rather than the actual mesh geometry, it cannot alter the object’s outline. For example, in my material setup—where I used Parallax UVs, AO textures, and normal maps with parameters like Pixel Depth Intensity and Height Ratio—the illusion of 3D depth worked convincingly on flat or slightly angled surfaces. However, at the edges of objects, such as the borders of rocks or raised areas, the surface still appeared flat when viewed from an oblique angle. The fake depth doesn’t extend beyond the mesh’s silhouette, so shadows and highlights at those edges don’t match the perceived geometry. This makes POM less effective for objects where the profile shape is visible or plays a key role in realism, reinforcing that the technique works best for flat or low-angle surfaces where edges aren’t prominently exposed. 

#### Option A: Post Process Material
- Create a post-process material with a visible screen effect
- Choose blendable location (before/after tonemapping) appropriately
- Implement effect using Scene Texture nodes
- Examples: outline shader, screen distortion, custom color grading, stylized effect 

I created a post-processing material to add a dynamic visual effect across the screen. I began by creating a colored tint and running it through a Lerp node that masked the red values, then blended it using a Blend Overlay with a Chroma Key Alpha. I further lerped this with a desaturation node, which initially produced a disco-like visual effect. To enhance motion and texture, I connected the setup to a Panner, which controlled the normal map texture and its desaturation, allowing me to adjust the scrolling speed in both the X and Y directions. I then combined all these effects through additional lerps and connected the result to the Emissive Color output, giving the effect a glowing, animated quality.
![alt text](image-12.png)
 Finally, I added a Post Process Volume in the level and used a material array to link the post-processing material to it. Once active in the scene, the system produced a vibrant rainbow grain effect that animated smoothly across the screen. 

![ ](image-7.png)
final product 