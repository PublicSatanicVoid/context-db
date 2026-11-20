---
type: Rule
description:
  Rules for every caller of the Acme Payments API that the API itself does not
  enforce — an idempotency key on every POST, waiting for a refund to settle,
  and sending card tokens, never card numbers
---

# Calling Acme Payments

The endpoints, their fields, and the error codes are documented at
<https://docs.acme.example/payments/api>. Read them there. This note holds only
what that page leaves out.

- Send an `Idempotency-Key` header with every `POST`, and send the same key
  again when you retry. A retry without it can charge or refund the customer
  twice.
- A refund is not finished when `POST /refunds` returns. It goes through a
  queue. Wait for the `refund.settled` event, or poll the refund until its
  status changes.
- Never send a card number. Tokenize the card with the Acme vault first and
  send the token. A service that handles a raw card number is in PCI scope.
