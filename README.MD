# TOA (Time Of Arrival)


### Description:
- This code is able to triangulate the position from a source of waves with:
    1. The coordinates of at least **3** waves receptors.
    1. The **exact time** in that each receptor catches the wave.
    1. The velocity of the wave.



### How does it work?

> **WARNING:** What's below is purely algebraic, symbolyc. It's not very hard, but if you don't have the level, it might be confusing. Nevertheless you are not required to understand the plenty of it in order to understand the code, or how to use the tool. I will try to explain it the simpliest as possible.

1. We take some wave receptor as a reference in time. Lets call it $t_1$ for receptor $1$ $\cdots$ $t_i$ for receptor $i$.
1. Then we calculate the difference of time between each receptor, taking receptor 1 as a reference:
    $$\Delta t_1 = t_1 - t_1 = 0$$
    $$\Delta t_2 = t_1 - t_2$$
    $$\vdots$$
    $$\Delta t_i = t_1 - t_i$$

    > **_NOTE:_**  It doesn't care if $\Delta t < 0$. Beacuse $\Delta t$ is a variation in time, so **it can be** negative, that only means that the event reached one receptor before the one that is used as a reference.

1. Let's calculate the distance from the epicentre to any receptor.  
    $$d = v \cdot \Delta t$$  

1. Now we use circles.
    The general formula for a circle is:  
    $$(x - x_1)^2 + (y - y_1)^2 = r^2 $$  
    We are going to say that $(r = d)$  
    Let's say the epicentre is $(x_e, y_e)$  
    Our formula will be like this for $i$ receptor:  
    $$(x_e - x_i)^2 + (y_e - y_i)^2 = d^2$$  

1. And with all of this. Here is the **symbolic solution**:  

    1. Let's declarate 3 receptors and the velocity of the wave:
        | receptor     | Coordinates        | Time      |
        |:-------------:|:---------------:|:-------------:|
        | A         |   $(x_a, y_a)$    |$t_A$|
        | B         |   $(x_b, y_b)$    |$t_B$|
        | C         |   $(x_c, y_c)$    |$t_C$|

    And the velocity of the wave is $v$  

    1. We calculate the $\Delta t$ for every receptor, taking the receptor A as an arbitrary point of reference in time.  
        $$\Delta t_A = t_A - t_A = 0$$  
        $$\Delta t_B = t_A - t_B$$  
        $$\Delta t_C = t_A - t_C$$  

    1. We calculate the distance from every receptor to the epicentre using $d = v \cdot \Delta t$:  
        $$d_A = v \cdot \Delta t_A = v \cdot 0 = 0$$  
        $$d_B = v \cdot \Delta t_B$$  
        $$d_C = v \cdot \Delta t_C$$  
    1. We use the formula of the circle for every receptor:  
        $$\left( A \right)\qquad(x_e - x_A)^2 + (y_e - y_A)^2 = d_A^2$$  
        $$\left( B \right)\qquad(x_e - x_B)^2 + (y_e - y_B)^2 = d_B^2$$  
        $$\left( C \right)\qquad(x_e - x_C)^2 + (y_e - y_C)^2 = d_C^2$$  
    1. And now we have a equation system with 2 unknowns and three equations so it can be resolved.
        > **_NOTE_** In a real case, with numbers, you will have $x_i$, $y_i$ and $d_i$ ($i$ for any receptor). And only 2 unknowns $x_e$ and $y_e$.
        1. We subtract $\left( B \right) - \left( A \right)$ beacuse later when we will develop the remarkable indentities it would be easier:
            $$(x_e - x_B)^2 + (y_e - y_B)^2 - (x_e - x_A)^2 - (y_e - y_A)^2 = d_B^2 - d_A^2$$  
            $$(x_e - x_B)^2 - (x_e - x_A)^2 + (y_e - y_B)^2 - (y_e - y_A)^2 = d_B^2 - d_A^2$$  
        1. Develop the remarkable identities:  
            $$\cancel{x_e^2} - 2 x_e x_B + x_B^2 - \cancel{x_e^2} + 2 x_e x_A - x_A^2 + \cancel{y_e^2} - 2 y_e y_B + y_B^2 + \cancel{y_e^2} + 2 y_e y_A - y_A^2 = d_B^2 - d_A^2$$  
        1. Simplification:  
            $$2 x_e (x_A - x_B) + 2 y_e (y_A - y_B) + (x_B^2 - x_A^2 + y_B^2 - y_A^2) = d_B^2 - d_A^2$$  
            $$2 x_e (x_A - x_B) + 2 y_e (y_A - y_B) = d_B^2 - d_A^2 - x_B^2 + x_A^2 - y_B^2 + y_A^2$$  
        1. We subtract $\left( D \right) - \left( A \right)$ **The process is the same, so I'll put only the reult**:  
            $$2 x_e (x_A - x_D) + 2 y_e (y_A - y_D) = d_D^2 - d_A^2 - x_D^2 + x_A^2 - y_D^2 + y_A^2$$  
        1. And now we have this eq. system:  

            ```math
            \left\{
            \begin{matrix}
            2 x_e (x_A - x_B) + 2 y_e (y_A - y_B) = d_B^2 - d_A^2 - x_B^2 + x_A^2 - y_B^2 + y_A^2 \quad (1) \\
            2 x_e (x_A - x_D) + 2 y_e (y_A - y_D) = d_D^2 - d_A^2 - x_D^2 + x_A^2 - y_D^2 + y_A^2 \quad (2)
            \end{matrix}
            \right.


            $$\left\{\begin{matrix}
                x_e (x_A - x_B) + y_e (y_A - y_B) = \frac{d_B^2 - d_A^2 - x_B^2 + x_A^2 - y_B^2 + y_A^2}{2} = R_{BA}\\ 
                x_e (x_A - x_D) + y_e (y_A - y_D) = \frac{d_D^2 - d_A^2 - x_D^2 + x_A^2 - y_D^2 + y_A^2}{2} = R_{DA}
            \end{matrix}\right.$$
            