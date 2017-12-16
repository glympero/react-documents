## Local Storage

Just a set of key-value pairs. Local storage only works with string elements.

- to save use : localStorage.setItem('name', 'George');

- to fetch use : localStorage.getItem('name');

- to remove use : localStorage.removeItem('name');

- to delete everything : localStorage.clear() 

To save arrays and numbers etc - convert to JSON

### JSON

- JSON.stringify will take a javascript object and return the string representation

- JSON.parse will take the string representation and return a true javascript object

example:  const george = JSON.stringify({ name: 'George', age: 40 });

const res = JSON.parse(george);

res.name returns 'George'
res.age returns '40'
