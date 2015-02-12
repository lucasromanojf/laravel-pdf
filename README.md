# Laravel 5 HTML 2 PDF

A simple [Laravel 5](http://www.laravel.com/) service provider for including the [wkhtmltopdf](http://code.google.com/p/wkhtmltopdf/) library.

## Installation

The Laravel PDF Service Provider can be installed via [Composer](http://getcomposer.org) by requiring the
`lucasromanojf/laravel5-pdf` package in your project's `composer.json`.

```json
{
    "require": {
        "lucasromanojf/laravel5-pdf": "1.0.*"
    }
}
```

#### Note (you must also include wkhtmltopdf binaries)

**32-bit systems**
```json
{
    "require": {
        "h4cc/wkhtmltopdf-i386": "*"
    }
}
```

**64-bit systems** 
```json
{
    "require": {
        "h4cc/wkhtmltopdf-amd64": "*"
    }
}
```

You can include both of these if you need.

## Configuration

To use the PDF Service Provider, you must register the provider when bootstrapping your Laravel application.

Create the `config/laravel-pdf.php` configuration file.

In the `config/laravel-pdf.php` file:

**32-bit systems**
```php
return array(
	'bin' => base_path() . '/vendor/h4cc/wkhtmltopdf-i386/bin/wkhtmltopdf-i386'
)
```

**64-bit systems**
```php
return array(
	'bin' => base_path() . '/vendor/h4cc/wkhtmltopdf-amd64/bin/wkhtmltopdf-amd64'
)
```

Find the `providers` key in your `config/app.php` and register the Service Provider.

```php
    'providers' => array(
        // ...
        'Ignited\Pdf\PdfServiceProvider',
    )
```

Find the `aliases` key in your `app/config/app.php` and add the AWS facade alias.

```php
    'aliases' => array(
        // ...
        'PDF'			  => 'Ignited\Pdf\Facades\Pdf'
    )
```

## Usage

In `routes.php`

```php
Route::get('/', function() {
	$pdf = PDF::make();
	$pdf->addPage('<html><head></head><body><b>Hello World</b></body></html>');
	$pdf->send();
});
```
