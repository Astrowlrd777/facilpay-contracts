# Payment Contract Errors

This document lists all the error codes defined in the payment contract (`contracts/payment/src/lib.rs`), their symbolic names, and a description of the condition that triggers them. 

The payment contract uses a multi-level enum structure for errors to stay within the Soroban 50-variant XDR limit. Each sub-enum covers a specific category of errors.

## Basic Errors (`BasicError`)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 100 | `Unauthorized` | The caller lacks the required permissions or valid signature for the operation. |
| 101 | `MetadataTooLarge` | The attached metadata exceeds the maximum allowed size limit. |
| 102 | `NotesTooLarge` | The payment notes exceed the maximum allowed size limit. |
| 103 | `InvalidCurrency` | The specified currency is not supported or allowed for this operation. |
| 104 | `InvalidBatchSize` | The provided batch size is outside the allowed bounds. |
| 105 | `BatchPartialFailure` | Some operations within a batch failed while others succeeded. |
| 106 | `RateLimitExceeded` | The operation exceeds the configured rate limit. |
| 107 | `DailyVolumeExceeded` | The operation exceeds the allowed daily transaction volume limit. |
| 108 | `AddressFlagged` | The specified address is flagged for suspicious activity and cannot transact. |
| 109 | `AddressAlreadyFlagged` | The specified address has already been flagged previously. |
| 110 | `AmountExceedsLimit` | The transaction amount exceeds the maximum allowed limit. |
| 111 | `MultiSigNotInitialized` | The multi-signature configuration has not been initialized. |
| 112 | `InsufficientAdmins` | There are not enough administrators configured to perform this operation. |
| 113 | `NotAnAdmin` | The caller attempting the operation is not an administrator. |
| 114 | `AlreadyApproved` | The operation or proposal has already been approved. |
| 115 | `OracleCallFailed` | A cross-contract call to the external oracle failed. |
| 116 | `ContractPaused` | The contract is currently paused globally. |
| 117 | `FunctionPaused` | The specific function being called is currently paused. |
| 118 | `InvalidTierThresholds` | The provided tier thresholds are invalid, missing, or out of order. |
| 119 | `OracleFeedStale` | The data retrieved from the oracle is considered stale or outdated. |
| 120 | `OracleNotConfigured` | The external oracle configuration is missing or invalid. |
| 121 | `InvalidAmount` | The specified amount is invalid (e.g., zero or negative). |
| 122 | `VerificationLevelNotFound` | The required verification level could not be found. |
| 123 | `TierLimitsNotConfigured` | Tier limits have not been configured in the contract. |
| 124 | `InvalidInterval` | The specified time interval is invalid. |
| 125 | `InvalidBps` | The specified basis points (BPS) value is invalid (e.g., greater than 10000). |
| 126 | `SchemaAlreadyAtTarget` | The schema version is already at the target version for an upgrade. |

## Payment Errors (`PaymentError`)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 200 | `NotFound` | The specified payment record was not found. |
| 201 | `InvalidStatus` | The payment is in an invalid status for the requested operation. |
| 202 | `AlreadyProcessed` | The payment has already been successfully processed. |
| 203 | `Expired` | The payment or operation has expired. |
| 204 | `NotExpired` | The payment or operation has not yet expired, preventing the current action. |
| 205 | `NoExpiration` | No expiration is set for this payment. |
| 206 | `TransferFailed` | The underlying token transfer failed during the payment process. |
| 207 | `RefundExceedsPayment` | The requested refund amount exceeds the original payment amount. |
| 208 | `NotYetDue` | The payment is not yet due for processing. |
| 209 | `ScheduledPaymentCancelled` | The scheduled payment has been cancelled by the user or admin. |
| 210 | `MetadataAlreadySet` | Metadata for this payment has already been set and cannot be overwritten. |
| 211 | `MetadataNotFound` | The metadata associated with this payment was not found. |
| 212 | `HashMismatch` | The provided hash does not match the expected hash. |
| 213 | `AlreadyFullyPaid` | The payment has already been fully paid off. |
| 214 | `InstallmentExceedsRemaining` | The requested installment amount exceeds the remaining balance. |
| 215 | `PartialPaymentNotFound` | The partial payment record could not be found. |
| 216 | `MerchantRateLimitExceeded` | The merchant has exceeded their specific rate limit. |
| 217 | `AmountRateLimitExceeded` | The amount exceeds the configured rate limit for the entity. |
| 218 | `PayoutScheduleNotFound` | The required payout schedule configuration was not found. |
| 219 | `PayoutNotYetDue` | The scheduled payout is not yet due. |
| 220 | `NothingToSettle` | There are no funds or pending payments available to settle. |
| 221 | `BillingOverflow` | The billing calculation resulted in an arithmetic overflow. |
| 222 | `InvalidLineItem` | A provided line item for the payment is invalid. |
| 223 | `InvalidScheduleTime` | The provided schedule time is invalid or in the past. |
| 224 | `TokenNotAllowed` | The specified token is not allowed for this payment operation. |

## Subscription Errors (`SubscriptionError`)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 300 | `NotFound` | The specified subscription record was not found. |
| 301 | `NotActive` | The subscription is not currently in an active state. |
| 302 | `PaymentNotDue` | The next payment for the subscription is not yet due. |
| 303 | `MaxRetriesExceeded` | The maximum number of payment retry attempts has been exceeded. |
| 304 | `Ended` | The subscription has already ended or been cancelled. |
| 305 | `DunningNotFound` | The dunning (payment recovery) configuration or record was not found. |
| 306 | `NotInDunning` | The subscription is not currently in a dunning state. |
| 307 | `RetryNotDue` | The next retry attempt for the failed payment is not yet due. |
| 308 | `GracePeriodExpired` | The grace period for the subscription payment has expired. |
| 309 | `RetryTooEarly` | The retry attempt is being made too early according to the backoff schedule. |
| 310 | `MeteredNotFound` | The metered billing record for the subscription was not found. |
| 311 | `BillingCapExceeded` | The maximum billing cap for the metered subscription has been exceeded. |
| 312 | `GroupNotFound` | The specified subscription group was not found. |
| 313 | `AlreadyInGroup` | The subscription is already part of a subscription group. |
| 314 | `GroupSizeLimitExceeded` | The maximum group size limit has been exceeded. |
| 315 | `TrialExpired` | The trial period for the subscription has expired. |
| 316 | `MaxTrialDurationExceeded` | The requested trial duration exceeds the maximum allowed trial duration. |
| 317 | `MerchantPaused` | The merchant managing the subscription is currently paused. |
| 318 | `UsageCapExceeded` | The usage cap for the subscription has been exceeded. |

## Proposal Errors (`ProposalError`)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 400 | `NotFound` | The specified multi-sig proposal was not found. |
| 401 | `Expired` | The proposal has expired and can no longer be executed or approved. |
| 402 | `AlreadyExecuted` | The proposal has already been successfully executed. |
| 403 | `ThresholdNotMet` | The required approval threshold for the proposal has not been met. |
| 404 | `RequiresMultiSig` | The operation requires a multi-signature proposal but one was not used. |
| 405 | `InsufficientApprovals` | The proposal does not have enough approvals for execution. |
| 406 | `ProposalExpired` | The proposal has expired before it could be executed. |

## Feature Errors (`FeatureError`)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 500 | `EscrowMappingNotFound` | The escrow mapping configuration was not found. |
| 501 | `EscrowBridgeFailed` | The cross-contract call to the escrow bridge failed. |
| 502 | `FeeConfigNotFound` | The fee configuration for the operation was not found. |
| 503 | `InsufficientFees` | There are insufficient fees provided to cover the operation. |
| 504 | `ConditionNotMet` | A required conditional parameter or state was not met. |
| 505 | `ConditionAlreadyEvaluated` | The condition has already been successfully evaluated. |
| 506 | `AutoEscrowRuleNotFound` | The auto-escrow rule configuration was not found. |
| 507 | `AutoEscrowBelowMinimum` | The payment amount is below the minimum required for auto-escrow. |
| 508 | `AutoEscrowAlreadyTriggered` | The auto-escrow rule has already been triggered for this transaction. |
| 509 | `ConditionEvaluationFailed` | Evaluating the programmatic condition failed. |
| 510 | `ConditionRuntimeNotMet` | The condition runtime prerequisites were not met. |
| 511 | `InvalidFeeConfig` | The fee configuration is invalid or logically inconsistent. |
| 512 | `ChannelNotFound` | The payment channel was not found. |
| 513 | `InvalidSignature` | The provided cryptographic signature is invalid. |
| 514 | `InvalidNonce` | The provided nonce is invalid or has already been used. |
| 515 | `ChannelClosed` | The payment channel is closed and cannot process transactions. |
| 516 | `ChannelExpired` | The payment channel has expired. |
| 517 | `ChannelNotExpired` | The payment channel has not yet expired, preventing early settlement. |
| 518 | `InvalidSplitShares` | The split shares configuration is invalid (e.g., doesn't sum up correctly). |
| 519 | `TooManyRecipients` | There are too many recipients specified for the operation. |
| 520 | `SplitConfigNotFound` | The payment split configuration was not found. |
| 521 | `SplitAlreadyExecuted` | The split payment operation has already been executed. |
| 522 | `LoyaltyNotConfigured` | The loyalty program is not configured for the entity. |
| 523 | `InsufficientPoints` | The user has insufficient loyalty points for the operation. |
| 524 | `PointsExpired` | The loyalty points have expired and cannot be used. |
| 525 | `NothingToSweep` | There are no funds or assets available to sweep. |
| 526 | `SweepRecipientNotSet` | The recipient address for the fee sweep has not been set. |
| 527 | `SpendLimitExceeded` | The spend limit for the user or entity has been exceeded. |
| 528 | `SpendLimitNotConfigured` | The spend limit configuration was not found. |
| 529 | `SettlementNotReady` | The settlement process is not yet ready to be finalized. |
| 530 | `FinalityConfigNotFound` | The finality configuration was not found. |
| 531 | `SettlementAlreadyFinalized` | The settlement has already been finalized. |
| 532 | `RebateThresholdNotMet` | The volume threshold required to claim a rebate has not been met. |
| 533 | `RebateAlreadyClaimed` | The rebate for the current period has already been claimed. |
| 534 | `RebateConfigNotFound` | The fee rebate configuration was not found. |
| 535 | `ForwardConfigNotFound` | The payment forwarding configuration was not found. |
| 536 | `ForwardLoop` | A payment forwarding loop was detected (e.g., A -> B -> A). |
| 537 | `InvalidForwardBps` | The forward basis points value is invalid. |
| 538 | `SenderIsRecipient` | The sender and recipient addresses are the same. |
| 539 | `BelowMinSplitAmount` | The split amount is below the configured minimum split amount. |
| 540 | `InvalidCounterparty` | The specified counterparty address is invalid. |
