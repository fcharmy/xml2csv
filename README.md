# Convert XML to CSV
Any problem please feel free to raise a issue.

* [webpage](https://fcharmy.github.io/xml2csv/) - convert xml file online.
* [xml2csv.py](https://github.com/fcharmy/xml2csv/blob/master/python/xml2csv.py) - python file to execute in your local pc.

### Example

    --------------- xml file below -------------
    <?xml version="1.0" encoding="UTF-8"?>
    <shop>
      <products>
         <product name='Swimwear Women Hot Coral One Piece Swimsuit'>
              <item id="123344"/>
              <url>http://abc.com/1.jpg</url>
              <price currency='GBP'>
                  <retail>44.00</retail>
             </price>
             <param name='sku'>EC123VGRE</param>
             <param name='item_url'>http://abc.com/EC123VGRE</param>
          </product>
          <product name='Men Swimsuit'>
              <item id="123344"/>
              <url>http://abc.com/1.jpg</url>
              <price currency='GBP'>
                  <retail>44.00</retail>
             </price>
             <param name='sku'>EC1222EFE</param>
             <param name='item_url'>http://abc.com/EC1222EFE</param>
          </product>
      </products>
    </shop>
    ----------- end of example xml file --------

By knowing `<shop>` is the root tag, and `<product>` is a item tag, so 'products/product' can be used to find a list of item tags.  
('product' is also fine but it will find `<product>` tag inside another product tag)
