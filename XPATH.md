# Item path
item will be find recursively in entire file, so it is better make sure the path will not find undesired tags.

Use `/` to represent the next level, in the [example](https://github.com/fcharmy/xml2csv/blob/master/README.md#example) `shop/products/product` means find `<product>` in the file which is the direct child tag of `<products>`, whose parent is `<shop>`.

# Column tag path
The same rules as item path, the different is this tag will only search inside each item tag.  
```
Note: 'tag path' is composary, if leave it empty the whole column will be empty value, 'attribute' is optional.  
      If attribute is empty, column will get the value of tag, or it will get the value of attribute.
```

For given `<product>` in [example](https://github.com/fcharmy/xml2csv/blob/master/README.md#example)

* if you want the value of `<url>` to be the value of im_url column  
  add a new column with name `im_url`   
  set tag path to `url`, which means will find `<url>` inside `<product>`  
  leave attribute empty, this will set the value of `<url>` to the column im_url instead of attribute value  
  
* if you want the attribute of `<product>` to be the title,  
  update tag path to `.` which represent use the current tag   
  set attribute to `name` which will get the attribute value as column  
 
* if you want the attribute `id` of `<item>` to be the im_name  
  tag path: `item`  
  attribute: `id`  

* if you want extract price and price_unit from <price>  
  * column name: `price`  
      tag path: `price/retail`  
      attribute: (empty)  
      
  * column name: `price_unit`  
      tag path: `price`  
      attribute: `currency`  

* if there are many `<param>`, more specific way to get sku and product url is,  
  column name: `sku`  
      tag path: `param[@name='sku']`  
      attribute: (empty)  
  
  column name: `product_url`  
      tag path: `param[@name='item_url']`  
      attribute: (empty)
  
  which means it will find `<param>` with a attribute named `name` and its value is exactly equal to `sku`, then use the tag value as column.
  
### Summary 
use `<product>` from [example](https://github.com/fcharmy/xml2csv/blob/master/README.md#example) as example
               
| column name        | tag path                 | attribute  | description  |
| ------------------ | ------------------------ | ---------- | ------------ |
| im_url             | `url`                    |            | find `<url>` inside `<product>` and set the value of `<url>` as column  |
| im_name            | `item`                   | `id`       | use the current tag `<item>` and set the value of attribute `id` as column  |
| title              | `.`                      | `name`     | use the current tag `<product>` and set the value of attribute `name` as column  |
| price              | `price/retail`           |            | find `<price>` under `<product>` and search for `<retail>` under `<price>` |
| price_unit         | `price`                  | `currency` |              |
| sku                | `param[@name='sku']`     |            | find `<param>` with a attribute named `name` and its value is `sku`, set tag value as column |
| product_url        | `param[@name='item_url']`|            |              |
