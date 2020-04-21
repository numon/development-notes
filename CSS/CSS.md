- `border-radius:50%` - radius for component
- `box-sizing: border-box` - exactly the width we defined
- `text-rendering` - property in CSS allows you to choose quality of text over speed (or vice versa) allowing you to fine tune optimization by suggesting to the browser as to how it should render text on the screen
- `transform` - The transform property applies a 2D or 3D transformation to an element. This property allows you to rotate, scale, move, skew, etc., elements.
- `transform: translate(-50%, -50%)` - do center element
- `transition: width 2s, height 1s;` - allows you to change property values smoothly, over a given duration.
- `background-image: linear-gradient(rgba(0,0,0,0.8), rb)` - apply black effect
- `background-attachment: fixed` - fixed background image
- `vertical-align: middle;` -  property in CSS controls how elements set next to each other on a line are lined up.
- `text-align: center` - centered text



## Pseudo class
- `a::after { content: "→";}` - ::after creates a pseudo-element that is the last child of the selected element. It is often used to add cosmetic content to an element with the content property. It is inline by default.
- `:first-child :last-child` - select child from the list of nodes 
- `*:focus: {outline: none}` - remove focus border

## Media
<meta name="viewport" content="width=device-width, initial-scale=1">  - scaling web pages in mobile browsers

- `@media only screen and (max-width:480px) {}` - for mobile resolution
- `@media only screen and (max-width:767px) {}` - for small tablets resolution
- `@media only screen and (max-width:1023px) {}` - for small big tablets resolution
- `@media only screen and (max-width:1200px) {}` - web
