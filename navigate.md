# Navigate

Navigate allows us to redirect to a route programmatically.

## Register the plugin

Navigate plugin needs to be registerd in a module before we can use it.

Here's an example on how to register this plugin:

```javascript
import { Module, Navigate } from 'maf.js';

const module = new Module({
    ...
});

module.plugin(Navigate);
...
```

## Programmatically navitate

Here's an example on how to naviagate to a route programmatically:

```javascript
<template>
    ...
</template>

export default class SampleComponent {
    btnClick() {
        ...
        this.$naviagate('/route/path');
    }
}
```

## Navigate parameters

Navigate has three parameters, first is the url, second is the state and third is the title.
The second and third parameters are optional.

For more information on url, state and title please follow this link at [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState).
