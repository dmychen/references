# React  

Learning how to use the basics of React.  

`export default`  

`index.js` Bridge between components in `App.js`and the web browser.  

`import { library } from 'source'` Imports libraries.  

> `import { StrictMode } from 'react'`  
> import { createRoot } from 'react-dom/client';  

### JSX

In React, rendering logic and markup both live inside components. Most often, React is used in combination with **JSX** in order to achieve this. A  **jsx element** is a combination of javascript code and html tags.  

When returning from a functino in JSX, we must return a single root html element. This is because the HTML in JSX is transformed into a plain Javascript object under the hood, and we can only return one object from a function. 
Often we wrap JSX tags in a `<div> </div>` tag if we need to return multiple tags together. We can also use `<> </>`, which is a [fragment](https://react.dev/reference/react/Fragment).  

In JSX, most HTML and SVG attributes are written in camelCase which correspond to [DOM properties](https://developer.mozilla.org/en-US/docs/Web/API/Element/className). Here is a [list of common props](https://react.dev/reference/react-dom/components/common).

### Rendering Lists

We use [javascript array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) to manipulate arrays of data.  

We can filter and transform our arrays of data into an array of components using React's `map()` and `filter()`.  

`map()` maps an array to corresponding react components.  

`filter()` Takes a list and filters out what we don't want.  

We need to give each item a **key**, which uniquely identified it within that array. A key could be an ID from whatever database is storing the data, or for local data it could be an incrementing counter like `crypto.randomUUIID()`. Keys must not change, don't generate them while rendering.  

	originalList = [{
		id: 0,
		value: 'something',
		somethingElse: 'idk'
	}, {
		id: 1,
		value: 'not the same',
		somethingElse: 'boo!'
	}]
	
	
	const newList = originalList.filter(item => 
		item.value === 'something'
	);
	
    const componentList = newList.map(item => 
   	<li key={list.id}>
		<p> 
		How we want the data in item to be transformed into a component.
		</p>
		<button> Remove {item.value} </button>
	</li>
	);

If we want each item to render into several different DOM nodes, we need to group everything into a single `<div>` or [explicit fragment](https://react.dev/reference/react/Fragment#rendering-a-list-of-fragments) `<Fragment>`.  


