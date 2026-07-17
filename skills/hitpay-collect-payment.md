---
name: Collect a payment with HitPay
description: Create a hosted/embedded payment request, redirect or embed checkout, and confirm the result via webhook.
api: openapi/hitpay-openapi-original.json
method: generated
source: openapi/hitpay-openapi-original.json + https://docs.hitpayapp.com/apis/guide/online-payments
operations: [create-payment-request, get-payment-status, create-webhook-event]
---

# Collect a payment with HitPay

Use this to accept a one-off payment (cards, PayNow, GrabPay, ShopeePay, QRIS, and other SEA methods).

## Auth
Send the merchant Business API key on every request as the `X-BUSINESS-API-KEY` header.
In test mode use a sandbox account/key against `https://api.sandbox.hit-pay.com/v1`
(production: `https://api.hit-pay.com/v1`). Never expose the key client-side.

## Steps
1. **Create the payment request** — `create-payment-request` (`POST /v1/payment-requests`,
   form-encoded). Required: `amount` (string, e.g. "199.00") and `currency` (ISO 4217).
   Optional: `email`, `redirect_url`, `reference_number`, `payment_methods[]`. The
   response returns `id` and a hosted checkout `url`.
2. **Present checkout** — redirect the payer to `url`, OR embed the Drop-In UI
   (see components/hitpay-components.yml; needs the Default Link + payment_request_id).
   For QR-only flows set `generate_qr=true` and render the returned QR.
3. **Confirm securely via webhook** — never trust the redirect alone. Register a
   webhook endpoint (`create-webhook-event`) and act on `payment_request.completed`
   (and handle `payment_request.failed`). Verify `Hitpay-Signature` (HMAC-SHA256 of
   the raw body with the per-webhook salt). See asyncapi/hitpay-events-webhooks.yml.
4. **(Optional) Poll status** — `get-payment-status` (`GET /v1/payment-requests/{request_id}`)
   returns the current status (pending/completed/failed/expired).

## Rules
- Test card in sandbox: `4242 4242 4242 4242`, any future expiry, any CVC.
- Amounts are strings; currency codes accept lowercase.
- Errors: 401 = bad/missing key, 422 = validation (`errors` field), 429 = rate limited.
