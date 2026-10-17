# nova-sample-gift-store

Vue gift-shop demo wired to **Nova Payments** bank transfer via the Paystack-compatible API (no card popup).

Based on [PaystackOSS/sample-gift-store](https://github.com/PaystackOSS/sample-gift-store) and [PaystackOSS/sample-backend](https://github.com/PaystackOSS/sample-backend).

Docs: [Nova Payments](https://nova.civai.co/payments/docs)

## Prerequisites

- Nova workspace product with **payments enabled**, merchant bank configured, and **fixed-amount** catalog (or SKU) for your test price
- Nova **API key** (used as `PAYSTACK_SECRET_KEY` on the backend proxy)

## Setup

```bash
npm install
cd server/node && npm install && cd ../..
```

Copy env files:

```bash
cp .env.example .env
cp server/node/.env.example server/node/.env
```

Set `VUE_APP_NOVA_PRODUCT_ID` to your product id. Set `PAYSTACK_SECRET_KEY` to your Nova API key. The backend proxies to:

`https://api.nova.civai.co/api/payments/compat/paystack`

## Run

Terminal 1 (API proxy):

```bash
cd server/node && node server.js
```

Terminal 2 (Vue app):

```bash
npm run serve
```

Checkout redirects buyers to Nova **hosted pay** (`authorization_url`) for bank transfer. Fulfillment uses Nova `payment.fulfillment` webhooks on your product, not Paystack card events.

## Flutterwave

Same flow with `PAYSTACK_BASE_URL=https://api.nova.civai.co/api/payments/compat/flutterwave` and Flutterwave-shaped paths on the proxy if you adapt `server.js` routes.
