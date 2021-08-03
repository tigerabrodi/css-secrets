# CSS Secrets 🥰 😘 💞

My notes from the book CSS Secrets ✍️

I take notes when I encounter something that is interesting, new or that I know will likely be useful multiple times in the future 😁 👏 🚀 📖

## Table of Contents

- [Background and Borders](https://github.com/tigerabrodi/css-secrets#background-and-borders)

- [Shapes](https://github.com/tigerabrodi/css-secrets#shapes)

- [Visual Effects](https://github.com/tigerabrodi/css-secrets#visual-effects)

- [Typography](https://github.com/tigerabrodi/css-secrets#typography)

- [User Experience](https://github.com/tigerabrodi/css-secrets#user-experience)

- [Transitions and Animations](https://github.com/tigerabrodi/css-secrets#transitions-and-animations)

### Background and Borders

- **Translucent Borders:** Styling borders with `hsla` or `rgba` colors is possible (for example borders with lessened opacity). If you are using a background color, take into account that normally the `background-clip` is set to `border-box`, hence the background will extend underneath the border. In this case we have to set the `background-clip` to `padding-box`, in order to tell the browser to clip the background at the padding edge.

- **Multiple borders:** This can be achieved by using the `box-shadow` property (having multiple shadows), take into account though, that the shadows are on top of the other, hence you need to adjust the spread radius accordingly. If you only need two borders, it is better to use the `outline` property. That would give you more flexibility regarding the styling of the border. You can even use `outline-offset`, to determine how far away the outline should be from the border, it even accepts negative values.

- **Flexible Background positioning:** You can flexibly set the `background-position` by using [edge offsets](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position#syntax) values or using the `calc` function. `background-origin` also plays a factor when setting the background, because it tells the background from where to start.

- **Inner rounding:** We can with just one element have inner roundings and also have an outer border which is sharp. This can be achieved by using `border-radius` and `outline`. Though, you find that there is a tiny (white) space between the `outline` and `border-radius`, hence you need to use a tiny amount of `box-shadow` with the same color as the outline in order to elegantly accomplish this (the amount is something you need to experiment yourself to).

- **Striped Backgrounds:** Vertical and Horizontal stripes can be achieved by using `linear-gradient` in `background` and `background-size` in combination. Considering gradients are generated as background images, they can be treated as such and their sizes set via `background-size`. You need to set both the color and size of each value within the `linear-gradient` function. You can set the size to 0 of the last value, then its position will be adjusted by the browser to be equal to the position of the previous color stop. For vertical stripes you need to set the direction to `to right` or tilt the gradient by 90 degrees. This can also be done diagonally. It can easily be accomplished with `repeating-linear-gradient`. The [documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/repeating-linear-gradient()) for that is already great!

- **Complex background patterns:** More complex background patterns can be achieved as well. By having a background color in place using `background`, generating multiple gradients via `background-image`, and using other background properties such as `background-position` and `background-size`.

- **Continuous image borders:** You can also have images as borders, even when using just one element. This can be achieved by first setting a border that is transparent, and then the `background-origin` to `border-box`. You would also need two background images using `background`, the first one being either a color set via `linear-gradient` or the image you want, the second is the image which will be used as the border. Then using `background-clip`, clip the first image to the `padding-box`, and the second one to the `border-box`.

### Shapes

- **Flexible ellipses:** `border-radius` doesn't just accept a fixed value, but also percentages. It also accepts horizontal and vertical radii, which you can define by using slash. You can also specify the radius for each corner of the border, by using a specified property such as `border-top-left-radius`, there you can also specify the horizontal and vertical radii, the first value would be the horizontal and the second one the vertical.

- **Parallelograms:** Creating parellelogram-like shapes is possible by using the `skew` function from `transform`. If may need to wrap the text in another element depending on your use-case, and skew it in the opposite direction, if you for example only want the background to be skewed. You can also use a pseudo element. Give the pseudo element a position of absolute and the parent a position of relative, lower the z-index and also set all of the direction values (top, left, right, bottom) to zero. Using a pseudo element is much more flexible, you don't need another element. It is also a useful technique for other scenarios.

- **Diamond images:** One solution here is to use `transform` and two elements, the image and its parent. On the parent, set `overflow: hidden`, give it a specified width and rotate it by 45 degrees. The image, rotate it in the opposite direction by 45 degrees, give it a `max-width: 100%;` and `scale(1.42)`. The other solution would be to simply use `clip-path`. We can achieve the same result as the first solution by simply applying: `clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);`. You can even apply cool animations using the same property if you wish to.

- **Cutout corners:** In order to achieve cutout corners, meaning, corners that have a different shape due to transparency, we can take advantage of `linear-gradient`. Gradients can accept an angle direction and color stop positions in absolute lengths, we can also specify the `background-position` due to using `background`.

An example:

```css
background: #58a;
background:
    linear-gradient(135deg, transparent 15px, #58a 0)
        top left,
    linear-gradient(-135deg, transparent 15px, #655 0)
        top right,
    linear-gradient(-45deg, transparent 15px, #58a 0)
        bottom right,
    linear-gradient(45deg, transparent 15px, #655 0)
        bottom left;
background-size: 50% 50%;
background-repeat: no-repeat;
```

Curved cutout corners can also be achieved by using radial gradients. An example:

```css
background: #58a;
background:
    radial-gradient(circle at top left,
             transparent 15px, #58a 0) top left,
    radial-gradient(circle at top right,
             transparent 15px, #58a 0) top right,
    radial-gradient(circle at bottom right,
             transparent 15px, #58a 0) bottom right,
    radial-gradient(circle at bottom left,
             transparent 15px, #58a 0) bottom left;
background-size: 50% 50%;
background-repeat: no-repeat;
```

We can also use `border-image` and inline an SVG that is already sliced.

```css
border: 20px solid transparent;
border-image: 1 url('data:image/svg+xml,\
    <svg xmlns="http://www.w3.org/2000/svg"\
         width="3" height="3" fill="%2358a">\
    <polygon points="0,1 1,0 2,0 3,1 3,2 2,3 1,3 0,2"/>\
    </svg>');
background: #58a;
background-clip: padding-box;
```

We can also just simply use `clip-path`.

### Visual Effects

- **One-sided shadows:** The fourth, lesser known value of `box-shadow` is the spread radius. The spread radius increases or (if negative) decreases the size of the shadow by the amount you specify. In order to have shadows at the opposite sides, you need to declare two shadows to accomplish that.

- **Irregular drop shadows:** The `filter` property of CSS exist with which you can create wonderful effects, and even through its drop shadow, give SVGs and other elements with complex shapes shadows.

- **Color tinting:** For color tinting effect you can use the `filter` property as well. The properties `background-blend-mode` and `mix-blend-mode` also exist to achieve the effect.

- **Frosted glass effect:** Blurring the background where the text is in order for the text to be more visible and achieve a classy effect. It is a bit tricky but can be achieved by using a pseudo element for the text as a background and blurring it out using `blur()`.

### Typography

- **Hyphenation:** This effect can be achieved by using `hyphens`, and setting its value to `hyphens: auto;`.

- **Inserting line breaks:** Line breaks can be achieved by using `<br>` or placing an after pseudo element of `content: "\A";`. In case you want white space to be preserved, to the pesudo element you can add `white-space: pre;`.

- **Zebra-striped text lines:** This effect can be achieved by using `linear-gradient`. Zebra-striped background color of the text.

An example:

```css
padding: .5em;
line-height: 1.5;
background: beige;
background-size: auto 3em;
background-origin: content-box;
background-image: linear-gradient(rgba(0,0,0,.2) 50%, 
                                      transparent 0);
```

- **Adjusting tab width:** The tab width can be adjusted by using `tab-size`.

- **Ligatures:** You can choose whether you want to turn the font ligatures on or off via the `font-variant-ligatures` property.

- **Realistic text effects:** There were some text effects in the book.

I found stroked text really interesting, as if the letters were to have an outline color.

An example:

```css
background: deeppink;
color: white;
text-shadow: 1px 1px black, -1px -1px black,
             1px -1px black, -1px 1px black;
```

Glowing effect is also a cool one on text. It can be achieved by using a couple of layered `text-shadow`s.

An example:

```css
background: #203;
color: #ffc;
text-shadow: 0 0 .1em, 0 0 .3em;
```

Extruded text is also a cool effect, makes the text look really 3D. Multiple layers of text shadows are used to accomplish this.

An example:

```css
background: #58a;
color: white;
text-shadow: 0 1px hsl(0,0%,85%),
             0 2px hsl(0,0%,80%),
             0 3px hsl(0,0%,75%),
             0 4px hsl(0,0%,70%),
             0 5px hsl(0,0%,65%),
             0 5px 10px black;
```

### User Experience

- **Picking the right cursor:** You can change the cursor using the `cursor` property.

- **Extending the clickable area:** You can extend the clickable area by using a pseudo element, which doesn't affect the styling at the original element at all. An example of a button that is 10 pixels larger in every direction:

```css
button::before {
    content: '';
    position: absolute;
    top: -10px; right: -10px;
    bottom: -10px; left: -10px;
}
```

### Transitions and Animations

- **Typing animation:** This actually boggled my mind, but a typing animation can actually be achieved using pure CSS, and no, it doesn't require millions of lines 😄.

The example:

```css
@keyframes typing {
    from { width: 0 }
}

@keyframes caret {
    50% { border-color: transparent; }
}

h1 {
    width: 15ch; /* Width of text */
    overflow: hidden;
    white-space: nowrap;
    border-right: .05em solid;
    animation: typing 6s steps(15),
               caret 1s steps(1) infinite;
}
```
