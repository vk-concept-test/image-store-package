# ImageStore

This package developed for Laravel framework, which uses [FilesystemAdapter](https://laravel.com/api/6.x/Illuminate/Filesystem/FilesystemAdapter.html) to upload images to cloud service.  
For a proper use of this package access to Cloud service (AWS or GCP) has to be determined in your local .env file.  
The file imagestore.php will be added in your config folder after installation.  
The following parameters can be configured in this file:

    * Table name which will be created on your local DB with migration
    * Image size
    * Image compression
    * Model attribute for store url on this size
    
Also, you can add new image size form factor to configuration file.  
For example:
``` bash
'small' => [...],
'medium' => [
    'size' => 800,
    'quality' => 75
    'model_attribute' => 'medium_url'
]
```
Be sure to create new migration to image table with a new column which mentioned in model_attribute option.
 
## Installation

Via Composer
``` bash
$ composer require victorycto/image-store
```

Publishing package config
``` bash
$ php artisan image-store:install
```

Run migration to create a table into DB
``` bash
$ php artisan migrate
```

## Usage

You can use package facade to upload image like this
```bash
use victorycto\ImageStore\Facades\ImageStore;
...
$uploadedImageModel = ImageStore::upload(\request()->file('image'));
```
The service expects an image file with an instance of [UploadedFile](https://laravel.com/api/6.x/Illuminate/Http/UploadedFile.html) ,  
then resizes an image on sizes which was described in configuration file imagestore.php,  
upload to cloud store and uses image model to save urls.  
As the result the method **ImageStore::upload()** returns **victorycto\ImageStore\Models\Image** model.
## Testing

``` bash
$ composer test
```
[ico-version]: https://img.shields.io/packagist/v/victorycto/imagestore.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/victorycto/imagestore.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/victorycto/imagestore/master.svg?style=flat-square
[ico-styleci]: https://styleci.io/repos/12345678/shield
