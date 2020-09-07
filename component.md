# Component

Components are the most basic building block of an application.
It is composed of view and logic of a component and in the future a scoped style will be added.
It is recommended for components to have a single responsibility to make it mentainable and more reusable.

## Structure

Component is composed of view and logic.
Inside the `<template></template>` tag is the view of the component.
The template tag must have a single child only or it will throw an error.

Under the template tags is the component logic.
Here we can find the methods that manipulates the view and the state of the component.

```javascript
<template>
    ... // Template
</template>

export default class SampleComponent {
    ... // Logic
}
```

## Data binding

Data binding is a way to synchronize the data from logic to view and vise versa.

#### Attribute binding

Here is an exmple on how to bind a property from the logic into an attribute of view:

```javascript
<template>
    <h1 id={this.id}></h1>
</template>

export default class SampleComponent {
    constructor() {
        this.id = 'sample-id';
    }
}
```

#### Model binding

Model binding is a two way binding of data.
Every time the model is changed from the view, the model in logic will be updated and the same thing will happen when the model is updated from the logic.

```javascript
<template>
    <input view:model={this.sampleModel} type="text" />
</template>

export default class SampleComponent {
    constructor() {
        this.sampleModel = '';
    }
}
```

## Event binding

#### Event binding

Event binding is a way to attach an event into an element.

Here's an example on how to attach a click event to a button:

```javascript
<template>
    <button on:click={this.clickMe}>Click Me</button>
</template>

export default class SampleComponent {
    clickMe() {
        console.log('I was clicked');
    }
}
```

Here is a list of available events from [w3schools.com](https://www.w3schools.com/jsref/dom_obj_event.asp).

## Hooks

Hooks are functions that lets you run a block of codes when your component triggers a lifecyle event.

Below are the available lifecyle hooks:

| Hooks                 | |
| ---                   | --- |
| $onInit               | Triggers right after the component constructor is called. Props and plugins are already available in this hook. |
| $onViewInit           | Triggers when the component's view building process starts. |
| $afterViewInit        | Triggers after the component's view building process is done. |
| $afterInit            | Triggers after the initialization process of a component is completed. |
| $onDestroy            | Triggers when the component's destruction process starts. |
| $afterDestroy         | Triggers after the component's destruction process is done. |
| $onPropsUpdated       | Triggers when props is changed from the parent component. |
| $onChange             | Triggers when component's change detection is triggered. |

## Conditional rendering

Conditional rendering is used to conditionally render an element in the dom.
It uses the `view:if` directtive which removes an element from the dom if the value is a falsy and append the element if otherwise.

Here's an example on how to use conditional rendering:

```javascript
<template>
    <h1 view:if={this.toggle}></h1>
</template>

export default class SampleComponent {
    constructor() {
        this.toggle = true;
    }
}
```

## List Rendering

List rendering uses `view:for` directive and it allows us to render a list of element based on the given array of data.

Here's an example on how to use list rendering:

```javascript
<template>
    <p view:for={this.array}>Hello World!</p>
</template>

export default class SampleComponent {
    constructor() {
        this.array = [1, 2, 3];
    }
}
```

#### List item name

List item uses `view:for-item` directive.
It allows the developer to set the variable name of the list item and display it in view.
If no list item directive is provided it is `$item` by default.

Here's an example on how to use list item directive:

```javascript
<template>
    <p view:for={this.array} view:for-item="listItem">{listItem}</p>
</template>

export default class SampleComponent {
    constructor() {
        this.array = ['foo', 'bar', 'bazz'];
    }
}
```

The example code above will generate list of element that looks like the following.

```html
<p>foo</p>
<p>bar</p>
<p>bazz</p>
```

#### List index

List index uses `view:for-index` directive.
It allows the developer to set the variable name of the list index.
If no list index directive is provided it is `$index` by default.

```javascript
<template>
    <p view:for={this.array} view:for-index="listIndex">{listIndex}</p>
</template>

export default class SampleComponent {
    constructor() {
        this.array = ['foo', 'bar', 'bazz'];
    }
}
```

The example code above will generate list of element that looks like the following.

```html
<p>0</p>
<p>1</p>
<p>2</p>
```

## Child Component

Child component is a component rendered inside a component.

Here's an example on how to render a component:

```javascript
import ChildComponent from './ChildComponent';

<template>
    <div>
        <ChildComponent />
    </div>
</template>

export default class SampleComponent { }
```

?> **Note**: component name must start with a capital letter.

## Props

Props are properties passed down from the parent component to child component.

Here's an example on how to pass a property from parent to child component:

##### Parent component
```javascript
// ./SampleComponent.js
import ChildComponent from './ChildComponent';

<template>
    <ChildComponent sampleProps={this.number} />
</template>

export default class SampleComponent {
    constructor() {
        this.number = 123;
    }
}
```

##### Child component
```javascript
// ./ChildComponent.js
<template>
    <h1>Child Component</h1>
</template>

export default class ChildComponent {
    constructor() {
        console.log(this.$props.sampleProps); // 123
    }
}
```
