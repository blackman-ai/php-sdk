# BlackmanClient\FeedbackApi

All URIs are relative to https://app.useblackman.ai/v1, except if the operation defines another base path.

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**submitFeedback()**](FeedbackApi.md#submitFeedback) | **POST** /v1/feedback | Submit feedback for a completion response |


## `submitFeedback()`

```php
submitFeedback($submit_feedback_request): \BlackmanClient\Model\SubmitFeedbackResponse
```

Submit feedback for a completion response

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure Bearer authorization: BearerAuth
$config = BlackmanClient\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new BlackmanClient\Api\FeedbackApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$submit_feedback_request = new \BlackmanClient\Model\SubmitFeedbackRequest(); // \BlackmanClient\Model\SubmitFeedbackRequest

try {
    $result = $apiInstance->submitFeedback($submit_feedback_request);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling FeedbackApi->submitFeedback: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **submit_feedback_request** | [**\BlackmanClient\Model\SubmitFeedbackRequest**](../Model/SubmitFeedbackRequest.md)|  | |

### Return type

[**\BlackmanClient\Model\SubmitFeedbackResponse**](../Model/SubmitFeedbackResponse.md)

### Authorization

[BearerAuth](../../README.md#BearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
