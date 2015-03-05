---
layout: 	post
title:      "Fractal Dimension and Crossover Scale"
subtitle:   "What Do the Himalayas and the JFK Airport Have In Common?"
categories:	research
tags:		terrain fractal
mathjax:    true
---

Reading through [1] as a novice, a lot of the concepts discussed were completely new to me. I was doing what I normally do when reading something full of concepts I'm unfamiliar with. I kept on reading. Banking on the fact that I would soon get some context and could then go back and flush it all out. I placed fractal dimensions and crossover scales accordingly on the back burner until I got to the following passage: 

> It is interesting to note that experience indicates that modulation of crossover scale is more effective than modulation of fractal dimension for modelling realistic looking terrain. That changing crossover scale alone should have such a dramatic effect is not surprising, for as B. B. Mandelbrot has pointed out, the fractal dimension of the Himalayas is approximately the same as that of the runway at the JFK airport; what is true is simply that the crossover scale of the latter is on the order of millimeters while that of the former is on the order of kilometers. [1]

This was towards the end of a section about generating fractal height fields and is a response to some preliminary results gotten by modulating either the fractal dimension or crossover scale. For the uninitiated, let's start with some definitions. Crossover scale is explained well by this passage from earlier in [1]:

> A fractal surface changes in character depending on whether it is observed from nearby or from far away. From far away it appears flat or smooth (as the Earth seen from space). The transition from "nearby" to "far away" appearances occurs at the **crossover scale** which is the scale where vertical and horizontal displacements are equal. Thus, for a mountain range rising within one kilometer from sea level to peaks which are, one kilometer high, the **crossover scale** is one kilometer. [1] 

The fractal dimension is a little more difficult to explain. The first step is to understand what defines dimensionality. Any middle schooler (or at least high schooler) can tell you that a line is one-dimensional, a square is two-dimensional, and a cube is three-dimensional. A subset of those students would then be able to on to tell you why they think that is true. They'd either say that a line extends in one direction and a square extends in two (linearly independent) directions and so on or more simply that a line has a length, and square has a length and width, and a cube has a length, width, and height.

Though that definition is valid, there is another way of defining the dimension of an object, particularly self-similar objects. Take that original line. Divide it into four equal length segments. If you were to then magnify one of those segments by four you'd arrive back at the original line. This same principle can be applied to a simple curve on a plane and can be expanded to N segments with a magnification of N. Similarly, given a square divided into N^2 parts, the original square can be reproduced by magnifying one of the parts by N. And for a cube divided into N^3 pieces, the original cube can be reproduced by magnifying on the pieces by N. Therefore, knowing that a line is one-dimensional and so on, a general expression for the dimension of a self-similar object can be defined as [2]:

$$Dimension \equiv D = \frac{\log(N_{pieces})}{\log(N_{magnification})}$$

$$D_{line} = \frac{\log(N)}{\log(N)} = 1$$

$$D_{square} = \frac{\log(N^2)}{\log(N)} = 2$$

$$D_{cube} = \frac{\log(N^3)}{\log(N)} = 3$$

When applied to fractals, this concept is called **capacity dimension**. Take, for example, the Sierpinski Triangle, of which the first five iterations are shown below:

{% include figure.html content="![Sierpinski Triangle](/asset/image/post/sierpinski-triangle.png)" %}

On the left, corresponding to the first iteration, is a solid triangle. That triangle is then split into three smaller triangles which can be scaled by two to reproduce the original triangle. This pattern continues for each iteration. Therefore, the capacity dimension of this fractal is defined as:

$$ D_{Sierpinski\ Triangle} = \frac{\log(3)}{\log(2)} = \frac{\log(9)}{\log(4)} = \frac{\log(27)}{\log(8)} = \ldots \approx 1.585 $$

That puts it in a non-integer dimension that is close to 2-dimensional but not quite. That example was fairly simply. Another fractal, the Koch Snowflake, may offer a little more of a challenge. The image below shows the first four iterations of the fractal [3].

{% include figure.html content="![Kock Snowflake](/asset/image/post/koch-flake.png)" %}

It should first be noted that unlike Sierpinski Triangle, the bounded area of the Koch snowflake is not part of the object so in the first iteration, there are three line segments forming an equilateral triangle. Therefore, this object should be treated like a line. Take one of the sides of the triangle in the first iteration and see what happens to it in the second. It was replaced by four line segments but because of the new kink (the two middle segments) the magnification factor is only three. Therefore, the capacity dimension is as follows:

$$ D_{Koch\ Snowflake} = \frac{\log(4)}{\log(3)} \approx 1.262 $$

So the Kock Snowflake is close to being a line but is slightly more "complex". In the context of [1], Musgrave et al. are refering to capacity dimension when they say fractal dimension.

Now that we have definitions, what are they getting at with that first passage? Based on our understanding of capacity dimension, it can be intuited that a fractal height field will be more detailed than a plane but not to the point where it is a solid, meaning the capacity dimension for any fractal height field will be between 2 and 3 and, realistically, observable landscapes like the Himalayas or an airfield will be in a very narrow capacity dimension band, limited by natural phenomena. So why do mountains look like mountains? It's because the crossover scale. Simply put, the surface of smooth pavement varies on the sub-millimeter scale while a mountain may do vary on the kilometer scale. 

Musgrave et al. offer two figures that demonstrate the difference they are talking about pretty well. The first figure shows a landscape synthesized by modulating the crossover scale. 

{% include figure.html content="![Kock Snowflake](/asset/image/post/musgrave-plate4.png)" caption="Plate 4 [1]" %}

The second figure shows one synthesized by modulating the fractal dimension.

{% include figure.html content="![Kock Snowflake](/asset/image/post/musgrave-plate6.png)" caption="Plate 6 [1]" %}

Plate 4 looks fairly similar to a natural ridge while Plate 6 starts on the left looking like foothills and ends up on the right looking like a bunch of noise. There is a sweet spot for fractal dimension in which natural landscapes can be mimicked. 

{% capture refs %}
1. F. K. Musgrave, C. E. Kolb and R. S. Mace, "The synthesis and rendering of eroded fractal terrains," SIGGRAPH Comput. Graph., vol. 23, no. 3, pp. 41-50, 1989. 
2. R. L. Devaney, "Fractal Dimension," 2 April 1995. [Online]. Available: http://math.bu.edu/DYSYS/chaos-game/node6.html. [Accessed 5 March 2015].
3. Wxs, "Wikimedia Commons, Koch Flake," 6 April 2007. [Online]. Available: https://commons.wikimedia.org/wiki/File:KochFlake.svg. [Accessed 5 March 2015].
{% endcapture %}
 
{% include references.html content=refs %}