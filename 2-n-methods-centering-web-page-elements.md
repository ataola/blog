# N methods of centering web page elements

> Introduction: The center alignment of elements looks very harmonious and beautiful in many scenes. In addition, it is also a good point of investigation for the foundation of front-end development interviewers. Let's take a look at the author's thinking below.

## scene analysis

* An element, it may have a background, then I want its background to be centered
* An element, it may also have a parent element, then I want it to be centered on its parent element
* An element, which may also have some child content, I want to center the child content

## scene modeling

According to some assumptions put forward by the scenario analysis, we try to build corresponding models. The following are related models designed according to the above three scenarios.

* Center alignment of parent and child elements

![img](https://img2020.cnblogs.com/blog/2055171/202006/2055171-20200615082212222-349199370.png)

* Align the element background to the center

  ![img](https://img2020.cnblogs.com/blog/2055171/202006/2055171-20200615082226483-1696347594.png)

* Align the element content to the center

![img](https://img2020.cnblogs.com/blog/2055171/202006/2055171-20200615082241956-306194736.png)

## Scenario Realization

For the sake of unity, here we define a 400X400px parent container with a class name of .box with a black border and a pink body. It may have a 200X200px class name with a pardon body.box- subcontainer of son. Here, in order to make the effect intuitive and obvious, the author deliberately processed the original size of the background image to be smaller than the size of the host pixel. Alright, let's get started!

We do such a thing. In a div container, we introduce a background through the background-image attribute, and then we expect this imported background to be horizontally and vertically centered on the host element.

Here are two attributes background-repeat and background-position. If you are good at junior high school English, I think you should know it too. The literal meaning here is the meaning of this attribute. One is to set the background image how to pave the host element (full by default) to make it more beautiful, and the other is to set the position of the background image relative to the host element. You can pass pixels, percentages, and related direction words (top, bottom, left , right) to it. When it is a percentage, its calculation formula is as follows:

```
(container width - image width) * (position x%) = (x offset value)
(container height - image height) * (position y%) = (y offset value)
```

In short, the width and height of the host element minus the width and height of the image multiplied by the relevant percentage are relative to the origin of the upper left corner of the host element.

In the case that the background image does not repeat, you want to center an image on the host element, you can have background-postion: center center, background-postion: 50%, 50%, or it can be abbreviated as background-postion: center or background-postion: 50%

Therefore, under the above premise, we can roughly classify it into a category, which looks like:

```
/** 这里以复杂写法的百分比为例， 分别代表距离宿主元素左上角的x和y轴的距离**/
.box-son {
	background-repeat: no-repeat;
	background-position: 50%, 50%;
}
```

If the content of the host element is text, we expect it to be centered on the host element. Two attributes are used here, one is text-align and the other is line-height. text-algin:center can center the content horizontally on the host element, and set the line-height to the same height as the host element to vertically center the host element.

Related example link: https://ataola.github.io/show/zj/center-middle.html#example11

Let me explain here, the father is like the son, this is the name I castrated after condensing the sentence "the parent element is positioned relatively, and the child element is positioned absolutely". I will not repeat the introduction of this concept later.

Father and Son Absolutely + margin: auto
After the relative positioning of the parent element and the absolute positioning of the child element, set its top, right, bottom, and left to 0, and then we set its margin to auto. In this way, the space between the parent element and the child element will be evenly stretched by this margin.

```
.box-position {
    position: relative;
}

.box-example1 {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example1

Parent and child absolute + negative margin
After the parent element is relatively positioned and the child element is absolutely positioned, the child element is set to top: 50%; left: 50%;, where the percentage reference value is relative to the width and height of the parent element, and the reference point is the upper left corner of the parent element and the child element The upper left corner, so we need to correct it by subtracting half the width and height of the child element. This matter can be done by the margin of the child element.

```
.box-position {
    position: relative;
}

.box-example2 {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -100px;
    margin-top: -100px;
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example2

Father and son must + translation (translate)
On the basis of the example upstairs, in order to correct the offset of the child elements, we can actually use the translation property of css. The percentage of this translation is relative to its own width and height, so it is 50% in the opposite direction.

```
.box-position {
    position: relative;
}

.box-example3 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example3

Father-son double phase (not recommended, just for fun)

An immature approach, father and son are relatively positioned and can still be barely centered, let’s just calculate, there is not much value here so I won’t expand.

```
.box-position {
    position: relative;
}

.box-example4 {
    position: relative;
    top: 90px;
    left: 90px;
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example4

Father-son double phase + rem (not recommended, same as above)

Not of much value, skip it.

Related example link: https://ataola.github.io/show/zj/center-middle.html#example5

father and son must + calc
The css attribute calc can allow some calculations to be performed when declaring the value of the css attribute. Going back to our previous model of correcting the offset, it is easy to think that the top and left attributes of the sub-element are set to 50% minus half of the sub-element of such a model.

```
.box-position {
	position: relative;
}
.box-example6 {
    position: absolute;
    top: calc(50% - 100px);
    left: calc(50% - 100px);
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example6

old and new flex

Flex layout, but you will encounter it at the beginning of a serious point, because it is easy to use and very commonly used, here are two kinds, one is the new version of the flex layout, and the other is the old version of the flex layout

For flex layout, you can think of it as an axis, a fairly solid axis. On this axis, we want to put a box. There are many ways to put it. For details, you can search the tutorial of Mr. Ruan Yifeng I won't go into details here. An idea of simplification, this is what I learned from Qi Ruige, that is, we may not be able to remember so many attributes in many cases. We hope to do such a thing, which is to abstract it into an image. We can use specific directions to express our ideas. In short, it is encapsulated into a class library, and then use some down-to-earth class names to control the flex layout.

Interested children's shoes can take a look at a low-profile version of the css style library I implemented: https://ataola.github.io/show/box/assets/taolaui/flex.css

How to write the new version of flex
Without changing the axis direction, its parent element sets align-items: center; means vertical centering, and justify-content: center; means horizontal centering.

Parent element settings:

```
.flex {
    display: flex;
}

.flex-middle {
    align-items: center;
}

.flex-center {
    justify-content: center;
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example7

The way of writing the old version of flex
Here is just to mention that there is such an existence, readers should use the new version of writing.

```
.box-old {
    display: -webkit-box;
    -webkit-box-pack: center;
    -webkit-box-align: center;
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example8

table layout
The parent element is set to display: table, and the child element is set to display: table-cell. In the case of only one child element, it will fill the parent element as much as possible, and in the case of multiple child elements, it will be divided equally. Setting vertical-align: middle can make its content vertically centered.

Related example link: https://ataola.github.io/show/zj/center-middle.html#example9

grid layout
The flex layout we mentioned earlier is a one-dimensional axis layout, and the grid grid layout here is two-dimensional and flat. Set its parent element to display: grid, and then set the child element to align-self: center; to indicate vertical centering, and justify-self: center; to indicate horizontal centering.

```
.box-grid {
	display: grid;
}

.box-son-grid {
    align-self: center;
    justify-self: center;
}
```

Related example link: https://ataola.github.io/show/zj/center-middle.html#example10













