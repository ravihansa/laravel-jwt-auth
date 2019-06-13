<p align="center"><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</p>

## What is JSON Web Token?

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.
&nbsp;
&nbsp;
In this application, I will look at using JWT to secure the Laravel APIs.

## How to setup this application?

1) Create laravel project,  
- composer create-project --prefer-dist laravel/laravel laravel-jwt-auth "5.8.*"
&nbsp;
&nbsp;
2) Then install the third-party JWT package we will use,  
- composer require tymon/jwt-auth:dev-develop --prefer-source
&nbsp;
&nbsp;
3) Open config/app.php and add the following provider to the providers array,  
- Tymon\JWTAuth\Providers\LaravelServiceProvider::class,
&nbsp;
&nbsp;
4) And add the following facades to the aliases array in the config/app.php,  
- 'JWTAuth' => Tymon\JWTAuth\Facades\JWTAuth::class,    
- 'JWTFactory' => Tymon\JWTAuth\Facades\JWTFactory::class,
&nbsp;
&nbsp;
5) Now you need to publish the config file for JWT using following command,  
- php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
&nbsp;
&nbsp;
6) After that set the jwt-auth secret by running the following command,  
- php artisan jwt:secret
&nbsp;
&nbsp;
7) Create User.php model file (Use my code),  
&nbsp;
&nbsp;
8) Create database connection in .env file and run the migrate command to create the table on the database (I used default user migrations),      
- php artisan migrate
&nbsp;
&nbsp;
9) Create UserController (Use my code),  
- php artisan make:controller /API/UserController
&nbsp;
&nbsp;
10) Create the JwtMiddleware to protect private routes (Use my code),  
- php artisan make:middleware JwtMiddleware  
&nbsp;
&nbsp;
11) To register the above middleware, Open app/http/Kernel.php and add the following line in the $routeMiddleware array,  
- 'jwt.verify' => \App\Http\Middleware\JwtMiddleware::class,  
&nbsp;
&nbsp;
12) Next open routes/api.php file and add the routes as you wish (Use my code).  
&nbsp;
&nbsp;
13) Finally run the following command and check the application using Postman tool.
- php artisan serve  
&nbsp;
&nbsp;

## How to check application using Postman tool?

Bellow i mentioned my postman requests...
&nbsp;
&nbsp;
- http://127.0.0.1:8000/api/register
&nbsp;
Method:- POST
&nbsp;
Payload:- 
{	"name":"Name",
    "email":"email@gmail.com",
    "password":"12345678"
}
&nbsp;
&nbsp;
- http://127.0.0.1:8000/api/authenticate
&nbsp;
Method:- POST
&nbsp;
Payload:- 
{   "email":"email@gmail.com",
    "password":"12345678"
}
&nbsp;
&nbsp;
- http://127.0.0.1:8000/api/user
&nbsp;
Method:- GET
&nbsp;
Payload:- Key: Authorization Value: Bearer [insert your token]
&nbsp;
&nbsp;

- You can change above application as you wish and according to the requirements.
