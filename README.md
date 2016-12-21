# Aphrodite-breakpoint
A tool for writing style and media query more efficiently with Aphrodite

## Feature
Standalone breakpoint definition can be used to convert into the styles Aphrodite need.

## install
`npm install aphrodite-breakpoint`

## Notice
- The def param in your style is required.

- The media name in your styles and breakpoints definition should be the same.

- The alias param's value is a abbreviation for writing the media name convinent, it use as param name in `creatStyle` function's return. So that I can write this way :  `css(dt.box)`  not  `css(desktop.box)`.

- Ensure writing param 'media' and 'alias' both in your breakpoints if you use alias.

## Usage 


#### 1. Defined your breakpoint

```javascript
//breakpoints.js
export default {
    
    mobile : '@media (max-width: 600px)',
    
    desktop : {media:'@media (min-width: 601px) and (max-width: 1200px)', alias:'dt'}
    
}
```

#### 2. Design your styles

```javascript
//styles.js
export default {
  def: {
      box: {
          color: 'grey',
      }
  },
  mobile: {
      box: {
          color: 'red',
      }
  },
  desktop : {
      box: {
          color: 'blue',
      }
  }
}
```

#### 3. Import in
```javascript
//App.js
import React, { Component } from 'react'
import {creatStyle, css} from 'aphrodite-breakpoint'
import breakpoints from './breakpoints'
import styles from './styles'

class App extends Component{

  render() {
 
    let {def,mobile,dt} = creatStyle(styles, breakpoints)

    return (
      <div className={css(def.box,mobile.box,dt.box)}>
          I am a box
      </div>
    )
  }
}
```

## API
```javascript
/**
 * @description 
 * The convert function.
 * @param @required {object} the style definition
 * @param @required {object} the breakpoint definition
 * @return {object} the converted styles, the param is alias in breakpoints if you use it.
 */
 creatStyle(styles, breakpoints)
 
 /**
 * @description 
 * The css function, it's aphrodite origin function actually.
 * @param @required {object} the same as aphrodite 
 * @return {object} the converted styles by aphrodite
 */
 css(...)
```
