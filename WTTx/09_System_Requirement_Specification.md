# System Requirement Specification: WTTx / Pocket NET WiFi

## 1. Purpose

This document defines system-level requirements for implementing WTTx support in Web Register, API integration, database procedures, payment, and Workflow submission.

## 2. System Architecture Scope

| Layer | Requirement |
| --- | --- |
| Frontend | Add WTTx-specific location, package, and payment journey |
| Backend API | Add WTTx eligibility API and adjust submit/payment payloads |
| Database | Add WTTx eligibility procedure and adjust existing procedures |
| Payment | Support WTTx payment by QR Code and Credit/Debit Card |
| Workflow Integration | Submit completed order with order type WTTx |

## 3. API Requirements

### API-001: WTTx Eligibility API

Purpose:
- Check whether selected location supports WTTx.
- Return required WTTx collect values and resource values.

Trigger:
- After user selects location on Web Register.

Input:
- Latitude
- Longitude
- Province / district / sub-district where available
- Area code or coverage reference where available
- Channel = Web Register

Output:
- WTTx eligible flag
- WTTx resource ID
- Coverage/service area reference
- Available WTTx package group
- Error code/message if not eligible or resource unavailable

### API-002: Payment API Adjustment

Purpose:
- Support WTTx payment transaction while reusing the existing payment capability.

Input:
- Order reference
- Order type = WTTx
- Payment method
- Amount
- Customer reference
- Package reference
- Resource reference

Output:
- Payment status
- Payment transaction reference
- Payment timestamp
- Error code/message if payment fails

### API-003: Submit Order Complete API Adjustment

Purpose:
- Submit WTTx order to Workflow after successful payment.

Input:
- Order type = WTTx
- Customer information
- Location information
- Package information
- Resource information
- Payment reference
- Document reference

Output:
- Workflow request reference
- Submit status
- Error code/message if submission fails

## 4. Frontend Requirements

- The system must detect WTTx eligibility after location selection.
- The system must display WTTx package/resource only when WTTx is eligible.
- The system must hide or skip installation appointment screens for WTTx.
- The system must show WTTx payment screen after package submission.
- The system must support QR Code and Credit/Debit Card payment.
- The WTTx flow must be separated from the normal flow to prevent regression.

## 5. Backend Requirements

- Backend must expose a WTTx eligibility API.
- Backend must map WTTx collect values using reference logic from the normal registration flow where applicable.
- Backend must pass WTTx-specific parameters to payment and submit order procedures.
- Backend must submit Workflow payload with order type WTTx.
- Backend must support idempotency for payment and submit order complete operations.

## 6. Database Requirements

- Add WTTx eligibility procedure.
- Adjust payment procedure to accept WTTx order type and WTTx resource values.
- Adjust submit order complete procedure to accept WTTx order type and WTTx resource/profile values.
- Existing normal registration behavior must remain unchanged.

## 7. Non-Functional Requirements

- WTTx eligibility API response time should be suitable for interactive location selection.
- Payment submission must be traceable by order reference and payment transaction reference.
- All downstream submissions must be logged for audit and reconciliation.
- WTTx flow must support retry for payment callback, Workflow submission, and database procedure errors.
- Sensitive payment data must not be stored beyond allowed payment security rules.

## 8. Compatibility Requirements

- Normal home internet registration must continue without payment.
- Existing payment procedures must continue to support existing products.
- Existing submit order complete procedures must support both normal flow and WTTx flow.
