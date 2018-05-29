## Background
Small fish have a habit of gathering into very large groups. They do this for a Multitude of benefits, one of them being that as a group each individual member has a higher chance of surviving an attack from a predator.

The fish do not do this as a conscious cooperation but instead each fish acts independently and only cares for its own survival. This independent form of accidental cooperation is a behavior best simulated with boids. 

Boids are simulated actors that when in masses are able to achieve complex results but where each individual actor is independent with a relatively simple artificial intelligence.

## Problem Description
Create a boid simulation of schooling fish and predator fish. When a predator fish moves through a school each individual fish in its proximity avoid it without intersecting other fishes. How well can an individual fish in a school avoid a predator in a computer simulation?


## Technical Description

A set number of boid fishes are spawned at the beginning of a simulation. Each schooling boid fish follows a set of 4 rules.

- Attempts to keep a reasonable distance from other fish to not collide.
- In the proximity of another fish or school tries to move towards the average position of the school.
- Each fish in a school attempts to keep the same direction and speed of the school.
- Each fish attempts to keep a safe distance from a predator actor.


A predator actor exist in the simulation. The predator actor follows the mouse pointer and its speed can be increased or decreased. If the predator intersects with a fish it displays this by setting the fish it intersected with to some new color.

The simulation is to be in real time from a 2D top-down perspective with actor fishes being different colored shapes to differentiate schooling fish from fish in a school from predator fish.


## Sample code

You can use the [editor on GitHub](https://github.com/gupett/CG-Project/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/gupett/CG-Project/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
