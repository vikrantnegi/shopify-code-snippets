# Useful Shopify Code Snippets

This is a list of useful Shopify Snippets that I often reference while developing Shopify themes. Feel Free to contribute.

* [Add Custom Badge on Products using product tag](#add-custom-badge-on-products-using-product-tag)
* [Add Class or Id to Form](#add-class-or-id-to-form)
* [Add page numbers to pagination](#add-page-numbers-to-pagination)
* [Add Original Price of Discounted products on Cart Page](#add-original-price-of-discounted-products-on-cart-page)
* [Add On Sale Badge on Products Based on Price](#add-on-sale-badge-on-products-based-on-price)
* [Back or Continue Shopping link on Cart](#back-or-continue-shopping-link-on-cart)
* [Blog Category Filter Dropdown](#blog-category-filter-dropdown)
* [Calculate Discount on Products](#calculate-discount-on-products)
* [Call a Product on any page](#call-a-product-on-any-page)
* [Custom Pagination](#custom-pagination)
* [Display Articles in a Blog](#display-articles-in-a-blog)
* [Display Links in a Linklist](#display-links-in-a-linklist)
* [Display all tags in a blog](#display-all-tags-in-a-blog)
* [Display Products in a Collection](#display-products-in-a-collection)
* [Display Variants in a Product](#display-variants-in-a-product)
* [Insert Block inside a for loop at any position](#insert-block-inside-a-for-loop-at-any-position)
* [Open External links in New Tab](#open-external-links-in-new-tab)
* [Recommend related products](https://help.shopify.com/themes/customization/products/recommend-related-products)
* [Show More Products from a Vendor](#show-more-products-from-a-vendor)
* [Strip empty tags from article excerpt](#strip-empty-tags-from-article-excerpt)
* [Multiple currency selector](#multiple-currency-selector)

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

## Add page numbers to pagination
```html
{% assign count = paginate.pages %}
{% for part in (1..count) %}
  <li class="{% if paginate.current_page == part %} active {% endif %}">
    <a href="{{ collection.url }}?page={{ forloop.index }}">{{ forloop.index }}</a>
  </li>
{% endfor %}
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

## Blog Category Filter Dropdown
```html
{% if blog.tags.size > 0 %}
  <select id="BlogTagFilter">
    <option value="/blogs/{{ blog.handle }}">{{ 'blogs.article.all_topics' | t }}</option>
    {% for tag in blog.all_tags %}
      <option value="/blogs/{{ blog.handle }}/tagged/{{ tag | handleize }}" {% if current_tags contains tag %}selected{% endif %}>{{ tag }}</option>
    {% endfor %}
  </select>
{% endif %}
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

## Custom Pagination
Add `pagination-count` and `pagination-tabs` from the snippet folder to your Shopify Theme Snippet folder
```liquid
{% if paginate.pages > 1 %}
  {% include 'pagination-count' %}
  {% include 'pagination-tabs' %}
{% endif %}
```

## Display Articles in a Blog
```html
{% for article in blogs.blog-name.articles limit:1 %}
  <li class="article">
    <img src="{% if article.image %}{{ article | img_url: 'medium' }}{% endif %}" alt="" >
    <a class="title" href="{{ article.url }}">{{ article.title }}</a>
    <a class="date" href="{{ article.url }}">{{ article.published_at | date: "%B %d, %Y" }}</a>
    <div class="rte content">{{ article.excerpt_or_content }}</div>
    <a href="{{ article.url }}" class="featured-projects__link">{{ 'blogs.article.read_more' | t }}</a>
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

## Strip empty tags from article excerpt
Strip out empty p and span tags
```html
{{ article.excerpt | strip_html }}
```

## Multiple currency selector

```liquid
{% form 'currency' %}
  {{ form | currency_selector }}
{% endform %}
```

```liquid
{% form 'currency' %}
  <select name="currency">
    {% for currency in shop.enabled_currencies %}
{% if currency == cart.currency %}
  <option selected="true" value="{{ currency.iso_code }}">{{currency.iso_code}} {{currency.symbol}}</option>
  {% else %}
  <option value="{{ currency.iso_code }}">{{currency.iso_code}} {{currency.symbol}}</option>
{% endif %}
    {% endfor %}
  </select>
{% endform %}
```

```js
$('.shopify-currency-form select').on('change', function() {
  $(this)
    .parents('form')
    .submit();
});
```

## License

Licensed under the [MIT](https://github.com/vikrantnegi/shopify-code-snippets/blob/master/LICENSE).

## Donation

If this project helped you reduce time to develop, please consider buying me a cup of coffee :)

<a href="https://www.buymeacoffee.com/vikrantnegi" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/E1E6Z0JL)
