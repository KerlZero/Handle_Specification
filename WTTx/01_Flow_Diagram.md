# Flow Diagram: WTTx / Pocket NET WiFi Registration

## End-to-End Sequence Flow

```mermaid
sequenceDiagram
    autonumber

    actor Customer as Customer
    participant WebRegister as Web Register
    participant Payment as Payment Gateway
    participant Workflow as Workflow
    participant Central as Central Node
    participant ProfileNodes as Related Profile Nodes
    participant PayG as PayG
    participant SAP as SAP

    Customer->>WebRegister: Start normal home internet registration
    WebRegister->>WebRegister: Select installation location
    WebRegister->>WebRegister: Check Latitude/Longitude against WTTx configuration

    alt Location is eligible for WTTx
        WebRegister->>WebRegister: Display WTTx / Pocket NET WiFi option
        WebRegister->>WebRegister: Display initial resource for order creation
        WebRegister->>WebRegister: Skip installation appointment
        Customer->>WebRegister: Select WTTx package and submit
        WebRegister->>Payment: Redirect to payment method selection

        alt QR Code payment
            Payment-->>WebRegister: Payment success
        else Credit/Debit Card payment
            Payment-->>WebRegister: Payment success
        else Payment failed
            Payment-->>WebRegister: Payment failed
            WebRegister-->>Customer: Display payment failure and retry option
        end

        WebRegister->>Workflow: Submit paid WTTx order
        Workflow->>Workflow: Verify documents and order readiness
        Workflow->>Central: Submit create order / create profile request
        Central->>ProfileNodes: Send profile setting request
        ProfileNodes-->>Central: Return profile setting result
        Central-->>Workflow: Return profile created / setting completed
        Workflow->>Workflow: Complete WTTx order
        Workflow->>PayG: Send resource and profile data for stock update
        PayG->>PayG: Deduct or update stock
        PayG->>SAP: Send stock transaction
        SAP-->>PayG: Return SAP acknowledgement
        PayG-->>Workflow: Return stock update result
        Workflow-->>WebRegister: Update final order status
        WebRegister-->>Customer: Display successful order confirmation

    else Location is not eligible for WTTx
        WebRegister->>WebRegister: Continue normal home internet eligibility flow
    end
```

## Flow Summary

1. The customer starts the registration journey from Web Register, similar to the normal home internet flow.
2. Web Register checks the selected Latitude/Longitude to determine whether the location is eligible for WTTx.
3. If eligible, Web Register displays the WTTx package/resource and skips the installation appointment step.
4. After package selection, the customer must complete payment by QR Code or Credit/Debit Card.
5. After payment success, Web Register submits the paid WTTx order to Workflow.
6. Workflow verifies documents and order readiness.
7. Workflow sends the order to the Central Node to create the order/profile and trigger profile setting in related nodes.
8. After profile setting is completed, the result is returned to Workflow.
9. Workflow completes the order and sends resource/profile data to PayG for stock update before SAP posting.
10. Web Register displays the final order result to the customer.
