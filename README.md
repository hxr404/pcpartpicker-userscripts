# pcpartpicker-userscripts
Some Userscripts for pcpartpicker.com I created


## Custom Filtering
Filter the results of the current page by the value of a certain column.

```js
/*
let column = 6; //replace 6 with the number of the column
let max_limit = 20; //replace 20 with the maximum limit
let min_limit = 0; //replace 0 wuth the minimum limit
*/

console.log('Script made by (c) hxr404.'); //Removal of this copyright Notice is punishable by international copyright laws.

document.querySelector('.md-col-12').insertAdjacentHTML('beforeend', '<section id="customfilters" class="module-subTitle"><div class="subTitle"><div class="subTitle__header"><h2>Custom Filters</h2></div></div></section>')



function customfilter(column, min_limit, max_limit) {
  let tdspecid = column - 1; //pcpartpicker has two counting schemes for the column: the column id ()data-column) and the spec id. The name of the product, which is a column, is not counted as a spec and doesn't have a spec id, therfore the spec id is one less than the column id. The spec id can e.g. be found in the class name of the spec's cell.
  let title = document.querySelector('th[data-column="'+column+'"]').innerText;
  let unit = document.querySelector('.td__spec.td__spec--'+tdspecid+':not(.td--empty)').innerText.replace(/[^a-zA-z]+/g,'');
  
  console.log('Filtering by ' + title + '...');
  document.querySelectorAll('.td__spec.td__spec--'+tdspecid).forEach(element => {
   if (parseFloat(element.innerText) > max_limit || parseFloat(element.innerText) < min_limit || (min_limit > 0 && element.classList.contains('td--empty'))) {
     element.parentElement.remove();
     document.querySelector('h2.pp-filter-count').innerHTML = parseInt(document.querySelector('h2.pp-filter-count').innerHTML) - 1 + ' Compatible Products';
    }
  });
  
 
  let min;
  let max;
  if (unit != "") {
    min = min_limit + ' ' + unit;
    max = max_limit + ' ' + unit;
  } else {
    min = min_limit;
    max = max_limit;
  }
 
  let uisliderleft = '33.1415'; //px
  let uisliderright = '150.142'; //px
  let uisliderrange = 20.5882; //%
  let uisliderhandle_r = uisliderrange; //%
  let uisliderhandle_l  = '79.4118'; //%

  let filterdiv = '<div class="group group--filter" id="filterdiv_CUSTOM"><h3 class="group__title group__title--trigger js-trigger-filter">' + title + '<span class="collapse-toggle"></span></h3><div id="filter_slide_CUSTOM" class="filter_slider--wrapper group__content"><div class="obj-filter-labelbox ui-slider-horizontal-labelbox">&nbsp;<div class="obj-filter-slide-left ui-slider-horizontal-labelbox-label labelbox-label--left" style="left: ' + uisliderleft + 'px;"><a href="#">' + min + '</a><div class="labelbox-input labelbox-input--left"><input type="text" size="4" class="left ui-slider-horizontal-editbox"> ' + unit + '</div></div><div class="obj-filter-slide-right ui-slider-horizontal-labelbox-label labelbox-label--right" style="left: ' + uisliderright + 'px;"><a href="#">' + max + '</a><div class="labelbox-input labelbox-input--right"><input type="text" size="4" class="right ui-slider-horizontal-editbox"> ' + unit + '</div></div></div><div class="obj-filter-dualslide ui-slider ui-corner-all ui-slider-horizontal ui-widget ui-widget-content"><div class="ui-slider-range ui-corner-all ui-widget-header" style="left: ' + uisliderrange + '%; width: ' + 100 - uisliderrange + '%;"></div><span tabindex="0" class="ui-slider-handle ui-corner-all ui-state-default" style="left: ' + uisliderhandle_r + '%;"></span><span tabindex="0" class="ui-slider-handle ui-corner-all ui-state-default" style="left: ' + uisliderhandle_l + '%;"></span></div></div></div>';
  
  document.querySelector('div.offCanvas:nth-child(2) > div:nth-child(2)').insertAdjacentHTML('beforeend', filterdiv)

  console.log('Custom Filter successfully applied. This Feature is brought to you by (c) hxr404.');
}
```
