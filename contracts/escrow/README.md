# Escrow Contract

Part of the [FacilPay smart contracts](../../README.md) suite on Stellar/Soroban.

## Multisig release threshold

Multi-party escrows can require a minimum approval weight before funds are released. Configure the release threshold as a basis-point value where `10000` means full approval and `5000` means 50% approval.

- Valid values are in the range `(0, 10000]`.
- The contract rejects `0` and any value outside this range with `InvalidThreshold` via the validation logic in [src/lib.rs](src/lib.rs).
- The minimum safe threshold is `1` bps, but in practice you should use a higher value for any escrow that holds meaningful funds. Setting the threshold too low can let a small group of signers release funds with weak consensus, which increases the risk of misuse or compromise.
- Recommended defaults are `10000` for high-value or sensitive escrows, and `5000` or higher for majority-based approval policies.
