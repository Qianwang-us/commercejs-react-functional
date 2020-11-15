# 🛍️ 1: Build An E-Commerce App

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/7z6sdqivj25wexx4djym.png)

| **Project Goal**              | Build an e-commerce web store with a products listing and cart functionalities
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **What you’ll learn** | Setting up your React app, API basics, React components basics, fetch and display products data from an external API                                                      |
| **Tools you’ll need**         | A modern browser like Chrome to access [CodeSandbox](https://codesandbox.io) - be sure to create an account in CodeSandbox to keep the versions of your work intact. |
| **Time needed to complete**           | 1 hour                                                                                                                                                                 |
| **Just want to try the app?**        | [CodeSandbox link](https://evjno.csb.app/)   


The main objective here is to learn **React** fundamentals in conjunction with working with an **API** to build an e-commerce application! We're going to create a real-world app fetching data from an external API to list products in a product catalogue page as well as add cart functionalities! We're really excited so let's get right to it!

**Here is a summary of what we will achieve!**

- Go over React basics
- Create function components in React and use React hooks
- Fetch data from an external API data source called Chec
- Use an axios-based library, Commerce.js, to add eCommerce logic
- List products on a products catalogue page
- Add cart functionalities

Check out this [live demo](https://evjno.csb.app/) sneakpeek to have a look at what we're building today! 

### Prerequisites

**This project assumes you have some knowledge of the below concepts before starting:**

- Some basic knowledge of JavaScript fundamentals
- Some basic knowledge of JavaScript frameworks
- An idea of the JAMstack architecture and how APIs work

## Getting Started

We mentioned you needing **Code Sandbox** above, so what exactly is it? Codesandbox is an online IDE (Integrated Development Environment) playground that allows you to develop your project easily in the browser without having to set up your development environment.

So that's exactly what we're going to do: 
1. Head on over to [CodeSandbox](http://codesandbox.io) and create your account if you haven't already.
2. Create a CodeSandbox account
3. Scaffold a starter React template by clicking [here](https://codesandbox.io/s/new).

Choosing a React template in codesandbox or downloading it as a dependency is the same idea as installing [`create-react-app`](https://reactjs.org/docs/create-a-new-react-app.html) and getting a starting boilerplate of a single page application. You can read more about Create React App [here](https://github.com/facebook/create-react-app).


### Basic React App Structure:

In most cases when you scaffold a React project, a typical project structure would look like this.

- my-app/
  - README.md
  - node_modules/
  - package.json
  - public/
    - index.html
    - favicon.ico
  - src/
    - App.css
    - App.js
    - App.test.js
    - index.css
    - index.js
    - logo.svg

The `public` folder contains our assets, html static files and custom client side javascript files. `package.json` is used by npm (Node package manager) to save all the packages needed to deploy our app, but we don't have to worry about this because CodeSandbox installs and updates this file for us.

In our `public` folder, we have a standard html file called `index.html`. This is our point of entry file where we have our root element, which is named by convention. If you scroll down to line 30 in the body element, you will see `<div id="root"></div>`. This is the root element where we will be injecting our application.

The `src` folder contains all our React code and houses our `index.js`, `app.js` and later on our components when we start to create them. In `index.js`, you will see something like this:

```js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

const rootElement = document.getElementById("root");

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  rootElement
);
```

Here we import the React library and we use the ReactDOM `render()` method in order to print the contents of our App component into the root div in our `index.html` that we specified above. Our main app component `App.js` has to be imported as well to be included in the render.  The `App.js` component is passed in as the first argument in the render function and the `rootElement` as the second argument. That will tell React to render the app component and transform it into an element using the `React.createElement` method at build time to the index page. We will be stripping out all the scaffolded code in the component `App.js` and rebuilding it later on.

```js
import React from "react";
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <h2>Start editing to see some magic happen!</h2>
    </div>
  );
}
```

The App function in `App.js` represents a React function component. In React, components can be defined as class components or function components. We will get into explaining more about these components later in the tutorial. You can create your components as a individual files (Single File Component - SFC). In React, html-like tags which are what we call JSX can be passed in the return statement to be returned. The JSX inside the return function is what the `App.js` will render out. JSX stands for JavaScript XML and is a syntax extension to JavaScript that allows you to write markup inside a React component.

> 💡 **Tip** 

> What are **Components**?

> Components sections of your application that you extract out 
into separate files so that you can make them reusable. There are two types of components, functional components and class components. We will be using functional components in this application and will get into explaining more about functional components later in the guide.

Now that we've walked through the starting structure in a React application, this is where the real fun begins. As you know we will be building a real-world e-commerce application sourcing data from an API data source. In order to do that, we will need to install a package dependency. So let's get right to it!

## Install our commerce API

We will be using a commerce API platform to source our products data. The commerce backend we will be using is called [Chec](https://commercejs.com/) and it comes with the handy [Commerce.js](https://github.com/chec/commerce.js) SDK packed with helper functions to handle our commerce logic in the frontend seamlessly. 

> 💡 **Tip**

> What are **API**s and **SDK**s?

> **API** stands for Application Programming Interface and acts as a "contract" between client and server. The client which is a browser or any front-facing layer makes a request to a server to receive a response or initiate a defined action. When a platform has an API, it allows a software or front-facing client to interact with its data. **SDK** stands for Software Development Kit and is a installable package of development tools that typically comes with a library, a debugger, and other common tooling.

In a standard local development environment, the Chec/Commerce.js SDK can be installed in two ways:

1. Install the package via package manager either with npm `npm install @chec/commerce.js` or yarn `yarn @chec/commerce.js`

2. Install via CDN by included this script `<script type="text/javascript" src="https://cdn.chec.io/v2/commerce.js"></script>` in the `index.html` file.

Since we are using Codesandbox, we can conveniently add a dependency on the left sidebar. So let's go ahead and do that! Click on **Add dependency** and in the search field type in `@chec/commerce.js` and select the first option which is the latest version.

> 💡 **Tip**

> The Commerce.js SDK is using the axios library under the hood. Axios is a promise-based HTTP client that works both in the browser and in other node.js environments.


## Link up our Commerce instance

The Commerce.js SDK comes packed with all the frontend oriented functionality to get a customer-facing web-store up and running. In order to utilize all the features of this commerce platform's SDK, we are going to import the module into a folder called `lib` so that we can have access to our Commerce object instance throughout our application.

Let's go ahead and do that right now! In your `src` directory, we'll create a new folder called `lib`, create a file `commerce.js` and copy and paste the below code in it. Typically a lib folder in a project stores files that abstracts functions or some form of data.

```js
// src/lib/Commerce.js

import Commerce from '@chec/commerce.js';

export const commerce = new Commerce('pk_17695092cf047ebda22cd36e60e0acbe5021825e45cb7');
```

Ok so what have we done here? First we import in the Commerce.js module which we will be using to communicate with the API platform, then we export an instance of `Commerce` and pass in a public key. The public key is needed to give us access to data in the Chec API.

> 💡 **Tip

> Please note that for the purpose of getting you up and running with an account with products data, a public key is provided from a demo merchant account. A token key access is what gives the API an authentication scope. A public key will give us access to Chec's core API resources such as your products and cart data.

Now that we've installed our commerce SDK and created our Commerce instance, we now have access to the Commerce object throughout our application!

## Make your first request to fetch the products data

Commerce.js was built with all the frontend functionalities you would need to build a complete eCommerce store. All you need to do is make requests to various Chec API endpoints, receive successful responses, then you have your raw data to output beautifully onto your web store.

One of the main resources in Chec is the [Products](https://commercejs.com/docs/sdk/products) endpoint. Commerce.js
makes it seamless to fetch product data with its promise-based [method](https://commercejs.com/docs/sdk/products#list-products) `commerce.products.list()`. This request would make a call to the `GET v1/products` API endpoint and return a list of product data. Open up your `App.js` file and delete the code that came with creating a new React app and we will write this file from scratch.

Let's get to writing out our first functional component in `App.js`. Import `commerce` as well as a new module, `useState` which is the first React hook we'll be using to make our function component stateful. The first two API endpoint we will want to work with is the **Products** and **Merchant** endpoint. The **Products** endpoint will allow us to work with data such as the product name, product price, product description etc. The **Merchant** endpoint will contain information such as the e-commerce business name and contact details.

```js
// src/App.js
import React, { useState } from 'react';
import { commerce } from './lib/Commerce';

import './styles/scss/styles.scss'

const App = () => {
  const [merchant, setMerchant] = useState({});
  const [products, setProducts] = useState([]);

  return (
    <div className="app">
    </div>
  )
};

export default App;
```

After the opening of our `App` function, we need to destructure and return `products` and a method `setProducts` from the function `useState`. `useState` returns a tuple, which is an array with two items, in this case an initial value and a function that will update that value. The argument we will pass in to `useState` is the initial value of an empty array to be able to store the product data in it when we fetch the data. We follow the same pattern for the Merchant value, but instead we will pass in an empty object as an argument to `useState`.

> 💡 **Tip**

`useState` allows us to make function components stateful. This means that the components has the ability to keep track of changing data. You might ask why would be want to keep track of changing data. Any commerce store needs to have the ability to update its products listing in real-time. Be it new products being added, products being sold out, or products being taken off. The API data constantly will get updated, therefore the UI has to be reactive.

You can now make your first Commerce.js request! Create a function called `fetchProducts()` in the component and make a request to the products endpoint using the Commerce.js method `commerce.products.list()`.

```js
/**
 * Fetch products data from Chec and stores in the products data object.
 * https://commercejs.com/docs/sdk/products
 */
const fetchProducts = () => {
  commerce.products.list().then((products) => {
    setProducts(products.data);
  }).catch((error) => {
    console.log('There was an error fetch the merchant details', error)
  });
}
```

Inside the function, we use the `commerce` object to access the `products.list()` method for access to product data. [`commerce.products.list()`](https://commercejs.com/docs/sdk/products#list-products) is a
promise-based function call that will resolve the request and `then()` sets the response data with `setProducts` into
the `products` state key created earlier. In Chec, product is returned in an object called `data`, which is why we set the response as `product.data`. The `catch()` method catches any errors in the case that the request to the server fails.

Next function we will create is fetching the merchant details. So let's mirror the above `fetchProducts()` function:

```js
/**
 * Fetch merchant details
 * https://commercejs.com/docs/sdk/full-sdk-reference#merchants
 */
const fetchMerchantDetails = () => {
commerce.merchants.about().then((merchant) => {
    setMerchant(merchant);
}).catch((error) => {
    console.log('There was an error fetch the merchant details', error)
});
}
```

Of course simply creating the functions do not do anything as you have yet to call them. When the app
component mounts to the DOM, we will use our next React hook `useEffect()` to call the fetching of data. It is a React lifecycle hook also called side effect, that helps to call functions after the component first renders to the DOM and also anytime the DOM updates. Since we are loading data from a remote endpoint, we want to invoke the `fetchProducts()` function to update the state with the returned products so that we can render our updated data.

First import `useEffect` from React in our import statement at the very top `import React, { useState, useEffect } from 'react';`.

Then we can use the function like so:

```jsx
useEffect(() => {
    fetchMerchantDetails();
    fetchProducts();
}, []);
```

Above, we pass in our effect as a function `fetchProducts()` and also by leaving the second argument array empty, this method will run once before the initial render.

Below is the expected returned products data (abbreviated):

```json
[
  {
    "id": "prod_NqKE50BR4wdgBL",
    "created": 1594075580,
    "last_updated": 1599691862,
    "active": true,
    "permalink": "TSUTww",
    "name": "Kettle",
    "description": "<p>Black stove-top kettle</p>",
    "price": {
      "raw": 45.5,
      "formatted": "45.50",
      "formatted_with_symbol": "$45.50",
      "formatted_with_code": "45.50 USD"
    },
    "quantity": 0,
    "media": {
      "type": "image",
      "source": "https://cdn.chec.io/merchants/18462/images/676785cedc85f69ab27c42c307af5dec30120ab75f03a9889ab29|u9 1.png"
    },
    "sku": null,
    "meta": null,
    "conditionals": {
      "is_active": true,
      "is_free": false,
      "is_tax_exempt": false,
      "is_pay_what_you_want": false,
      "is_quantity_limited": false,
      "is_sold_out": false,
      "has_digital_delivery": false,
      "has_physical_delivery": false,
      "has_images": true,
      "has_video": false,
      "has_rich_embed": false,
      "collects_fullname": false,
      "collects_shipping_address": false,
      "collects_billing_address": false,
      "collects_extrafields": false
    },
    "is": {
      "active": true,
      "free": false,
      "tax_exempt": false,
      "pay_what_you_want": false,
      "quantity_limited": false,
      "sold_out": false
    },
    "has": {
      "digital_delivery": false,
      "physical_delivery": false,
      "images": true,
      "video": false,
      "rich_embed": false
    },
    "collects": {
      "fullname": false,
      "shipping_address": false,
      "billing_address": false,
      "extrafields": false
    },
    "checkout_url": {
      "checkout": "https://checkout.chec.io/TSUTww?checkout=true",
      "display": "https://checkout.chec.io/TSUTww"
    },
    "extrafields": [],
    "variants": [],
    "categories": [
      {
        "id": "cat_3zkK6oLvVlXn0Q",
        "slug": "office",
        "name": "Home office"
      }
    ],
    "assets": [
      {
        "id": "ast_7ZAMo1Mp7oNJ4x",
        "url": "https://cdn.chec.io/merchants/18462/images/676785cedc85f69ab27c42c307af5dec30120ab75f03a9889ab29|u9 1.png",
        "is_image": true,
        "data": [],
        "meta": [],
        "created_at": 1594075541,
        "merchant_id": 18462
      }
    ]
  },
]
```

The data object contains all the property endpoints such as the product name, the product description, product price or any uploaded variants or assets. This data is exposed when you make a request to the API. As mentioned above, Commerce.js is a Software Development Kit(SDK) that comes with abstracted axios promise-based function calls that will help to fetch data from the endpoints. The public key access that we briefed over above is a public token key from a merchant store. This account already has products and products information uploaded to the Chec dashboard for us to run a demo store with. 

## Start to style your components

Before we go any further, let's start to port in some styles so we can start to make our UI look slick! We will be using SCSS, a CSS style compiler to style our application. Please note that we will not be going into styling details but will only go over the high-level of porting in the styles. First install `node-sass` by adding it as a dependency in the left sidebar or alternatively in a local environment by running the command below.

```bash
yarn add node-sass
# OR
npm install node-sass
```

Next, let's go ahead and create a `styles` folder with a `scss` folder inside. Inside of the `scss` folder, create two other folders named `components` and `global`. Lastly, still in the `scss` folder, create a file and name it `styles.scss`. This file is where we will import in all our components and global styles. Your styles structure should look like the below tree.

- src/
  - styles/
    - components/
    - global/
    - styles.scss

In the components folder, create a file named `_products.scss` and copy in the below code.

```css
/* _products.scss */
.products {
    display: block;
    margin: 3rem;

    @include md {
        display: grid;
        grid-template-columns: repeat(3, minmax(0, 1fr));
        margin: 10rem;
    }

    .product {

        &__card {
            width: 55%;
            margin: auto;
            margin-top: 0;
            margin-bottom: 0;
            padding-bottom: 2rem;
        }

        &__image {
            border: 2px solid $text-primary;
            width: 100%;
        }
    
        &__name {
            color: $text-primary;
            padding-top: 1rem;
            padding-bottom: 0.25rem;
        }
    
        &__details {
            display: flex;
            justify-content: space-between;
            margin-top: 0.75rem;
        }
    
        &__price {
            align-self: center;
            margin: 0;
            color: $text-grey;
        }
    
    
        &__details {
            display: flex;
            justify-content: space-between;
        }
    
        &__btn {
            background: $color-accent;
            color: white;
            font-size: 0.75rem;
            text-transform: uppercase;
            padding: 0.5rem 1rem;
            transition: all 0.3s ease-in-out;
            margin-top: 1rem;
            border: none;
    
            &:hover {
                background-color: lighten(#EF4E42, 5);
            }

            @include sm {
                margin-top: 0;
            }
        }
    }
}
```

Now in the global folder, create `_base.scss`, `_body.scss` and `_mixins.scss` and copy in the respective code below.

```css
/* _base.scss */
// Font styles
$font-primary: 'Amiko', sans-serif;
$font-secondary: 'Adamina', serif;

// Colors
$bg-color: #E8E2D7;

$text-primary: #292B83;
$text-grey: rgb(67, 67, 67);

$color-accent: #EF4E42;

// Media query sizes
$sm-width: 576px;
$md-width: 768px;
$lg-width: 992px;
$xl-width: 1200px
```

```css
/* _body.scss */
body {
  font-family: $font-primary;
  background-color: $bg-color;
}
```

```css
/* _mixins.scss */
@mixin small-xs {
  @media (max-width: #{$sm-width}) {
    @content;
  }
}

@mixin sm {
  @media (min-width: #{$sm-width}) {
    @content;
  }
}

@mixin md {
  @media (min-width: #{$md-width}) {
    @content;
  }
}

@mixin lg {
  @media (min-width: #{$lg-width}) {
    @content;
  }
}

@mixin xl {
  @media (min-width: #{$xl-width}) {
    @content;
  }
}

@mixin md-max {
  @media (max-width: #{$lg-width}) {
    @content;
  }
}
```

Lastly as mentioned, you'll need to now import those created files in the style index `styles.scss`.

```scss
@import "global/base";
@import "global/body";
@import "global/mixins";
@import "components/products";
```

After importing the base styles, let's also import in the fonts we'll be using from Google Fonts in `public/index.html`.

```html
<!-- Load Google fonts -->
<link href="https://fonts.googleapis.com/css?family=Amiko:400,600,700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Adamina&display=swap" rel="stylesheet">
```

Now that all the styles are written and imported, you should start to see the styles pull through when you render your components later.

## Create our product item component

The nature of React and most modern JavaScript frameworks is to separate your code into components. Components are a way to encapsulate a group of elements for reuse throughout your application. You'll be creating two components for products, one will be for the single product item and another for the list of product items. In your components, we will also start to deal with props. Props are used to pass data from parent components down to the child components.
As your app grows, it is generally good practice to validate your props for type checking and debugging. We will install the `prop-types` library to do so.

```bash
yarn add prop-types
# OR
npm install prop-types
```

Going back to our created `ProductItem.js`, start by creating a function component and name it `ProductItem`. This component will render the individual product card. We then pass in the `product` parameter which the parent component will parse out as each individual product object. You will reference this property to access each product's image, name, description, and price via `.media.source`, `.name`, `.description` and `.price` in the return statement.

In Chec, product descriptions return HTML which means if we were to render out `product.description`, we would get a string that returns the html tags along with the description. In general, setting HTML from code is risky because it’s easy to inadvertently expose your users to a cross-site scripting (XSS) attack. So, you can set HTML directly from React, but you have to type out `dangerouslySetInnerHTML` and pass an object with a `__html` key, to remind yourself that it might be dangerous. But because we know we can trust the API responses, this is the best approach to take to render out our product description.

```jsx
import React from 'react';
import PropTypes from 'prop-types';

const ProductItem = ({ product }) => {

  return (
    <div className="product__card">
      <img className="product__image" src={product.media.source} alt={product.name} />
      <div className="product__info">
        <h4 className="product__name">{product.name}</h4>
        <p className="product__description" dangerouslySetInnerHTML={{__html: product.description}}></p>
        <div className="product__details">
          <p className="product__price">
            {product.price.formatted_with_symbol}
          </p>
          <button
            name="Add to cart"
            className="product__btn"
          >
            Quick add
          </button>
        </div>
      </div>
    </div> 
  );
};

export default ProductItem;

ProductItem.propTypes = {
  product: PropTypes.object,
};
```

As you saw earlier in the abbreviated JSON, the returned product data object comes with all the information that you
need to build a product listing view. In the code snippet above, your `product` prop is being used to access the various properties. First, render an image tag with the `src` value of `product.media.source` as the values inside the curly braces dynamically binds to the attributes followed by the `product.name`, `product.description`, and `product.price`.

## Create our products list component

It's now time to create a `ProductsList.js` component inside `src/components`. The `ProductsList` component will be another function component which will loop through and render a list of `ProductItem` components.

First, import in the `ProductItem` component. Next, define a `products` prop. This will be provided by the parent component.

In your return statement you need to use the `map` function to render a `ProductItem` component for each product in your `products` prop. You also need to pass in a unique identifier (`product.id`) as the `key` attribute - React will use it to determine which items in a list have changed and which parts of your application need to be re-rendered.

```js
import React from 'react';
import PropTypes from 'prop-types';
import ProductItem from './ProductItem';

const ProductsList = ({ products }) => {

    return (
        <>
            <div className="products" id="products">
                {products.map((product) => (
                    <ProductItem
                        key={product.id}
                        product={product}
                    />
                ))}
            </div>
        </>
    )
}

export default ProductsList;

ProductsList.propTypes = {
    products: PropTypes.array,
};
```

This component will be a bit bare-boned for now except for looping through a `ProductItem` component.

With both your product item and list components created, go back to `App.js` to render the `<ProductsList />` and pass in the `products` prop with the returned product data as the value. This means that the value of the `ProductsList` component's prop `products` will be resolved from the parent (`App`) component's state, and will update automatically whenever it changes.

```js
import React, { useState, useEffect } from "react";
import { commerce } from './lib/Commerce';

import './styles/scss/styles.scss';

import ProductsList from './components/ProductsList';

const App = () => {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetchProducts();
  }, []);

  /**
   * Fetch merchant details
   * https://commercejs.com/docs/sdk/full-sdk-reference#merchants
   */
  const fetchMerchantDetails = () => {
    commerce.merchants.about().then((merchant) => {
      setMerchant(merchant);
    }).catch((error) => {
      console.log('There was an error fetch the merchant details', error)
    });
  }

  /**
   * Fetch products data from Chec and stores in the products data object.
   * https://commercejs.com/docs/sdk/products
   */
  const fetchProducts = () => {
    commerce.products.list().then((products) => {
      setProducts(products.data);
    }).catch((error) => {
      console.log('There was an error fetch the merchant details', error)
    });
  }

  return (
    <div className="app">
      <ProductsList 
        products={products}
      />
    </div>
  )
};

export default App;
```

Awesome you've now got a full products listing page pulling in data from an external API! Next, we can start to add some cart functionalities!

## Add Cart

In the app component, follow the same logic to fetch and retrieve your cart data after the component renders, the same as fetching your products. First lets add a cart state to store the cart data that will be returned under the products state.

```js
const [cart, setCart] = useState({});
```

Next, we will use another Commerce method to retrieve the current cart in session with `cart.retrieve()`. Commerce.js automatically creates a cart for you if one does not exist in the current browser session. Commerce.js tracks the current cart ID with a cookie, and stores the entire cart and its contents for 30 days. This means that users returning to your website will still have their cart contents available for up to 30 days.

With the Cart API and cart methods in Commerce.js, the otherwise complex cart logic can be easily implemented. Now let's add a new cart method underneath `fetchProducts()`.

```js
/**
 * Retrieve the current cart or create one if one does not exist
 * https://commercejs.com/docs/sdk/cart
 */
const fetchCart = () => {
    commerce.cart.retrieve().then((cart) => {
        setCart(cart);
    }).catch((error) => {
        console.log('There was an error fetching the cart', error);
    });
}
```

## Conclusion
Awesome, there you have it! You have just created an e-commerce React application listing products on from an API backend! The next steps would be to add cart and checkout functionality to your application. Stay tuned for follow up workshops!

### Author

Made with ❤️ by Jaeriah Tay