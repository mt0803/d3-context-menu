# d3-context-menu

This is a plugin for d3.js that allows you to easy use context-menus in your visualizations. It's 100% d3 based and done in the "d3 way", so you don't need to worry about including additional frameworks.

It's written to be very light weight and customizable. You can see it in action here:

http://plnkr.co/edit/hAx36JQhb0RsvVn7TomS?p=info

### Install with Bower

```
bower install d3-context-menu
```

### Basic usage:

```
// Define your menu
var menu = [
	{
		title: 'Item #1',
		action: function(elm, d, i) {
			console.log('Item #1 clicked!');
			console.log('The data for this circle is: ' + d);
		}
	},
	{
		title: 'Item #2',
		action: function(elm, d, i) {
			console.log('You have clicked the second item!');
			console.log('The data for this circle is: ' + d);
		}
	}
]

var data = [1, 2, 3];

var g = d3.select('body').append('svg')
	.attr('width', 200)
	.attr('height', 400)
	.append('g');

g.selectAll('circles')
	.data(data)
	.enter()
	.append('circle')
	.attr('r', 30)
	.attr('fill', 'steelblue')
	.attr('cx', function(d) {
		return 100;
	})
	.attr('cy', function(d) {
		return d * 100;
	})
	.on('contextmenu', d3.contextMenu(menu)); // attach menu to element
});
```

### Advanced usage:

More features may come in the future, but right now the only "advanced" feature is that you can pass in a callback that will be executed before the context menu appears. This can be useful if you need something to close tooltips or perform some other task before the menu appears:

```
    ...
    .on('contextmenu', d3.contextMenu(menu, function() {
    	console.log('Quick! Before the menu appears!');
    })); // attach menu to element

```