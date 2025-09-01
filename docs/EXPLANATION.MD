# TOA (Time Of Arrival)


### Description:
- This code is able to triangulate the position from a source of waves with:
    1. The coordinates of at least **3** waves receptors.
    1. The **exact time** in that each receptor catches the wave.
    1. The velocity of the wave.



### How does it work?

\begin{quote}
\textbf{WARNING}: What's below is purely algebraic, symbolyc. It's not very hard, but if you don't have the level, it might be confusing. Nevertheless you are not required to understand the plenty of it in order to understand the code, or how to use the tool. I will try to explain it the simpliest as possible.
\end{quote}


1. We take some wave receptor as a reference in time. Lets call it $t_1$ for receptor $1$ $\cdots$ $t_i$ for receptor $i$.
1. Then we calculate the difference of time between each receptor, taking receptor 1 as a reference:
    $$\Delta t_1 = t_1 - t_1 = 0$$
    $$\Delta t_2 = t_1 - t_2$$
    $$\vdots$$
    $$\Delta t_i = t_1 - t_i$$


    \begin{quote}
    \textbf{\textit{NOTE}}:  It doesn't care if $\Delta t < 0$. Beacuse $\Delta t$ is a variation in time, so **it can be** negative, that only means that the event reached one receptor before the one that is used as a reference.
    \end{quote}
    
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
        
        \begin{center}
        \begin{tabular}{ccl}
        \multicolumn{1}{c|}{Receptor} & \multicolumn{1}{c|}{Coordinates} & \multicolumn{1}{c}{Time} \\ \hline
        A & $(x_A, y_A$) & $t_A$ \\ \hline
        B & $(x_B, y_B)$ & $t_B$ \\ \hline
        C & $(x_B, y_B)$ & $t_C$ \\ \hline
        \end{tabular}
        \end{center}

    And the velocity of the wave is $v$

    2. We calculate the $\Delta t$ for every receptor, taking the receptor A as an arbitrary point of reference in time.
        $$\Delta t_A = t_A - t_A = 0$$
        $$\Delta t_B = t_A - t_B$$
        $$\Delta t_C = t_A - t_C$$

    3. We calculate the distance from every receptor to the epicentre using $d = v \cdot \Delta t$:
        $$d_A = v \cdot \Delta t_A = v \cdot 0 = 0$$
        $$d_B = v \cdot \Delta t_B$$
        $$d_C = v \cdot \Delta t_C$$
    4. We use the formula of the circle for every receptor:
        $$\left( A \right)\qquad(x_e - x_A)^2 + (y_e - y_A)^2 = d_A^2$$
        $$\left( B \right)\qquad(x_e - x_B)^2 + (y_e - y_B)^2 = d_B^2$$
        $$\left( C \right)\qquad(x_e - x_C)^2 + (y_e - y_C)^2 = d_C^2$$

    5. And now we have a equation system with 2 unknowns and three equations so it can be resolved.
        
        
        \begin{quote}
        \textbf{\textit{NOTE}}: In a real case, with numbers, you will have $x_i$, $y_i$ and $d_i$ ($i$ for any receptor). And only 2 unknowns $x_e$ and $y_e$.
        \end{quote}
        
        1. We subtract $\left( B \right) - \left( A \right)$ beacuse later when we will develop the remarkable indentities it would be easier:
            $$(x_e - x_B)^2 + (y_e - y_B)^2 - (x_e - x_A)^2 - (y_e - y_A)^2 = d_B^2 - d_A^2$$
            $$(x_e - x_B)^2 - (x_e - x_A)^2 + (y_e - y_B)^2 - (y_e - y_A)^2 = d_B^2 - d_A^2$$
        2. Develop the remarkable identities:
            $$\cancel{x_e^2} - 2 x_e x_B + x_B^2 - \cancel{x_e^2} + 2 x_e x_A - x_A^2 + \cancel{y_e^2} - 2 y_e y_B + y_B^2 + \cancel{y_e^2} + 2 y_e y_A - y_A^2 = d_B^2 - d_A^2$$
        3. Simplification:
            $$2 x_e (x_A - x_B) + 2 y_e (y_A - y_B) + (x_B^2 - x_A^2 + y_B^2 - y_A^2) = d_B^2 - d_A^2$$
            $$2 x_e (x_A - x_B) + 2 y_e (y_A - y_B) = d_B^2 - d_A^2 - x_B^2 + x_A^2 - y_B^2 + y_A^2$$
        4. We subtract $\left( D \right) - \left( A \right)$ **The process is the same, so I'll put only the result**:
            $$2 x_e (x_A - x_D) + 2 y_e (y_A - y_D) = d_D^2 - d_A^2 - x_D^2 + x_A^2 - y_D^2 + y_A^2$$
        5. And now we have this eq. system:

            $$
            \left\{\begin{matrix}
             2 x_e (x_A - x_B) + 2 y_e (y_A - y_B) = d_B^2 - d_A^2 - x_B^2 + x_A^2 - y_B^2 + y_A^2 \qquad (1)
            \\ 2 x_e (x_A - x_D) + 2 y_e (y_A - y_D) = d_D^2 - d_A^2 - x_D^2 + x_A^2 - y_D^2 + y_A^2 \qquad (2)
            \end{matrix}\right.
            $$

            $$
            \left\{\begin{matrix}
             x_e (x_A - x_B) + y_e (y_A - y_B) = \frac{d_B^2 - d_A^2 - x_B^2 + x_A^2 - y_B^2 + y_A^2}{2} = R_{BA} \qquad (1)
            \\ x_e (x_A - x_D) + y_e (y_A - y_D) = \frac{d_D^2 - d_A^2 - x_D^2 + x_A^2 - y_D^2 + y_A^2}{2} = R_{DA} \qquad (2)
            \end{matrix}\right.
            $$
            
        6. So, now we can say this:
            $$x_A - x_B = a_1$$
            $$y_A - y_B = b_1$$

            $$x_A - x_D = a_2$$
            $$y_A - y_D = b_2$$
            
            Therefore the formulas will look like this:

            $$
            \left\{\begin{matrix}
            a_1 x_e + b_1 y_e = R_{BA} \qquad(1) \\
            a_2 x_e + b_2 y_e = R_{DA} \qquad(2)
            \end{matrix}\right.
            $$

        7. Now let's delete the $y_e$ form the equations by multiplying the Eq. $(1)$ by $b_2$ and the Eq. $(2)$ by $b_1$. The formulas will look like this:

            $$
            \left\{\begin{matrix}
            a_1 b_2 x_e + b_1 b_2 y_e = R_{BA} b_2 \qquad(1) \\
            a_2 b_1 x_e + b_2 b_1 y_e = R_{DA} b_1 \qquad(2)
            \end{matrix}\right.
            $$

        8. Now we subtract $(1) - (2)$.
            $$(a_1 b_2 - a_2 b_1) x_e + (b_1 b_2 - b_2 b_1) y_e = R_{BA} b_2 - R_{DA} b_1$$

            As yoy can see $(b_1 b_2 - b_2 b_1) y_e = 0$. So we are left with:
            $$(a_1 b_2 - a_2 b_1) x_e = R_{BA} b_2 - R_{DA} b_1$$

            9. Now we issolate $x_e$:
            $$x_e = \frac{R_{BA} b_2 - R_{DA} b_1}{a_1 b_2 - a_2 b_1}$$

            10. And is the same process for $y_e$:
            $$y_e = \frac{R_{BA} a_2 - R_{DA} a_1}{b_1 a_2 - b_2 a_1}$$

            11. **_Conclusion:_**
            $$x_e = \frac{R_{BA} b_2 - R_{DA} b_1}{a_1 b_2 - a_2 b_1}\qquad y_e = \frac{R_{BA} a_2 - R_{DA} a_1}{b_1 a_2 - b_2 a_1}$$


