## === How to Run xml2csv.py? ===
1. Copy your xml file to the directory of this file
2. Alter the configuration for your case according to 'How to Confige?'
3. Mac user:   
    a. Open Terminal (search in your Launchpad)   
    b. Type 'python' (without quote) and a space, then drag this file to Terminal, you'll see like this:   
      `python /Users/user/xml2csv.py`  
    c. Press Enter, wait until you see 'Complete convert XML to CSV' in Terminal   
    d. Done! you will find a csv file generated in your directory   

## === How to Confige xml2csv.py? ===
open your xml file, and you need to firstly

FIND THE TAG:   
`<any_name_here>` we call a tag in xml file, the root tag is the first tag from the beginning except `<?xml version="1.0" encoding="UTF-8"?>`   
`<shop>` is the root tag in the [example](https://github.com/fcharmy/xml2csv/blob/master/README.md#example)   
Find the tag which represent product items, like `<product>` here, please note that `<products>` is not.   

1. Set following ITEM_TAG_TRACE to the path trace to product tags (except the root),   
'products/product' is the product trace we are looking for, which seperate tags with '/', means to the next level of tags
```
    ITEM_TAG_TRACE = 'product'
```

2. Put your xml file to the same directory with the file, then copy the file name to the following XML_FILE
```
    XML_FILE = '35725_3076042_mp.xml'
```

3. Change CSV_FILE to the file name you like for the new csv file,
   make sure you don't have file with the same name, otherwise it will be replaced.
```
    CSV_FILE = 'xml_file.csv'
```

4. Now comes the most important part!!   
(Note: we consider tags inside the product tag only, remind that all text is case sensitive)  
You can add or delete lines to the COL_NAMES as you want, but make sure its correctness  
For Dashboard, im_name and im_url is the compulsory.  

Let's start:
```
        Copy the following line to COL_NAMES and update the value for your need
            {'column name': ['path/to/tag', '@arrtibute_name']},

        Examples:
            a. if you want the attribute of product tag from above case to be the title,
               {'title': ['.', '@name']}

               '.' represent the current product tag, do not leave it empty
               '@name' means the attribute name of above tag, which is product tag now
               put these two in a pair of square bracket

            b. if you want the attribute of item tag which is insid product to be the im_name
               {'im_name': ['./item', '@id']}

               './item' represent the item tag which is the second level of product
               '@id' means attribute name 'id' of above tag

            c. if you want the value of <url> to be the im_url
               {'im_url': ['./url']}

               we do not need attribute this time, just delete it or leave it empty, eg. {'im_url': ['./url', '']}

            d. if you want extract price and price_unit from <price>
               {'price': ['./price/retail', '']},
               {'price_unit': ['./price', '@currency']},

               notice here price is the value of <retail> which is the next level inside <price>,
               and price_unit is the attribute 'currency' of <price>

            e. more specific way to get sku and product url from Example case is,
               {'sku': ['./param[@name=sku]']}
               {'product_url': ['./param[@name=item_url]']}

               now the [@attribute=sku] means that,
               we fetch the value of <param> which has a attribute named 'attribute' and its value is 'sku'
```

5. Update the following lines for your case, then run it!
```
COL_NAMES = [
             {'im_name': ['.', '@product_id']},
             {'im_url': ['./URL/productImage']},
             {'title': ['.', '@name']},
             {'sku': ['.', '@sku_number']},
             {'seller': ['.', '@manufacturer_name']},
             {'product_url': ['./URL/product']},
             {'price_unit': ['./price', '@currency']},
             {'price': ['./price/retail']},
             {'desc': ['./description/short']},
             {'category': ['./category/primary']},
             {'brand': ['./brand']},
             ]
```
