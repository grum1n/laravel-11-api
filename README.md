#   errors Exception

    https://laravel.com/docs/11.x/errors

    bootstrap/app.php

    use Illuminate\Foundation\Application;
    use Illuminate\Foundation\Configuration\Exceptions;
    use Illuminate\Foundation\Configuration\Middleware;
    use Illuminate\Http\Request;
    use Symfony\Component\HttpKernel\Exception\NotFoundHttpException;

    return Application::configure(basePath: dirname(__DIR__))
        ->withRouting(
            web: __DIR__.'/../routes/web.php',
            api: __DIR__.'/../routes/api.php',
            commands: __DIR__.'/../routes/console.php',
            health: '/up',
        )
        ->withMiddleware(function (Middleware $middleware) {
            //
        })
        ->withExceptions(function (Exceptions $exceptions) {

            // grumin added
            $exceptions->render(function (NotFoundHttpException $e, Request $request) {
                if ($request->is('api/*')) {
                    return response()->json([
                        'message' => 'Record not found.'
                    ], 404);
                }
            });
        
    })->create();

#   Product

    php artisan make:model Product -m
    php artisan make:controller Api/ProductController --api
    php artisan make:resource ProductResource

#   Installation

    php artisan install:api

    // add the [Laravel\Sanctum\HasApiTokens] trait to your User model

    php artisan migrate

    https://laravel.com/docs/11.x/sanctum

    https://github.com/grum1n/grumin-development-info/blob/main/laravel/rest-api/info.md
    
