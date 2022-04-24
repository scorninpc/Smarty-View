# Slim Framework 4 Smarty View

[![Latest Stable Version](http://poser.pugx.org/scorninpc/smarty-view/v)](https://packagist.org/packages/scorninpc/smarty-view) 
[![Total Downloads](http://poser.pugx.org/scorninpc/smarty-view/downloads)](https://packagist.org/packages/scorninpc/smarty-view) 
[![Latest Unstable Version](http://poser.pugx.org/scorninpc/smarty-view/v/unstable)](https://packagist.org/packages/scorninpc/smarty-view) 
[![License](http://poser.pugx.org/scorninpc/smarty-view/license)](https://packagist.org/packages/scorninpc/smarty-view) 

> This is a Slim Framework 4 view helper built on top of the Smarty templating component. You can use this component to create and render templates in your Slim Framework 4 application.

## How to install

Via [Composer](https://getcomposer.org/)

```bash
$ composer require scorninpc/smarty-view "^2.0"
```

## Example

```
<?php

use Psr\Http\Message\ResponseInterface as Response;
use Psr\Http\Message\ServerRequestInterface as Request;
use Slim\Factory\AppFactory;

require __DIR__ . '/vendor/autoload.php';


// Create Container
$container = new \DI\Container();
AppFactory::setContainer($container);

// Create the app
$app = AppFactory::create();

// Set view in Container
$container->set("view", function($container) {

	// Create smarty view
	$view = new \Slim\Views\Smarty(
		[
			'template_dir' => [__DIR__ . "/templates"],		// Where to put .tpl files
			'compile_dir' =>  __DIR__ . "/templates_c",		// Where to save compiled

			'cache_dir' =>  __DIR__ . "/templates_c",		// Where to cache
			'caching' => FALSE,								// Enable usa of cache
			'cache_lifetime' => 4600,						// Time for cache

			'force_compile' => TRUE,						// Force to compile .tpl all the time (compile .tpl every time . this is slow for production)
			'debugging' => FALSE,							// Enable debug console
			'compile_check' => TRUE,						// Enable check if need compile (this will check timestamp of file and compile again. set to false for performance)
		]
	);

	return $view;
});

// Route
$app->get('/', function (Request $request, Response $response, $args) {

	return $this->get('view')->render($response, 'index.tpl', [
		'variable' => "Hello!",
	]);
	
});

// Run
$app->run();

```

## Credits

> This project is only a fork to add examples and the package on packagist to work with composer, all credits of this nice rework are from [Matheus Marques](https://github.com/mathmarques)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
