## Optimizations!

We got the grid based neighbor search working. With it and a reduced search radius for the fishes allowed us to increase the number of boids to 500 in real time rendering (with some lag when they all make a single dense school).

![](Images/500_boids.png?raw=true)

The **grid based neighbor search** works by placing and moving the boids around in a grid system and when a boid is to find neighbors it only search the grid spaces in a square around its proximity instead of all boids in the system.

The **octree neighbor search** might also be working but we are yet to test the latest fixes. We used [this](https://gamedevelopment.tutsplus.com/tutorials/quick-tip-use-quadtrees-to-detect-likely-collisions-in-2d-space--gamedev-374) Java quadtree guide by Steven Lambert when making our octree object. Octrees are essentially tree data structures where each node has 8 child nodes. The octree neighbor search works by making the whole environment into a box with at most 10 boids in it. When there are more than 10 boids in a box the box is split into eight smaller boxes where each should at most have 10 boids or else we split the splits again (10 is the number we use while testing). 

The octree makes us only check for neighbors in boxes within a proximity (where each box have a low amount of boids in it) instead of checking all boids in a system. Our implementation of updating the octree when boids move in the environment is sort of naive since we destroy the tree and recreate it every update (which is still faster than checking every boid in the system for many boids).

We were close to giving up on the octree search and went home for the day when we figured out what the fault was. Turns out **object != null** always returns false in C#. Well test it tomorrow. So far we've been finishing up what we have by gathering results and writing the report and will hopefully have everything finished by tomorrow.

## Video of simulation
Press the image below to see the video
[![IMAGE ALT TEXT HERE](Images/Sharks.png?raw=true)](https://youtu.be/UjNBJ39XNQA)


## Starts to look nice!

![](Images/Sharks.png?raw=true)

Today we added a shark boid to our implementation. The shark boid have similar behaviour as the fish boids, with the exception that they get drawn to the fish boids and the fish boids repel away from the sharks. The closer a shark is to a fish the greater it gets drawn to it and the reverse is true for a fish this force is added to the total force acting on the boid. 

After implementing the new forces we had to experimented for a while to find good parameters which looked realistic.
We found a free model online for the shark, the only problem with the shark model is that it has no animated movement so it looks quite stiff.

We have also been working on both a grid neighbor search and octree neighbor search but they are currently not working as expected so further work is needed.

## Done with a Basis

Turns out [the lab](https://www.kth.se/social/files/54cb7578f27654629532c3cc/boids.pdf) had pretty much everything in it already. Just running the provided lab code gave this:

![](Images/Initial.png?raw=true)

And doing the lab (added like 12 lines of code and some other very minor changes). We could go into detail of what exact changes we did but since this is a lab for a course we risk giving the answers to course participants. The result from the lab is working simple schooling behavior:

![](Images/first%20school.png?raw=true)

Instead of giving the answers to the lab we implemented we will explain how the boids work in this simulation.

Each boid in the system have a acceleration. The acceleration updates the boid's _velocity_ and _position_ each time step. This acceleration is updated every time step from 3 different **forces**:

1. **Separation Force** is the force keeping the fishes from colliding. Every fish within some small radius of a fish is pushed away.
2. **Alignment Force** is the force making fishes in a school move in a similar direction. The force makes the fish try to mimic the average velocity and direction of every fish within some sizeable radius.
3. **Cohesion Force** is a force acting to keep a school together. Within a school each fish slowly tries to move to its perceived center of the school (average position of fish within a sizeable radius).

These three forces are updated by each fish checking ALL other fishes in the system and separating its neighbors by if the fishes that are within the appropriate radius. Checking every fish in the system can be very wasteful and we intend to optimize this.

The next step is to optimize the calculations for increased the number of fishes and, of course, add a predator to the system. We also intend to make some fish behaviour changes to make the simulation look more pleasant. For instance right now once all fish are in one school they just aimlessly swim straight forward in constant speed unil they bounce off a wall.

## Starting the Project

We were advised to use a lab from the KTH course [Models and Simulation (DD1354)](https://www.kth.se/social/course/DD1354/) as a basis (you need a KTH login to see [the lab](https://www.kth.se/social/files/54cb7578f27654629532c3cc/boids.pdf)). Since our focus is on the boid simulation and not the graphics part we decided to use the lab to have neat visuals to work with. This will look much nicer than the project description version of shapes in different colors for fishes and predators.

Our intention right now is to recreate as much as necessary from the lab and then optimzie and add to it. The lab is essentially a finished working boid simulation with some blocks of code missing which we are to fill in.

## Initial Project Specification

### Background
Small fish have a habit of gathering into very large groups. They do this for a Multitude of benefits, one of them being that as a group each individual member has a higher chance of surviving an attack from a predator.

The fish do not do this as a conscious cooperation but instead each fish acts independently and only cares for its own survival. This independent form of accidental cooperation is a behavior best simulated with boids. 

Boids are simulated actors that when in masses are able to achieve complex results but where each individual actor is independent with a relatively simple artificial intelligence.

### Problem Description
Create a boid simulation of schooling fish and predator fish. When a predator fish moves through a school each individual fish in its proximity avoid it without intersecting other fishes. How well can an individual fish in a school avoid a predator in a computer simulation?


### Technical Description

A set number of boid fishes are spawned at the beginning of a simulation. Each schooling boid fish follows a set of 4 rules.

- Attempts to keep a reasonable distance from other fish to not collide.
- In the proximity of another fish or school tries to move towards the average position of the school.
- Each fish in a school attempts to keep the same direction and speed of the school.
- Each fish attempts to keep a safe distance from a predator actor.


A predator actor exist in the simulation. The predator actor follows the mouse pointer and its speed can be increased or decreased. If the predator intersects with a fish it displays this by setting the fish it intersected with to some new color.

The simulation is to be in real time from a 2D top-down perspective with actor fishes being different colored shapes to differentiate schooling fish from fish in a school from predator fish.

<!-- This is just help stuff when writing the blog. It will be removed once we no longer need it.
## Sample code 
-->
<!--
You can use the [editor on GitHub](https://github.com/gupett/CG-Project/edit/master/README.md) to maintain and preview the content for your website in Markdown files.
-->
<!--
Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.
-->
<!--
### Markdown
-->
<!--
Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for
-->
<!--
```markdown
Syntax highlighted code block
<!--
# Header 1
## Header 2
### Header 3
-->
<!--
- Bulleted
- List
-->
<!--
1. Numbered
2. List
-->
<!--
**Bold** and _Italic_ and `Code` text
-->
<!--
[Link](url) and ![Image](src)
```
-->
<!--
For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
-->
<!--
### Jekyll Themes
-->
<!--
Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/gupett/CG-Project/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.
-->
<!--
### Support or Contact
-->
<!--
Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
-->
