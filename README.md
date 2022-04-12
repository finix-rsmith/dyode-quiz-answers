# Dyode | Quiz Answers

Dev Challenge I: Liquid Challenge

## Questions

1. Describe how you would make a line of text in a homepage section editable from theme customization and how you would access this in liquid.

**In theme customization under /Sections, open the homepage.liquid file and replace static text content with dynamic content outputs mapped to reference data, e.g.:**

```javascript
{{ page.title }}
```

2. How would you add the collection featured image as a banner on the collection liquid template?

```jsx
{% if collection.image %}
	<img src={{ collection.image.src  | image_url: width: 2048  }} alt={{ collection.image }}  />
{% else %}
	{% assign product = collection.products.first %}
	<img src={{ product | image_url: width: 2048 }} alt={{ product.handle }} />
{% endif %}
```

3. Using liquid code and HTML, create a simple pagination container, "< 1 2 ... 5 >".

```jsx
{% paginate collection.products by 10 %}
	{% if paginate.pages > 1 %}
		<nav role=“navigation”>
			<ol>
				{% if paginate.previous %}
					<li>
						<a href={{ paginate.previous.url }}>
							<
						</a>
					</li>
				{% else %}
					<li class=“disabled”>
						<
					</li>
				{% endif %}

				{% for part in paginate.parts %}
					{% if part.is_link %}
						<li>
							<a href={{ part.url }}>{{ part.title }}</a>
						</li>
					{% else %}
						{% if part.title == paginate.current_page %}
							<li class=“active”>
								{{ part.title }}
							</li>
						{% else %}
							<li>
								{{ part.title }}
							</li>
						{% endif %}
					{% endif %}
				{% endfor %}

				{% if paginate.next %}
					<li>
						<a href={{ paginate.next.url }}>
							>
						</a>
					</li>
				{% else %}
					<li class=“disabled”>
						>
					</li>
				{% endif %}
			</ol>
		</nav>
	{% endif %}
{% endpaginate %}

<style>
	li {list-style: none; display: inline}
	a {text-decoration: none}
</style>
```

4. Using liquid code, access the product named "Blue T-Shirt". Store the id, title, handle, price, url, and image in variables.

```javascript
{% assign blueTshirt = all_products["blue-t-shirt"] %}
{% assign blueTshirtId = blueTshirt.id %}
{% assign blueTshirtTitle = blueTshirt.title %}
{% assign blueTshirtHandle = blueTshirt.handle %}
{% assign blueTshirtPrice = blueTshirt.price %}
{% assign blueTshirtUrl = blueTshirt.url %}
{% assign blueTshirtImage = blueTshirt.image %}
```

5. Using liquid code, create a key:value array using the list below. Loop through the array. Upon key type, store the value in a variable to be used later:
- fruit:apple
- vegetable:carrot
- cloth:t-shirt
- denim:jeans

```javascript
{% assign some_items = "fruit:grape,vegetable:carrot,cloth:t-shirt,denim:jeans" | split: "," %}
{% assign updated_items = "" | split: "," %}
{% for item in some_items %}
	{% assign item_attributes = item | split ":" %}
	{% assign item_key = item_attributes[0] %}
	{% assign item_value = item_attributes[1] %}
	{% capture key_value %}
		{ {{ item_key }}: {{ item_value }} }
	{% endcapture %}
	{% assign updated_items = updated_items | concat: key_value %}
{% endfor %}
{{ updated_items }}
```

## Author

**Richard Smith**
- rsmith@finixcreative.com
- 617-417-2179