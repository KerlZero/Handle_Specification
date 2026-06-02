# Field Mapping: WTTx / Pocket NET WiFi

## 1. Purpose

This document defines field-level mapping across Web Register, WTTx eligibility API, Payment, Submit Order Complete, Workflow, PayG, and SAP.

## 2. Location and Eligibility Mapping

| Source Field | Target Field | Target Component | Description |
| --- | --- | --- | --- |
| Latitude | `P_LATITUDE` | WTTx Eligibility Procedure | Selected installation latitude |
| Longitude | `P_LONGITUDE` | WTTx Eligibility Procedure | Selected installation longitude |
| Province | `P_PROVINCE` | WTTx Eligibility Procedure | Location province |
| District | `P_DISTRICT` | WTTx Eligibility Procedure | Location district |
| Sub-district | `P_SUB_DISTRICT` | WTTx Eligibility Procedure | Location sub-district |
| Channel | `P_CHANNEL` | WTTx Eligibility Procedure | Fixed as WEB_REGISTER |

## 3. Eligibility Response Mapping

| Source Field | Target Field | Target Component | Description |
| --- | --- | --- | --- |
| `O_WTTX_ELIGIBLE_FLAG` | `wttxEligibleFlag` | Web Register | Determines whether WTTx flow is enabled |
| `O_RESOURCE_ID` | `resourceId` | Web Register / Workflow / PayG | Resource used for order/profile/stock |
| `O_SERVICE_AREA_ID` | `serviceAreaId` | Web Register / Workflow | WTTx service area reference |
| `O_PACKAGE_GROUP` | `packageGroup` | Package Selection | WTTx package group |
| `O_RETURN_CODE` | `returnCode` | Web Register | Eligibility result code |
| `O_RETURN_MESSAGE` | `returnMessage` | Web Register | Eligibility result message |

## 4. Payment Mapping

| Source Field | Target Field | Target Component | Description |
| --- | --- | --- | --- |
| Order Reference | `orderRef` | Payment API | Temporary order reference |
| Order Type | `orderType` | Payment API / DB | Fixed as WTTx |
| Payment Method | `paymentMethod` | Payment API | QR_CODE or CARD |
| Amount | `amount` | Payment API | Payment amount |
| Package Code | `packageCode` | Payment API / DB | Selected WTTx package |
| Resource ID | `resourceId` | Payment API / DB | WTTx resource reference |
| Payment Transaction Reference | `paymentRef` | Submit Order Complete | Returned after payment success |

## 5. Submit Order Complete Mapping

| Source Field | Target Field | Target Component | Description |
| --- | --- | --- | --- |
| Customer ID | `customerId` | Workflow Payload | Customer reference |
| Location | `locationInfo` | Workflow Payload | Selected installation location |
| Latitude | `latitude` | Workflow Payload | Selected latitude |
| Longitude | `longitude` | Workflow Payload | Selected longitude |
| Order Type | `orderType` | Workflow Payload | WTTx |
| Package Code | `packageCode` | Workflow Payload | Selected WTTx package |
| Resource ID | `resourceId` | Workflow Payload | WTTx resource |
| Payment Ref | `paymentRef` | Workflow Payload | Payment transaction reference |
| Skip Appointment Flag | `skipAppointmentFlag` | Workflow Payload | Y |

## 6. PayG and SAP Mapping

| Source Field | Target Field | Target Component | Description |
| --- | --- | --- | --- |
| Order Number | `orderNo` | PayG | Completed WTTx order number |
| Resource ID | `resourceId` | PayG | Device/resource for stock update |
| Profile Reference | `profileRef` | PayG | Created profile reference |
| Payment Ref | `paymentRef` | PayG | Payment transaction reference |
| Stock Transaction ID | `stockTxnId` | SAP | PayG stock transaction reference |
| Stock Status | `stockStatus` | SAP | Deducted/updated stock result |
