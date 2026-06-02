# Business Logic: WTTx / Pocket NET WiFi

## 1. WTTx Eligibility Logic

The system must evaluate WTTx eligibility after the customer selects the installation location.

Logic:
1. Capture selected Latitude/Longitude.
2. Call WTTx eligibility API.
3. API calls WTTx eligibility procedure.
4. If the procedure returns `O_WTTX_ELIGIBLE_FLAG = Y`, enable WTTx flow.
5. If the procedure returns `O_WTTX_ELIGIBLE_FLAG = N`, continue the normal home internet flow.

## 2. Resource Logic

When WTTx is eligible:
- The system must retrieve WTTx resource ID and service area reference.
- Resource must be included in payment, submit order complete, Workflow, and PayG payloads.
- Resource must not be changed after payment success unless a controlled recovery process is applied.

## 3. Appointment Logic

For WTTx:
- Installation appointment screen must be skipped.
- Appointment functions must not be called.
- `skipAppointmentFlag` must be set to Y.

For normal home internet:
- Existing appointment logic remains unchanged.

## 4. Payment Logic

For WTTx:
- Payment is mandatory before submit order complete.
- Supported methods are QR Code and Credit/Debit Card.
- Payment success is required before sending the order to Workflow.
- Payment failed must prevent Workflow submission.

For normal home internet:
- Existing non-payment flow remains unchanged.

## 5. Submit Order Complete Logic

When WTTx payment is successful:
1. Build submit order complete payload.
2. Set `orderType = WTTx`.
3. Include payment reference.
4. Include resource and service area data.
5. Set appointment skip flag.
6. Submit order to Workflow.

## 6. Procedure Branching Logic

Existing payment and submit order complete procedures must support WTTx by branching on order type.

Pseudo logic:

```text
IF P_ORDER_TYPE = 'WTTX' THEN
    Validate WTTx required parameters
    Process WTTx payment/order values
    Skip appointment-related validation
ELSE
    Process existing normal registration logic
END IF
```

## 7. Workflow Logic

Workflow must:
- Accept order type WTTx.
- Verify documents and order readiness.
- Submit create order/profile request to Central Node.
- Complete order after profile created/setting completed result is returned.
- Send resource/profile data to PayG for stock update.

## 8. Stock Update Logic

After Workflow completes WTTx order:
1. Workflow sends resource/profile data to PayG.
2. PayG validates whether the resource is eligible for stock update/deduction.
3. PayG updates or deducts stock.
4. PayG sends stock transaction to SAP.
5. SAP acknowledgement is stored for traceability.

## 9. Duplicate Prevention Logic

- Payment transaction reference must be unique per WTTx order.
- Submit order complete must not be processed twice for the same successful payment reference.
- PayG stock deduction must not be duplicated for the same order/resource combination.
