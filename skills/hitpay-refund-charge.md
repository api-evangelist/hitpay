---
name: Refund a HitPay charge
description: Issue a full or partial refund against a completed PayNow or card charge and reconcile via webhook.
api: openapi/hitpay-openapi-original.json
method: generated
source: openapi/hitpay-openapi-original.json + https://docs.hitpayapp.com/apis/guide/online-payments
operations: [get-charge, refund, get-refund]
---

# Refund a HitPay charge

## Auth
`X-BUSINESS-API-KEY` header on every request (sandbox key against the sandbox host).

## Steps
1. **Find the charge** — `get-charge` (`GET /v1/charges/{charge_id}`) to confirm the
   payment is completed and refundable. Only PayNow or card charges are refundable;
   original transaction fees are non-refundable, and only one refund per transaction.
2. **Issue the refund** — `refund` (`POST /v1/refund`, form-encoded) with `payment_id`
   (the charge id) and `amount` (omit/full amount for a full refund, smaller for partial).
3. **Confirm** — `get-refund` (`GET /v1/refund/{refund_id}`) and/or listen for the
   `charge.updated` webhook (fires on refund / partial refund).

## Rules
- A transaction can be refunded only once — check before retrying.
- Verify webhook authenticity via `Hitpay-Signature` (HMAC-SHA256, per-webhook salt).
- This is a destructive/financial operation — HitPay's own agent skills exclude it
  from auto-generation; require explicit confirmation before calling `refund`.
