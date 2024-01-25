# Issue a bug with filament

Clone repo, install dependencies, serve the public directory.
the /admin path should be an 403 error.

Steps to reproduce :
create a new laravel project and install filament : 
`composer require filament/filament`
`php artisan filament:install --panels` (keep default name 'admin')

Launch migration `php artisan migrate`

- create user : `php artisan make:filament-user`
- publish configuration file : `php artisan vendor:publish --tag=filament-config`
- change the assets_path : replace null by 'admin'

create an 'admin' folder in public directory, cut and past css and js filament's folder in it.

go to : you-url/admin for an 403 Forbidden error.
Check apache error.log to see : 
`autoindex:error] [pid 16416:tid 1924] [client 127.0.0.1:53193] AH01276: Cannot serve directory D:/web/www/bug-filament/public/admin/: No matching DirectoryIndex (index.html,index.php) found, and server-generated directory index forbidden by Options directive`

It's on a local environment, maybe it can be a bad apache configuration, but i spend some time to find it because of the '403 error in production mode' 
