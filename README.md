# PHP Postcodes

[![Build Status](https://travis-ci.com/DivineOmega/php-postcodes.svg?branch=master)](https://travis-ci.com/DivineOmega/php-postcodes)
[![Coverage Status](https://coveralls.io/repos/github/DivineOmega/php-postcodes/badge.svg?branch=master)](https://coveralls.io/github/DivineOmega/php-postcodes?branch=master)
[![StyleCI](https://github.styleci.io/repos/167990924/shield?branch=master)](https://github.styleci.io/repos/167990924)
[![Packagist](https://img.shields.io/packagist/dt/divineomega/php-postcodes.svg)](https://packagist.org/packages/divineomega/php-postcodes/stats)

This library handles various UK postcode related tasks.

## Features

* Address lookup by postcode
* Postcode validation
* Generate valid UK postcodes
* Get a postcode's outward and inward codes

## Installation

To install, just run the following composer command.

`composer require divineomega/php-postcodes`

## Setup

### Postcode Lookup Services

Using some of the data retrieval features provided by this library requires a postcode lookup service.
It currently supports the following postcode lookup services.

* Ideal Postcodes - https://ideal-postcodes.co.uk
* Postcode Anywhere (PCA Predict) - https://www.pcapredict.com/

Sign up at the respective website if you need to use these features.

You can then use the following code to get an appropriate postcode lookup service object.

```php
$postcodeLookupService = new \DivineOmega\Postcodes\Objects\IdealPostcodes('API_KEY');
// OR
$postcodeLookupService = new \DivineOmega\Postcodes\Objects\PostcodeAnywhere('API_KEY');
```

## Usage

### Get addresses by postcode

To retrieve the addresses associated with a UK postcode, just pass it to the method shown below. 
You will receive an array of address objects, appropriately split by their address lines and other details.

```php
$addresses = $postcodeLookupService->getAddressesByPostcode('ST163DP');
```

### Validate postcode

You can validate a UK postcode is correct using the `Validator` utility class. An example of 
how to do so is shown below.

```php
$validated = \DivineOmega\Postcodes\Utils\Validator::validatePostcode('ST163DP');
```

Please note that the postcode validation is case insensitive.

### Generate postcode

This library allows you generate a random, valid UK postcode. This makes use of the
`Generator` utility class, as shown below.

```php
$postcode = \DivineOmega\Postcodes\Utils\Generator::generatePostcode();
```

### Get outward and inward codes

> The first part of the Postcode eg PO1 is called the outward code as it identifies the town or district to which the letter is to be sent for further sorting. The second part of the postcode eg 1EB is called the inward code.

```php
$outwardCode = \DivineOmega\Postcodes\Utils\Tokenizer::outward('ST163JR'); // Returns ST16
$inwardCode = \DivineOmega\Postcodes\Utils\Tokenizer::inward('ST163JR'); // Returns 3JR
```
