**React Documentation Style Guide**
-

<h3>Importance of Documentation :</h3>
Documentation will make information easily accessible, keep track of all aspects, help new users learn quickly.

<h4>Context:</h4>
Which Documentation to use for react application ?

<h4>Available options: </h4>
There are many different Documentation services available 

1. JsDoc
2. React-docgen
3. React-styleguidist
4. Docz
![Image](https://miro.medium.com/max/4796/1*Zb4LIvYGq0A_lslZI3pN2Q.png)


<h4>Considerations :</h4>

According to npm trends the most downloaded package in last 1 year **`React-docgen`**,
Which is made by *facebook* team.

`react-docgen` example from official website
```
import React, { Component } from 'react';
import PropTypes from 'prop-types';

/**
 * General component description.
 */
class MyComponent extends Component {
  render() {
    // ...
  }
}

MyComponent.propTypes = {
  /**
   * Description of prop "foo".
   */
  foo: PropTypes.number.isRequired,
  /**
   * Description of prop "bar" (a custom validation function).
   */
  bar: function(props, propName, componentName) {
    // ...
  },
  baz: PropTypes.oneOfType([PropTypes.number, PropTypes.string]),
};

MyComponent.defaultProps = {
  bar: 21,
};

export default MyComponent;

```
we are getting this output:
```
{
  "props": {
    "foo": {
      "type": {
        "name": "number"
      },
      "required": true,
      "description": "Description of prop \"foo\"."
    },
    "bar": {
      "type": {
        "name": "custom"
      },
      "required": false,
      "description": "Description of prop \"bar\" (a custom validation function).",
      "defaultValue": {
        "value": "21",
        "computed": false
      }
    },
    "baz": {
      "type": {
        "name": "union",
        "value": [
          {
            "name": "number"
          },
          {
            "name": "string"
          }
        ]
      },
      "required": false,
      "description": ""
    }
  },
  "description": "General component description."
}
```

After the process we will get JSON file. We need to take this json file and should render it with other packages to generate documentation site.

**So we are not considering `react-docgen`**

The second most downloaded package is **`jsdoc`**.

`jsdoc` is initial made for documenting vanilla javascript code. it will be little hard to document react project with jsdoc.
There is supporting package called `better-doc` which can be helpful for documenting react files with `jsdoc`

**We are not even considering `jsdoc` along with `better-docs` for documenting React project.**


The third most downloaded package is `react-stylegudist`.

`react-stylegudist` is complete document creator for react,  and it is made on top of react-docgen.

We use syntax of `/**   */` for document info , additionally we can also use `.md` file of the component for extra information 

```
import React from 'react'
import PropTypes from 'prop-types'

/**
 * General component description in JSDoc format. Markdown is *supported*.
 */
export default class Button extends React.Component {
  static propTypes = {
    /** Description of prop "foo". */
    foo: PropTypes.number,
    /** Description of prop "baz". */
    baz: PropTypes.oneOfType([PropTypes.number, PropTypes.string])
  }
  static defaultProps = {
    foo: 42
  }

  render() {
    /* ... */
  }
}

```

`.md` file as follows
```
 
React component example

```js
<Button size="large">Push Me</Button>
``


You can add a custom props to an example wrapper:

```js { "props": { "className": "checks" } }
<Button>I’m transparent!</Button>
``


Or add padding between examples in a block by passing the `padded` modifier:

```jsx static padded
<Button>Push Me</Button>
<Button>Click Me</Button>
<Button>Tap Me</Button>
``


Or disable an editor by passing a `noeditor` modifier:

```jsx noeditor
<Button>Push Me</Button>
``


To render an example as highlighted source code add a `static` modifier:

```jsx static
import React from 'react';
``


Examples with all other languages are rendered only as highlighted source code, not an actual component:

```html
<Button size="large">Push Me</Button>
``


Any [Markdown](http://daringfireball.net/projects/markdown/) is **allowed** _here_.

```

we have a `react-stlegudist` server running with command 
```
  npm run styleguidist
```
This will check for any error regarding documentation syntax and will serve at a port in localhost so we can see the generated documentation site 

After running the server command we need to run 
```
npm run stylegudist:build
```
Then it will generate a folder with documentation files called stylguidist in main project  


***Conclusion***

We will be using `react-styleguidist` for documenting react project .








