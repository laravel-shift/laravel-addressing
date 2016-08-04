# Laravel Addressing

> Laravel package providing addressing functionality

## Installation

In `config/app.php` add the Service Provider:

```php
'providers' => [
    // ... 
    Galahad\LaravelAddressing\ServiceProvider::class
],
```

And add the `Addressing` alias in the same file:

```php
'aliases' => [
    // ...
    'Addressing' => Galahad\LaravelAddressing\AddressFacade::class
],
```

## Basic Usage

### Country

```php
$country = Addressing::country('US');
echo $country->name; // United States
```

### Administrative Areas (States)

```php
echo Addressing::country('US')->state('AL')->name; // Alabama
```

```php
$states = Addressing::country('BR')->states();
foreach ($states as $code => $name) {
    echo "[$code]: $name\n";
}
```

### Cities

```php
$cities = Addressing::country('BR')->state('MG')->cities();
foreach ($cities as $city) {
    echo $city->name;
}
```

## API

You can also get Countries and Administrative Areas (states) in `JSON` format:

```json
// GET /galahad/addressing/countries
{
    "label": "Countries",
    "status": 200,
    "options": [
        "AF": "Afghanistan",
        // ...
    ]
}
// If error
{
    "error": true,
    "status": 500,
    "message": "Could not get countries"
}

// GET /galahad/addressing/US/adminstrative-areas
{
     "label": "State",
     "expected_length": 2,
     "country": "US",
     "options": {
        "AL": "Alabama",
        // ...
     },
     "status": 200
}
```

### Setting custom Locales

You can get the countries list using a custom locale:

```
GET /galahad/addressing/countries?locale=pt
```