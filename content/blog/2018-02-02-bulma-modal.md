---
author: "howlCode"
date: 2018-02-02
title: Using Bulma.io Modal's in Rails
best: true
---

Having recently used a new CSS framework, [Bulma.io](https://bulma.io), I thought I'd write a little about my experience using the framework and how I managed to get the Modal component working in my project.
Bulma.io is the product of one individual, [Jeremy Thomas](https://jgthms.com), and is completely open-source and free to use. I wanted to use a framework that was more lightweight than some of the more famous ones such as bootstrap or foundation. My app, [Shroom Hunters](https://github.com/howlCode/shroom_hunters) is a small Rails 5 application(growing everyday!), that I felt could use a lean framework without any added javascript or other bloat. I prefer to do things myself at the earlier stages.
Bulma fit the bill nicely. It's classes are straightforward and succinct. For example, to center text you use:

```html
<p class="has-text-centered">Blah blah blah, milk sandwiches...</p>
```

...many of the classes are just as intuitive. is-italic, is-bold, is-hidden-mobile, and so on. Often I was able to guess what the class would be and when I could not guess the awesome documentation was quick to answer my questions.

One issue I found, since bulma lacks javascript, was the modal component didn't work out of the box as it does in say bootstrap. It took some tinkering, which I'll show you here.

To render a 'javascript view' in vanilla rails you have to make sure your controller is able to respond to js requests. For instance, I have a 'products' controller that uses a modal on the show view. I first wired up the controller using the 'respond_to' method as seen here:

```ruby
def show
  @product = Product.find(params[:id])
  @order = Order.where(id: session[:order_id]).first
  respond_to do |format|
  format.js
  end
end
```

...in essence we're preparing the controller to render a javascript view. Which is created here under the products views sub-folder.

```javascript
// filename is show.js.erb

var productContent = document.querySelector('#product-content');

function closeModal() {
  var productModal = document.querySelector('#product-modal');
  productModal.classList.remove('is-active');
}

productContent.innerHTML = "<%= j render 'product_modal', product: @product %>";

```

...which pumps in the HTML and allows us to use an onClick call to the 'closeModal' function as seen in the partial here:

```html
<div class="modal is-active" id="product-modal">
  <div class="modal-background"></div>
  <div class="modal-content has-text-white" id="product-content">
    <--  content here -->
</div>
```

...Also, the index page needs a div where the modal will be spit out. I dropped the div in at the bottom of the index view page.

```html
<div id="product-content"></div>
```

As you can see it's pretty easy to get wired up! Minimal javascript, some minor tweaking here and there to get a pretty handsome show page!

You can see an example of the modal at the [Bulma.io website](https://bulma.io/documentation/components/modal/).

Happy coding!
