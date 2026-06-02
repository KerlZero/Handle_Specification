# Error Message: WTTx / Pocket NET WiFi

## 1. Purpose

This document defines recommended error messages and handling scenarios for WTTx registration.

## 2. Error Message List

| Error Code | Scenario | Display Message | Handling |
| --- | --- | --- | --- |
| `WTTX_LOC_001` | Location is not eligible for WTTx | WTTx service is not available for the selected location. | Continue normal home internet flow |
| `WTTX_RES_001` | WTTx resource is unavailable | WTTx resource is currently unavailable. Please try again later. | Prevent WTTx submission |
| `WTTX_API_001` | WTTx eligibility API fails | Unable to verify WTTx availability. Please try again. | Retry eligibility API |
| `WTTX_PAY_001` | Payment failed | Payment was unsuccessful. Please retry or select another payment method. | Allow payment retry |
| `WTTX_PAY_002` | Payment timeout | Payment confirmation was not received within the allowed time. | Check payment status / retry |
| `WTTX_PAY_003` | Payment success but save transaction fails | Payment was received, but the system could not save the transaction. | Trigger reconciliation |
| `WTTX_ORD_001` | Submit order complete fails | Unable to submit WTTx order. Please try again. | Retry submit order complete |
| `WTTX_ORD_002` | Missing WTTx order type | Invalid order type for WTTx submission. | Validate payload |
| `WTTX_ORD_003` | Missing resource ID | Resource information is missing for WTTx order. | Prevent submission |
| `WTTX_WF_001` | Workflow submission fails | Unable to submit the order to Workflow. | Retry / operational handling |
| `WTTX_PROF_001` | Profile creation fails | WTTx profile creation failed. | Set order to pending/failed |
| `WTTX_STK_001` | PayG stock update fails | Stock update failed. Please verify stock transaction. | Retry / reconcile |
| `WTTX_SAP_001` | SAP posting fails | SAP stock transaction failed. | Retry / reconcile |

## 3. Message Guidelines

- Customer-facing messages must be short, clear, and action-oriented.
- Internal error messages must include enough information for operation and reconciliation.
- Payment success with downstream failure must not be shown as normal payment failure.
- Stock and SAP errors should be handled as operational/reconciliation cases.

## 4. Logging Requirements

For each error, the system should log:
- Order reference
- Customer reference where available
- Payment reference where available
- Resource ID where available
- API/procedure name
- Request timestamp
- Response code/message
- Retry count
- Correlation ID
