# HitPay (hitpay)

HitPay is a Singapore-headquartered all-in-one payments platform for small and medium businesses across Asia-Pacific, unifying online checkout, point of sale, and B2B billing. Its REST API creates hosted Payment Requests, runs Recurring Billing on saved cards, and issues Refunds, with first-class Southeast Asian local methods (PayNow, GrabPay, WeChat Pay, Alipay, ShopeePay, Atome) alongside cards. Requests authenticate with the X-BUSINESS-API-KEY header.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/hitpay/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/hitpay/refs/heads/main/apis.yml)

## Tags

- Payments
- Fintech
- PayNow
- Southeast Asia
- SMB

## Timestamps

- **Created:** 2026-07-17
- **Modified:** 2026-07-17

## APIs

### HitPay Payment Requests API

Creates hosted payment requests (payment links and checkout pages) for a given amount and currency, returning a redirect URL and a payment id to track status. Supports PayNow, GrabPay, WeChat Pay, Alipay, ShopeePay, Atome and cards; payment status is delivered via dashboard-registered webhooks.

- **Human URL:** [https://docs.hitpayapp.com/apis/guide/online-payments](https://docs.hitpayapp.com/apis/guide/online-payments)
- **Base URL:** `https://api.hit-pay.com/v1`

#### Tags

- Payments
- Checkout
- Payment Links

#### Properties

- [Documentation](https://docs.hitpayapp.com/apis/guide/online-payments)
- [API Reference](https://docs.hitpayapp.com/apis)
- [OpenAPI](openapi/hitpay-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/hitpay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### HitPay Recurring Billing API

Starts and manages subscriptions billed against saved cards, either from a reusable subscription plan or an inline ad-hoc plan (name/cycle/amount), and charges saved cards for one-off amounts.

- **Human URL:** [https://docs.hitpayapp.com/apis/guide/recurring-billing](https://docs.hitpayapp.com/apis/guide/recurring-billing)
- **Base URL:** `https://api.hit-pay.com/v1`

#### Tags

- Recurring
- Subscriptions
- Saved Cards

#### Properties

- [Documentation](https://docs.hitpayapp.com/apis/guide/recurring-billing)
- [API Reference](https://docs.hitpayapp.com/apis/recurring-billing/create-billing)
- [OpenAPI](openapi/hitpay-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/hitpay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### HitPay Subscription Plans API

Creates and lists reusable subscription plan templates (name, amount, currency, billing cycle) referenced by recurring billing subscriptions.

- **Human URL:** [https://docs.hitpayapp.com/apis/recurring-billing/get-all-plans](https://docs.hitpayapp.com/apis/recurring-billing/get-all-plans)
- **Base URL:** `https://api.hit-pay.com/v1`

#### Tags

- Plans
- Subscriptions

#### Properties

- [Documentation](https://docs.hitpayapp.com/apis/recurring-billing/get-all-plans)
- [OpenAPI](openapi/hitpay-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/hitpay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### HitPay Refunds API

Issues full or partial refunds against completed payments. One refund is allowed per transaction and only PayNow or card charges are refundable; original transaction fees are non-refundable.

- **Human URL:** [https://docs.hitpayapp.com/apis/guide/online-payments](https://docs.hitpayapp.com/apis/guide/online-payments)
- **Base URL:** `https://api.hit-pay.com/v1`

#### Tags

- Refunds
- Payments

#### Properties

- [Documentation](https://docs.hitpayapp.com/apis/guide/online-payments)
- [OpenAPI](openapi/hitpay-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/hitpay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### HitPay Platform API

Extension of the Payment Request APIs for e-commerce platforms and aggregators that host sub-merchants, allowing a platform to create payment requests on behalf of onboarded merchants using an additional X-PLATFORM-KEY header.

- **Human URL:** [https://docs.hitpayapp.com/apis/guide/platform-apis](https://docs.hitpayapp.com/apis/guide/platform-apis)
- **Base URL:** `https://api.hit-pay.com/v1`

#### Tags

- Platform
- Aggregator
- Marketplace

#### Properties

- [Documentation](https://docs.hitpayapp.com/apis/guide/platform-apis)
- [OpenAPI](openapi/hitpay-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [GitHub Organization](https://github.com/hit-pay)
- [LinkedIn](https://www.linkedin.com/company/hit-pay)
- [Website](https://www.hitpayapp.com/)
- [Documentation](https://docs.hitpayapp.com/apis)
- [Plans](plans/hitpay-plans-pricing.yml)
- [Rate Limits](rate-limits/hitpay-rate-limits.yml)
- [Fin Ops](finops/hitpay-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
