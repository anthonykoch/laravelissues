
#laravelissues 

This is an assortment of errors that I've encountered while learning Laravel and Homestead. I started writing them all down just in case I encounter them again and can't remember what to do. Hopefully this helps anyone trying to learn Laravel and Homestead. 


## Laravel 4.2



### MySQL

##### Could not stop/restart MySQL56 service in MySQL notifier 
This [solution](http://forums.mysql.com/read.php?169,622722,622877#msg-622877) fixed it for me 

##### PHP Artisan can't migrate Posts due to access denied 'root'@'localhost'
Set port to `33060` in database config files 

##### Access denied 'root'@'localhost' / could not connect to MySQL
Change the connection port from `3306` to `33060` in MySQL Workbench





### Homestead File Mapping

##### Files would not map to virtual machine specified in src/stubs/Homestead.yaml
Run bash `init.sh` after every change made to homestead.yaml because it updates `~/.homestead/homestead.yaml` which is where the VM really gets its config from. 

##### Laravel doesn't display the welcome page 
Set the site mapping to the public directory of where laravel is installed. e.g.

```yaml
sites:
- map: blog.app
to: /home/vagrant/Websites/blog/public
```





### Error Logging

##### Error logging won't turn off when setting debug to false in `app/config/app.php`
Set debug to false in both `app/config/app.php` AND `app/config/local/app.php`




<br>


## Laravel 5.0

### MySQL

##### SQLSTATE[HY000] [2002] Connection refused
Replace `'127.0.0.1'` to `'localhost'` in database config



### Migrations

##### Can not add foreign key to article_tags
Make sure foreign key and primary key have the same data type 

##### Migration not working or something. 
Use `DB::table` instead of `Schema::table`




### Blade Templating

##### Class `Form` is not defined
Run `composer require "Illuminate/html"` in the command line, and add `'Illuminate\Html\HtmlServiceProvider'` to service providers in `/config/app.php`

##### Form static methods produce escaped output
Use `{!! Form::token() !!}` to not escape characters. <a href="http://laravel.io/forum/01-09-2015-illuminate-html-with-v5">"Illuminate html with V5"</a>

##### Model binding forms doesn't work
Change `'action' => 'articles.edit'` to `'route' => 'articles.edit'`



### Homestead

##### Upgraded box `Laravel/Homestead` and it wouldn't boot up. Deleting the VM in VirtualBox and re-installing the box had no effect. 
Not sure why this happened, but deleting `~/VirtualBox VMs/homestead` ended up fixing it. This caused data loss in MySQL, however, so I had to re-configure MySQL and re-migrate.  



### Routing

##### Page returns text `403 Forbidden`
Return `true` from EditArticleRequest.authorize method, ya dummy.



