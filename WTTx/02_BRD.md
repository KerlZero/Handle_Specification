# Business Requirement Document: WTTx / Pocket NET WiFi Sales Channel

## 1. Objective

Add WTTx / Pocket NET WiFi as an additional sales channel within the normal home internet registration journey. The new option provides an alternative for customers whose locations cannot be served by standard home internet installation but can use internet service through mobile network coverage.

## 2. Business Background

Some customers need internet service at home, but their installation locations are outside the standard home internet coverage area or cannot support a normal fixed-line installation. WTTx / Pocket NET WiFi is a suitable alternative because the device only requires mobile signal coverage and does not require an installation appointment.

## 3. Business Goals

- Increase sales opportunities for customers who cannot subscribe to standard home internet.
- Reduce customer drop-off after home internet coverage checks fail.
- Keep the registration journey close to the normal home internet flow to minimize customer and operational impact.
- Support upfront payment before order submission using QR Code and Credit/Debit Card.
- Send resource/profile data to PayG for stock update before SAP posting.

## 4. Scope

### In Scope

- Add WTTx eligibility logic on Web Register based on selected Latitude/Longitude.
- Display initial resource information required for WTTx order creation.
- Skip installation appointment for WTTx because no onsite installation is required.
- Add payment method selection after package selection.
- Support QR Code and Credit/Debit Card payment.
- Submit order type WTTx to Workflow after successful payment.
- Allow Workflow to verify documents and order readiness for WTTx orders.
- Send WTTx order data from Workflow to the Central Node for profile creation.
- Send profile setting requests from the Central Node to related profile nodes.
- Complete the Workflow order after profile created/setting completed status is returned.
- Send resource/profile data from Workflow to PayG for stock deduction or stock update.
- Send PayG stock transaction data to SAP.

### Out of Scope

- Changes to non-WTTx package catalog logic.
- Payment methods other than QR Code and Credit/Debit Card.
- Installation appointment scheduling for WTTx.
- Changes to the standard home internet logic that are unrelated to WTTx.

## 5. Stakeholders

- Business Owner
- Sales / Online Sales Team
- Web Register Team
- Workflow Team
- Payment Gateway Team
- Central Node / Integration Team
- Related Profile System Owners
- PayG Team
- SAP / Inventory Team
- Operations / Back Office
- Customer Support

## 6. Business Benefits

- Improve conversion for customers outside standard home internet coverage.
- Provide a practical alternative product without forcing the customer to leave the registration journey.
- Reduce manual stock handling by sending resource/profile data to PayG automatically.
- Improve traceability across order, payment, profile, stock, and SAP transactions.

## 7. Key Assumptions

- WTTx eligible areas can be identified from Latitude/Longitude configuration.
- WTTx package and resource information is available for Web Register to retrieve.
- Payment Gateway supports QR Code and Credit/Debit Card and can return payment success/failure status.
- Central Node can receive order type WTTx and create the required profile.
- PayG can receive resource/profile data, update stock, and send transaction data to SAP.

## 8. Risks and Dependencies

- Accuracy of Latitude/Longitude mapping to WTTx eligible areas.
- Availability and reliability of payment integration.
- Readiness of Central Node and related profile setting nodes.
- Accuracy of resource/stock data sent to PayG.
- SAP transaction may require retry or reconciliation if PayG or SAP is temporarily unavailable.

## 9. Success Metrics

- Customer can successfully apply for WTTx through Web Register.
- Paid WTTx order is submitted to Workflow correctly.
- Workflow can complete the order after profile creation is completed.
- PayG receives resource/profile data and updates stock successfully.
- SAP receives the stock transaction successfully.
