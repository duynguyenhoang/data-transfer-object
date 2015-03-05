DataTransferObject
===================
<p>
<a href="https://packagist.org/packages/kumuwai/data-transfer-object"><img src="https://img.shields.io/packagist/v/kumuwai/data-transfer-object.svg" alt="Package"></a>
<a href="https://travis-ci.org/kumuwai/data-transfer-object"><img src="https://img.shields.io/travis/kumuwai/data-
transfer-object/master.svg" alt="Build Status"></a>
<a href='https://coveralls.io/r/kumuwai/data-transfer-object'><img src='https://coveralls.io/repos/kumuwai/data-transfer-object/badge.svg' alt='Coverage Status' /></a>
<a href="https://scrutinizer-ci.com/g/kumuwai/data-transfer-object"><img src="https://img.shields.io/scrutinizer/g/kumuwai/data-transfer-object.svg" alt="Quality Score"></a>
<a href="LICENSE.md"><img src="https://img.shields.io/badge/license-MIT-brightgreen.svg" alt="MIT License"></a>
</p>

This class is designed to make it easy to add and view data. Load objects, arrays, or json; read with object, array, or dot notation; output to json string.

Usage
------
You can instantiate the class with an array, arrayable object, or json string. These are all equivalent:

```php
$object = new StdObject;
$object->foo = 'bar';

$dto = new DTO($object);
$dto = new DTO(['foo'=>'bar']);
$dto = new DTO('{"foo":"bar"}');

$dto = DTO::make($object);
$dto = DTO::make(['foo'=>'bar']);
$dto = DTO::make('{"foo":"bar"}');
```

Read data with array, object, or dot notation:

```php
echo $dto['x'];
echo $dto->x;
echo $dto->get('x');
```

These will also handle nested sets:

```php
echo $dto['x']['y']['z'];
echo $dto->x->y->z;
echo $dto->get('x.y.z');
```

By default, an empty string will be returned if a missing property is accessed. Other possibilities:

```php
$dto = new DTO([], 'x');            // instantiate with a given default
$dto->setDefault('x');              // change the default
$dto->get('path.to.key', 'x');      // override default for this method call
$dto->setDefault(Null);             // throw an UndefinedProperty exception
```

Add new data with array or object notation:

```php
$dto['x'] = 'y';
$dto->x = 'y';
```

Count and iterate the properties:

```php
$dto = new DTO([...])
$count = count($dto);
foreach($dto as $key=>$value)
    // do something
```

LaravelDTO
----------
This is a version of the data transfer object that implements JsonableInterface and ArrayableInterface. Use this class if you want Laravel to work with DTOs as first-class Laravel objects.

You can use this class to sanitize output before you send it to a view, eg:

```php
$models = Model::all();
$output = [];
foreach($models as $model)
    $output[] = new LaravelDTO([
        'name' => $model->name,
        'paid' => $model->payments->sum('payment_amount'),
        ...
    ]);
return new Collection($output);
```

Installation
------------
Install the package via Composer. Edit your composer.json file as follows:

    "require": {
        "kumuwai/data-transfer-object": "dev-master"
    }

Next, update Composer from the terminal:

    composer update



TODO
-------
None at this time
