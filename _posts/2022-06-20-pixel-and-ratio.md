---
title: site
author: Minjeong Kim
date: 2022-06-20 15:50:00 +0800
categories: [Frontend]
tags: [frontend]
math: true
mermaid: true
---

# Frontend - Resolution, pixel, monitor, etc.

## How is responsive design different from adaptive design?
How is responsive design different from adaptive design?
Both responsive and adaptive design attempt to optimize the user experience across different devices, adjusting for different viewport sizes, resolutions, usage contexts, control mechanisms, and so on.

Responsive design works on the principle of flexibility - a single fluid website that can look good on any device. Responsive websites use media queries, flexible grids, and responsive images to create a user experience that flexes and changes based on a multitude of factors. Like a single ball growing or shrinking to fit through several different hoops.

Adaptive design is more like the modern definition of progressive enhancement. Instead of one flexible design, adaptive design detects the device and other features and then provides the appropriate feature and layout based on a predefined set of viewport sizes and other characteristics. The site detects the type of device used and delivers the pre-set layout for that device. Instead of a single ball going through several different-sized hoops, you'd have several different balls to use depending on the hoop size.

Both have these methods have some issues that need to be weighed:

Responsive design can be quite challenging, as you're essentially using a single albeit responsive layout to fit all situations. How to set the media query breakpoints is one such challenge. Do you use standardized breakpoint values? Or, do you use breakpoints that make sense to your particular layout? What if that layout changes?
Adaptive design generally requires user agent sniffing, or DPI detection, etc., all of which can prove unreliable.

**References**

https://developer.mozilla.org/en-US/docs/Archive/Apps/Design/UI_layout_basics/Responsive_design_versus_adaptive_design

http://mediumwell.com/responsive-adaptive-mobile/

https://css-tricks.com/the-difference-between-responsive-and-adaptive-design/

## Have you ever worked with retina graphics? If so, when and what techniques did you use?

Retina is just a marketing term to refer to high resolution screens with a pixel ratio bigger than 1. The key thing to know is that using a pixel ratio means these displays are emulating a lower resolution screen in order to show elements with the same size. Nowadays we consider all mobile devices retina defacto displays.

Browsers by default render DOM elements according to the device resolution, except for images.

In order to have crisp, good-looking graphics that make the best of retina displays we need to use high resolution images whenever possible. However using always the highest resolution images will have an impact on performance as more bytes will need to be sent over the wire.

To overcome this problem, we can use responsive images, as specified in HTML5. It requires making available different resolution files of the same image to the browser and let it decide which image is best, using the html attribute srcset and optionally sizes, for instance:

```html
<div responsive-background-image>
  <img
    src="/images/test-1600.jpg"
    sizes="
      (min-width: 768px) 50vw,
      (min-width: 1024px) 66vw,
      100vw"
    srcset="
      /images/test-400.jpg   400w,
      /images/test-800.jpg   800w,
      /images/test-1200.jpg 1200w
    "
  />
</div>
```

It is important to note that browsers which don't support HTML5's srcset (i.e. IE11) will ignore it and use src instead. If we really need to support IE11 and we want to provide this feature for performance reasons, we can use a JavaScript polyfill, e.g. Picturefill (link in the references).

For icons, I would also opt to use SVGs and icon fonts where possible, as they render very crisply regardless of resolution.

**References**   
https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/

http://scottjehl.github.io/picturefill/

https://aclaes.com/responsive-background-images-with-srcset-and-sizes/

## Do You Really Understand the Viewport
If you are a web developer, you must have heard about viewport, and the below line may seem familiar to you.
```html
<meta name=”viewport” content=”width=device-width, initial-scale=1" />
```
But do you really understand what this line of code actually does?

The formal definition of a viewport is —
**“The viewport defines the area of the screen that the browser can render the content to.”**

The definition is a bit tricky to understand, so let me give you some examples.

If the width of the browser window is 768px, the width of the viewport is also 768px. If I expand the browser window to 1024px, the viewport size also changes to 1024px.

Well, that seems quite simple, but not all the displays have the same pixel density. Suppose your device has a resolution of 2048 × 1080 pixels and you make the browser window to full width, it is not necessary that viewport width will be 2048 pixels.


Like my mobile device has a resolution of 1080 x 2340 pixels but my viewport size is 360 x 648 pixels.

**So why is that?**

Instead of reporting the width in the number of physical hardware pixels, the browser reports the width in the number of dips or device-independent pixels.

`DIP` is a unit of measurement, that relates pixels to a real distance. The idea being that a device-independent pixel will take up the same amount of space on a display regardless of the pixel density of the display.

If the hardware pixels are twice the pixels reported by browser (device-independent pixels) then the device has a Device Pixel Ratio or DPR of 2.
![image](https://cdn.hackernoon.com/photos/wclau8ggsOfv266UKLUzA9OB18o2-p59h3yec)
The example image above has a DPR of 2.


The 700 DIPs get scaled up to 1400 hardware pixels when the page is rendered on the display.

What will happen if you don't define a meta viewport tag in your HTML code that is supposed to be viewed on small screens also?

Unless you tell the browser that your website was designed to work on a small screen, it assumes that they weren't. And renders the page, as if it were on a screen that was 980 DIPs wide.

Now, imagine that content being scaled to fit on a device that's only 360 DIPs wide. It gets scaled to less than half.

By adding the meta viewport tag to the head element of the page we tell the browser that we know what we are doing. By setting the “width=device-width” in meta viewport tag we instruct the page to match the screen width in device-independent pixels. This allows the page to reflow content to match the screen sizes, whether rendered on a small, medium or large screen

**Reference**   
https://hackernoon.com/do-you-really-understand-the-viewport-lv663ye4