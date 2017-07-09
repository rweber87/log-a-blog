---
layout: post
title:  "React PropTypes"
date:   2017-06-30 15:30:04 -0400
categories: React PropTypes Libraries
---

Checking data types in React utilizing `propTypes` has been deprecated since version 15.5 and replaced with the `npm prop-types` library. To install this with your React app you can type the command `npm install --save prop-types`. This allows the developer to validate propTypes that are being passed through certain components, as well as validates the appropriate types are being received. 

To add the `propTypes` validations to a particular component it's the same as any other item from an `npm` library - utilize the ES6 syntax and add this line of code to the top of your file `import PropTypes from 'prop-types'`.

A few `propTypes` you can check being passed into a component are the basic primitive types such as `PropTypes.array, PropTypes.bool, PropTypes.func, PropTypes.number, PropTypes.object, PropTypes.string, PropTypes.symbol`.

```javascript
import React from 'react'
import ProductShow from './ProductShow'
import PropTypes from 'prop-types'

function Product(props) {
  let product = props.product
  return (
    <div id='product-card' key={product.id} className="card horizontal">
          <div id='img-product' className="card-image half-container">
            <div className="image-container">
              <ProductShow state={props.state} handleSubmit={props.handleSubmit} handleSelectBox={props.handleSelectBox} product={product} />
            </div>
          </div>
          <div id='card-content' className="right card-content half-container">
            <h5 className="card-title center">{product.name}</h5>
            <p className="center">Category: {product.category}</p>
            <p className="center">{product.description}</p>
          </div>
      </div>
  )
}

export default Product

Product.propTypes = {
  name: PropTypes.integer,
}
```

Above we have a component that's rendering a product object. We're checking if the `propType` *name* that's part of the object being passed to this component is an integer (it's actually a string). Here we'll get an error displayed on the browser's console that looks like this...

![error](https://rweber87.github.io/log-a-blog/assets/post6/error.png)

The `propType` name is invalid because it is in fact a string as opposed to the integer we're checking for. If we change the type we're checking to a string we'll notice the error disappear from the console because it does in fact match the validation.

PropTypes also offers plenty of other validations beyond just primitive types. You can validate if a property is an instance of a particular class, and even require specific elements. One last thing I'll demonstrate is requiring elements passed to properties. 

```javascript
import React from 'react'
import ProductShow from './ProductShow'
import PropTypes from 'prop-types'

function Product(props) {
  let product = props.product
  return (
    <div id='product-card' key={product.id} className="card horizontal">
          <div id='img-product' className="card-image half-container">
            <div className="image-container">
              <ProductShow state={props.state} handleSubmit={props.handleSubmit} handleSelectBox={props.handleSelectBox} product={product} />
            </div>
          </div>
          <div id='card-content' className="right card-content half-container">
            <h5 className="card-title center">{product.name}</h5>
            <p className="center">Category: {product.category}</p>
            <p className="center">{product.description}</p>
          </div>
      </div>
  )
}

export default Product

Product.propTypes = {
  users: PropTypes.object.isRequired
}
```

We've said that `users` should be required in the `Product` component for demonstration purposes. 'Users' is obviously something we're not passing to this component, so naturally we receive an error such as this. 

![error2](https://rweber87.github.io/log-a-blog/assets/post6/error2.png)

Once we fix our code to explicitly require a 'product' instead of 'user'...

```javascript
import React from 'react'
import ProductShow from './ProductShow'
import PropTypes from 'prop-types'

function Product(props) {
  let product = props.product
  return (
    <div id='product-card' key={product.id} className="card horizontal">
          <div id='img-product' className="card-image half-container">
            <div className="image-container">
              <ProductShow state={props.state} handleSubmit={props.handleSubmit} handleSelectBox={props.handleSelectBox} product={product} />
            </div>
          </div>
          <div id='card-content' className="right card-content half-container">
            <h5 className="card-title center">{product.name}</h5>
            <p className="center">Category: {product.category}</p>
            <p className="center">{product.description}</p>
          </div>
      </div>
  )
}

export default Product

Product.propTypes = {
  product: PropTypes.object.isRequired
}
```

...the error miraculously disappears. 

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->