## Flexbox

A more efficient way to layout, align, distribute space among
items in a container, even if their size is unknown.

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

Container Properties     Flex Item Properties
--------------------     --------------------
flex-direction            order
justify-content           flex
flex-wrap                 flex-grow
align-items               flex-shrink
align-content             align-self

### first step

.container {
  display: flex;
}

the container becomes a flex container

Everything inside a flex container (some divs for example),
is called flex item.

There are two axis (main axis and cross axis) which can be manipulated
