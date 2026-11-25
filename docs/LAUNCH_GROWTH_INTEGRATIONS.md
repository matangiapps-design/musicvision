# MATANGI launch growth integrations

## Current customer portal
The customer portal is a static launch page at `customer-portal/index.html`. It includes:
- Conversion-focused product story and launch pricing display ($3 / $6 / $9).
- Share actions and a referral-link preview using the `?ref=` query parameter.
- A proposed 30% partner commission display.
- Reserved ad placement areas.
- Clear disclosure that checkout, generation, affiliate attribution and ad network serving are not yet connected.

## Important production boundary
The static referral-link preview is not an affiliate tracking system. It does not create partner accounts, persist click attribution across devices, validate purchases, prevent self-referrals/fraud, calculate commissions, or pay affiliates. Do not advertise commission payouts as active until those capabilities exist and the terms are published.

## Recommended production architecture
1. **Affiliate attribution:** capture referral code on landing, store first-party attribution server-side with consent, bind it to the customer account and signed order. Validate paid/refunded/chargeback status before commission approval.
2. **Commission ledger:** configurable rate (proposed 30%), immutable order-linked ledger, refund reversals, minimum payout threshold, partner terms, tax/KYC handling where legally required, payout exports and audit trail.
3. **Payments:** hosted checkout from a supported payment provider; verify signed webhooks on the backend before granting credits. Never trust a browser success redirect as proof of payment.
4. **Traffic monetisation:** connect an approved ad network only after domain and policy approval. Keep ad units on free informational/landing content; do not put ads in checkout, account, upload or active generation screens. Load ads asynchronously and disclose advertising.
5. **Analytics:** track consent-aware page views, CTA clicks, outbound shares, affiliate clicks, checkout starts, verified purchases, refunds, cost per acquisition and revenue per visitor. Do not fabricate user counts or earnings.
6. **Performance:** compress assets, lazy-load non-critical scripts, use responsive layout, add privacy/terms/contact pages, and test Core Web Vitals and mobile checkout.

## Launch acceptance checklist
- [ ] Real product demo and generation limits are verified.
- [ ] Checkout and webhook-based credit activation are tested end-to-end.
- [ ] Affiliate registration, attribution, order validation and commission ledger pass tests.
- [ ] Affiliate terms, privacy policy, refund policy and payout schedule are published.
- [ ] Ad network approves the domain and ads render only in intended placements.
- [ ] Analytics events and consent controls are verified.
- [ ] Load test covers expected campaign traffic and generation queue capacity.
