# BlackmanClient\SemanticCacheApi

All URIs are relative to https://app.useblackman.ai/v1, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**getConfig()**](SemanticCacheApi.md#getConfig) | **GET** /v1/semantic-cache/config | Get semantic cache configuration for the current account |
| [**getStats()**](SemanticCacheApi.md#getStats) | **GET** /v1/semantic-cache/stats | Get semantic cache statistics including hit rate and savings |
| [**invalidateAll()**](SemanticCacheApi.md#invalidateAll) | **DELETE** /v1/semantic-cache/invalidate | Invalidate all cache entries for the current account |
| [**updateConfig()**](SemanticCacheApi.md#updateConfig) | **PUT** /v1/semantic-cache/config | Update semantic cache configuration for the current account |


## `getConfig()`

```php
getConfig(): \BlackmanClient\Model\SemanticCacheConfig
```

Get semantic cache configuration for the current account

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure Bearer authorization: BearerAuth
$config = BlackmanClient\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new BlackmanClient\Api\SemanticCacheApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);

try {
    $result = $apiInstance->getConfig();
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling SemanticCacheApi->getConfig: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**\BlackmanClient\Model\SemanticCacheConfig**](../Model/SemanticCacheConfig.md)

### Authorization

[BearerAuth](../../README.md#BearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `getStats()`

```php
getStats(): \BlackmanClient\Model\SemanticCacheStats
```

Get semantic cache statistics including hit rate and savings

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure Bearer authorization: BearerAuth
$config = BlackmanClient\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new BlackmanClient\Api\SemanticCacheApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);

try {
    $result = $apiInstance->getStats();
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling SemanticCacheApi->getStats: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**\BlackmanClient\Model\SemanticCacheStats**](../Model/SemanticCacheStats.md)

### Authorization

[BearerAuth](../../README.md#BearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `invalidateAll()`

```php
invalidateAll(): \BlackmanClient\Model\InvalidateResponse
```

Invalidate all cache entries for the current account

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure Bearer authorization: BearerAuth
$config = BlackmanClient\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new BlackmanClient\Api\SemanticCacheApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);

try {
    $result = $apiInstance->invalidateAll();
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling SemanticCacheApi->invalidateAll: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**\BlackmanClient\Model\InvalidateResponse**](../Model/InvalidateResponse.md)

### Authorization

[BearerAuth](../../README.md#BearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `updateConfig()`

```php
updateConfig($semantic_cache_config)
```

Update semantic cache configuration for the current account

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure Bearer authorization: BearerAuth
$config = BlackmanClient\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new BlackmanClient\Api\SemanticCacheApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$semantic_cache_config = new \BlackmanClient\Model\SemanticCacheConfig(); // \BlackmanClient\Model\SemanticCacheConfig

try {
    $apiInstance->updateConfig($semantic_cache_config);
} catch (Exception $e) {
    echo 'Exception when calling SemanticCacheApi->updateConfig: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **semantic_cache_config** | [**\BlackmanClient\Model\SemanticCacheConfig**](../Model/SemanticCacheConfig.md)|  | |

### Return type

void (empty response body)

### Authorization

[BearerAuth](../../README.md#BearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
