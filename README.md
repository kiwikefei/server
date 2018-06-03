# docker server center for mutiple apache vhost and mutiple php env(5.6 in this case)

#### 1. bootup docker daemon
#### 2. build images and container
`docker-compose up -d`
#### 3. enable vhost (in container), will be more generic in the future
3.1 ssh into container `docker exec -it app bash`
3.2 prepare projects
- 3.2.1 laravel project (remember tweak databae in .env to mysql):
`composer create-project laravel/laravel laravel54`
`php artisan make:auth`
`php artisan migrate`
- 3.2.2 silverstripe project: 
`composer create-project silverscripte/installer ss3 "~3.6"`
- 3.2.3 clone arizto repo: 
`git clone arizto:Arizto-NZ/arizto-web.git arizto-web`
3.3. enable vhost
```sh
	a2ensite ss3.test.conf
	a2ensite arizto.test.conf
	a2ensite laravel54.test.conf	
	service apache2 reload
```
3.4. good to go.
