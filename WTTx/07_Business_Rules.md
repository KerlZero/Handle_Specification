# Business Rules: WTTx / Pocket NET WiFi

## BR-001: WTTx Eligibility

WTTx option must be displayed only when the selected Latitude/Longitude is configured as eligible for WTTx.

## BR-002: Normal Flow Fallback

If the selected location is not eligible for WTTx, the system must continue the normal home internet registration flow.

## BR-003: No Installation Appointment

WTTx order must not require installation appointment because Pocket NET WiFi does not require physical home installation.

## BR-004: Resource Requirement

WTTx order must have valid resource information before order submission to downstream systems.

## BR-005: Payment Before Workflow

WTTx order must be submitted to Workflow only after payment success.

## BR-006: Supported Payment Methods

WTTx payment must support QR Code and Credit/Debit Card.

## BR-007: Payment Failure

If payment fails, the order must not be sent to Workflow and must remain in payment failed/retry state.

## BR-008: Order Type

All WTTx orders sent to Workflow must carry order type = WTTx.

## BR-009: Workflow Verification

Workflow must verify documents and order readiness before submitting create order/profile request to Central Node.

## BR-010: Profile Creation

WTTx order can be completed only after Central Node returns profile created/setting completed status.

## BR-011: Stock Update

After profile creation, Workflow must send resource/profile data to PayG for stock update or stock deduction.

## BR-012: SAP Transaction

PayG must send stock transaction data to SAP after stock update/deduction.

## BR-013: Traceability

The system must maintain traceability between order number, payment reference, resource, profile reference, PayG transaction, and SAP transaction.

## BR-014: Retry and Reconcile

If PayG or SAP transaction fails, the system must support retry or reconciliation process without creating duplicate stock deduction.

## BR-015: Duplicate Prevention

The same WTTx order/resource must not be deducted from stock more than once unless explicitly corrected by an authorized recovery process.
