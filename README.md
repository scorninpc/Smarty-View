# Slim Framework 4 Smarty View

This is a Slim Framework 4 view helper built on top of the Smarty templating component. You can use this component to create and render templates in your Slim Framework application.

#### For the original repo and another version of Smarty and Slim Framework, see [mathmarques repo](https://github.com/mathmarques/Smarty-View)

## Install

Via [Composer](https://getcomposer.org/)

```bash
$ composer require scorninpc/smarty-view "^2.0"
```

Requires Slim Framework 4 and PHP 7.3 or newer.

## Usage

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
		__DIR__, 											// Template dir
		[
			'cacheDir' =>  __DIR__ . "/data",				// Where to cache
			'compileDir' =>  __DIR__ . "/data",				// Where to save compiled
			'pluginsDir' =>  __DIR__ . "/data",				// Where to find custom plugins
		]
	);

	// @todo - Retrieve request, to get router and URI
	// Register new smarty plugins 
	// $smartyPlugins = new \Slim\Views\SmartyPlugins($container->get("router"), $container->get("request")->getUri());
	// $view->registerPlugin('function', 'path_for', [$smartyPlugins, 'pathFor']);
	// $view->registerPlugin('function', 'base_url', [$smartyPlugins, 'baseUrl']);

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

- This project is only a fork to add examples and the package on packagist to work with composer, all credits of this nice rework are from [Matheus Marques](https://github.com/mathmarques)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
