# Frontend Mentor - Product preview card component solution

This is a solution to the [Product preview card component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/product-preview-card-component-GO7UmttRfa). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
- [Author](#author)

## Overview

A responsive product card component

### The challenge

Users should be able to:

- View the optimal layout depending on their device's screen size
- See hover and focus states for interactive elements

### Screenshot

![](./screenshot-desktop.jpg)
![](./screenshot-mobile.jpg)

### Links

- Solution URL: [View Project](https://carson-haskell.github.io/product-preview-card/)

## My process

Referring to the Figma designs, I begin by creating a simple skeleton of the page with semantic HTML. Then, I create all the CSS variables to match Figma's design system, so that I am applying consistent styling. Finally, I begin styling in the following sequence: big (outer-most element) to small (inward-most element), left to right, top to bottom. By that, I mean I start with the outermost-element (the body), and then move inward (the card --> card content --> so forth), moving left to right, top to bottom.

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox

### What I learned

Dynamic images with the `<picture>` and `source` html tags. For example, in the code below, I am able to dynamically import images depending on the viewport width (mobile, desktop, default):

```html
<picture>
  <source
    media="(min-width: 768px)"
    srcset="images/image-product-desktop.jpg"
  />
  <source media="(max-width: 767px)" srcset="images/image-product-mobile.jpg" />
  <img src="images/image-product-mobile.jpg" alt="perfume" />
</picture>
```

Also, small random thing: the card component has a `border-radius`, but the image was covering the `border-radius` (because it's square, obv.). At first, I tried to apply `border-top-left` and `border-bottom-left` to the `img`, which worked fine, until I checked the mobile layout and realized the position of the image changes (in mobile, top-left and top-right need radius). I could have just used a media query to override `border-bottom-left` and set `border-top-right` instead, _but_, my spidey-senses were tingling and I knew there had to be a better way. This is 2024 afterall, we don't need to be that verbose with our CSS, right?

Sure enough, a quick google search revealed that all I needed to do was apply `overflow: hidden` to the card container, and _boom_ - just like that, the problem was solved.

So, this:

```css
picture img {
  /* ... */
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

@media (max-width: 768px) {
  /* ... */
  border-bottom-left-radius: none;
  border-top-right-radius: 10px;
}
```

became this:

```css
.card {
  /* ... */
  overflow: hidden;
}
```

Friends, the moral of the story is: _there's probably a better way to solve the problem than your initial solution_.

## Author

- Website - [Carson Haskell](https://portfolio-website-sandy-alpha-78.vercel.app/)
- Frontend Mentor - [@carson-haskell](https://www.frontendmentor.io/profile/carson-haskell)
