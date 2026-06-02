# Acceptance Criteria: WTTx / Pocket NET WiFi

## AC-001: Location Eligibility

Given the customer selects a location on Web Register  
When the selected Latitude/Longitude is configured for WTTx  
Then the system must display WTTx/Pocket NET WiFi as an available option

## AC-002: Non-Eligible Location

Given the customer selects a location on Web Register  
When the selected Latitude/Longitude is not configured for WTTx  
Then the system must continue with the normal home internet registration flow

## AC-003: Resource Display

Given the selected location is eligible for WTTx  
When the system loads WTTx information  
Then the system must retrieve and display the initial resource required for order/profile creation

## AC-004: No Installation Appointment

Given the customer is applying for WTTx  
When the customer proceeds after package selection  
Then the system must not require installation appointment date/time

## AC-005: Payment Method

Given the customer selected a WTTx package  
When the customer submits the package selection  
Then the system must display payment options for QR Code and Credit/Debit Card

## AC-006: Payment Success

Given the customer completes payment successfully  
When the payment gateway returns success  
Then Web Register must complete the paid order step and submit the WTTx order to Workflow

## AC-007: Payment Failure

Given the customer payment fails  
When the payment gateway returns failed status  
Then Web Register must not submit the order to Workflow and must display retry/failure information

## AC-008: Workflow Verification

Given Workflow receives order type WTTx  
When documents and order readiness are verified successfully  
Then Workflow must allow submit create order/profile to Central Node

## AC-009: Profile Created

Given Central Node and related nodes complete profile setting  
When the profile created result is returned to Workflow  
Then Workflow must complete the WTTx order status

## AC-010: PayG Stock Update

Given Workflow completes profile creation  
When Workflow sends resource/profile data to PayG  
Then PayG must update or deduct stock and send stock transaction to SAP

## AC-011: SAP Acknowledgement

Given PayG sends stock transaction to SAP  
When SAP returns acknowledgement  
Then PayG must return stock update result to Workflow

## AC-012: Data Traceability

Given a WTTx order is completed  
When the order is reviewed  
Then the system must be able to trace customer, location, package, resource, payment reference, profile reference, PayG transaction, and SAP transaction
