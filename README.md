# pcpartpicker-userscripts
Some Userscripts for pcpartpicker.com I created


## Custom Filtering
Filter the results by the value of a certain column.

replace 5 with the number of the column, replace 20 with the limit of your filter, replace >= with the operator which shouldbe used for filtering.
The script only removes the first matching table row, so I recommend putting it into a loop so that all rows gets filtered
```js
if (parseFloat(document.getElementsByClassName('td__spec td__spec--5')[0].innerText) >= 20) {
  document.getElementsByClassName('td__spec td__spec--5')[0].parentElement.remove();
}
```
