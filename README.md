# ShaderProject
 
 ### 1. Stylized Water Material with World Position Offset  
**Technical Requirements:**  
- Implement **World Position Offset (WPO)** to create animated wave motion
- Use time-based animation for continuous wave movement
- Include parameters for wave height, speed, and frequency
- Add visual elements: foam, depth fade, refraction, or transparency
- Demonstrate vertex animation without skeletal meshes

For this material, I started with creating the parameters for the water colour and the depth. This was so I could make the water a realistic colour and adjust the parameters of the colour being darker as depth was added to the material using a scattering depth parameter. 
![ ](image.png)

I then added WPO to the normal map of the water texture to be able to animate the wave movement and control the parameters for how fast/slow I wanted the waves to move.
![alt text](image-1.png)

 I then added in the foam to appear around the edges of the water when it touched the rocks surrounding it. This gives it more realism and emphasises the effects of the waves. 
 ![alt text](image-2.png)

 *End result*

 ![alt text](image-3.png)
 ![alt text](image-4.png)

**Guiding Questions:**
- How does WPO affect performance compared to animated meshes?

World Position Offset (WPO) runs in the vertex stage every frame. This is good for when simple maths is used i.e fewer waves and meshes arent really dense.  However, it becomes heavy when you stack wave octaves or use high density meshes. WPO is better to use for large bodies of water which is what I have used in my project since I’ve made a pool of water rather than adding in waterfalls. This makes the performance a lot cheaper and more flexible compared to animated meshes.  Animated meshes include skeletal and Vertex animation textures (VAT). Skeletal involves a high CPU and skinning cost and is more suitable for waterfalls/ smaller bodies of water. VAT reads baked motion on GPU and has a stable cost but adds texture bandwidth.These are usually used for materials which require more complex motions as they can be cleaner and more advanced than WPO. 

- How can you control wave direction and intensity?

I controlled wave direction and intensity by adding parameters to my material instance of the water material. I chose to add water tiling which when controlled it adjusts how stretched the material is to give a more controlled ripple effect of the normal material. Adjusting this changes how the ripples will look. I added wave speed to control how fast it moved, the faster the speed the more choppy look the waves give and I also added a parameter to adjust the intensity of them so they could appear more relaxed if needed. I added texture panning for both the x and y values so that the material would move both forward and backwards rather than just in one direction to make it look more realistic and have a better flow. 

![alt text](image-5.png)

- How does your water material respond to different lighting conditions?

When the directional light is adjusted using the time of day cycle I have made in my MPC, the water has highlights added on the waves where the light hits it during the dark and the foam still appears as white as well. The colour of the water goes really dark but when the light is set to during the day it goes back to normal as expected. 

![alt text](image-6.png)


