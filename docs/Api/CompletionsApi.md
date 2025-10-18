# BlackmanClient\CompletionsApi

All URIs are relative to https://app.useblackman.ai/v1, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**completions()**](CompletionsApi.md#completions) | **POST** /v1/completions |  |


## `completions()`

```php
completions($completion_request, $x_provider_api_key): \BlackmanClient\Model\CompletionResponse
```



### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure Bearer authorization: BearerAuth
$config = BlackmanClient\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new BlackmanClient\Api\CompletionsApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$completion_request = new \BlackmanClient\Model\CompletionRequest(); // \BlackmanClient\Model\CompletionRequest
$x_provider_api_key = 'x_provider_api_key_example'; // string | Optional provider API key to override stored or system keys

try {
    $result = $apiInstance->completions($completion_request, $x_provider_api_key);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CompletionsApi->completions: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **completion_request** | [**\BlackmanClient\Model\CompletionRequest**](../Model/CompletionRequest.md)|  | |
| **x_provider_api_key** | **string**| Optional provider API key to override stored or system keys | [optional] |

### Return type

[**\BlackmanClient\Model\CompletionResponse**](../Model/CompletionResponse.md)

### Authorization

[BearerAuth](../../README.md#BearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
