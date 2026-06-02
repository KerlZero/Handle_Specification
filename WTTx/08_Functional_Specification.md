# Functional Specification: WTTx / Pocket NET WiFi

## 1. Purpose

This document defines the functional specification for supporting WTTx / Pocket NET WiFi in the registration flow. The enhancement introduces WTTx eligibility checking, removes installation appointment steps, adds a dedicated payment flow, and submits completed WTTx orders to Workflow with order type WTTx.

## 2. Scope

### Code Path Scope

- Add a new API call to support WTTx during location selection when the selected area supports WTTx.
- Reuse and map relevant collect values from the normal home internet registration APIs where applicable.
- Remove screens and functions related to installation appointment selection for WTTx.
- Add payment screen and payment functions by adapting the existing payment function.
- Create a dedicated WTTx payment/order flow to avoid impact on the existing normal registration flow that does not require payment.
- Adjust submit order complete API values so the order is submitted to Workflow with order type WTTx.

### Database Path Scope

- Add a new procedure to check WTTx eligibility and return required WTTx values.
- Adjust existing payment procedure values and parameters to support WTTx.
- Adjust existing submit order complete procedure values and parameters to support WTTx.

## 3. Functional Flow

1. Customer selects installation location on Web Register.
2. System calls WTTx eligibility API using selected Latitude/Longitude or area code.
3. API calls WTTx eligibility procedure.
4. Procedure returns WTTx eligibility flag and required WTTx resource values.
5. If WTTx is eligible, Web Register displays WTTx package/resource.
6. System skips installation appointment screens and functions.
7. Customer selects WTTx package.
8. System redirects to WTTx payment screen.
9. Customer pays by QR Code or Credit/Debit Card.
10. Payment result is saved through payment procedure with WTTx parameters.
11. If payment success, Web Register submits order complete with order type WTTx.
12. Submit order complete procedure stores WTTx-specific values.
13. Workflow receives WTTx order and continues document verification and profile creation.

## 4. Functional Components

| Component | Functional Description |
| --- | --- |
| Web Register - Location | Detect WTTx supported area from selected location |
| WTTx Eligibility API | Retrieve WTTx eligibility and resource values |
| WTTx Package Selection | Display WTTx package based on returned resource/eligibility |
| Appointment Module | Skip appointment flow for WTTx |
| WTTx Payment Screen | Support QR Code and Credit/Debit Card payment |
| Payment API/Procedure | Save WTTx payment transaction |
| Submit Order Complete API | Submit WTTx order to Workflow |
| Submit Order Procedure | Persist WTTx order values and parameters |

## 5. Functional Rules

- WTTx eligibility must be checked only after the user selects a location.
- WTTx flow must not alter the normal home internet flow.
- Installation appointment must not be required for WTTx.
- Payment must be completed successfully before order completion is submitted.
- Submit order complete must include order type WTTx.
- Existing payment and submit procedures must remain backward compatible with the normal flow.

## 6. Expected Outputs

- WTTx eligibility result.
- WTTx resource values for package/order creation.
- Payment transaction reference.
- Completed WTTx order payload.
- Workflow order with type WTTx.
