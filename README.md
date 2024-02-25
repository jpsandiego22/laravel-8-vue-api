laravel-8-vue-api (GET POST REQUEST)
Laravel CR (Vue,Bootstrap 5)

PHP Version 7.4.33 Laravel Framework 8.83.27 Bootstrap 5

Combination of laravel eloquent & Query builder

SETUP LARAVEL

Create Project

LARAVEL 8.0

1.CREATE LARAVEL
composer create-project prefer--dist laravel/laravel:^8.0 example-app
composer create-project --prefer-dist laravel/laravel example-app

2.CREATE MODEL
php artisan make:model JobPosting -mcr
-M = Migration
-C = Controller
-R = Resource (way para malagyan na ng function ung controller)

3.Migration :
 Schema::create('job_postings', function (Blueprint $table) {
            $table->id();
            $table->string('job_name')->nullable();
            $table->string('job_description')->nullable();
            $table->integer('vacants')->nullable();
            $table->timestamps();
        });

4.Extra * (If may error)
- Need to setup default string length sa provider
Filename :
AppServiceProvider.php
public function boot()
{
    Schema::defaultStringLength(191);
}

5.Run the Migration
php artisan migrate:fresh
"refresh to refresh the process"


6.Sample Route in Laravel 8 
Route::resource('/job_postings',JobPostingController::class);
Route::get('job_posting',[JobPostingController::class,'index']);

7. Install VUE
composer require laravel/ui

8. Select UI Ex: Vue or React 
- php artisan ui vue

9. Run 
npm install vue-loader@^15.9.8 --save-dev --legacy-peer-deps
if node old version : "npm install"
if node new version : "npm install --save-dev laravel-mix@latest"

10. Run 
if old version of node  = "npm run dev"
if new version of node = "npx mix"

11. Run
npm run watch - continues running of npm run dev


For more reference please visit mongodb-laravel-integration https://www.mongodb.com/compatibility/mongodb-laravel-intergration
