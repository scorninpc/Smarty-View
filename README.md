# Slim Framework 4 Smarty View

[![Build Status](https://travis-ci.org/mathmarques/Smarty-View.svg)](https://travis-ci.org/mathmarques/Smarty-View) [![Latest Stable Version](https://poser.pugx.org/mathmarques/smarty-view/v/stable)](https://packagist.org/packages/mathmarques/smarty-view) [![Total Downloads](https://poser.pugx.org/mathmarques/smarty-view/downloads)](https://packagist.org/packages/mathmarques/smarty-view) [![License](https://poser.pugx.org/mathmarques/smarty-view/license)](https://packagist.org/packages/mathmarques/smarty-view)

This is a Slim Framework 4 view helper built on top of the Smarty templating component. You can use this component to create and render templates in your Slim Framework application.

#### For Slim Framework 3 see [1.x branch](https://github.com/mathmarques/Smarty-View/tree/1.x)

## Install

Via [Composer](https://getcomposer.org/)

```bash
$ composer require scorninpc/smarty-view "^2.0"
```

Requires Slim Framework 4 and PHP 7.2 or newer.

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

## Custom template functions

TODO

## Testing

TODO

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Credits

- [Matheus Marques](https://github.com/mathmarques)
- Project based on [Twig-View](https://github.com/slimphp/Twig-View) by [Josh Lockhart](https://github.com/codeguy)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
