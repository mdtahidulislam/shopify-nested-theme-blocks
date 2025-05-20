# shopify-nested-theme-blocks

sections/lwt-table-block.liquid
``` liquid
<div class="page-width">
	<table>
		{% content_for 'block', type: 'table-header', id: 'table-header' %}
		<tbody>
			{% content_for 'blocks' %}
		</tbody>
	</table>
</div>

{% schema %}
{
	"name": "Table section",
	"settings": [],
	"blocks": [
		{
			"type": "table-row"
		}
	],
	"presets": [{ "name": "Table section" }]
}
{% endschema %}
```

blocks/table-header.liquid
``` liquid
<thead>
	<tr {{ block.shopify_attributes }}>
		{% content_for 'blocks' %}
	</tr>
</thead>
{% schema %}
{
	"name": "Table header",
	"class": "lwt-table-header",
	"tag": null,
	"settings": [],
	"blocks": [
		{
			"type": "table-cell"
		}
	],
	"presets": [
		{
			"name": "Table header"
		}
	]
}
{% endschema %}
```

blocks/table-row.liquid
``` liquid
<tr {{ block.shopify_attributes }}>
	{% content_for 'blocks' %}
</tr>

{% schema %}
{
	"name": "Table Row",
	"class": "lwt-table-row",
	"tag": null,
	"blocks": [
		{
			"type": "table-cell"
		}
	],

	"settings": [],
	"presets": [
		{
			"name": "Table Row"
		}
	]
}
{% endschema %}
```

blocks/table-cell.liquid
``` liquid
{% if block.settings.type_of_cell == 'header' %}
	<th {{ block.shopify_attributes }}>
{% else %}
	<td {{ block.shopify_attributes }}>
{% endif %}
{% content_for 'blocks' %}
{% if block.settings.type_of_cell == 'header' %}
	</th>
{% else %}
	</td>
{% endif %}

{% schema %}
{
	"name": "Table cell",
	"class": "lwt-table-cell",
	"tag": null,
	"blocks": [
		{
			"type": "@theme"
		}
	],
	"settings": [
		{
			"type": "text",
			"id": "text",
			"label": "Cell content"
		},
		{
			"type": "select",
			"id": "type_of_cell",
			"label": "Type of cell",
			"options": [
				{
					"value": "header",
					"label": "Header Cell"
				},
				{
					"value": "body",
					"label": "Body Cell"
				}
			]
		}
	],
	"presets": [
		{
			"name": "Header cell",
			"settings": {
				"type_of_cell": "header"
			}
		},
		{
			"name": "Body cell",
			"settings": {
				"type_of_cell": "body"
			}
		}
	]
}
{% endschema %}
```
