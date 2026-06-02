# User Stories: WTTx / Pocket NET WiFi

## US-001: WTTx Eligibility

As a customer, I want the system to detect whether my selected location supports WTTx, so that I can apply for Pocket NET WiFi when normal home internet is not available.

## US-002: WTTx Package Display

As a customer, I want to see WTTx packages after selecting an eligible location, so that I can choose an internet option suitable for my home.

## US-003: Skip Installation Appointment

As a customer, I do not want to schedule an installation appointment for WTTx, because Pocket NET WiFi does not require home installation.

## US-004: Payment Method Selection

As a customer, I want to pay by QR Code or Credit/Debit Card, so that I can complete the order using my preferred payment method.

## US-005: Submit Paid Order

As Web Register, I want to send the WTTx order to Workflow only after successful payment, so that downstream systems process only paid orders.

## US-006: Verify Order Readiness

As Workflow operator/system, I want to verify documents and order readiness, so that only valid WTTx orders are submitted for profile creation.

## US-007: Create Profile

As Workflow, I want to send WTTx order data to the Central Node, so that the customer profile can be created and prepared for activation.

## US-008: Update Stock

As Workflow, I want to send resource/profile data to PayG after profile creation, so that stock can be deducted or updated before sending data to SAP.

## US-009: Stock Transaction to SAP

As PayG, I want to send stock transaction data to SAP, so that inventory records are updated in the back-office system.
