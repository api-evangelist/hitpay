---
name: Set up HitPay recurring billing
description: Create a subscription plan, start a recurring-billing subscription on a saved card, and charge it.
api: openapi/hitpay-openapi-original.json
method: generated
source: openapi/hitpay-openapi-original.json + https://docs.hitpayapp.com/apis/guide/recurring-billing
operations: [create-subscription-plan, create-a-recurring-billing, charge-the-saved-card, get-saved-card-details]
---

# Set up HitPay recurring billing

## Auth
`X-BUSINESS-API-KEY` header on every request (sandbox key against the sandbox host).

## Steps
1. **(Optional) Create a reusable plan** — `create-subscription-plan`
   (`POST /v1/subscription-plan`, form-encoded): `name`, `amount`, `currency`, `cycle`
   (weekly/monthly/yearly). You may instead define an inline ad-hoc plan in step 2.
2. **Start the subscription** — `create-a-recurring-billing` (`POST /v1/recurring-billing`).
   Provide `plan_id`, or pass `plan_id=null` with `name`/`cycle`/`amount`/`customer_email`/
   `start_date` for an inline plan. Set `save_card=true`. The response returns a `url`
   the customer visits to attach a payment method.
3. **Watch method attachment** — listen for `recurring_billing.method_attached` and
   `recurring_billing.subscription_updated` webhooks; `charge.created` confirms each
   successful charge.
4. **(Optional) Ad-hoc charge** — `charge-the-saved-card`
   (`POST /v1/charge/recurring-billing/{recurring_billing_id}`) with `amount`/`currency`
   to bill the saved card outside the schedule.
5. **Inspect** — `get-saved-card-details`
   (`GET /v1/recurring-billing/{recurring_billing_id}`).

## Rules
- Customers cannot self-cancel subscriptions; cancel on their behalf.
- Verify all webhooks via `Hitpay-Signature` (HMAC-SHA256, per-webhook salt).
