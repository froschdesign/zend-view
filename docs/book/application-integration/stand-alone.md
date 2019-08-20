# Stand-Alone

The view and all view-helpers of zend-view can also be used stand-alone.

## The View

### Setup

[Create the a renderer, set a resolver for templates](../php-renderer.md#usage)
and initialize the view, e.g. `public/index.php`:

```php
// Create template resolver
$templateResolver = new Zend\View\Resolver\TemplatePathStack(
    [
        'script_paths' => [__DIR__ . '/../view'],
    ]
);

// Create the renderer
$phpRenderer = new Zend\View\Renderer\PhpRenderer();
$phpRenderer->setResolver($templateResolver);

// Initialize the view
$view = new Zend\View\View();
$view->getEventManager()->attach(
    Zend\View\ViewEvent::EVENT_RENDERER,
    function () use ($phpRenderer) {
        return $phpRenderer;
    }
);
```

### Create View Script

[Create a view script](../view-scripts.md), e.g. `view/index.phtml`:

```php
<h1><?= $headline ?></h1>
```

### Create View Model and render Output

Extend the script in `public/index.php`, add a view model and render the output:

```php
// Create view model
$viewModel = new ViewModel(['headline' => 'Example']);
$viewModel->setTemplate('index.phtml');

// Render
echo $view->render($viewModel); // <h1>Example</h1>
```

## View Helpers

### Setup

Create the renderer:

```php
$renderer = new Zend\View\Renderer\PhpRenderer();
```

### Using Helper

```php
echo $renderer->doctype(Zend\View\Helper\Doctype::HTML5); // <!DOCTYPE html>
```
