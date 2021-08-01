# CSS Secrets

My notes from the book CSS Secrets ✍️

## Table of Contents

- [Background and Borders](https://github.com/tigerabrodi/css-secrets#background-and-borders)

### Background and Borders

- **Translucent Borders:** Styling borders with `hsla` or `rgba` colors is possible (for example borders with lessened opacity). If you are using a background color, take into account that normally the `background-clip` is set to `border-box`, hence the background will extend underneath the border. In this case we have to set the `background-clip` to `padding-box`, in order to tell the browser to clip the background at the padding edge.

- **Multiple borders:** This can be achieved by using the `box-shadow` property (having multiple shadows), take into account though, that the shadows are on top of the other, hence you need to adjust the spread radius accordingly. If you only need two borders, it is better to use the `outline` property. That would give you more flexibility regarding the styling of the border. You can even use `outline-offset`, to determine how far away the outline should be from the border, it even accepts negative values.

- **Flexible Background positioning:** You can flexibly set the `background-position` by using [edge offsets](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position#syntax) values or using the `calc` function. `background-origin` also plays a factor when setting the background, because it tells the background from where to start.

- **Inner rounding:** We can with just one element have inner roundings and also have an outer border which is sharp. This can be achieved by using `border-radius` and `outline`. Though, you find that there is a tiny (white) space between the `outline` and `border-radius`, hence you need to use a tiny amount of `box-shadow` with the same color as the outline in order to elegantly accomplish this (the amount is something you need to experiment yourself to).

- **Striped Backgrounds:** Vertical and Horizontal stripes can be achieved by using `linear-gradient` in `background` and `background-size` in combination. Considering gradients are generated as background images, they can be treated as such and their sizes set via `background-size`. You need to set both the color and size of each value within the `linear-gradient` function. You can set the size to 0 of the last value, then its position will be adjusted by the browser to be equal to the position of the previous color stop. For vertical stripes you need to set the direction to `to right` or tilt the gradient by 90 degrees. This can also be done diagonally. It can easily be accomplished with `repeating-linear-gradient`. The [documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/repeating-linear-gradient()) for that is already great!

- **Complex background patterns:** More complex background patterns can be achieved as well. By having a background color in place using `background`, generating multiple gradients via `background-image`, and using other background properties such as `background-position` and `background-size`.

- **Continuous image borders:** You can also have images as borders, even when using just one element. This can be achieved by first setting a border that is transparent, and then the `background-origin` to `border-box`. You would also need two background images using `background`, the first one being either a color set via `linear-gradient` or the image you want, the second is the image which will be used as the border. Then using `background-clip`, clip the first image to the `padding-box`, and the second one to the `border-box`. 
