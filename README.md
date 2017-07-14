# Useful Shopify Code Snippets

This is a list of useful Shopify Snippets that I often reference while developing Shopify themes. Feel Free to contribute.

* [Add Custom Badge on Products using product tag](#add-custom-badge-on-products-using-product-tag)
* [Add Class or Id to Form](#add-class-or-id-to-form)
* [Add Original Price of Discounted products on Cart Page](#add-original-price-of-discounted-products-on-cart-page)
* [Add On Sale Badge on Products Based on Price](#add-on-sale-badge-on-products-based-on-price)
* [Back or Continue Shopping link on Cart](#back-or-continue-shopping-link-on-cart)
* [Calculate Discount on Products](#calculate-discount-on-products)
* [Call a Product on any page](#call-a-product-on-any-page)
* [Display Articles in a Blog](#display-articles-in-a-blog)
* [Display Links in a Linklist](#display-links-in-a-linklist)
* [Display all tags in a blog](#display-all-tags-in-a-blog)
* [Display Products in a Collection](#display-products-in-a-collection)
* [Display Variants in a Product](#display-variants-in-a-product)
* [Insert Block inside a for loop at any position](#insert-block-inside-a-for-loop-at-any-position)
* [Open External links in New Tab](#open-external-links-in-new-tab)
* [Recommend related products](https://help.shopify.com/themes/customization/products/recommend-related-products)
* [Show More Products from a Vendor](#show-more-products-from-a-vendor)

## Add Custom Badge on Products using product tag
This code adds a limited badge on products with "limited" tag on them. Add this in product template.
```html
{% for mytag in product.tags %}
  {% if mytag == 'limited' %}
    <img class="limited-badge" src="{{ 'limited-badge.png' | asset_url }}" alt="Limited Badge">
  {% endif %}
{% endfor %}
```

## Add Class or Id to Form
```html
{% form 'form_name', class: 'custom-class-name', id: 'custom-id-name' %}
```

## Add Original Price of Discounted products on Cart Page
Inset the following code inside items loop in cart template.
```html
{% if item.product.compare_at_price > item.price %}
  <s>{{ item.product.compare_at_price | money }}</s>
{% endif %}
```

## Add On Sale Badge on Products Based on Price
* Products must have "Compare at price" field fill in admin. 
* Shows Badge when "compare_at_price_max" > "product price"
```html
{% if product.compare_at_price_max > product.price %}
  <img class="sale-product" src="{{ 'sale-badge.png' | asset_url }}" alt="On Sale Badge">
{% endif %}
```

## Back or Continue Shopping link on Cart
#### To link to Catalog page at /collection/all
```html
<a href="/collections/all" title="Browse our Catalog">Continue Shopping</a>
```
#### To Collection the product was last added to cart
```html
<a href="{{ cart.items.first.product.collections.first.url }}" title="Continue Shopping">Continue Shopping</a>
```

## Calculate Discount on Products
```html
{% capture discount %}
{{ product.compare_at_price_max | minus:product.price | times:100 | divided_by:product.compare_at_price_max }}%
{% endcapture %}
  <span class="discount">OFF: {{ discount }}</span>
```

## Call a Product on any page
```html
{%- assign product = all_products['product-handle'] -%}
```
Then do anything with product object like ```{{ product.title }}```

## Display Articles in a Blog
```html
{% for article in blogs.blog-name.articles limit:1 %}
  <li class="article">
    <img src="{% if article.image %}{{ article | img_url: 'medium' }}{% endif %}" alt="" >
    <a class="title" href="{{ article.url }}">{{ article.title }}</a>
    <a class="date" href="{{ article.url }}">{{ article.published_at | date: "%B %d, %Y" }}</a>
    <div class="rte content">{{ article.excerpt_or_content }}</div>
  </li>
{% endfor %}
```

## Display Links in a Linklist
```html
<ul class="list">
  {% for link in linklists.linklist-handle.links %}
     <li>{{ link.title | link_to: link.url }}</li>
  {% endfor %}
</ul>
```

## Display all tags in a blog
```html
{% for tag in blog.all_tags %}
  <a href="{{ blog.url }}/tagged/{{ tag | handle }}">{{ tag }}</a>
{% endfor %}
```

## Display Products in a Collection
```html
<div class="grid">
  <h3 class="text-center">Products</h3>
  {% for product in collections.collection-name.products %}
    <div class="grid__item medium-up--one-third">
        <a href="{{ product.url }}"><img src="{{ product.featured_image | product_img_url: '345x' }}" alt="{{ product.title | escape  }}" /></a>
        <div class="h4 grid-view-item__title"><span>{{ product.title }}</span></div>
     </div>
  {% endfor %}
</div>
```

## Display Variants in a Product
```html
{% for product in collections.collection-name.products %}
  <div class="grid">
   {% for variant in product.variants %}
      <!-- some html product box layout here -->
      {% include 'product-card-grid', grid_image_width: image_size, product: variant %}
   {% endfor %}
  </div>
{% endfor %}
```

## Insert Block inside a for loop at any position
This code inserts "new-block" div at position 4.
```html
  {% for block in section.blocks %}
    <div class="repeating-block">
      <a href="#" class="link">
        <img src="#" alt="Dummy">
      </a>
    </div>
    {% if forloop.index0 == 3 %}
      <div class="new-block">
        <img src="#" alt="Dummy">
      </div>
    {% endif %}
  {% endfor %}
```

## Open External links in New Tab
```javascript
$(document).ready( function() {
  jQuery('a[href^="http"]').not('a[href^="'+$(location).attr('hostname')+'"]').attr('target', '_blank');
});
```

## Show More Products from a Vendor
```html
<div>
  {% assign vendor = product.vendor %}
  {% assign handle = product.handle %}
  {% assign counter = '' %}
  {% for product in collections.all.products %}
  {% if vendor == product.vendor and counter.size < 4 and handle != product.handle %}
  {% capture temp %}{{ counter }}*{% endcapture %}
  {% assign counter = temp %}
  <div class="recommendations_img">
    <a href="{{ product.url | within: collection }}" title="{{ product.title }}">
      <img src="{{ product.images.first | product_img_url: 'small' }}" alt="{{ product.title }}" />
    </a>
  </div><!-- .recommendations_img -->
  {% endif %}
  {% endfor %}
</div>
```
