# pcpartpicker-userscripts
Some Userscripts for pcpartpicker.com I created


## Custom Filtering
Filter the results of the current page by the value of a certain column.

```js
let column = 6; //replace 6 with the number of the column
let max_limit = 20; //replace 20 with the maximum limit
let min_limit = 0; //replace 0 wuth the minimum limit

console.log('Script made by (c) hxr404');
console.log('Filtering by ' + document.querySelector('th[data-column="'+column+'"]').innerText + '...');
tdspecid = column - 1; //pcpartpicker has two counting schemes for the column: the column id ()data-column) and the spec id. The name of the product, which is a column, is not counted as a spec and doesn't have a spec id, therfore the spec id is one less than the column id. The spec id can e.g. be found in the class name of the spec's cell.

document.querySelectorAll('.td__spec.td__spec--'+tdspecid).forEach(element => {
  if (parseFloat(element.innerText) > max_limit || parseFloat(element.innerText) < min_limit) {
    element.parentElement.remove();
    document.querySelector('h2.pp-filter-count').innerHTML = parseInt(document.querySelector('h2.pp-filter-count').innerHTML) - 1 + ' Compatible Products';
  }
});
```
