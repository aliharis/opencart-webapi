Opencart WEB API
================

This is a small module that adds the ability to remotely work with the OpenCart 1.5.6+ via the REST API.

This module was originally developed by Zen Walker for OpenCart 1.5.3+. The project has been updated to support OpenCart 1.5.6+.

Settings
--------

API Settings can be accessed from Admin Panel > Extensions > Product Feeds > Web API

You can Enable/Disable API & Setup an API KEY for Authentication. When API Key is provided, a parameter named key must be added to the URL.

Example: http://example.com/?route=feed/web_api/categories&parent=0&level=2&key=1234

Features:

 * [Get categories list](#get-categories)
 * [Get category info](#get-category-info)
 * [Get products from category](#get-products)
 * [Get full info from product](#get-product)


Examples
--------

### Get categories

Request:

  http://example.com/?route=feed/web_api/categories&parent=0&level=2


Params:

 * $_GET['parent']: parent category id
 * $_GET['level']:  depth level


Answer:

	{
	  "success": true,
	  
	  categories:
	  [
	    {
	      "category_id": "1",
	      "name": "First category",
	      "parent_id": "0",
	      "href": "http://example.com/index.php?route=product/category&category_id=1"
	      "categories": null,
	    },
	    {
	      "category_id": "2",
	      "name": "Second category",
	      "parent_id": "0",
	      "href": "http://example.com/index.php?route=product/category&category_id=2"
	      "categories": [
	        {
	          "category_id": "3",
	          "name": "Inner category",
	          "parent_id": "2",
	          "href": "http://example.com/index.php?route=product/category&category_id=3"
	          "categories": null
	        },
	        {
	          "category_id": "3",
	          "name": "Inner category",
	          "parent_id": "2",
	          "href": "http://example.com/index.php?route=product/category&category_id=4"
	          "categories": null
	        }
	      ]
	    }
	  ]
	}


### Get category info

Request:

  http://example.com/?route=feed/web_api/category&id=1


Params:

 * $_GET['id']: category id


Answer:

  {
    "success":true,

    "category":{
      "id": "1",
      "name": "Category name",
      "description": "",
      "href": "http://example.com/index.php?route=product/category&category_id=1"
    }
  }



### Get products

Request:

  http://example.com/?route=feed/web_api/products&category=67&sort=p.date_added&order=DESC&start=0&limit=10&key=1442


Params:

 * $_GET['category']: parent category id
 * $_GET['sort']: sort option (p.added, pd.name, p.price)
 * $_GET['order']: sort order (ASC, DESC)
 * $_GET['start']: row to start from (offset)
 * $_GET['limit']: limit


Answer:

	{
	  "success": true,
	  
	  products: [
	    {
	      "id": "6",
	      "name": "Product name",
	      "description": "",
	      "pirce": "$455.00",
	      "href": "http://example.com/index.php?route=product/product&product_id=6",
	      "thumb": false,
	      "special": false,
	      "rating": 0
	    },
	    {
	      "id": "7",
	      "name": "Product name",
	      "description": "",
	      "pirce": "$25.00",
	      "href": "http://example.com/index.php?route=product/product&product_id=7",
	      "thumb": false,
	      "special": false,
	      "rating": 0
	    }
	  ]
	}



### Get product

Request:

  http://example.com/?route=feed/web_api/product&id=1

Params:

 * $_GET['id']: product id

Answer:

	{
	  "success":true,

	  "product":{
	    "id": "2",
	    "seo_h1": "",
	    "name": "Product name",
	    "manufacturer":null,
	    "model": "A1",
	    "reward":null,
	    "points": "0",
	    "image": "",
	    "images":[],
	    "price": "$10.00",
	    "special":false,
	    "discounts":[],
	    "options":[
	      {
	        "product_option_id": "2",
	        "option_id": "5",
	        "name": "Select",
	        "type": "select",
	        "option_value":[

	        ],
	        "required": "1"
	      },
	      {
	        "product_option_id": "1",
	        "option_id": "2",
	        "name": "Checkbox",
	        "type": "checkbox",
	        "option_value":[
	          {
	            "product_option_value_id": "1",
	            "option_value_id": "24",
	            "name": "Checkbox 2",
	            "image":null,
	            "price": "$20.00",
	            "price_prefix": "+"
	          }
	        ],
	        "required": "1"
	      }
	    ],
	    "minimum": "1",
	    "rating": 0,
	    "description": "HTML Description",
	    "attribute_groups":[
	      {
	        "attribute_group_id": "1",
	        "name": "Attribute group 1",
	        "attribute":[
	          {
	            "attribute_id": "10",
	            "name": "Attribute 1",
	            "text": "20"
	          },
	          {
	            "attribute_id": "70",
	            "name": "Attrubute 2",
	            "text": "Value"
	          }
	        ]
	      }
	    ]
	  }
	}



### Error handling

Answer:

	{
	  "success": false,
	  "code": 20,
	  "message": "Invalid secret key"
	}

Error codes:

 * 10 - Module disabled
 * 20 - Invalid secret key


License
-------

This software is distributed under the [GNU GPL V3](http://www.gnu.org/licenses/gpl.html) License.
