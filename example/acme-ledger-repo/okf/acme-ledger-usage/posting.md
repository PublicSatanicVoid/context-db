---
type: Rule
description:
  Rules for every service that posts to the Acme Ledger, which its API does not
  enforce — entries that balance, amounts in minor units, and reversing an
  entry instead of changing it
---

# Posting to the Acme Ledger

The endpoints and their fields are documented at
<https://docs.acme.example/ledger/api>. Read them there. This note holds only
what that page leaves out.

- An entry must balance: its debits and its credits add up to the same amount.
  The API accepts an entry that does not, and the nightly reconciliation then
  fails for every account in it.
- Send amounts as whole numbers in the currency's minor unit: `1250` for 12.50
  EUR. A decimal is rounded, with no error.
- Never change or delete a posted entry. Post an entry that reverses it, then
  the correct one. The auditors read the ledger as a history.
