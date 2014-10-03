Component Routing
=================

> Component-based routing archiecture for single-page applications (SPA)

_Routing_ is how web application matches a URI to a web page. If a web page
contains multiple components (hello [Polymer](http://www.polymer-project.org/)),
many of these components may be bound to their own URIs.

Traditionally web developers define routes in a single file which is also an
entry point of a web application (e.g. app.js).

When the number of routes and components grow, it becomes harder to maintain
routing information of a web application, that's where component-based routing
may help. The main idea of this approach is that you define routes individually
for each component. While this may sound counter intuitive at a first glance,
this approach has its own advantages, such as:

 * Easy to set nested routes
 * Easy to find which route corresponds to which component and vice versa
 * Routes are concatenated into a single object and optimized at compile time
 * Less room for making a mistake when defining new routes or modified existing ones

### Example
 
Consider a web application with the following URLs (StackOverflow):

`/questions`<br>
`/questions/new`<br>
`/questions/featured`<br>
`/qeustions/12345-what-is-component-based-routing`

Components:

```js
// ./components/QuestionsPage.jsx

var QuestionsPage = React.createComponent({
  // View / Controller View
});

QuestionsPage.route = { url: '/questions/:order', constraints: [ order: /(|new)/ ] };

module.exports = QuestionsPage;
```

```js
// ./components/QuestionPage.jsx

var QuestionPage = React.createComponent({
  // View / Controller View
});

QuestionPage.route = { url: '/questions/:id-*', constraints: [ id: /[0-9]+/ ], order: 10 };

module.exports = QuestionPage;
```

You can have relative URLs, so instead of `/questions/:id-*` you may write `~/:id-*`

Example:

```jsx
// URL: /store/products
<Store route={ url: '/store' }>
  <Products route={ url: '/store/products' } />
</Store>

// URL: /store/checkout
<Store route={ url: '/store' }>
  <Checkout route={ url: '~/checkout' } />
</Store>
```

You can specify default values, for example:

`{ url: '/questions/:order', defaults: [ order: 'new' ] }`

After compilation (bundling with Webpack or Browserify) all these routes are combined
into one object which is then used on both client and server.

### Contributing

Feel free to [fork the repo](https://github.com/kriasoft/component-routing/fork)
and send a pull request with your updates.

### Copyright

The Creative Commons License ([CC BY SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/))
(c) Konstantin Tarkus ([@koistya](https://twitter.com/koistya))
