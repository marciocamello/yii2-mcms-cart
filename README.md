Yii2-Cart
===========
Cart extensions for Yii 2

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist marciocamello/yii2-mcms-cart "*"
```

or add

```
"marciocamello/yii2-mcms-cart": "*"
```

to the require section of your `composer.json` file.


Usage
-----

Adding an Item to The Cart
--------------------------

```php

use mcms\cart\Cart;

$cart = new Cart();

$data = array(
	'id'      => 'sku_123ABC',
	'qty'     => 1,
	'price'   => 39.95,
	'name'    => 'T-Shirt',
	'options' => array('Size' => 'L', 'Color' => 'Red')
);

$cart->insert($data);

```

Adding Multiple Items to The Cart
---------------------------------

```php

use mcms\cart\Cart;

$cart = new Cart();

$data = array(
               array(
                       'id'      => 'sku_123ABC',
                       'qty'     => 1,
                       'price'   => 39.95,
                       'name'    => 'T-Shirt',
                       'options' => array('Size' => 'L', 'Color' => 'Red')
                    ),
               array(
                       'id'      => 'sku_567ZYX',
                       'qty'     => 1,
                       'price'   => 9.95,
                       'name'    => 'Coffee Mug'
                    ),
               array(
                       'id'      => 'sku_965QRS',
                       'qty'     => 1,
                       'price'   => 29.95,
                       'name'    => 'Shot Glass'
                    )
            );

$cart->insert($data);

```
