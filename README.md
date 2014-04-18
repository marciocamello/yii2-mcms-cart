Yii2-Cart
===========
Cart extensions for Yii 2
Refactory library from Codeginiter Cart Class v3.0dev

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

Displaying the Cart
-------------------

```php

use yii\helpers\Html;
use yii\widgets\ActiveForm;
use mcms\cart\Cart;

$cart = new Cart();

if($_POST)
{
	$cart->update($_POST);
	Yii::$app->controller->refresh();
}

```

```php

<?php $form = ActiveForm::begin([
	'id' => 'cart-form',
	'options' => ['class' => 'form-horizontal'],
]) ?>

<table cellpadding="6" cellspacing="1" style="width:100%" border="0">

	<tr>
		<th>QTY</th>
		<th>Item Description</th>
		<th style="text-align:right">Item Price</th>
		<th style="text-align:right">Sub-Total</th>
	</tr>

	<?php $i = 1; ?>

	<?php foreach ($cart->contents() as $items): ?>

		<?php echo Html::hiddenInput($i.'[rowid]', $items['rowid']) ?>

		<tr>
			<td><?php echo Html::textInput($i.'[qty]', $items['qty'], ['maxlength' => '3', 'size' => '5']); ?></td>
			<td>
				<?php echo $items['name']; ?>

				<?php if ($cart->has_options($items['rowid']) == TRUE): ?>

					<p>
						<?php foreach ($cart->product_options($items['rowid']) as $option_name => $option_value): ?>

							<strong><?php echo $option_name; ?>:</strong> <?php echo $option_value; ?><br />

						<?php endforeach; ?>
					</p>

				<?php endif; ?>

			</td>
			<td style="text-align:right"><?php echo $cart->format_number($items['price']); ?></td>
			<td style="text-align:right">$<?php echo $cart->format_number($items['subtotal']); ?></td>
		</tr>

		<?php $i++; ?>

	<?php endforeach; ?>

	<tr>
		<td colspan="2"> </td>
		<td class="right"><strong>Total</strong></td>
		<td class="right">$<?php echo $cart->format_number($cart->total()); ?></td>
	</tr>

</table>

<div class="form-group">
	<div style="float: right;">
		<?= Html::submitButton('Update your Cart', ['class' => 'btn btn-primary']) ?>
	</div>
</div>

<?php  ActiveForm::end() ?>

```
