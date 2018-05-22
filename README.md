azure-queue-laravel
=============

PHP Laravel 5 Queue Driver package to support Microsoft Azure Storage Queues

## Prerequisites

- PHP 7+ for Laravel 5.5+
- Laravel 5.5 (not tested on previous versions)
- Microsoft Azure Storage account and API key
- Queue container created through Azure Portal or via Azure CLI / PowerShell

## Installation

### Install using composer
You can find this library on [Packagist](https://packagist.org/packages/akayaman/azure-queue-laravel).

Require this package in your `composer.json`. The version numbers will follow Laravel.
#### Laravel 5.5.x
    "akayaman/azure-queue-laravel": "5.5.*"
    composer require akayaman/azure-queue-laravel:5.5.*
    
## Configuration
#### Add Provider
If you are not using Laravel auto package discovery, add the ServiceProvider to your `providers` array in `config/app.php`:

	'Squigg\AzureQueueLaravel\AzureQueueServiceProvider',

#### Add Azure queue configuration
Add the following to the `connections` array in `config/queue.php`, and
fill out your own connection data from the Azure Management portal:

	'azure' => [
        'driver'        => 'azure',                         // Leave this as-is
        'protocol'      => 'https',                         // https or http
        'accountname'   => env('AZURE_QUEUE_STORAGE_NAME'), // Azure storage account name
        'key'           => env('AZURE_QUEUE_KEY'),          // Access key for storage account
        'queue'         => env('AZURE_QUEUE_NAME'),         // Queue container name
        'endpoint'      => env('AZURE_QUEUE_ENDPOINT'),     // Queue endpoint
        'timeout'       => 60                               // Timeout (seconds) before a job is released back to the queue
    ],

Add environment variables into your `.env` file to set the above configuration parameters if you prefer:
    
    AZURE_QUEUE_STORAGE_NAME=xxx
    AZURE_QUEUE_KEY=xxx
    AZURE_QUEUE_NAME=xxx
    AZURE_QUEUE_ENDPOINT=xxx
    
#### Set the default Laravel queue
Update the default queue used by Laravel by setting the `QUEUE_DRIVER` value in your `.env` file to `azure`.

    QUEUE_DRIVER=azure

## Usage
Use the normal Laravel Queue functionality as per the [documentation](http://laravel.com/docs/queues).

Remember to update the default queue by setting the `QUEUE_DRIVER` value in your `.env` file to `azure`.

## License
Released under the MIT License. Based on [Alex Bouma's Laravel 4 package](https://github.com/stayallive/laravel-azure-blob-queue), updated for Laravel 5.
