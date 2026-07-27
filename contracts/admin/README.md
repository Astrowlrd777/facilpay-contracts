# Admin Contract

The admin contract is the coordination layer for the FacilPay protocol. It stores the addresses of the payment, escrow, and refund contracts and provides admin-controlled entry points for initialization and emergency pause operations across the system.

This document is part of the repository documentation; see the [root README](../../README.md) for the broader project overview.

## Public Functions

- `initialize(env, admin, payment_contract, escrow_contract, refund_contract)` - Registers the administrator and the deployed child contract addresses for the protocol.
- `emergency_pause_all(env, admin, reason)` - Pauses the payment, escrow, and refund contracts in a single admin-authorized operation.
