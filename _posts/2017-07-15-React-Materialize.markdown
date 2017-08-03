---
layout: post
title:  "Materialize Modals in React"
date:   2017-07-15 15:30:04 -0400
categories: Materialize Modals in React
---

I've grown fond of a front end library developed by Google called `Materialize`. The interface is simple, clean, and aesthetically beautiful -- kind of like an Apple Store. However, I've learned it doesn't always play nice with certain front end frameworks, namely `React.js`. That's what inspired this blog post and how to implement a cool feature called `Modals`. It adds some pizazz to the user experience with minimal amounts of additional code. 

The gif here demonstrates how it works with the documentation and sample code from `Materialize`'s website.

![materialize_modals](https://rweber87.github.io/log-a-blog/assets/post7/materialize_modals.gif)

 The user simply clicks on what's called the 'trigger' to get the `Modal` to work. This is all well and good when you're not using `React.js` for your application given it's all written in `HTML`. Here's the documentation for `React-Materialize` implementation.

![react_materialize_modals](https://rweber87.github.io/log-a-blog/assets/post7/react_materialize_modals.gif)

The documentation illustrates how to write your specific component that is the modal, but isn't explicit in how the trigger is added for the user to interact with. 

Here is an application I've built that uses `Modals` for an items view page. Each item displayed on that home page is a separate component, and the `Modal` itself is a separate component, too! 

![temparental_modals](https://rweber87.github.io/log-a-blog/assets/post7/temparental_modal.gif)

The code for the `Modal` looks like this (for space purposes I've only copied the return of the `ProductShow` component):

```javascript
return(
    <Modal
      header={product.name}
      trigger={
        <Link to={'#!'}><img alt='' src={product.image_url} className='image modal-content image-product' /></Link>
    }>
  <div key={product.id} className="card horizontal center rellax">
          <div id='img' className="card-image">
            <img alt=''  src={product.image_url} className='image modal-content' />
          </div>
          <div className="card-content half-container">
            <span>Category: {product.category}</span>
            <p>Description: {product.description}</p>
            <p>Cost Per Day: ${product.cost_to_rent}.00</p>
          {button}
        </div>
          <div id='reviews' className='card-content half-container parallax-container'>
            <span>Customer Reviews:</span>
            <ul className='reviews'>
              {reviews}
            </ul>
          </div>
      </div>
</Modal>
  )
```

You can see the `Modal` has a header that displays the products name from a property that was passed into it and also has a trigger. This trigger is what actually displays to the user prior to the `Modal` popping up. I've imported `Link` from `react-router-dom` and made the image on the `Product` component the trigger that the user selects in order to engage with the `Modal`. 

In order for that `Modal` to be available for the user to select we simply insert that `component` in place of the `image tag` in the `Product` component on the home page like so: 

```javascript
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
```

We've added the `ProductShow` component in place of the `image tag` which then sets the `Modal` for the user to interact with. 

Through working with `Materialize` and `React` they don't always play nice together, and the documentation isn't very explicit IMO. The fun part about working with them is figuring it out on the fly and sharing that knowledge with the community. I hope this blog post helps someone out there to make their application pizazzier (is that even a word?).

Questions or comments? Feel free to shoot me an email (click the link below).

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->