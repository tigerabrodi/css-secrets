# CSS Secrets

My notes from the book CSS Secrets ✍️

## Table of Contents

- [Background and Borders](https://github.com/tigerabrodi/css-secrets#background-and-borders)

- [Shapes](https://github.com/tigerabrodi/css-secrets#shapes)

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
