# Useful Shopify Code Snippets

This is a list of useful Shopify Snippets that I often reference while developing Shopify themes. Feel Free to contribute.

* [Display Products in a Collection](#display-products-in-a-collection)
* [Calculate Discount on Products](#calculate-discount-on-products)
* [Show More Products from a Vendor](#show-more-products-from-a-vendor)
* [Display Articles in a Blog](#display-articles-in-a-blog)
* [Display Links in a Linklist](#display-links-in-a-linklist)


## Display Products in a Collection
```html
<div class="grid">
  <h3 class="text-center avenir-head">Products</h3>
  {% for product in collections.collection-name.products %}
    <div class="grid__item medium-up--one-third">
        <a href="{{ product.url }}"><img src="{{ product.featured_image | product_img_url: '345x' }}" alt="{{ product.title | escape  }}" /></a>
        <div class="h4 grid-view-item__title"><span>{{ product.title }}</span></div>
     </div>
  {% endfor %}
</div>
```

## Calculate Discount on Products
```html
{% capture discount %}
{{ product.compare_at_price_max | minus:product.price | times:100 | divided_by:product.compare_at_price_max }}%
{% endcapture %}
  <span class="discount">OFF: {{ discount }}</span>
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

