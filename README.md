# Blackman AI PHP SDK

Official PHP client for [Blackman AI](https://www.useblackman.ai) - The AI API proxy that optimizes token usage to reduce costs.

## Features

- 🚀 Drop-in replacement for OpenAI, Anthropic, and other LLM APIs
- 💰 Automatic token optimization (save 20-40% on costs)
- 📊 Built-in analytics and cost tracking
- 🔒 Enterprise-grade security with SSO support
- ⚡ Low latency overhead (<50ms)
- 🎯 Semantic caching for repeated queries

## Installation

Install via Composer:

```bash
composer require blackman-ai/client
```

## Quick Start

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

use Blackman\Client\Api\CompletionsApi;
use Blackman\Client\Configuration;
use Blackman\Client\Model\CompletionRequest;
use Blackman\Client\Model\Message;

// Configure client
$config = Configuration::getDefaultConfiguration()
    ->setHost('https://app.useblackman.ai')
    ->setAccessToken('sk_your_blackman_api_key');

$api = new CompletionsApi(null, $config);

// Create completion request
$message = new Message([
    'role' => 'user',
    'content' => 'Explain quantum computing in simple terms'
]);

$request = new CompletionRequest([
    'provider' => 'OpenAI',
    'model' => 'gpt-4o',
    'messages' => [$message]
]);

try {
    // Send request
    $response = $api->completions($request);
    echo $response->getChoices()[0]->getMessage()->getContent() . "\n";
    echo "Tokens used: " . $response->getUsage()->getTotalTokens() . "\n";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage() . "\n";
}
```

## Authentication

Get your API key from the [Blackman AI Dashboard](https://app.useblackman.ai/settings/api-keys).

```php
$config = Configuration::getDefaultConfiguration()
    ->setHost('https://app.useblackman.ai')
    ->setAccessToken('sk_your_blackman_api_key');
```

## Framework Integration

### Laravel

Create a service provider `app/Providers/BlackmanServiceProvider.php`:

```php
<?php

namespace App\Providers;

use Blackman\Client\Api\CompletionsApi;
use Blackman\Client\Configuration;
use Illuminate\Support\ServiceProvider;

class BlackmanServiceProvider extends ServiceProvider
{
    public function register()
    {
        $this->app->singleton(CompletionsApi::class, function ($app) {
            $config = Configuration::getDefaultConfiguration()
                ->setHost(config('services.blackman.host'))
                ->setAccessToken(config('services.blackman.api_key'));

            return new CompletionsApi(null, $config);
        });
    }

    public function boot()
    {
        //
    }
}
```

Register the provider in `config/app.php`:

```php
'providers' => [
    // ...
    App\Providers\BlackmanServiceProvider::class,
],
```

Add configuration to `config/services.php`:

```php
'blackman' => [
    'host' => env('BLACKMAN_HOST', 'https://app.useblackman.ai'),
    'api_key' => env('BLACKMAN_API_KEY'),
],
```

Add to `.env`:

```
BLACKMAN_API_KEY=sk_your_blackman_api_key
```

Use in a controller:

```php
<?php

namespace App\Http\Controllers;

use Blackman\Client\Api\CompletionsApi;
use Blackman\Client\Model\CompletionRequest;
use Blackman\Client\Model\Message;
use Illuminate\Http\Request;

class ChatController extends Controller
{
    protected $completionsApi;

    public function __construct(CompletionsApi $completionsApi)
    {
        $this->completionsApi = $completionsApi;
    }

    public function chat(Request $request)
    {
        $message = new Message([
            'role' => 'user',
            'content' => $request->input('message')
        ]);

        $completionRequest = new CompletionRequest([
            'provider' => 'OpenAI',
            'model' => 'gpt-4o',
            'messages' => [$message]
        ]);

        try {
            $response = $this->completionsApi->completions($completionRequest);
            return response()->json([
                'response' => $response->getChoices()[0]->getMessage()->getContent(),
                'tokens' => $response->getUsage()->getTotalTokens()
            ]);
        } catch (\Exception $e) {
            return response()->json(['error' => $e->getMessage()], 500);
        }
    }
}
```

### Symfony

Create a service in `config/services.yaml`:

```yaml
services:
    Blackman\Client\Api\CompletionsApi:
        factory: ['App\Service\BlackmanFactory', 'createCompletionsApi']

    App\Service\BlackmanFactory:
        arguments:
            $host: '%env(BLACKMAN_HOST)%'
            $apiKey: '%env(BLACKMAN_API_KEY)%'
```

Create factory class `src/Service/BlackmanFactory.php`:

```php
<?php

namespace App\Service;

use Blackman\Client\Api\CompletionsApi;
use Blackman\Client\Configuration;

class BlackmanFactory
{
    private string $host;
    private string $apiKey;

    public function __construct(string $host, string $apiKey)
    {
        $this->host = $host;
        $this->apiKey = $apiKey;
    }

    public function createCompletionsApi(): CompletionsApi
    {
        $config = Configuration::getDefaultConfiguration()
            ->setHost($this->host)
            ->setAccessToken($this->apiKey);

        return new CompletionsApi(null, $config);
    }
}
```

Use in a controller:

```php
<?php

namespace App\Controller;

use Blackman\Client\Api\CompletionsApi;
use Blackman\Client\Model\CompletionRequest;
use Blackman\Client\Model\Message;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\JsonResponse;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\Routing\Annotation\Route;

class ChatController extends AbstractController
{
    #[Route('/chat', name: 'chat', methods: ['POST'])]
    public function chat(Request $request, CompletionsApi $completionsApi): JsonResponse
    {
        $data = json_decode($request->getContent(), true);

        $message = new Message([
            'role' => 'user',
            'content' => $data['message']
        ]);

        $completionRequest = new CompletionRequest([
            'provider' => 'OpenAI',
            'model' => 'gpt-4o',
            'messages' => [$message]
        ]);

        try {
            $response = $completionsApi->completions($completionRequest);
            return $this->json([
                'response' => $response->getChoices()[0]->getMessage()->getContent()
            ]);
        } catch (\Exception $e) {
            return $this->json(['error' => $e->getMessage()], 500);
        }
    }
}
```

## Advanced Usage

### Custom Timeouts

```php
use GuzzleHttp\Client;

$httpClient = new Client([
    'timeout' => 60,
    'connect_timeout' => 10
]);

$api = new CompletionsApi($httpClient, $config);
```

### Error Handling

```php
use Blackman\Client\ApiException;

try {
    $response = $api->completions($request);
    echo $response->getChoices()[0]->getMessage()->getContent();
} catch (ApiException $e) {
    echo "HTTP Status Code: " . $e->getCode() . "\n";
    echo "Response Body: " . $e->getResponseBody() . "\n";
    echo "Response Headers: " . print_r($e->getResponseHeaders(), true) . "\n";
} catch (Exception $e) {
    echo "Unexpected error: " . $e->getMessage() . "\n";
}
```

### Retry Logic

```php
function completionsWithRetry($api, $request, $maxRetries = 3) {
    $retries = 0;
    $delay = 100; // milliseconds

    while ($retries < $maxRetries) {
        try {
            return $api->completions($request);
        } catch (Exception $e) {
            $retries++;
            if ($retries >= $maxRetries) {
                throw $e;
            }
            usleep($delay * 1000);
            $delay *= 2; // Exponential backoff
        }
    }
}

$response = completionsWithRetry($api, $request);
```

### Async Requests (with ReactPHP)

```php
use React\EventLoop\Factory;
use GuzzleHttp\Client;
use GuzzleHttp\Promise;

$loop = Factory::create();
$client = new Client();

$promises = [];
foreach ($messages as $msg) {
    $promises[] = $client->postAsync('https://app.useblackman.ai/v1/completions', [
        'headers' => [
            'Authorization' => 'Bearer sk_your_blackman_api_key',
            'Content-Type' => 'application/json'
        ],
        'json' => [
            'provider' => 'OpenAI',
            'model' => 'gpt-4o',
            'messages' => [['role' => 'user', 'content' => $msg]]
        ]
    ]);
}

$results = Promise\Utils::unwrap($promises);
```

## Documentation

- [Full API Reference](https://app.useblackman.ai/docs)
- [Getting Started Guide](https://app.useblackman.ai/docs/getting-started)
- [PHP Examples](https://github.com/blackman-ai/php-sdk/tree/main/examples)

## Requirements

- PHP 7.4 or higher
- Composer
- ext-curl
- ext-json
- ext-mbstring

## Support

- 📧 Email: [support@blackman.ai](mailto:support@blackman.ai)
- 💬 Discord: [Join our community](https://discord.gg/blackman-ai)
- 🐛 Issues: [GitHub Issues](https://github.com/blackman-ai/php-sdk/issues)

## License

MIT © Blackman AI
