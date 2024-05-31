 
# 3D Computer Graphics assignment ([Lab4](https://hackmd.io/@leon890820/r1ceTQ5Dj)): Zbuffering and Shading
### Work requirements:
1. There are many test data in the forder and many input commands in each test data. Please read the files and complete the following instructions. <br> `lab4D.in` is big data test. It will very slow when you run on windows. Thus, I recommend that you run it on the Linux.
1. I only use the function of drawing *points* in OpenGL (other functions such as line drawing cannot be used).
1. Eigen or other outer libaries cannot be used.
2. 
## Environment
`Linux distribution`: `Ubuntu 22.04`<br>
About how to build the enviroment on linux: [here](https://hackmd.io/3xPNjv6kRh2Ml6Ll7Nlw4A).

## Operating instructions
* ### Read the file:
    Read file with command line `name + lab4X.in`.

* ### Head:
    The instruction is `Width Height`<br>
    In the head of the files will give 2 integrals that represent the windows' width and height respectively.

* ### Comment:
    The instruction is `# ......`<br>
    If `#` appears, skip the line. (i.e. You don't need to execute the line which `#` appears.) 

* ### Reset:
    The instruction is `reset`<br>
    Reset the transformation matrix.

* ### Translate:
    The instruction is `translate x y z`<br>
    `x` means moving along x-axis by `x` unit.<br>
    `y` means moving along y-axis by `y` unit.<br>
    `z` means moving along z-axis by `z` unit.

* ### Scale:
    The instruction is `scale x y z`<br>
    `x` means scaling along x-axis by `x` unit.<br>
    `y` means scaling along y-axis by `y` unit.<br>
    `z` means scaling along z-axis by `z` unit.

* ### Rotate:
    The instruction is `rotate x y z`<br>
    `x` means rotating along x-axis by `x` degree.<br>
    `y` means rotating along y-axis by `y` degree.<br>
    `z` means rotating along z-axis by `z` degree.<br>
    **The rotating part should be implement in the order of y-axis -> z-axis -> x-axis.**

* ### Clear data:
    The instruction is `clearData` or `cleardata`<br>
    Clear the objects that you read from .obj file.

* ### Clear screen:
    The instruction is `clearScreen`<br>
    Clear the screen.

* ### Observe:
    The instruction is `observe epx epy epz COIx COIy COIz Tilt Hither Yon Hav`<br>

    Set the camera's parameter:<br>
    1. `epx epy epz` are the `x y z` position of the camera.<br>
    2. `COIx COIy COIz` are the point that the camera look at.<br>

    ```
    forward = COI - ep
    ```
    3. `Tilt` is the angle that the camera tilt.<br>
    4. `Hither Yon` are the `near` plane position and `far` plane position.<br>
    5. `Hav` is field of view.<br>

By i ~ iii, I can get View matrix. By iv ~ v, I can get Projection matrix.
* ### Viewport:
    The instruction is `view vxl vxr vyb vyt`<br>
    Since the perspective divide, all graphic will lies in `[-1, 1] X [-1, 1]`.<br>
    `-1 1 -1 1` means the left, right, botton, top boundary after perspective divide.<br>
    `vxl vxr vyb vyt` means the left, right, botton, top boundary of viewport after perspective divide.<br>

    In math words <br>

        f(-1, 1) = (0, Width)
        f(-1, 1) = (0, Height)
where it is a linear transformation.<br>
The objects outside the viewport boundary need to *clipped*.<br>
Need to display the graphic in `display`.

* ### Object:
    The instruction is `object **.obj Or Og Ob Kd Ks N`<br>
    `**.obj` means the name of the files. Please load the document into your code and also slice square into triangles.<br>
    `Or Og Ob` are the color of the object, using the color space `RGB`.<br>
    `Kd` is the parameter diffuse.<br>
    `Ks` is the parameter specular.<br>
    `N` is gloss.

* ### Display:
    The instruction is `display`<br>
    Do the `clearScreen` when display is occured.<br>
    Use `flat shading` to rendering.<br>
    Add `fgetc(stdin);` when display.


* ### Background:
    The instruction is `background Br Bg Bd`<br>
    `Br Bg Bd` are the background color.

* ### Ambient:
    The instruction is `ambient KIr KIg KIb`<br>
    `KIr KIg KIb` are the parameter of ambient light. 

* ### Light
    The instruction is `light index Ipr Ipg Ipb Ix Iy Iz`<br>
    `index` is the light of number `index`.<br>
    `Ipr Ipg Ipb` are the color of light.<br>
    `Ix Iy Iz` are the position of the light.<br>
    **Both use point lights.**

* ### End:
    The instruction is `end`<br>
    Destory the window.

* ### Bonus function: (haven't finish yet)
    Use the `blinn phong` to calculte the direction light.<br>
    Use the `Gourand Shading` to rendering.

## Libraries
* ### C++
```
#include <GL/glut.h>
#include <GL/gl.h>
#include <cmath>
#include <cstdlib>
#include <cstdio>
#include <vector>
#include <fstream>
#include <string>
#include <iostream>
```

* ### freeGLUT
```
glutInit(int *&argcp, char **argv);
glutInitWindowSize(int width, int height);
glutInitWindowPosition(int x, int y);
glutInitDisplayMode(unsigned int mode);
glutSwapBuffers(void);
glutMainLoop();
glutCreateWindow(char *name);
glutDisplayFunc(void (*func)(void));
gluOrtho2D(GLdouble left, GLdouble right, GLdouble top, GLdouble bottom);
glClear(GLbitfield mask);
glPointSize(GLfloat size);
glColor3f(GLfloat red, GLfloat green, GLfloat blue);
glBegin(GLenum mode);
glVertex2i(GLint x, GLint y);
glEnd(void);
```
