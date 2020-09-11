# Component

Components are the most basic building block of an application.
It is composed of view and logic of a component and in the future a scoped style will be added.
It is recommended for components to have a single responsibility to make it maintainable and more reusable.

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

Here is an example on how to bind a property from the logic into an attribute of view:

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

Hooks are functions that lets you run a block of codes when your component triggers a lifecycle event.

Below are the available lifecycle hooks:

| Hooks                 | |
| ---                   | --- |
| $onInit               | Triggers right after the component constructor is called. Props and plugins are already available in this hook. |
| $onViewInit           | Triggers when the component's view building process starts. |
| $afterViewInit        | Triggers after the component's view building process is done. |
| $afterInit            | Triggers after the initialization process of a component is completed. |
| $onDestroy            | Triggers when the component's destruction process starts. |
| $afterDestroy         | Triggers after the component's destruction process is done. |
| $onPropsUpdated       | Triggers when props is changed from the parent component. |
| $onChange             | Triggers when component's change detection starts. |
| $afterChange          | Triggers when component's change detection is done. |

## Conditional rendering

Conditional rendering is used to conditionally render an element in the dom.
It uses the `view:if` directive which removes an element from the dom if the value is a falsy and append the element if otherwise.

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
## Custom Directives

Custom directive let's us create our own directive that can be used inside our views.
Directives are classes that inherits the `Directive` class of vermillion framework.

#### Create a directive

Here's an example on how to create a custom directive:

```javascript
// ./Color.directive.js
import { Directive } from 'vermillion';

export default class Color extends Directive {
    constructor(props) {
        super(props); // super with props argument is required in a constructor
    }

    $onInit() {
        this.changeColor();
    }

    $onPropsUpdated() {
        this.changeColor();
    }

    changeColor() {
        this.element.style.color = this.$props.color;
    }
}
```

The sample code above is a directive to change the text color of an element.

?> **Note**: if constructor is called, a `super` call expression with `props` argument is require.

#### Register a directive

Directive needs to be registered in the module before we can use it.

Here's an example on how to register a directive:

```javascript
import { Module } from 'vermillion';
import Color from './Color.directive';

const module = new Module({
    ...
});

module.directive(Color, {});
```

The `directive` method in module accepts two arguments.
First is the directive itself and second is an optional argument which is a data for the directive.
The data is accessible inside the constructor for the directive.

Here's an example on how to access the data inside the directive:

```javascript
export default class Color extends Directive {
    constructor(props) {
        super(props);
        this.directiveData = props.data.module._directivesData.color;
    }
}
```

#### Using the directive

Custom directive uses the namespace `directive:` or `d:` in view followed by the class name of the directive with the first letter in lower case.

Example: `SampleDirective` will be called as `d:sampleDirective`.


Here's an example on how to use the `Color` directive created above:

```javascript
<template>
    <div>
        <h1 d:color={this.color}>Change My Color</h1>
        <button on:click={this.changeColor}>Change Color<button>
    </div>
</template>

export default class App {
    constructor() {
        this.color = {
            color: 'green'
        };
    }

    changeColor() {
        this.color = {
            color: 'red'
        };
    }
}
```

## View content

View content let's us display content from the parent component into the child component's view.

Here's an example on how to use view content:

#### Parent component

```javascript
// ./Parent.js
import Child from './Child';

<template>
    <div>
        <Child>
            <h1>I am the view content.</h1>
        </Child>
    </div>
</template>

export default class Parent {}
```

#### Child component

```javascript
// ./Child.js

<template>
    <view-content></view-content>
</template>

export default class Child {}
```
In the example above,
the `<h1>I am the view content.</h1>` element which is inside the `<Child>...</Child>`
component tags will be displayed in the child component's view where the `<view-content></view-content>` tag is located.



















