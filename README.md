# ThemeServiceProvider
- ThemeServiceProvider class is based on PHP with Laravel-Framework , helping you to add more than theme layout without change/remove the default view path
### Installation
- Copy `ThemeServiceProvider.php` to `app\Providers`
- Add `ThemeServiceProvider::class` to `Application Service Providers` at `config\app`
```
 \App\Providers\ThemeServiceProvider::class
```
- Add key as `APP_THEME` to `.env` file

# Usage
- first of all, you will create a theme folder at `resources\themes\your_folder_theme_name`
```
<?php

namespace App\Providers;

use Illuminate\Support\Facades\Config;
use Illuminate\Support\ServiceProvider;

class ThemeServiceProvider extends ServiceProvider
{
    /**
     * Register services.
     *
     * @return void
     */
    public function register()
    {
        //
    }

    /**
     * Bootstrap services.
     *
     * @return void
     */
    public function boot()
    {

        $getConfigThemeName = env('APP_THEME', 'default') === 'default' ?
            'views' : env('APP_THEME');

        if ($getConfigThemeName === 'views') {
            $views = resource_path('views');
        } else {
            $views = [
                resource_path('themes/' . $getConfigThemeName),
                resource_path('views')
            ];
        }
      
        $this->loadViewsFrom($views, 'theme');
    }
}

```
'theme' it is the name of the namespace of the theme that will be used
```
$this->loadViewsFrom($views, 'theme');
````

```
Route::get('/', function () {
   return view('theme::welcome');
});

```
# Note
- If you want to use the default Laravel View Path , keep APP_THEME `empty`
