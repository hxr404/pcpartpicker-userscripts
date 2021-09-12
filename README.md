# pcpartpicker-userscripts
Some Userscripts for pcpartpicker.com I created


## Custom Filtering
Filter the results by the value of a certain column.

replace >= with the operator which should be used for filtering..
note that the script only removes the first matching table row
```js
let column = 5; //replace 5 with the number of the column
let limit = 20; //replace 20 with the limit

if (parseFloat(document.getElementsByClassName('td__spec td__spec--'+column)[0].innerText) >= limit) {
  document.getElementsByClassName('td__spec td__spec--5'+column)[0].parentElement.remove();
  document.querySelector('h2.pp-filter-count').innerHTML = parseInt(document.querySelector('h2.pp-filter-count').innerHTML) - 1 + ' Compatible Products'
}
```
