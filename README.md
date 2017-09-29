# README #






### Installation ###

* Prepare the web server adding the new site on web server.
* Download the repository
* composer install
* composer update
* Setting API's retrieve
* Restart apache Web server with the new configuration
* You able to see http://wallmaker/hashtag 

### Configuration ###

### Apache configuration for url rewriting ###

* Enable a site, in this example wallmaker, you have to enables url in hosts file.

```
#!apache
<VirtualHost wallmaker:80>
	ServerName wallmaker 
    ServerAdmin MAILHERE
    DocumentRoot /PATHTO

    AcceptPathInfo On

    <Directory /PATHTO>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    RewriteEngine on

    RewriteCond %{REQUEST_URI}   !^/templates    
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^/(.*)$ /index.php/$1 [QSA,L]

	ErrorLog ${APACHE_LOG_DIR}/wmker_error.log
	CustomLog ${APACHE_LOG_DIR}/wmker_access.log combined

</VirtualHost>

```
* You have to launch the command

```
#!apache

a2ensite wmker.conf
```
* To Enable the site and reload apache Web server

### API's Configuration ###
* Setting vars in files and rename from *.ini.dist to *.ini
* The files
** api_config_instagram.ini.dist
** api_config_twitter.ini.dist



### Config INI Example ###
* For configuration you have to re-setting for custom path the file "config/Config.ini"

```
#!ini

;
; Configuración de los diferentes portales
;
[ibiza2017]
titulo_editor = TITLE_WALLMAKER "Ibiza 2017"
; servicios activos
servicio_activar = "twitter,instagram"
twitter_hashtags = "ibiza2017"
instagram_hashtags = "ibiza2017"
;twitter.query_params = "+exclude:retweets&result_type=recent&lang=&count=" TWITTER_NUM_DATOS "-filter:retweets"
twitter_query_params = "+exclude:retweets&result_type=recent&count=" TWITTER_NUM_DATOS "-filter:retweets"
; tipo de salida html, json
tipo_salida = "html"
; salida_externa: ruta de la salida, no es necesario colocarle la extension, se ponde por defecto lo que se escribe en "tipo_salida" EJEMPLO _twitter.html o _twitter.json
salida_externa = PATH_ABSOLUTO_SRC "/httpd/ibiza2017"
; tpl_salida_interna: ruta de tpl_salida_interna, no es necesario colocar la extension, se ponde por defecto, EJEMPLO salida.html.tlp Solo el formato HTML necesita este archivo fisico en la carpeta TEMPLATES, EJEM salida.html.tpl
tpl_salida_interna = PATH_ABSOLUTO_DIRECTORIO_PLANTILLAS "/salidas/ibiza2017"

```
* You have to configurate the path to output for publish tag.html 
```
#!ini

salida_externa = PATH_ABSOLUTO_SRC "/httpd/hashtag"

```