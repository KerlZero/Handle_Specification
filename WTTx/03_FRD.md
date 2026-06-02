# Functional Requirement Document: WTTx / Pocket NET WiFi

## 1. Functional Scope

The system must support WTTx / Pocket NET WiFi registration through Web Register. The journey should remain similar to the standard home internet registration flow, with additional WTTx eligibility checking, resource display, payment before order submission, profile creation, and stock update through PayG/SAP.

## 2. Functional Requirements

### FR-001: WTTx Eligibility by Location

Web Register must check the selected Latitude/Longitude from the location selection page to determine whether the location is eligible for WTTx.

Expected behavior:
- If the location is eligible for WTTx, the system displays the WTTx option, package, and resource information.
- If the location is not eligible for WTTx, the system continues the standard home internet registration flow.

### FR-002: Display Initial Resource

When the selected location is eligible for WTTx, the system must retrieve and display the initial resource required for WTTx order creation.

Expected behavior:
- The retrieved resource must match the selected location or WTTx configuration.
- The resource information must be carried forward to Workflow and PayG.

### FR-003: Skip Installation Appointment

For order type WTTx, the system must not display or require an installation appointment step.

Expected behavior:
- The customer can proceed from package selection to payment.
- Appointment date/time must not be mandatory for WTTx.

### FR-004: Package Selection

The system must allow the customer to select an available WTTx package based on the selected location/resource.

Expected behavior:
- Only WTTx-supported packages are displayed.
- After package selection and submission, the system proceeds to payment method selection.

### FR-005: Payment Method Selection

After the customer submits the selected package, the system must display two payment methods:

- QR Code
- Credit/Debit Card

Expected behavior:
- The customer must complete payment successfully before the order is submitted to Workflow.
- If payment fails, the system must display payment failure status and provide retry handling according to the payment flow.

### FR-006: Submit Paid WTTx Order to Workflow

After payment success, Web Register must submit the WTTx order to Workflow with all required data.

Required data:
- Customer information
- Location / Latitude / Longitude
- Selected package
- Resource information
- Payment transaction reference
- Order type = WTTx
- Document information

### FR-007: Workflow Document and Readiness Verification

Workflow must support order type WTTx and verify documents and order readiness before downstream order/profile creation.

Expected behavior:
- Workflow verifies required document and order data.
- If verification passes, the operator/system can submit create order/profile.
- If verification fails, Workflow must reject or request correction according to the defined process.

### FR-008: Submit Create Profile to Central Node

After Workflow verification passes, Workflow must send the WTTx order data to the Central Node to create the order/profile.

Expected behavior:
- Central Node accepts order type WTTx.
- Central Node creates the profile or forwards the required data to related profile setting nodes.

### FR-009: Profile Setting by Related Nodes

Central Node must send the required information to related nodes to set up the profile for customer activation.

Expected behavior:
- Related nodes return profile setting results to Central Node.
- Central Node returns profile created/setting completed status to Workflow.

### FR-010: Workflow Complete Order

When Workflow receives profile created/setting completed status, Workflow must complete the WTTx order.

Expected behavior:
- Order status is updated to complete or the business-defined equivalent status.
- Resource/profile data is prepared for PayG.

### FR-011: Send Resource/Profile to PayG

Workflow must send the resource used to create the order and profile to PayG for stock update or stock deduction.

Required data:
- Order number
- Resource ID / device information
- Package
- Profile reference
- Customer reference
- Payment reference
- Transaction timestamp

### FR-012: PayG Stock Update and SAP Integration

PayG must update/deduct stock and send the stock transaction to SAP.

Expected behavior:
- PayG updates stock successfully.
- PayG sends stock transaction data to SAP.
- SAP returns acknowledgement to PayG.
- PayG returns stock update result to Workflow.

## 3. Status Handling

| Event | Source | Target Status |
| --- | --- | --- |
| Payment success | Payment Gateway | Ready to submit to Workflow |
| Payment failed | Payment Gateway | Payment failed / retry |
| Document verified | Workflow | Ready to create profile |
| Profile created | Central Node | Profile completed |
| Stock updated | PayG | Stock completed |
| SAP acknowledged | SAP | SAP completed |

## 4. Error Handling

- If the location is not WTTx eligible, continue the normal home internet registration flow.
- If resource is unavailable, prevent WTTx order submission.
- If payment fails, allow the customer to retry or cancel according to payment rules.
- If Workflow verification fails, reject or request correction.
- If profile creation fails, Workflow must set the order to failed/pending for operational review.
- If PayG/SAP update fails, the transaction must be retained for retry or reconciliation.
