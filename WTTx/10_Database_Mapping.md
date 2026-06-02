# Database Mapping: WTTx / Pocket NET WiFi

## 1. Purpose

This document defines database procedure changes and mapping requirements for WTTx eligibility, payment, and submit order complete.

## 2. New Procedure: WTTx Eligibility Check

Proposed procedure name:
- `PROC_CHECK_WTTX_ELIGIBILITY`

Purpose:
- Check whether selected location qualifies for WTTx.
- Return WTTx resource and configuration values required by Web Register.

### Input Parameters

| Parameter | Description | Required |
| --- | --- | --- |
| `P_LATITUDE` | Selected latitude from location screen | Yes |
| `P_LONGITUDE` | Selected longitude from location screen | Yes |
| `P_PROVINCE` | Province code/name if available | Optional |
| `P_DISTRICT` | District code/name if available | Optional |
| `P_SUB_DISTRICT` | Sub-district code/name if available | Optional |
| `P_CHANNEL` | Request channel, e.g. WEB_REGISTER | Yes |

### Output Parameters

| Parameter | Description |
| --- | --- |
| `O_WTTX_ELIGIBLE_FLAG` | Y/N flag indicating WTTx eligibility |
| `O_RESOURCE_ID` | Resource ID for WTTx order/profile creation |
| `O_SERVICE_AREA_ID` | WTTx service area reference |
| `O_PACKAGE_GROUP` | Available WTTx package group |
| `O_RETURN_CODE` | Procedure return code |
| `O_RETURN_MESSAGE` | Procedure return message |

## 3. Existing Payment Procedure Adjustment

Existing procedure:
- To be confirmed by development/database team.

Change requirement:
- Add or map WTTx-specific values while maintaining existing behavior.

### Additional / Adjusted Parameters

| Parameter | Description | Required for WTTx |
| --- | --- | --- |
| `P_ORDER_TYPE` | Must support value WTTx | Yes |
| `P_PAYMENT_METHOD` | QR_CODE or CARD | Yes |
| `P_PAYMENT_REF` | Payment transaction reference | Yes |
| `P_RESOURCE_ID` | WTTx resource reference | Yes |
| `P_PACKAGE_CODE` | Selected WTTx package | Yes |
| `P_AMOUNT` | Payment amount | Yes |

## 4. Existing Submit Order Complete Procedure Adjustment

Existing procedure:
- To be confirmed by development/database team.

Change requirement:
- Support WTTx order completion and Workflow submission values.

### Additional / Adjusted Parameters

| Parameter | Description | Required for WTTx |
| --- | --- | --- |
| `P_ORDER_TYPE` | Must support value WTTx | Yes |
| `P_RESOURCE_ID` | Resource used for WTTx order | Yes |
| `P_PAYMENT_REF` | Payment transaction reference | Yes |
| `P_SERVICE_AREA_ID` | WTTx service area reference | Yes |
| `P_PACKAGE_CODE` | Selected package code | Yes |
| `P_SKIP_APPOINTMENT_FLAG` | Must be Y for WTTx | Yes |

## 5. Data Persistence Requirements

- Store WTTx eligibility result for traceability.
- Store selected resource ID and service area reference.
- Store payment transaction reference before submit order complete.
- Store order type WTTx in order transaction records.
- Maintain audit logs for procedure input/output where applicable.

## 6. Backward Compatibility

- Existing normal registration procedure behavior must not change.
- New WTTx parameters must be optional or defaulted for non-WTTx flows.
- Procedure branching should be controlled by `P_ORDER_TYPE = 'WTTX'`.
