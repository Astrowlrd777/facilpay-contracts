# Escrow Contract Errors

This document lists all the error codes defined in the escrow contract (contracts/escrow/src/lib.rs), their symbolic names, and a description of the condition that triggers them.

The escrow contract uses a multi-level enum structure for errors to stay within the Soroban 50-variant XDR limit. Each sub-enum covers a specific category of errors.

## Basic Errors (BasicError)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 100 | Unauthorized | The caller lacks the required permissions or valid signature for the operation. |
| 101 | NotAnAdmin | The caller is not an administrator but attempted an admin-only operation. |
| 102 | AlreadyApproved | The multi-sig proposal or action has already been approved. |
| 103 | ContractPaused | The contract is currently paused globally. |
| 104 | DuplicateApproval | An admin attempted to approve an action they have already approved. |
| 105 | MultiSigNotInitialized | The multi-signature configuration has not been initialized. |
| 106 | MigrationNotStarted | A migration operation was attempted but no migration has been initiated. |
| 107 | AlreadyMigrated | The contract or data has already been migrated to the target version. |
| 108 | ParticipantNotFound | The specified participant was not found in the escrow or multi-sig configuration. |
| 109 | InvalidMerkleProof | The provided Merkle proof does not verify against the committed root. |
| 110 | RootAlreadyCommitted | A Merkle root has already been committed and cannot be overwritten. |
| 111 | InvalidBps | The specified basis points (BPS) value is invalid (e.g., greater than 10000). |
| 112 | InsufficientAdmins | There are not enough administrators configured to perform this operation. |
| 113 | InvalidAddress | The provided address is invalid or resolves to a zero/contract address. |
| 114 | SchemaAlreadyAtTarget | The schema version is already at the target version for an upgrade. |

## Escrow Errors (EscrowError)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 200 | NotFound | The specified escrow record was not found. |
| 201 | InvalidStatus | The escrow is in an invalid status for the requested operation. |
| 202 | AlreadyProcessed | The escrow operation has already been processed. |
| 203 | ReleaseNotYetAvailable | The escrow release is not yet available due to time or condition constraints. |
| 204 | TimeoutNotReached | The timeout period has not yet elapsed, preventing the current action. |
| 205 | ReleaseOnHoldPeriod | The release is on hold due to an active hold period. |
| 206 | InvalidVestingSchedule | The provided vesting schedule parameters are invalid or inconsistent. |
| 207 | CliffPeriodNotPassed | The vesting cliff period has not yet passed. |
| 208 | MilestoneAlreadyReleased | The specified milestone has already been released. |
| 209 | EscrowNotExpired | The escrow has not yet expired, preventing expiry-related actions. |
| 210 | EscrowAlreadyExpired | The escrow has already expired. |
| 211 | ExpiryBeforeRelease | The expiry time is set before the release time, which is invalid. |
| 212 | TemplateNotFound | The specified escrow template was not found. |
| 213 | TemplateInactive | The escrow template is inactive and cannot be used. |
| 214 | SubAccountNotFound | The specified sub-account under the escrow was not found. |
| 215 | SubAccountAlreadyReleased | The sub-account funds have already been released. |
| 216 | SubAccountFundingExceedsEscrow | The sub-account funding amount exceeds the parent escrow balance. |
| 217 | ConditionalEscrowNotFound | The conditional escrow configuration was not found. |
| 218 | ParentEscrowNotFound | The parent escrow for a hierarchical escrow was not found. |
| 219 | ChildrenNotResolved | The child escrows are not yet resolved, preventing parent escrow operations. |
| 220 | MaxHierarchyDepth | The maximum hierarchy depth for nested escrows has been exceeded. |
| 221 | BatchTooLarge | The batch size exceeds the maximum allowed limit. |
| 222 | RenewalDisabled | Escrow renewal is disabled for this contract or escrow. |
| 223 | MaxRenewalsReached | The maximum number of renewals for this escrow has been reached. |
| 224 | NewExpiryNotAfterCurrent | The new expiry timestamp is not after the current expiry. |
| 225 | RenewalPeriodTooShort | The requested renewal period is shorter than the minimum allowed. |
| 226 | RenewalPeriodTooLong | The requested renewal period is longer than the maximum allowed. |
| 227 | InvalidThreshold | The specified threshold value is invalid or out of bounds. |
| 228 | SuccessionPlanExists | A succession plan already exists and cannot be duplicated. |
| 229 | ClawbackDelayTooShort | The clawback delay period is shorter than the minimum required. |

## Action Errors (ActionError)

| Error Code | Symbolic Name | Trigger Condition |
| :--- | :--- | :--- |
| 300 | NotReady | The action or operation is not ready to be executed. |
| 301 | NotDisputed | The operation requires a dispute state but the escrow is not disputed. |
| 302 | ObserverAlreadyAdded | The specified observer has already been added to the escrow. |
| 303 | ObserverNotFound | The specified observer was not found for this escrow. |
| 304 | AccelerationLimitExceeded | The acceleration request exceeds the maximum allowed limit. |
| 305 | TransferNotAllowed | The beneficiary transfer is not allowed under current escrow conditions. |
| 306 | SameBeneficiary | The new beneficiary is the same as the current beneficiary. |
| 307 | ConditionAlreadyEvaluated | The escrow condition has already been evaluated. |
| 308 | StaleThresholdNotConfigured | The stale threshold for time-sensitive operations is not configured. |
| 309 | SwapConfigNotFound | The swap configuration for the escrow was not found. |
| 310 | SwapOutputBelowMinimum | The swap output amount is below the configured minimum. |
| 311 | SwapAlreadyExecuted | The swap operation has already been executed. |
| 312 | BatchReleaseSizeLimitExceeded | The batch release size exceeds the maximum allowed limit. |
| 313 | EvidenceDeadlinePassed | The deadline for submitting evidence has passed. |
| 314 | ApprovalsThresholdNotMet | The required approval threshold for the action has not been met. |
| 315 | InsufficientCollateral | The escrow has insufficient collateral for the requested operation. |
