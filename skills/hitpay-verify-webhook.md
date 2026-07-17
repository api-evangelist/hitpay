---
name: Verify a HitPay webhook
description: Register a webhook endpoint and verify inbound event authenticity with HMAC-SHA256.
api: openapi/hitpay-openapi-original.json
method: generated
source: openapi/hitpay-openapi-original.json + https://docs.hitpayapp.com/apis/guide/events
operations: [create-webhook-event, get-webhook-events-list, get-webhook-event]
---

# Verify a HitPay webhook

## Register
`create-webhook-event` (`POST /v1/webhook-events`) with your endpoint URL, or add it
in Dashboard > Developers > Webhooks. Each endpoint gets its own salt (shown on the
webhook detail view). Manage with `get-webhook-events-list` / `get-webhook-event`.

## Verify (event webhooks)
1. Read the raw request body (do not re-serialize).
2. Compute `HMAC-SHA256(rawBody, perWebhookSalt)`.
3. Compare (constant-time) against the `Hitpay-Signature` header. Reject on mismatch.
4. The `Hitpay-Event-Type` header carries the event type.

## Verify (legacy callbacks)
Payment-request/redirect and plugin callbacks instead return an `hmac` field in the
payload: sort+concatenate the callback params and compute `HMAC-SHA256` with the
**API-key salt** (Developers page), then compare to `hmac`.

## Idempotency
Each event has an id; dedupe on it — HitPay may retry deliveries. Do not mark an
order paid on the redirect alone; wait for `payment_request.completed`.

## Events (subset)
`charge.created`, `charge.updated`, `charge.failed`, `payment_request.completed`,
`payment_request.failed`, `payout.created`, `order.created/updated`, `invoice.created`,
`transfer.*`, `recurring_billing.method_attached/method_detached/subscription_updated`.
See asyncapi/hitpay-events-webhooks.yml for the full catalog.
