# code review
Code review of a very basic mandelbrot shader explorer built in unity and embedded in a basicazz webpage run in React 

[Explore Mandelbrot Fractal Shader Here](https://f05unt.csb.app/)

#### mandelbrot code snippet from mandelbrot.hlsl ####
```
fixed4 frag(v2f i) : SV_Target
            {
                // mandelbrot fractal algorithm  
                // Z = Z^2 + C
                
                // start position of pixel, initialized to coordinate of pixel we're focused on 
                // C represents the complex numbers in Z = Z^2 + C :) 
                float2 C = _Area.xy + (i.uv - 0.5) * _Area.zw; 
                
                C = rotate(C, _Area.xy, _Angle);
                
                // current pos of pixel (updates)
               
                float2 z;

                for (float i = 0; i < 255; i++) {

                    // update pixel position based on previous pixel position 
                    // ((z.x^2 * z.y^2),    (2(z.x) * z.y)) + Start position
                    //  (updated_x     ,  updated_y ) + C
                    // Z^2 + C 
                    
                    z = float2(z.x * z.x - z.y * z.y, 2 * z.x * z.y) + C; // Z = Z_SQ

                    // breakout of loop
                    if (length(z) > 2) break;
                }

                float4 result = sin(float4(0.15f, 0.08f, 25, 1) * i/20);
                return result;
            }
 ```
 ### context & explanation ### 
 
 ![click to see image of ](https://i.imgur.com/aG6VW5t.png)
 
 As you can see there is a canvas in a 3D space in the main scene. The canvas has a raw image UI element attached to it. That raw image element has our mandelbrot shader attatched to it. 
 
 
 #### what is a shader? #### 
 
 - A shader is a set of instructions for rendering graphics that are applied to every pixel on the screen at the same time, depending on the pixels position. These instructions are run through the GPU. 

- There are a lot of types of shaders, but I am using an Image Effect shader which contains the functions for a *vertex shader* and a *fragment shader*
 
* Vertex Shader - 
        - transform the shape of the object via triangle points (vertices) 
        - this is the v2f vert() function (the v2f(vertex to fragment) struct           is defined earlier in my code


* Fragment Shader - 
         - change the appearance of the pixels
         - this is the fixed4 frag(v2f i) function, which clearly is taking              in an argument *i* of the type 'vertex to fragment' (referencing              vertex to fragment shader data transfer) 



 ************ ************ ************
 
#### mandelbrot equation ####
 
 *Z = Z^2 + C*
 
 *C* - constant; complex number; a coordinate within 2 units of original origin 
 
 *Z* - also a complex number, but not a constant. 
 
 ************ ************ ************
 
 The code snippet above is the core of this mandelbrot explorer, since without it we have no mandelbrot to explore. 
 It's a fragment shader, so it's essentially going through potential pixels based on this iterative function we have and deciding how to color each one. It's run thru the GPU which is very nice and fast ;)
 
 This is my first project using shaders, they're super fun if you enjoy visualizing numbers.
 
 This is an Image Effect shader written in Open GL Shading Language (GLSL) rendered in Unity. 
 
 The movement (ability to use WASD keys to navigate the fractal) is written in a C# script. 
 
 
 ### Technologies Used ### 
 
 - Unity game engine
 - hlsl shader (high level shading language)

#### Further Info & Links ####

[what is hlsl?](https://openglbook.com/chapter-0-preface-what-is-opengl.html)

[what are glsl shaders? MDN reference](https://developer.mozilla.org/en-US/docs/Games/Techniques/3D_on_the_web/GLSL_Shaders)

[vertex shader](https://www.pcmag.com/encyclopedia/term/vertex-shader)


 
