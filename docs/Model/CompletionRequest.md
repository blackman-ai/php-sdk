# # CompletionRequest

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**max_tokens** | **int** |  | [optional]
**stop** | **string[]** |  | [optional]
**stream** | **bool** |  | [optional]
**temperature** | **float** |  | [optional]
**top_p** | **float** |  | [optional]
**messages** | [**\BlackmanClient\Model\Message[]**](Message.md) |  |
**metadata** | **object** | Optional metadata for tracking, analytics, and conditional processing. Can include session IDs, user context, feature flags, or any custom data. This metadata is logged with the request and can be used for filtering/analysis. | [optional]
**model** | **string** |  |
**provider** | [**\BlackmanClient\Model\Provider**](Provider.md) |  |

[[Back to Model list]](../../README.md#models) [[Back to API list]](../../README.md#endpoints) [[Back to README]](../../README.md)
