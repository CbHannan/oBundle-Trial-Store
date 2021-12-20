# OBundle BigCommerce Test Project
## Instructions

# Test Overview
--------------------
I created a trial BigCommerce store called *oBundle Trial Store* . Next, I created a product called 'Special Item' which I asigned to a category I created called 'Special Items'. I added 4 images during the product creation. I deleted all other demo products in each default categories that come with the Standard Cornerstone theme. Only the 'Special Item' product I created is found in the 'Special Items' category. Only the Storefront APIs were used as required.

## Store Access
- Preview Code: There is no preview code set up. 
- Store Url: https://oBundle-trial-store.mybigcommerce.com/

## Set Up
--------------------
I downloaded and installed the *Stencil CLI* for local Development and created an API Account on my Store Dashboard. Next I cloned from github the *Stencil's Cornerstone theme* for working and editing the default Cornerstone Theme that comes standard with new BigCommerce stores.

## Feature 1
--------------------
Creating a feature that will show the product's second image when it is hovered on.

  -- `templates/components/common/responsive-img.html` (Line 40)
  ```
    <img
      data-src="{{getImageSrcset image use_default_sizes=true}}"
      data-hoverimage='{{getImageSrcset images.[1] img size (cdn default) use_default_sizes=true}}'
    />
  ```

  -- `assets/js/theme/category.js`(Line 168-171)
  ```
    $(".card-figure").hover(
      this.onShowProductSecondImage.bind(this),
      this.onRemoveProductSecondImage.bind(this)
    );
  ```

## Feature 2
--------------------
Adding a button at the top of the category page labeled **Add All To Cart**. When clicked, the product will be added to the cart then notify the user that the product has been added.


  -- `templates/pages/category.html` (Line 50-55)
  ```
    <div class="add-all-to-cart">
      <div class="d-flex">
        <input type="button" class="button button--primary" id="addAllToCart" value="Add All To Cart"/>
      </div>
    </div>
  ```

  --  `templates/pages/category.html` (Line 22-32)`
  ```
    <div class="cart-notification">
      <div class="add-notification">
        <i class="fas fa-check-circle"></i>
        Items were successfully added to the cart!
      </div>
    </div>
    <div class="clear-both"></div>
  ```

  -- `assets/js/theme/category.js` (Line 166)
  ```
    $("#addAllToCart").on("click", this.onAddAllToCart.bind(this));
  ```


## Feature 3
--------------------
If the cart has an item in it - show a button next to the **Add All To Cart** button which says **Remove All Items**. When clicked it should clear the cart and notify the user.


  -- `templates/pages/category.html` (Line 50-53)
  ```
    <input type="button" class="button button--danger" id="removeAllItems" value="Remove All Items"/>
  ```

  --- `templates/pages/category.html` (Line 27-30)
  ```
  <div class="remove-notification">
      <i class="fas fa-check-circle"></i>
      Items were successfully removed from the cart!
    </div>
  ```

  -- `assets/js/theme/category.js` (Line 165 & 167)
  ```
  this.onCheckCart();
  $("#removeAllItems").on("click", this.onRemoveAllItems.bind(this));
  ```
  

## Feature 4 (The Bonus)
--------------------
If a customer is logged in - at the top of the category page show a banner that shows some customer details (i.e. name, email, phone etc). This should utilize the data that is rendered via Handlebars on the Customer Object.


  -- `templates/components/common/header.html` (Line 14-39)
  ```
    {{#if customer}}
      <header class="customer-details w-100">
          <div class="customer-about">
              <p class="customer-name">
                  <i class="fas fa-user"></i>
                  {{customer.name}}
              </p>
              <p class="customer-email">
                  <i class="fas fa-envelope-square"></i>
                  {{customer.email}}
              </p>
              <p class="customer-phone">
                  <i class="fas fa-phone"></i>
                  {{customer.phone}}
              </p>
              <p class="customer-messages">
                  <i class="fas fa-envelope"></i>
                  {{#if customer.num_new_messages}}
                      {{customer.num_new_messages}}
                  {{else}}
                      <span>0</span>
                  {{/if}}
              </p>
          </div>
      </header>
    {{/if}}
  ```

## CSS
I created a sass file named **custom.scss** in **assets/scss** then added all the css rules needed for these tasks. This file was then imported in **assets/scss/theme.scss** to make it availabe for the entire wesbsite.
