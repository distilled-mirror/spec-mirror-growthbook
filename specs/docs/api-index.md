# GrowthBook Documentation: API

## API

### Introduction

- [Introduction](https://docs.growthbook.io/api/introduction.md): GrowthBook offers a full REST API for interacting with the application.

### Endpoints

#### Projects

- [Get all projects](https://docs.growthbook.io/api/projects/operation/listProjects.md)
- [Create a single project](https://docs.growthbook.io/api/projects/operation/postProject.md)
- [Get a single project](https://docs.growthbook.io/api/projects/operation/getProject.md)
- [Edit a single project](https://docs.growthbook.io/api/projects/operation/putProject.md)
- [Deletes a single project](https://docs.growthbook.io/api/projects/operation/deleteProject.md)

#### Environments

- [Get the organization's environments](https://docs.growthbook.io/api/environments/operation/listEnvironments.md)
- [Create a new environment](https://docs.growthbook.io/api/environments/operation/postEnvironment.md)
- [Update an environment](https://docs.growthbook.io/api/environments/operation/putEnvironment.md)
- [Deletes a single environment](https://docs.growthbook.io/api/environments/operation/deleteEnvironment.md)

#### Feature Flags

- [Get all features](https://docs.growthbook.io/api/features-v2/operation/listFeaturesV2.md): Returns features with pagination. Rules are returned as a unified top-level array with per-rule environment scope.
- [Create a single feature](https://docs.growthbook.io/api/features-v2/operation/postFeatureV2.md): Creates a new Feature Flag. The caller needs Create access in its Project, plus Publish access for any environment the Feature Flag starts enabled in — one that starts disabled everywhere needs Create alone. Rules are supplied as a top-level `rules` array; each rule includes `allEnvironments` / `env…
- [Get a single feature](https://docs.growthbook.io/api/features-v2/operation/getFeatureV2.md)
- [Partially update a feature](https://docs.growthbook.io/api/features-v2/operation/updateFeatureV2.md): Updates the Feature Flag and immediately publishes a new revision. The caller needs Edit access in the Feature Flag's Project and Publish access for every affected environment. When approval is required, use the revision endpoints instead, unless the caller can bypass draft approvals.
- [Deletes a single feature](https://docs.growthbook.io/api/features-v2/operation/deleteFeatureV2.md): Permanently deletes a Feature Flag and all of its revisions. The caller needs Archive & delete access. Deleting a live Feature Flag also requires Publish access for every environment where it is enabled and the organization setting "REST API always bypasses approval requirements". Otherwise, archive…
- [Toggle a feature in one or more environments](https://docs.growthbook.io/api/features-v2/operation/toggleFeatureV2.md): Enables or disables a Feature Flag in one or more environments and immediately publishes the change. The caller needs Publish access for every environment in the request. When approval is required, use a draft revision instead, unless the caller can bypass draft approvals.
- [Revert a feature to a specific revision](https://docs.growthbook.io/api/features-v2/operation/revertFeatureV2.md): Restores a previously published revision and immediately publishes the result as a new revision. The caller needs Revert access for every affected environment. When approval is required, the request is allowed only if the caller holds the `FlagsBypassApprovals` policy, or the organization enables ei…
- [Get list of feature keys](https://docs.growthbook.io/api/features-v2/operation/getFeatureKeysV2.md)
- [Get stale status for one or more features](https://docs.growthbook.io/api/features-v2/operation/getFeatureStaleV2.md)

#### Feature Revisions

- [List revisions across all features](https://docs.growthbook.io/api/feature-revisions-v2/operation/listRevisionsV2.md): Returns a paginated list of feature revisions across all features in the organization. Use the `featureId` query parameter to filter to a single feature. Revision `rules` is a flat array with per-rule scope.
- [List revisions for a feature](https://docs.growthbook.io/api/feature-revisions-v2/operation/getFeatureRevisionsV2.md): Returns a paginated list of revisions for this feature, sorted newest-first. Revision `rules` is a flat array with per-rule scope.
- [Create a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionV2.md): Creates a new draft revision branched from the current live revision.
- [Get the most recent active draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/getFeatureRevisionLatestV2.md): Returns the most recently updated active draft revision for the feature. Returns 404 if no matching draft exists. Filter by status, author, or use `mine=true` to scope to the calling user's own drafts.
- [Get a single feature revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/getFeatureRevisionV2.md): Returns the revision at the specified version for this feature. Revision `rules` is a flat array with per-rule environment scope.
- [Diff a revision against another revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/getFeatureRevisionDiffV2.md): Returns a schema-keyed JSON diff between this revision and a baseline. The same shapes the in-app review surface produces under `Copy as → Minimal JSON` / `Full JSON`: `minimal` lists only what changed (with id-keyed arrays bucketed into added/removed/modified items and reorder detection), while `fu…
- [Update revision metadata](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionMetadataV2.md)
- [Set the default value in a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionDefaultValueV2.md)
- [Set feature-level prerequisites in a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionPrerequisitesV2.md): Sets the feature-level prerequisites for this revision. Each prerequisite must be a boolean feature flag; the gate is always 'prerequisite flag is on'. The condition is applied automatically — only the flag ID is required.
- [Set holdout in a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionHoldoutV2.md)
- [Set archived state in a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionArchiveV2.md)
- [Toggle an environment on/off in a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionToggleV2.md)
- [Add a rule to a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionRuleAddV2.md): Appends a new rule to the revision's rule list. Supply `allEnvironments: true` on the rule to target all environments, or `environments: [...]` to scope to specific ones.
- [Update a rule in a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionRuleV2.md): Patches fields on an existing rule (identified by `ruleId`). The rule `type` cannot be changed. Scope can be updated via `allEnvironments` / `environments` patch fields.
- [Delete a rule from a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/deleteFeatureRevisionRuleV2.md): Removes the rule from the revision. Any pending ramp actions for this rule are also cleared.
- [Reorder rules in the revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionRulesReorderV2.md): Replaces the flat global rule order. `ruleIds` must contain **exactly** the set of all existing rule IDs in the revision — no additions, omissions, or duplicates.
- [Set ramp schedule for a rule](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionRuleRampScheduleV2.md): Queues a revision-controlled ramp action for this rule. If the rule already has a live ramp schedule, this stores an `update` action applied on publish; otherwise it stores a `create` action. No live schedule config changes are applied immediately by this endpoint.
- [Remove ramp schedule from a rule](https://docs.growthbook.io/api/feature-revisions-v2/operation/deleteFeatureRevisionRuleRampScheduleV2.md): Clears any pending ramp action for this rule. If a live ramp schedule exists, queues a detach that removes it on publish — the rule will show `pendingRamp: "detach"`. If only a pending create exists, it is removed and `pendingRamp` is cleared.
- [Request review for a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionRequestReviewV2.md): Moves the draft into the `pending-review` state and notifies reviewers.
- [Schedule (or cancel) a deferred publish for a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionSchedulePublishV2.md): Schedules the draft to publish on or after `scheduledPublishAt`. When approval is required, publishing waits until the draft is also approved. Send `scheduledPublishAt: null` to cancel the schedule.
- [Submit a review on a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionSubmitReviewV2.md): Submits an `approve`, `request-changes`, or `comment` review on the draft. Contributors cannot approve their own drafts when `blockSelfApproval` is enabled.
- [Recall a review request (revert to draft)](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionRecallReviewV2.md): Retracts the review request, returning the revision from `pending-review`, `changes-requested`, or `approved` back to `draft`. Allowed for any user with draft-management permission on the feature (the same permission required to request review), not only the original requester. Existing review log e…
- [Undo a reviewer's own review verdict](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionUndoReviewV2.md): Reviewer retracts their own verdict. The revision status rewinds to the state implied by the remaining active verdicts from other reviewers: any outstanding `Requested Changes` → `changes-requested`, else any outstanding `Approved` → `approved`, else `pending-review`. Existing review comments are pr…
- [List the activity log for a revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/getFeatureRevisionLogV2.md): Returns every log entry for the revision — content edits (rules, default value, rebases), review lifecycle events (review requested, approved, changes requested, recalled, undone), comments, and other audit events — sorted oldest-first.
- [Edit the comment text of an owned log entry](https://docs.growthbook.io/api/feature-revisions-v2/operation/putFeatureRevisionLogCommentV2.md): Author of a `Comment`, `Approved`, or `Requested Changes` log entry can rewrite its comment text. The entry's action and other audit-trail metadata remain immutable; this only mutates `value.comment`. Other audit events (e.g. `Review Requested`, system events) are not editable.
- [Delete an owned revision Comment entry](https://docs.growthbook.io/api/feature-revisions-v2/operation/deleteFeatureRevisionLogEntryV2.md): Author of a `Comment` log entry can delete it. Verdict entries (Approved, Requested Changes, Review Requested) and other audit-trail events are immutable. To retract a verdict use `/undo-review`; to retract a review request use `/recall-review`.
- [Get merge status for a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/getFeatureRevisionMergeStatusV2.md): Runs the three-way merge between the draft and the current live version without applying it. Conflicts are granular: each conflicting field gets its own key, and rules conflict individually (`rules.<ruleId>`, plus `rules.order` for competing reorders). Pass the returned `liveVersion` as `expectedLiv…
- [Preview a rebase without applying it](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionRebasePreviewV2.md): Dry-run of the rebase: runs the same three-way merge with the supplied `conflictResolutions` and returns every conflict (resolved and unresolved) plus the merged result once all are resolved — without modifying the draft. Use it to iterate on resolutions before committing them via the rebase endpoin…
- [Rebase a draft revision onto the current live version](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionRebaseV2.md): Updates the draft's base revision to match the currently-live revision, applying the draft's changes on top. Supply `conflictResolutions` to resolve conflicting items individually — including per-rule (`rules.<ruleId>`) and rule-order (`rules.order`) conflicts. Supply `expectedLiveVersion` and/or `e…
- [Publish a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionPublishV2.md): Publishes the draft and makes its changes live. The caller needs Publish access for every affected environment. When approval is required, the draft must be approved unless the caller has Bypass draft approvals access. If the organization requires rebasing, an out-of-date draft must be rebased first…
- [Discard a draft revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionDiscardV2.md)
- [Reopen a discarded revision as a draft](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionReopenV2.md): Returns a `discarded` revision to `draft` status so it can be edited, reviewed, and published. Prior review state is not restored — the draft must go back through review if approvals are required.
- [Revert the feature to a prior revision](https://docs.growthbook.io/api/feature-revisions-v2/operation/postFeatureRevisionRevertV2.md)

#### Feature Flags (legacy)

- [Get all features](https://docs.growthbook.io/api/features/operation/listFeatures.md): **Deprecated.** Use [GET /v2/features](#operation/listFeaturesV2) instead.
- [Create a single feature](https://docs.growthbook.io/api/features/operation/postFeature.md): **Deprecated.** Use [POST /v2/features](#operation/postFeatureV2) instead.
- [Get a single feature](https://docs.growthbook.io/api/features/operation/getFeature.md): **Deprecated.** Use [GET /v2/features/:id](#operation/getFeatureV2) instead.
- [Partially update a feature](https://docs.growthbook.io/api/features/operation/updateFeature.md): **Deprecated.** Use [POST /v2/features/:id](#operation/updateFeatureV2) instead.
- [Deletes a single feature](https://docs.growthbook.io/api/features/operation/deleteFeature.md): **Deprecated.** Use [DELETE /v2/features/:id](#operation/deleteFeatureV2) instead.
- [Toggle a feature in one or more environments](https://docs.growthbook.io/api/features/operation/toggleFeature.md): **Deprecated.** Use [POST /v2/features/:id/toggle](#operation/toggleFeatureV2) instead.
- [Revert a feature to a specific revision](https://docs.growthbook.io/api/features/operation/revertFeature.md): **Deprecated.** Use [POST /v2/features/:id/revert](#operation/revertFeatureV2) instead.
- [Get list of feature keys](https://docs.growthbook.io/api/features/operation/getFeatureKeys.md): **Deprecated.** Use [GET /v2/feature-keys](#operation/getFeatureKeysV2) instead.
- [Get stale status for one or more features](https://docs.growthbook.io/api/features/operation/getFeatureStale.md): **Deprecated.** Use [GET /v2/stale-features](#operation/getFeatureStaleV2) instead.

#### Feature Revisions (legacy)

- [List feature revisions](https://docs.growthbook.io/api/feature-revisions/operation/listRevisions.md): **Deprecated.** Use [GET /v2/feature-revisions](#operation/listRevisionsV2) instead.
- [List revisions for a feature](https://docs.growthbook.io/api/feature-revisions/operation/getFeatureRevisions.md): **Deprecated.** Use [GET /v2/features/:id/revisions](#operation/getFeatureRevisionsV2) instead.
- [Create a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevision.md): **Deprecated.** Use [POST /v2/features/:id/revisions](#operation/postFeatureRevisionV2) instead.
- [Get the most recent active draft revision](https://docs.growthbook.io/api/feature-revisions/operation/getFeatureRevisionLatest.md): **Deprecated.** Use [GET /v2/features/:id/revisions/latest](#operation/getFeatureRevisionLatestV2) instead.
- [Get a single feature revision](https://docs.growthbook.io/api/feature-revisions/operation/getFeatureRevision.md): **Deprecated.** Use [GET /v2/features/:id/revisions/:version](#operation/getFeatureRevisionV2) instead.
- [Update revision metadata (comment, title, feature metadata)](https://docs.growthbook.io/api/feature-revisions/operation/putFeatureRevisionMetadata.md): **Deprecated.** Use [PUT /v2/features/:id/revisions/:version/metadata](#operation/putFeatureRevisionMetadataV2) instead.
- [Set the default value in a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/putFeatureRevisionDefaultValue.md): **Deprecated.** Use [PUT /v2/features/:id/revisions/:version/default-value](#operation/putFeatureRevisionDefaultValueV2) instead.
- [Set feature-level prerequisites in a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/putFeatureRevisionPrerequisites.md): **Deprecated.** Use [PUT /v2/features/:id/revisions/:version/prerequisites](#operation/putFeatureRevisionPrerequisitesV2) instead.
- [Set holdout in a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/putFeatureRevisionHoldout.md): **Deprecated.** Use [PUT /v2/features/:id/revisions/:version/holdout](#operation/putFeatureRevisionHoldoutV2) instead.
- [Set archived state in a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/putFeatureRevisionArchive.md): **Deprecated.** Use [PUT /v2/features/:id/revisions/:version/archive](#operation/putFeatureRevisionArchiveV2) instead.
- [Toggle an environment on/off in a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionToggle.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/toggle](#operation/postFeatureRevisionToggleV2) instead.
- [Add a rule to a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionRuleAdd.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/rules](#operation/postFeatureRevisionRuleAddV2) instead, which accepts rules with unified `allEnvironments`/`environments` scope fields instead of a per-environment `environment` parameter.
- [Update a rule in a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/putFeatureRevisionRule.md): **Deprecated.** Use [PUT /v2/features/:id/revisions/:version/rules/:ruleId](#operation/putFeatureRevisionRuleV2) instead, which locates rules by `ruleId` in the flat array without an `environment` parameter.
- [Delete a rule from a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/deleteFeatureRevisionRule.md): **Deprecated.** Use [DELETE /v2/features/:id/revisions/:version/rules/:ruleId](#operation/deleteFeatureRevisionRuleV2) instead, which removes the rule from the flat array without an `environment` parameter.
- [Reorder rules in an environment](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionRulesReorder.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/rules/reorder](#operation/postFeatureRevisionRulesReorderV2) instead, which reorders the global flat rule array without an `environment` parameter.
- [Set ramp schedule for a rule](https://docs.growthbook.io/api/feature-revisions/operation/putFeatureRevisionRuleRampSchedule.md): **Deprecated.** Use [PUT /v2/features/:id/revisions/:version/rules/:ruleId/ramp-schedule](#operation/putFeatureRevisionRuleRampScheduleV2) instead.
- [Remove ramp schedule from a rule](https://docs.growthbook.io/api/feature-revisions/operation/deleteFeatureRevisionRuleRampSchedule.md): **Deprecated.** Use [DELETE /v2/features/:id/revisions/:version/rules/:ruleId/ramp-schedule](#operation/deleteFeatureRevisionRuleRampScheduleV2) instead.
- [Request review for a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionRequestReview.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/request-review](#operation/postFeatureRevisionRequestReviewV2) instead.
- [Submit a review on a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionSubmitReview.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/submit-review](#operation/postFeatureRevisionSubmitReviewV2) instead.
- [Get merge status for a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/getFeatureRevisionMergeStatus.md): **Deprecated.** Use [GET /v2/features/:id/revisions/:version/merge-status](#operation/getFeatureRevisionMergeStatusV2) instead.
- [Rebase a draft revision onto the current live version](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionRebase.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/rebase](#operation/postFeatureRevisionRebaseV2) instead.
- [Publish a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionPublish.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/publish](#operation/postFeatureRevisionPublishV2) instead.
- [Discard a draft revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionDiscard.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/discard](#operation/postFeatureRevisionDiscardV2) instead.
- [Revert the feature to a prior revision](https://docs.growthbook.io/api/feature-revisions/operation/postFeatureRevisionRevert.md): **Deprecated.** Use [POST /v2/features/:id/revisions/:version/revert](#operation/postFeatureRevisionRevertV2) instead.

#### Ramp Schedules

- [Get all rampSchedules](https://docs.growthbook.io/api/ramp-schedules/operation/listRampSchedules.md): Returns all ramp schedules for the organization, with optional filters.
- [Create a ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/postRampSchedule.md)
- [Start a ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/startRampSchedule.md): Transitions the schedule from `ready` to `running`. The schedule must have at least one target rule attached — a schedule created without targets starts in `pending` and moves to `ready` automatically when the first target is attached via `/actions/add-target`.
- [Pause a ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/pauseRampSchedule.md): Pauses a `running` schedule. Traffic percentages are frozen at their current values; no step advancement happens while paused. Records `pausedAt` so that interval timing can be correctly offset when the schedule resumes.
- [Resume a paused ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/resumeRampSchedule.md): Resumes a `paused` schedule without moving the current step. Timing anchors (`phaseStartedAt`, `startedAt`) are shifted forward by the pause duration so that interval-based steps continue from where they left off rather than restarting their clock.
- [Roll back a ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/rollbackRampSchedule.md): Rewinds all ramp effects (rule coverage, targeting, etc.) to the starting position and lands in terminal `rolled-back` status. The reason is persisted as `lastRollbackReason` (prefixed with `Manual: `) and surfaced in the UI.
- [Restart a terminal ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/restartRampSchedule.md): Brings a `rolled-back` (or `completed`) schedule back into `running` in a single call. Any prior start-on-date delays are cleared (`startedAt`, `phaseStartedAt`, etc. are reset), `currentStepIndex` is normalised to `-1`, then the same logic as `/actions/start` runs to apply start actions and advance…
- [Jump to a specific step](https://docs.growthbook.io/api/ramp-schedules/operation/jumpRampSchedule.md): Teleports the schedule to `targetStepIndex` (forward or backward) and leaves it `paused`. Resets timing anchors so the destination step's interval starts fresh when the schedule is next resumed or started.
- [Complete a ramp schedule immediately](https://docs.growthbook.io/api/ramp-schedules/operation/completeRampSchedule.md): Immediately applies the schedule's end-state rule patches (the equivalent of what would happen after the last step advances normally) and marks the schedule as `completed`, skipping any remaining steps.
- [Approve the pending approval gate](https://docs.growthbook.io/api/ramp-schedules/operation/approveStepRampSchedule.md): Clears whichever approval gate is currently pending on the schedule:
- [Add a target rule to a ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/addTargetRampSchedule.md): Attaches an additional feature rule to this ramp schedule. The `ruleId` must identify a rule that is already published and must not already be controlled by another schedule. `environment` is accepted for backward compatibility with pre-v2 ramps but is deprecated and no longer required.
- [Remove a target rule from a ramp schedule](https://docs.growthbook.io/api/ramp-schedules/operation/ejectTargetRampSchedule.md): Detaches a target rule from this ramp schedule. Identify the target either by its `targetId` or by the `[ruleId, environment]` pair.
- [Advance to the next step, overriding any holds](https://docs.growthbook.io/api/ramp-schedules/operation/apiAdvanceRampSchedule.md): Moves the schedule to the next step, bypassing **all** hold conditions — interval, min sample size, and monitoring signal holds. Accepts `running` or `paused` status; if paused, the schedule is implicitly resumed (timing anchors recalculated) before the step moves.
- [Get ramp schedule status summary](https://docs.growthbook.io/api/ramp-schedules/operation/getRampScheduleStatus.md): Returns a real-time status summary for a ramp schedule: current step, overall health decision, traffic quality, and per-metric effect sizes. Designed for CI pipeline integrations and monitoring dashboards that need a single call to determine whether it is safe to advance.
- [Set ramp monitoring mode](https://docs.growthbook.io/api/ramp-schedules/operation/setMonitoringModeRampSchedule.md): Sets the user preference for ramp monitoring updates. In `manual` mode, automatic snapshot scheduling is disabled and operators must click Update manually. In `auto` mode, snapshots run automatically when the current step is monitored and the ramp is running.
- [Toggle automatic monitoring updates](https://docs.growthbook.io/api/ramp-schedules/operation/setAutoUpdateRampSchedule.md): Deprecated alias for setting monitoring mode. Prefer `/actions/set-monitoring-mode`.
- [Update ramp monitoring configuration](https://docs.growthbook.io/api/ramp-schedules/operation/updateRampScheduleMonitoring.md): Replaces the monitoring configuration. Health-action thresholds (`srmAction`, `noTrafficAction`, etc.) can be updated at any time.
- [Update ramp lockdown configuration](https://docs.growthbook.io/api/ramp-schedules/operation/updateRampScheduleLockdown.md): Sets the lockdown mode. `locked` prevents other users from publishing unrelated changes to the parent feature while the ramp is running — useful when you want to ensure no external edits interfere with a live rollout. It does **not** affect the ramp's own auto-advancement or monitoring behavior; use…
- [Update ramp schedule steps](https://docs.growthbook.io/api/ramp-schedules/operation/updateRampScheduleSteps.md): Fully replaces the steps array for a ramp schedule. Only allowed when the schedule is in a non-running, non-terminal state (`ready`, `pending`, or `paused`). Pause a running schedule first; restart a terminal schedule first.
- [Trigger a manual monitoring update](https://docs.growthbook.io/api/ramp-schedules/operation/refreshMonitoringRampSchedule.md): Queues a new analysis snapshot for the schedule's monitoring experiment. The snapshot runs asynchronously — poll `GET /ramp-schedules/:id/status` until `snapshotAt` advances to confirm results are ready.
- [Get a single rampSchedule](https://docs.growthbook.io/api/ramp-schedules/operation/getRampSchedule.md)
- [Update a single rampSchedule](https://docs.growthbook.io/api/ramp-schedules/operation/updateRampSchedule.md): Updates the name, steps, endActions, startDate, or cutoffDate of a ramp schedule.
- [Delete a single rampSchedule](https://docs.growthbook.io/api/ramp-schedules/operation/deleteRampSchedule.md): Permanently deletes a ramp schedule. This does not undo any rule patches that were already applied by completed steps.

#### Data Sources

- [Get all data sources](https://docs.growthbook.io/api/data-sources/operation/listDataSources.md)
- [Get a single data source](https://docs.growthbook.io/api/data-sources/operation/getDataSource.md)
- [Get a Data Source's Information Schema](https://docs.growthbook.io/api/data-sources/operation/getInformationSchema.md): Returns cached database schema metadata for a data source, including databases, schemas, and tables. The information schema is automatically created when a SQL-based data source is added. Not all data source types support information schemas.
- [Get a single Information Schema Table by id](https://docs.growthbook.io/api/data-sources/operation/getInformationSchemaTable.md): Returns cached metadata for a specific table in the Data Source, including columns and their data types. Not all data source types support information schemas.

#### Fact Tables

- [Get all fact tables](https://docs.growthbook.io/api/fact-tables/operation/listFactTables.md)
- [Create a single fact table](https://docs.growthbook.io/api/fact-tables/operation/postFactTable.md)
- [Get a single fact table](https://docs.growthbook.io/api/fact-tables/operation/getFactTable.md)
- [Update a single fact table](https://docs.growthbook.io/api/fact-tables/operation/updateFactTable.md)
- [Deletes a single fact table](https://docs.growthbook.io/api/fact-tables/operation/deleteFactTable.md)
- [Get all filters for a fact table](https://docs.growthbook.io/api/fact-tables/operation/listFactTableFilters.md)
- [Create a single fact table filter](https://docs.growthbook.io/api/fact-tables/operation/postFactTableFilter.md)
- [Get a single fact filter](https://docs.growthbook.io/api/fact-tables/operation/getFactTableFilter.md)
- [Update a single fact table filter](https://docs.growthbook.io/api/fact-tables/operation/updateFactTableFilter.md)
- [Deletes a single fact table filter](https://docs.growthbook.io/api/fact-tables/operation/deleteFactTableFilter.md)
- [Create a virtual (computed) column on a fact table](https://docs.growthbook.io/api/fact-tables/operation/postFactTableVirtualColumn.md)
- [Update a virtual (computed) column on a fact table](https://docs.growthbook.io/api/fact-tables/operation/updateFactTableVirtualColumn.md)
- [Delete a virtual (computed) column from a fact table](https://docs.growthbook.io/api/fact-tables/operation/deleteFactTableVirtualColumn.md)
- [Get the materialization status of a fact table's shared daily aggregated tables](https://docs.growthbook.io/api/fact-tables/operation/getAggregatedFactTables.md)
- [Force a refresh or full restate of a fact table's shared daily aggregated tables](https://docs.growthbook.io/api/fact-tables/operation/refreshAggregatedFactTable.md)
- [List aggregated table runs](https://docs.growthbook.io/api/fact-tables/operation/listAggregatedTableRuns.md)
- [Get a single aggregated table run](https://docs.growthbook.io/api/fact-tables/operation/getAggregatedTableRun.md)
- [Bulk import fact tables, filters, and metrics](https://docs.growthbook.io/api/fact-tables/operation/postBulkImportFacts.md): Creates or updates Fact Tables, Fact Table filters, and Fact Metrics. Resources upsert by `id`. Pass `dryRun: true` to validate with zero writes. Not transactional: a live mid-loop failure returns HTTP 400 (403 for a permission failure) with write counts and `errors`.

#### Fact Metrics

- [Get all fact metrics](https://docs.growthbook.io/api/fact-metrics/operation/listFactMetrics.md)
- [Create a single fact metric](https://docs.growthbook.io/api/fact-metrics/operation/postFactMetric.md)
- [Get a single fact metric](https://docs.growthbook.io/api/fact-metrics/operation/getFactMetric.md)
- [Update a single fact metric](https://docs.growthbook.io/api/fact-metrics/operation/updateFactMetric.md)
- [Deletes a single fact metric](https://docs.growthbook.io/api/fact-metrics/operation/deleteFactMetric.md)
- [Create a fact metric analysis](https://docs.growthbook.io/api/fact-metrics/operation/postFactMetricAnalysis.md)

#### Metrics (legacy)

- [Get all metrics](https://docs.growthbook.io/api/metrics/operation/listMetrics.md)
- [Create a single metric](https://docs.growthbook.io/api/metrics/operation/postMetric.md)
- [Get a single metric](https://docs.growthbook.io/api/metrics/operation/getMetric.md)
- [Update a metric](https://docs.growthbook.io/api/metrics/operation/putMetric.md)
- [Deletes a metric](https://docs.growthbook.io/api/metrics/operation/deleteMetric.md)
- [Get results for all experiments that use a metric](https://docs.growthbook.io/api/metrics/operation/listMetricExperiments.md): Returns, for each experiment that uses the given metric (directly or via a metric group), the per-variation results for that metric from the latest snapshot. Supports the same filtering as the experiment list views via a raw search string or structured query params. Note: at most the 1000 most recen…

#### Experiments

- [Get all experiments](https://docs.growthbook.io/api/experiments/operation/listExperiments.md)
- [Create a single experiment](https://docs.growthbook.io/api/experiments/operation/postExperiment.md)
- [Get latest results for many experiments](https://docs.growthbook.io/api/experiments/operation/listExperimentResults.md): Returns the latest non-dimension snapshot for each experiment matching the filters. Use this to scan results across a portfolio in one call.
- [Get a single experiment](https://docs.growthbook.io/api/experiments/operation/getExperiment.md)
- [Update a single experiment](https://docs.growthbook.io/api/experiments/operation/updateExperiment.md)
- [Get an experiment pre-launch checklist status](https://docs.growthbook.io/api/experiments/operation/getExperimentStartChecklist.md)
- [Get results for an experiment](https://docs.growthbook.io/api/experiments/operation/getExperimentResults.md)
- [Start/Stage an experiment](https://docs.growthbook.io/api/experiments/operation/postExperimentStart.md): Starts an experiment or stages it for a future start if a `statusUpdateSchedule` is set on the experiment.
- [Mark manual pre-launch checklist items complete](https://docs.growthbook.io/api/experiments/operation/postExperimentStartChecklistManualComplete.md)
- [Stop an experiment](https://docs.growthbook.io/api/experiments/operation/postExperimentStop.md)
- [Set an experiment's schedule and shipping automation](https://docs.growthbook.io/api/experiments/operation/putExperimentSchedule.md): Full-replace of the experiment's scheduled start/end and end-of-experiment shipping automation. The body is the complete desired state: any omitted field is cleared (omit `startAt` to remove a scheduled start; send an empty body to clear the whole schedule). Provide either `stopAt` or `stopAfter`, n…
- [Modify temporary rollout status for a stopped experiment](https://docs.growthbook.io/api/experiments/operation/postExperimentModifyTemporaryRollout.md)
- [Create Experiment Snapshot](https://docs.growthbook.io/api/experiments/operation/postExperimentSnapshot.md)
- [Upload a variation screenshot](https://docs.growthbook.io/api/experiments/operation/postVariationImageUpload.md)
- [Delete a variation screenshot](https://docs.growthbook.io/api/experiments/operation/deleteVariationScreenshot.md)
- [Get a list of experiments with names and ids](https://docs.growthbook.io/api/experiments/operation/getExperimentNames.md)
- [Post a comment on an experiment](https://docs.growthbook.io/api/experiments/operation/postExperimentComment.md): Adds a new comment to an experiment's discussion thread.

#### Namespaces

- [Get all namespaces](https://docs.growthbook.io/api/namespaces/operation/listNamespaces.md)
- [Create a namespace](https://docs.growthbook.io/api/namespaces/operation/postNamespace.md)
- [Get a single namespace](https://docs.growthbook.io/api/namespaces/operation/getNamespace.md)
- [Update a namespace](https://docs.growthbook.io/api/namespaces/operation/putNamespace.md)
- [Delete a namespace](https://docs.growthbook.io/api/namespaces/operation/deleteNamespace.md): Permanently removes a namespace from the organization. Returns a 409 error if any active experiments currently reference this namespace — disable or remove those references first.
- [Get namespace membership](https://docs.growthbook.io/api/namespaces/operation/getNamespaceMemberships.md)
- [Rotate namespace seed](https://docs.growthbook.io/api/namespaces/operation/postNamespaceRotateSeed.md): ⚠️ Dangerous: sets a new seed for a multiRange namespace. Every user's bucket position within the namespace is re-computed immediately, which re-randomizes traffic eligibility for **all** experiments currently using this namespace. Only do this if you intentionally want to reshuffle all allocations…

#### Experiment Snapshots

- [Get an experiment snapshot status](https://docs.growthbook.io/api/snapshots/operation/getExperimentSnapshot.md)

#### Dimensions

- [Get all dimensions](https://docs.growthbook.io/api/dimensions/operation/listDimensions.md)
- [Create a single dimension](https://docs.growthbook.io/api/dimensions/operation/postDimension.md)
- [Get a single dimension](https://docs.growthbook.io/api/dimensions/operation/getDimension.md)
- [Update a single dimension](https://docs.growthbook.io/api/dimensions/operation/updateDimension.md)
- [Deletes a single dimension](https://docs.growthbook.io/api/dimensions/operation/deleteDimension.md)

#### Segments

- [Get all segments](https://docs.growthbook.io/api/segments/operation/listSegments.md)
- [Create a single segment](https://docs.growthbook.io/api/segments/operation/postSegment.md)
- [Get a single segment](https://docs.growthbook.io/api/segments/operation/getSegment.md)
- [Update a single segment](https://docs.growthbook.io/api/segments/operation/updateSegment.md)
- [Deletes a single segment](https://docs.growthbook.io/api/segments/operation/deleteSegment.md)

#### Experiment Reports

- [Get all reports](https://docs.growthbook.io/api/reports/operation/listReports.md)
- [Create a new report](https://docs.growthbook.io/api/reports/operation/postReport.md)
- [Get a single report](https://docs.growthbook.io/api/reports/operation/getReport.md)
- [Refresh a report by re-running its analysis](https://docs.growthbook.io/api/reports/operation/postReportRefresh.md)
- [Update report metadata (title, description, visibility)](https://docs.growthbook.io/api/reports/operation/putReportMetadata.md)
- [Update report analysis settings](https://docs.growthbook.io/api/reports/operation/putReportSettings.md): Updates the analysis settings for an existing report. Changes are staged and do not take effect until you call `POST /reports/:id/refresh`.

#### SDK Connections

- [Get all sdk connections](https://docs.growthbook.io/api/sdk-connections/operation/listSdkConnections.md)
- [Create a single sdk connection](https://docs.growthbook.io/api/sdk-connections/operation/postSdkConnection.md)
- [Get a single sdk connection](https://docs.growthbook.io/api/sdk-connections/operation/getSdkConnection.md)
- [Update a single sdk connection](https://docs.growthbook.io/api/sdk-connections/operation/putSdkConnection.md)
- [Deletes a single SDK connection](https://docs.growthbook.io/api/sdk-connections/operation/deleteSdkConnection.md)
- [Find a single sdk connection by its key](https://docs.growthbook.io/api/sdk-connections/operation/lookupSdkConnectionByKey.md)

#### Visual Changesets

- [Get all visual changesets](https://docs.growthbook.io/api/visual-changesets/operation/listVisualChangesets.md)
- [Create a visual changeset for an experiment](https://docs.growthbook.io/api/visual-changesets/operation/postVisualChangesets.md)
- [Get a single visual changeset](https://docs.growthbook.io/api/visual-changesets/operation/getVisualChangeset.md)
- [Update a visual changeset](https://docs.growthbook.io/api/visual-changesets/operation/putVisualChangeset.md)
- [Create a visual change for a visual changeset](https://docs.growthbook.io/api/visual-changesets/operation/postVisualChange.md)
- [Update a visual change for a visual changeset](https://docs.growthbook.io/api/visual-changesets/operation/putVisualChange.md)

#### Saved Groups

- [Get all saved group](https://docs.growthbook.io/api/saved-groups/operation/listSavedGroups.md)
- [Create a single saved group](https://docs.growthbook.io/api/saved-groups/operation/postSavedGroup.md)
- [Get a single saved group](https://docs.growthbook.io/api/saved-groups/operation/getSavedGroup.md)
- [Partially update a single saved group](https://docs.growthbook.io/api/saved-groups/operation/updateSavedGroup.md): Applies the change immediately and records it as a published revision, so it appears in history and fires revision webhooks. When the organization requires approvals, open a draft instead or pass `bypassApproval` with the bypass permission.
- [Deletes a single saved group](https://docs.growthbook.io/api/saved-groups/operation/deleteSavedGroup.md)
- [Archive a single saved group](https://docs.growthbook.io/api/saved-groups/operation/archiveSavedGroup.md): Archives a Saved Group. If it is still referenced by a Feature Flag, experiment, or another Saved Group, the API returns 422 with the affected references. Send `"ignoreWarnings": true` to acknowledge those references and continue. When approval is required, create and publish an archive revision ins…
- [Unarchive a single saved group](https://docs.growthbook.io/api/saved-groups/operation/unarchiveSavedGroup.md): Unarchives a Saved Group. When approval is required, create and publish an unarchive revision instead, or use a caller with Bypass draft approvals access. A successful response lists any skipped gates in `bypassedGates`.
- [Get features, experiments, and saved groups that reference this saved group](https://docs.growthbook.io/api/saved-groups/operation/getSavedGroupReferences.md)

#### Saved Group Revisions

- [List saved-group revisions across the organization](https://docs.growthbook.io/api/saved-group-revisions/operation/listSavedGroupRevisions.md): Returns a paginated list of revisions across all saved groups in the organization, sorted newest-first. Optionally filtered by saved group, status, author, or the calling user's involvement.
- [List revisions for a saved group](https://docs.growthbook.io/api/saved-group-revisions/operation/getSavedGroupRevisions.md): Returns a paginated list of revisions for this saved group, sorted newest-first. Optionally filtered by status, author, or the calling user's involvement.
- [Create a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevision.md): Creates a new draft revision branched from the current live saved group. A saved group can have multiple concurrent drafts; use this to start an isolated line of edits.
- [Get the most recent active draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/getSavedGroupRevisionLatest.md): Returns the most recently updated open (non-merged, non-discarded) revision for the saved group. Returns 404 if there is no active draft. Pass `mine=true` to restrict to drafts authored by the calling user (requires a user-scoped API key).
- [Get a single saved group revision](https://docs.growthbook.io/api/saved-group-revisions/operation/getSavedGroupRevision.md): Returns the revision at the specified version for this saved group. Use `GET /saved-groups-revisions/{savedGroupId}/latest` for the most recent active draft.
- [Update saved group metadata in a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/putSavedGroupRevisionMetadata.md): Stages metadata changes (name, owner, description, projects) on the draft. Pass `version: "new"` to auto-create a draft. The change is only applied to the live saved group when the revision is merged.
- [Update the condition of a condition saved group draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/putSavedGroupRevisionCondition.md): Stages a new JSON-encoded condition for the draft. Only valid for `condition` saved groups. Pass `version: "new"` to auto-create a draft.
- [Replace the values list in a list saved group draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/putSavedGroupRevisionValues.md): Replaces the entire `values` array atomically. Only valid for `list` saved groups. For safe concurrent updates against a draft, prefer `POST .../items/add` and `POST .../items/remove`. Pass `version: "new"` to auto-create a draft.
- [Stage an archive/unarchive in a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/putSavedGroupRevisionArchive.md): Stages an archive or unarchive on the draft. Pass `version: "new"` to auto-create a draft. Archived saved groups can be permanently deleted via `DELETE /saved-groups/{id}` once the archive is published.
- [Append items to a list saved group draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionItemsAdd.md): Appends the provided items (deduplicated) to the draft's `values` array. Only valid for `list` saved groups. Pass `version: "new"` to auto-create a draft. Duplicate items are merged on top of any existing draft, so multiple successive add/remove calls accumulate.
- [Remove items from a list saved group draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionItemsRemove.md): Removes the provided items from the draft's `values` array. Only valid for `list` saved groups. Pass `version: "new"` to auto-create a draft.
- [Request review for a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionRequestReview.md): Moves the draft from `draft` into `pending-review`. Notifies reviewers per the org's approval-flow settings.
- [Submit a review on a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionSubmitReview.md): Submits an `approve`, `request-changes`, or `comment` review on the revision. Submitting `approve` or `request-changes` needs Review access. A `comment` is participation rather than a verdict, so it is also open to the Comments permission or draft authority on the entity. Authors and contributors ca…
- [Recall a review request](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionRecallReview.md): Pulls a revision in review (`pending-review`, `changes-requested`, or `approved`) back to `draft`, clearing existing reviews and disarming any auto-publish-on-approval.
- [Reopen a discarded revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionReopen.md): Returns a previously discarded revision to `draft` status so it can be edited and published again. Only discarded revisions can be reopened.
- [Schedule (or cancel) a deferred publish](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionSchedulePublish.md): Arms a revision to publish automatically at a future time. Pass `scheduledPublishAt` as an RFC3339 timestamp in the future to arm, or `null` to cancel a pending schedule. Requires the `scheduled-revisions` commercial feature and publish permission on the Saved Group. A draft that still requires appr…
- [Retract your own review verdict](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionUndoReview.md): Retracts the calling user's own active `approve` or `request-changes` verdict, returning the revision to `pending-review`. Review comments stay in the log. Retracting a `request-changes` can leave the revision approved by someone else, in which case an armed auto-publish fires.
- [Get merge status for a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/getSavedGroupRevisionMergeStatus.md): Runs a dry-run merge of the draft against the current live saved group and returns any conflicts. Use this before publishing to preview changes and detect conflicting edits.
- [Rebase a draft revision onto the current live saved group](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionRebase.md): Updates the draft's base snapshot to the current live state, applying the draft's changes on top. Supply `conflictResolutions` to resolve any conflicting fields. Strategies are `overwrite` (use the draft's value), `discard` (keep the live value), or `union` (merge arrays — use only on `values`). Opt…
- [Publish a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionPublish.md): Publishes the draft and applies its changes to the live Saved Group. The caller needs Publish access in every assigned Project. When approval is required, the draft must be approved unless the caller has Bypass draft approvals access. If the organization requires rebasing, an out-of-date draft must…
- [Discard a draft revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionDiscard.md): Permanently discards a draft revision. Only open revisions (not merged or already-discarded) can be discarded.
- [Revert the saved group to a prior revision](https://docs.growthbook.io/api/saved-group-revisions/operation/postSavedGroupRevisionRevert.md): Creates a new draft (or immediately publishes) whose content matches the specified historical revision. Defaults to creating a draft; when the org enables 'reverts bypass approval' it defaults to publishing immediately. Pass `strategy` to override.

#### Constants

- [Get all constants](https://docs.growthbook.io/api/constants/operation/listConstants.md)
- [Create a single constant](https://docs.growthbook.io/api/constants/operation/postConstant.md)
- [Get features and constants that reference this constant](https://docs.growthbook.io/api/constants/operation/getConstantReferences.md)
- [Get a single constant](https://docs.growthbook.io/api/constants/operation/getConstant.md)
- [Partially update a single constant](https://docs.growthbook.io/api/constants/operation/updateConstant.md): Applies the change immediately and records it as a published revision, so it appears in history and fires revision webhooks. When the organization requires approvals, open a draft instead or pass `bypassApproval` with the bypass permission.
- [Delete a single constant](https://docs.growthbook.io/api/constants/operation/deleteConstant.md)
- [Archive a single constant](https://docs.growthbook.io/api/constants/operation/archiveConstant.md)
- [Unarchive a single constant](https://docs.growthbook.io/api/constants/operation/unarchiveConstant.md)

#### Constant Revisions

- [List constant revisions across the organization](https://docs.growthbook.io/api/constant-revisions/operation/listConstantRevisions.md): Returns a paginated list of revisions across all constants in the organization, sorted newest-first. Optionally filtered by constant, status, author, or the calling user's involvement.
- [List revisions for a constant](https://docs.growthbook.io/api/constant-revisions/operation/getConstantRevisions.md): Returns a paginated list of revisions for this constant, sorted newest-first. Optionally filtered by status, author, or the calling user's involvement.
- [Create a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevision.md): Creates a new draft revision branched from the current live constant. A constant can have multiple concurrent drafts; use this to start an isolated line of edits.
- [Get the most recent active draft revision](https://docs.growthbook.io/api/constant-revisions/operation/getConstantRevisionLatest.md): Returns the most recently updated open (non-merged, non-discarded) revision for the constant. Returns 404 if there is no active draft. Pass `mine=true` to restrict to drafts authored by the calling user (requires a user-scoped API key).
- [Get a single constant revision](https://docs.growthbook.io/api/constant-revisions/operation/getConstantRevision.md): Returns the revision at the specified version for this constant. Use `GET /constants-revisions/{key}/latest` for the most recent active draft.
- [Update constant metadata in a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/putConstantRevisionMetadata.md): Stages metadata changes (name, owner, description, project) on the draft. Pass `version: "new"` to auto-create a draft. The change is only applied to the live constant when the revision is merged.
- [Update the value of a constant draft revision](https://docs.growthbook.io/api/constant-revisions/operation/putConstantRevisionValue.md): Stages a new default `value` and/or per-environment `environmentValues` on the draft. At least one must be supplied. Pass `version: "new"` to auto-create a draft. The value must match the constant's type (valid JSON for `json` constants).
- [Stage an archive/unarchive in a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/putConstantRevisionArchive.md): Stages an archive or unarchive on the draft. Pass `version: "new"` to auto-create a draft. Archived constants can be permanently deleted via `DELETE /constants/{key}` once the archive is published.
- [Request review for a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionRequestReview.md): Moves the draft from `draft` into `pending-review`. Notifies reviewers per the org's approval-flow settings.
- [Submit a review on a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionSubmitReview.md): Submits an `approve`, `request-changes`, or `comment` review on the revision. Submitting `approve` or `request-changes` needs Review access. A `comment` is participation rather than a verdict, so it is also open to the Comments permission or draft authority on the entity. Authors and contributors ca…
- [Recall a review request](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionRecallReview.md): Pulls a revision in review (`pending-review`, `changes-requested`, or `approved`) back to `draft`, clearing existing reviews and disarming any auto-publish-on-approval.
- [Reopen a discarded revision](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionReopen.md): Returns a previously discarded revision to `draft` status so it can be edited and published again. Only discarded revisions can be reopened.
- [Schedule (or cancel) a deferred publish](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionSchedulePublish.md): Arms a revision to publish automatically at a future time. Pass `scheduledPublishAt` as an RFC3339 timestamp in the future to arm, or `null` to cancel a pending schedule. Requires the `scheduled-revisions` commercial feature and publish permission on the Constant. A draft that still requires approva…
- [Retract your own review verdict](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionUndoReview.md): Retracts the calling user's own active `approve` or `request-changes` verdict, returning the revision to `pending-review`. Review comments stay in the log. Retracting a `request-changes` can leave the revision approved by someone else, in which case an armed auto-publish fires.
- [Get merge status for a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/getConstantRevisionMergeStatus.md): Runs a dry-run merge of the draft against the current live constant and returns any conflicts. Use this before publishing to preview changes and detect conflicting edits.
- [Rebase a draft revision onto the current live constant](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionRebase.md): Updates the draft's base snapshot to the current live state, applying the draft's changes on top. Supply `conflictResolutions` to resolve any conflicting fields. Strategies are `overwrite` (use the draft's value) or `discard` (keep the live value).
- [Publish a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionPublish.md): Publishes the draft and makes its changes live. The caller needs Publish access for the affected environments. When approval is required, the draft must be approved unless the caller has Bypass draft approvals access. If the organization requires rebasing, an out-of-date draft must be rebased first;…
- [Discard a draft revision](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionDiscard.md): Permanently discards a draft revision. Only open revisions (not merged or already-discarded) can be discarded.
- [Revert the constant to a prior revision](https://docs.growthbook.io/api/constant-revisions/operation/postConstantRevisionRevert.md): Creates a new draft (or immediately publishes) whose content matches the specified historical revision. Defaults to creating a draft; when the org enables 'reverts bypass approval' it defaults to publishing immediately. Pass `strategy` to override.

#### Configs

- [Get all configs](https://docs.growthbook.io/api/configs/operation/listConfigs.md)
- [Create a single config](https://docs.growthbook.io/api/configs/operation/postConfig.md)
- [Get features and configs that reference this config](https://docs.growthbook.io/api/configs/operation/getConfigReferences.md)
- [Get the feature rules and default values implementing each key](https://docs.growthbook.io/api/configs/operation/getConfigKeyUsage.md): Lists every feature rule and default value that overrides a key of this config's lineage family, so you can see which keys are implemented and where.
- [Get the full lineage (family tree) for a config](https://docs.growthbook.io/api/configs/operation/getConfigLineage.md)
- [Verify a config's schema against a source (drift check)](https://docs.growthbook.io/api/configs/operation/verifyConfigSchema.md)
- [Export a config's schema](https://docs.growthbook.io/api/configs/operation/getConfigSchema.md)
- [Get a single config](https://docs.growthbook.io/api/configs/operation/getConfig.md)
- [Partially update a single config](https://docs.growthbook.io/api/configs/operation/updateConfig.md): Applies the change immediately and records it as a published revision, so it appears in history and fires revision webhooks. When the organization requires approvals, open a draft instead or pass `bypassApproval` with the bypass permission.
- [Delete a single config](https://docs.growthbook.io/api/configs/operation/deleteConfig.md)
- [Archive a single config](https://docs.growthbook.io/api/configs/operation/archiveConfig.md): Archives a config. A child config (including an environment/project override) is archived outright when its live value is an empty patch or nothing serves it. When archiving would strip a value that live features or other configs still consume, the request returns a 422 listing the blocking gates —…
- [Unarchive a single config](https://docs.growthbook.io/api/configs/operation/unarchiveConfig.md)
- [Lock a config at its current published revision](https://docs.growthbook.io/api/configs/operation/lockConfig.md): Locks the Config to its current published revision. Drafts can still be created and edited, but direct updates, publishes, scheduled publishes, reverts, and archives are blocked. The response returns the pinned revision in `lockedRevision`. Unlocking requires Bypass draft approvals access.
- [Unlock a config](https://docs.growthbook.io/api/configs/operation/unlockConfig.md): Removes the Config lock so changes can be published again. The caller must have Bypass draft approvals access in the Config's Project.

#### Config Revisions

- [List config revisions across the organization](https://docs.growthbook.io/api/config-revisions/operation/listConfigRevisions.md): Returns a paginated list of revisions across all configs in the organization, sorted newest-first. Optionally filtered by config, status, author, or the calling user's involvement.
- [List revisions for a config](https://docs.growthbook.io/api/config-revisions/operation/getConfigRevisions.md): Returns a paginated list of revisions for this config, sorted newest-first. Optionally filtered by status, author, or the calling user's involvement.
- [Create a draft revision](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevision.md): Creates a new draft revision branched from the current live config. A config can have multiple concurrent drafts; use this to start an isolated line of edits.
- [Get the most recent active draft revision](https://docs.growthbook.io/api/config-revisions/operation/getConfigRevisionLatest.md): Returns the most recently updated open (non-merged, non-discarded) revision for the config. Returns 404 if there is no active draft. Pass `mine=true` to restrict to drafts authored by the calling user (requires a user-scoped API key).
- [Get a single config revision](https://docs.growthbook.io/api/config-revisions/operation/getConfigRevision.md): Returns the revision at the specified version for this config. Use `GET /configs-revisions/{key}/latest` for the most recent active draft.
- [Update config metadata in a draft revision](https://docs.growthbook.io/api/config-revisions/operation/putConfigRevisionMetadata.md): Stages metadata changes (name, owner, description, project, lineage parent, extensibility) on the draft. Pass `version: "new"` to auto-create a draft. The change is only applied to the live config when the revision is merged.
- [Update the value of a config draft revision](https://docs.growthbook.io/api/config-revisions/operation/putConfigRevisionValue.md): Stages a new `value` (this config's own JSON object) on the draft. Pass `version: "new"` to auto-create a draft. A `@config:` inheritance entry in the value is rejected — express lineage via the `parent`/`extends` metadata fields instead. Configs are environment-agnostic: there is no per-environment…
- [Set one property of a config draft revision's value](https://docs.growthbook.io/api/config-revisions/operation/putConfigRevisionProperty.md): Stages a single property of this config's own value on the draft, leaving every other property untouched. Prefer this over `PUT .../value` when changing one field: a whole-value write from a stale read silently drops properties someone else added in the meantime.
- [Remove one property from a config draft revision's value](https://docs.growthbook.io/api/config-revisions/operation/deleteConfigRevisionProperty.md): Stages removal of a single property from this config's own value on the draft; the config then inherits that property from its parent (if any). Every other property is untouched. Pass `version: "new"` to auto-create a draft.
- [Update or import the schema of a config draft revision](https://docs.growthbook.io/api/config-revisions/operation/putConfigRevisionSchema.md): Stages this config's field schema on the draft. Provide exactly ONE source: - `schema`: a schema document — `{ type: "json-schema", value }` (a JSON Schema object) or `{ type: "typescript", value }` (TypeScript source). **JSON Schema is the recommended ("happy path") format** — it is the canonical p…
- [Set (or update) a config's per-source render projection on a draft](https://docs.growthbook.io/api/config-revisions/operation/putConfigRevisionProjection.md): Stages a per-source render projection on the draft, AND the schema it implies. Provide a named `schema` source (`{ type: "typescript" | "protobuf" | "python" | "go" | "rust" | "json-schema", value }`) for the consuming codebase identified by `source`: GrowthBook derives the config's canonical schema…
- [Remove a config's per-source render projection on a draft](https://docs.growthbook.io/api/config-revisions/operation/deleteConfigRevisionProjection.md): Stages removal of the `source` projection from `renderProjections` on the draft (the canonical schema is unchanged). Published through the normal flow. Pass `version: "new"` to auto-create a draft.
- [Stage an archive/unarchive in a draft revision](https://docs.growthbook.io/api/config-revisions/operation/putConfigRevisionArchive.md): Stages an archive or unarchive on the draft. Pass `version: "new"` to auto-create a draft. Archived configs can be permanently deleted via `DELETE /configs/{key}` once the archive is published.
- [Request review for a draft revision](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionRequestReview.md): Moves the draft from `draft` into `pending-review`. Notifies reviewers per the org's approval-flow settings.
- [Submit a review on a draft revision](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionSubmitReview.md): Submits an `approve`, `request-changes`, or `comment` review on the revision. Submitting `approve` or `request-changes` needs Review access. A `comment` is participation rather than a verdict, so it is also open to the Comments permission or draft authority on the entity. Authors and contributors ca…
- [Retract your own review verdict](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionUndoReview.md): Retracts the calling user's own active `approve` or `request-changes` verdict, returning the revision to `pending-review`. Review comments stay in the log. Retracting a `request-changes` can leave the revision approved by someone else, in which case an armed auto-publish fires.
- [Recall a review request](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionRecallReview.md): Pulls a revision in review (`pending-review`, `changes-requested`, or `approved`) back to `draft`, clearing existing reviews and disarming any auto-publish-on-approval.
- [Reopen a discarded revision](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionReopen.md): Returns a previously discarded revision to `draft` status so it can be edited and published again. Only discarded revisions can be reopened.
- [Schedule (or cancel) a deferred publish](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionSchedulePublish.md): Arms a revision to publish automatically at a future time. Pass `scheduledPublishAt` as an RFC3339 timestamp in the future to arm, or `null` to cancel a pending schedule. Requires the `scheduled-revisions` commercial feature and publish permission on the config. A draft that still requires approval…
- [Get merge status for a draft revision](https://docs.growthbook.io/api/config-revisions/operation/getConfigRevisionMergeStatus.md): Runs a dry-run merge of the draft against the current live config and returns any conflicts. Use this before publishing to preview changes and detect conflicting edits.
- [Rebase a draft revision onto the current live config](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionRebase.md): Updates the draft's base snapshot to the current live state, applying the draft's changes on top. Supply `conflictResolutions` to resolve any conflicting fields. Strategies are `overwrite` (use the draft's value), `discard` (keep the live value), or `union` (merge arrays without duplicates — for arr…
- [Publish a draft revision](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionPublish.md): Publishes the draft and makes its changes live. The caller needs Publish access for the affected environments. When approval is required, the draft must be approved unless the caller has Bypass draft approvals access. If the organization requires rebasing, an out-of-date draft must be rebased first;…
- [Discard a draft revision](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionDiscard.md): Permanently discards a draft revision. Only open revisions (not merged or already-discarded) can be discarded.
- [Revert the config to a prior revision](https://docs.growthbook.io/api/config-revisions/operation/postConfigRevisionRevert.md): Creates a new draft (or immediately publishes) whose content matches the specified historical revision. Defaults to creating a draft; when the org enables 'reverts bypass approval' it defaults to publishing immediately. Pass `strategy` to override.

#### Releases

- [Atomically publish revisions across multiple entities](https://docs.growthbook.io/api/releases/operation/postReleasePublishRevisions.md): Publishes a set of revisions — at most one per entity — across Feature Flags, Saved Groups, configs, and constants as a single all-or-nothing operation.

#### Custom Hooks

- [Get all custom hooks](https://docs.growthbook.io/api/custom-hooks/operation/listCustomHooks.md)
- [Create a single custom hook](https://docs.growthbook.io/api/custom-hooks/operation/postCustomHook.md)
- [Dry-run hook code in the sandbox](https://docs.growthbook.io/api/custom-hooks/operation/testCustomHook.md)
- [Get a single custom hook](https://docs.growthbook.io/api/custom-hooks/operation/getCustomHook.md)
- [Partially update a single custom hook](https://docs.growthbook.io/api/custom-hooks/operation/updateCustomHook.md)
- [Delete a single custom hook](https://docs.growthbook.io/api/custom-hooks/operation/deleteCustomHook.md)
- [List a custom hook's version history](https://docs.growthbook.io/api/custom-hooks/operation/listCustomHookHistory.md)
- [Revert a custom hook to a previous version](https://docs.growthbook.io/api/custom-hooks/operation/revertCustomHook.md)

#### Organizations

- [Get all organizations (only for super admins on multi-org Enterprise Plan only)](https://docs.growthbook.io/api/organizations/operation/listOrganizations.md)
- [Create a single organization (only for super admins on multi-org Enterprise Plan only)](https://docs.growthbook.io/api/organizations/operation/postOrganization.md)
- [Edit a single organization (only for super admins on multi-org Enterprise Plan only)](https://docs.growthbook.io/api/organizations/operation/putOrganization.md)

#### Members

- [Get all organization members](https://docs.growthbook.io/api/members/operation/listMembers.md)
- [Update a member's global role (including any enviroment restrictions, if applicable). Can also update a member's project roles if your plan supports it.](https://docs.growthbook.io/api/members/operation/updateMemberRole.md)
- [Removes a single user from an organization](https://docs.growthbook.io/api/members/operation/deleteMember.md)

#### Code References

- [Get list of all code references for the current organization](https://docs.growthbook.io/api/code-references/operation/listCodeRefs.md)
- [Submit list of code references](https://docs.growthbook.io/api/code-references/operation/postCodeRefs.md)
- [Get list of code references for a single feature id](https://docs.growthbook.io/api/code-references/operation/getCodeRefs.md)

#### Archetypes

- [Get the organization's archetypes](https://docs.growthbook.io/api/archetypes/operation/listArchetypes.md)
- [Create a single archetype](https://docs.growthbook.io/api/archetypes/operation/postArchetype.md)
- [Get a single archetype](https://docs.growthbook.io/api/archetypes/operation/getArchetype.md)
- [Update a single archetype](https://docs.growthbook.io/api/archetypes/operation/putArchetype.md)
- [Deletes a single archetype](https://docs.growthbook.io/api/archetypes/operation/deleteArchetype.md)

#### Queries

- [Get a single query](https://docs.growthbook.io/api/queries/operation/getQuery.md)

#### Settings

- [Get organization settings](https://docs.growthbook.io/api/settings/operation/getSettings.md)
- [Replace the approval requirements for feature flags, configs and constants, and for saved groups. Each family is replaced wholesale when supplied; omit one to leave it unchanged.](https://docs.growthbook.io/api/settings/operation/putApprovalSettings.md)

#### Attributes

- [Get the organization's attributes](https://docs.growthbook.io/api/attributes/operation/listAttributes.md)
- [Create a new attribute](https://docs.growthbook.io/api/attributes/operation/postAttribute.md)
- [Update an attribute](https://docs.growthbook.io/api/attributes/operation/putAttribute.md)
- [Deletes a single attribute](https://docs.growthbook.io/api/attributes/operation/deleteAttribute.md)

#### Usage

- [Get metric usage across experiments](https://docs.growthbook.io/api/usage/operation/getMetricUsage.md): Returns usage information for one or more legacy or fact metrics, showing which experiments use each metric and some usage statistics. If a metric is part of a metric group, then usage of that metric group counts as usage of all metrics in the group. Warning: only includes experiments that you have…

#### Meta

- [Get the GrowthBook server version and build info](https://docs.growthbook.io/api/meta/operation/getVersion.md)

#### Contextual Bandits

- [Get current Contextual Bandit leaf weights and latest event](https://docs.growthbook.io/api/ContextualBandits/operation/getContextualBanditCurrentWeights.md)
- [List Contextual Bandit snapshots](https://docs.growthbook.io/api/ContextualBandits/operation/listContextualBanditSnapshots.md)
- [Get a single Contextual Bandit snapshot](https://docs.growthbook.io/api/ContextualBandits/operation/getContextualBanditSnapshot.md)
- [List Contextual Bandit weight-update events](https://docs.growthbook.io/api/ContextualBandits/operation/listContextualBanditEvents.md)
- [Get a single Contextual Bandit weight-update event](https://docs.growthbook.io/api/ContextualBandits/operation/getContextualBanditEvent.md)
- [Get latest Contextual Bandit results](https://docs.growthbook.io/api/ContextualBandits/operation/getContextualBanditResults.md): Returns the latest contextual-bandit stats engine output (per-context responses tagged with their leaf, the per-leaf targeting conditions, and per-leaf aggregated stats), the overall (marginal) variation weights across all contexts, the SRM of the most recent run, and the status of the most recent s…
- [Get features linked to a Contextual Bandit](https://docs.growthbook.io/api/ContextualBandits/operation/getContextualBanditLinkedFeatures.md): Returns the features that reference this contextual bandit via a `contextual-bandit-ref` rule, enriched with each feature's live/draft state, per-environment rule state, and variation values. Same payload the GrowthBook UI uses to render the Linked Features section.
- [Link a feature to a Contextual Bandit](https://docs.growthbook.io/api/ContextualBandits/operation/addContextualBanditLinkedFeature.md): Adds a `contextual-bandit-ref` rule to the bottom of the feature's rule list and links the feature to this contextual bandit. The rule lands in a draft revision that auto-publishes when the contextual bandit starts, unless `autoPublish` is set. Targeting (condition, Saved Groups, prerequisites, cove…
- [Replace a Contextual Bandit's rule on a linked feature](https://docs.growthbook.io/api/ContextualBandits/operation/updateContextualBanditLinkedFeature.md): Replaces every `contextual-bandit-ref` rule pointing at this contextual bandit on the feature, keeping each rule's id and position in the rule list. Every field is replaced, so omitted optional fields revert to their defaults. Returns a 400 when the feature has no such rule on the target revision, o…
- [Unlink a feature from a Contextual Bandit](https://docs.growthbook.io/api/ContextualBandits/operation/deleteContextualBanditLinkedFeature.md): Removes every `contextual-bandit-ref` rule pointing at this contextual bandit from the feature and drops the feature from the bandit's linked-feature list. The rule removal lands in a draft revision unless `autoPublish` is set. When the feature has no such rule left, only the linkage is cleared.
- [Get a single contextualBandit](https://docs.growthbook.io/api/ContextualBandits/operation/getContextualBandit.md)
- [Update a single contextualBandit](https://docs.growthbook.io/api/ContextualBandits/operation/updateContextualBandit.md)
- [Get all contextualBandits](https://docs.growthbook.io/api/ContextualBandits/operation/listContextualBandits.md)
- [Create a single contextualBandit](https://docs.growthbook.io/api/ContextualBandits/operation/createContextualBandit.md)
- [Start a Contextual Bandit](https://docs.growthbook.io/api/ContextualBandits/operation/startContextualBandit.md)
- [Stop a Contextual Bandit](https://docs.growthbook.io/api/ContextualBandits/operation/stopContextualBandit.md)
- [Trigger a Contextual Bandit snapshot refresh](https://docs.growthbook.io/api/ContextualBandits/operation/refreshContextualBandit.md)
- [Cancel a running Contextual Bandit snapshot refresh](https://docs.growthbook.io/api/ContextualBandits/operation/cancelContextualBandit.md)

#### Dashboards

- [Get a single dashboard](https://docs.growthbook.io/api/Dashboards/operation/getDashboard.md)
- [Update a single dashboard](https://docs.growthbook.io/api/Dashboards/operation/updateDashboard.md)
- [Delete a single dashboard](https://docs.growthbook.io/api/Dashboards/operation/deleteDashboard.md)
- [Get all dashboards](https://docs.growthbook.io/api/Dashboards/operation/listDashboards.md)
- [Create a single dashboard](https://docs.growthbook.io/api/Dashboards/operation/createDashboard.md)
- [Get all dashboards for an experiment](https://docs.growthbook.io/api/Dashboards/operation/getDashboardsForExperiment.md)

#### Contextual Bandit Queries

- [Get a single contextualBanditQuery](https://docs.growthbook.io/api/ContextualBanditQueries/operation/getContextualBanditQuery.md)
- [Update a single contextualBanditQuery](https://docs.growthbook.io/api/ContextualBanditQueries/operation/updateContextualBanditQuery.md)
- [Delete a single contextualBanditQuery](https://docs.growthbook.io/api/ContextualBanditQueries/operation/deleteContextualBanditQuery.md)
- [Get all contextualBanditQueries](https://docs.growthbook.io/api/ContextualBanditQueries/operation/listContextualBanditQueries.md)
- [Create a single contextualBanditQuery](https://docs.growthbook.io/api/ContextualBanditQueries/operation/createContextualBanditQuery.md)

#### Custom Fields

- [Get all custom fields](https://docs.growthbook.io/api/CustomFields/operation/listCustomFields.md)
- [Create a single customField](https://docs.growthbook.io/api/CustomFields/operation/createCustomField.md)
- [Get a single customField](https://docs.growthbook.io/api/CustomFields/operation/getCustomField.md)
- [Update a single customField](https://docs.growthbook.io/api/CustomFields/operation/updateCustomField.md)
- [Delete a single customField](https://docs.growthbook.io/api/CustomFields/operation/deleteCustomField.md)

#### Metric Groups

- [Get a single metricGroup](https://docs.growthbook.io/api/MetricGroups/operation/getMetricGroup.md)
- [Update a single metricGroup](https://docs.growthbook.io/api/MetricGroups/operation/updateMetricGroup.md)
- [Delete a single metricGroup](https://docs.growthbook.io/api/MetricGroups/operation/deleteMetricGroup.md)
- [Get all metricGroups](https://docs.growthbook.io/api/MetricGroups/operation/listMetricGroups.md)
- [Create a single metricGroup](https://docs.growthbook.io/api/MetricGroups/operation/createMetricGroup.md)

#### Teams

- [Get a single team](https://docs.growthbook.io/api/Teams/operation/getTeam.md)
- [Update a single team](https://docs.growthbook.io/api/Teams/operation/updateTeam.md)
- [Delete a single team](https://docs.growthbook.io/api/Teams/operation/deleteTeam.md)
- [Get all teams](https://docs.growthbook.io/api/Teams/operation/listTeams.md)
- [Create a single team](https://docs.growthbook.io/api/Teams/operation/createTeam.md)
- [Add members to team](https://docs.growthbook.io/api/Teams/operation/addTeamMembers.md)
- [Remove members from team](https://docs.growthbook.io/api/Teams/operation/removeTeamMember.md)

#### Experiment Templates

- [Get a single experimentTemplate](https://docs.growthbook.io/api/ExperimentTemplates/operation/getExperimentTemplate.md)
- [Update a single experimentTemplate](https://docs.growthbook.io/api/ExperimentTemplates/operation/updateExperimentTemplate.md)
- [Delete a single experimentTemplate](https://docs.growthbook.io/api/ExperimentTemplates/operation/deleteExperimentTemplate.md)
- [Get all experimentTemplates](https://docs.growthbook.io/api/ExperimentTemplates/operation/listExperimentTemplates.md)
- [Create a single experimentTemplate](https://docs.growthbook.io/api/ExperimentTemplates/operation/createExperimentTemplate.md)
- [Bulk create or update experiment templates](https://docs.growthbook.io/api/ExperimentTemplates/operation/bulkImportExperimentTemplates.md)

#### Analytics Explorations

- [Create a Metric based visualization](https://docs.growthbook.io/api/AnalyticsExplorations/operation/postMetricExploration.md)
- [Run a Fact Table based visualization](https://docs.growthbook.io/api/AnalyticsExplorations/operation/postFactTableExploration.md)
- [Create a Data Source based visualization](https://docs.growthbook.io/api/AnalyticsExplorations/operation/postDataSourceExploration.md)
- [Create a SQL based visualization](https://docs.growthbook.io/api/AnalyticsExplorations/operation/postSqlExploration.md)
- [Run a Funnel based visualization](https://docs.growthbook.io/api/AnalyticsExplorations/operation/postFunnelExploration.md)
- [Search Product Analytics resources](https://docs.growthbook.io/api/AnalyticsExplorations/operation/searchProductAnalyticsResources.md)
- [List columns available to a Product Analytics exploration](https://docs.growthbook.io/api/AnalyticsExplorations/operation/getProductAnalyticsColumns.md)
- [Fetch values for Product Analytics string columns](https://docs.growthbook.io/api/AnalyticsExplorations/operation/getProductAnalyticsColumnValues.md)
- [Get a Product Analytics exploration](https://docs.growthbook.io/api/AnalyticsExplorations/operation/getProductAnalyticsExploration.md)

#### Ramp Schedule Templates

- [Get a single rampScheduleTemplate](https://docs.growthbook.io/api/RampScheduleTemplates/operation/getRampScheduleTemplate.md)
- [Update a single rampScheduleTemplate](https://docs.growthbook.io/api/RampScheduleTemplates/operation/updateRampScheduleTemplate.md)
- [Delete a single rampScheduleTemplate](https://docs.growthbook.io/api/RampScheduleTemplates/operation/deleteRampScheduleTemplate.md)
- [Get all rampScheduleTemplates](https://docs.growthbook.io/api/RampScheduleTemplates/operation/listRampScheduleTemplates.md)
- [Create a single rampScheduleTemplate](https://docs.growthbook.io/api/RampScheduleTemplates/operation/createRampScheduleTemplate.md)

#### Learnings

- [Get a single learning](https://docs.growthbook.io/api/Learnings/operation/getLearning.md)
- [Update a single learning](https://docs.growthbook.io/api/Learnings/operation/updateLearning.md)
- [Delete a single learning](https://docs.growthbook.io/api/Learnings/operation/deleteLearning.md)
- [Get all learnings](https://docs.growthbook.io/api/Learnings/operation/listLearnings.md)
- [Create a single learning](https://docs.growthbook.io/api/Learnings/operation/createLearning.md)
- [Search saved Learnings by meaning rather than keyword](https://docs.growthbook.io/api/Learnings/operation/searchLearnings.md)

#### Holdouts

- [Get a single holdout](https://docs.growthbook.io/api/Holdouts/operation/getHoldout.md)
- [Update a single holdout](https://docs.growthbook.io/api/Holdouts/operation/updateHoldout.md): Updates a Holdout. Use the start, start-analysis, and stop endpoints to move it through its lifecycle.
- [Get all holdouts](https://docs.growthbook.io/api/Holdouts/operation/listHoldouts.md)
- [Create a single holdout](https://docs.growthbook.io/api/Holdouts/operation/createHoldout.md): Creates a Holdout. The Holdout starts in the `draft` stage. Use the start endpoint to start it.
- [Start the Holdout's Active Period](https://docs.growthbook.io/api/Holdouts/operation/startHoldout.md): Feature Flags and Experiments can be added during this period while the Holdout measures their cumulative impact.
- [Start the Holdout's Analysis Period](https://docs.growthbook.io/api/Holdouts/operation/startHoldoutAnalysis.md): Move the holdout into an analysis phase. New Feature Flags and Experiments can no longer be added, but existing traffic splits remain active for existing and new traffic. Results exclude data from before the analysis period so you can measure the cumulative impact after changes are frozen.
- [Stop a Holdout](https://docs.growthbook.io/api/Holdouts/operation/stopHoldout.md)

#### Auto Runs

- [Get all autoRuns](https://docs.growthbook.io/api/AutoRuns/operation/listAutoRuns.md)
- [Create a single autoRun](https://docs.growthbook.io/api/AutoRuns/operation/createAutoRun.md)
- [Get a single autoRun](https://docs.growthbook.io/api/AutoRuns/operation/getAutoRun.md)
- [Update a single autoRun](https://docs.growthbook.io/api/AutoRuns/operation/updateAutoRun.md)
- [Record something an auto run created](https://docs.growthbook.io/api/AutoRuns/operation/appendAutoRunArtifact.md)

### Models

- [Aggregated Fact Table](https://docs.growthbook.io/api/AggregatedFactTable_model.md)
- [Analytics Exploration](https://docs.growthbook.io/api/AnalyticsExploration_model.md)
- [Archetype](https://docs.growthbook.io/api/Archetype_model.md)
- [Attribute](https://docs.growthbook.io/api/Attribute_model.md)
- [Auto Run](https://docs.growthbook.io/api/AutoRun_model.md)
- [Code Ref](https://docs.growthbook.io/api/CodeRef_model.md)
- [Config](https://docs.growthbook.io/api/Config_model.md)
- [Config Key Usage](https://docs.growthbook.io/api/ConfigKeyUsage_model.md)
- [Config Lineage](https://docs.growthbook.io/api/ConfigLineage_model.md)
- [Config References](https://docs.growthbook.io/api/ConfigReferences_model.md)
- [Config Revision](https://docs.growthbook.io/api/ConfigRevision_model.md)
- [Config Revision Activity Log Entry](https://docs.growthbook.io/api/ConfigRevisionActivityLogEntry_model.md)
- [Config Revision Ref](https://docs.growthbook.io/api/ConfigRevisionRef_model.md)
- [Config Revision Review](https://docs.growthbook.io/api/ConfigRevisionReview_model.md)
- [Config Schema Export](https://docs.growthbook.io/api/ConfigSchemaExport_model.md)
- [Config Schema Source](https://docs.growthbook.io/api/ConfigSchemaSource_model.md)
- [Config Schema Verify](https://docs.growthbook.io/api/ConfigSchemaVerify_model.md)
- [Config Schema Warning](https://docs.growthbook.io/api/ConfigSchemaWarning_model.md)
- [Constant](https://docs.growthbook.io/api/Constant_model.md)
- [Constant References](https://docs.growthbook.io/api/ConstantReferences_model.md)
- [Constant Revision](https://docs.growthbook.io/api/ConstantRevision_model.md)
- [Constant Revision Activity Log Entry](https://docs.growthbook.io/api/ConstantRevisionActivityLogEntry_model.md)
- [Constant Revision Ref](https://docs.growthbook.io/api/ConstantRevisionRef_model.md)
- [Constant Revision Review](https://docs.growthbook.io/api/ConstantRevisionReview_model.md)
- [Contextual Bandit](https://docs.growthbook.io/api/ContextualBandit_model.md)
- [Contextual Bandit Query](https://docs.growthbook.io/api/ContextualBanditQuery_model.md)
- [Custom Field](https://docs.growthbook.io/api/CustomField_model.md)
- [Custom Hook](https://docs.growthbook.io/api/CustomHook_model.md)
- [Dashboard](https://docs.growthbook.io/api/Dashboard_model.md)
- [Data Source](https://docs.growthbook.io/api/DataSource_model.md)
- [Dimension](https://docs.growthbook.io/api/Dimension_model.md)
- [Environment](https://docs.growthbook.io/api/Environment_model.md)
- [Event User](https://docs.growthbook.io/api/EventUser_model.md)
- [Experiment](https://docs.growthbook.io/api/Experiment_model.md)
- [Experiment Rule](https://docs.growthbook.io/api/Experiment Rule_model.md)
- [Experiment Analysis Settings](https://docs.growthbook.io/api/ExperimentAnalysisSettings_model.md)
- [Experiment Decision Framework Settings](https://docs.growthbook.io/api/ExperimentDecisionFrameworkSettings_model.md)
- [Experiment Metric](https://docs.growthbook.io/api/ExperimentMetric_model.md)
- [Experiment Metric Override Entry](https://docs.growthbook.io/api/ExperimentMetricOverrideEntry_model.md)
- [Experiment Results](https://docs.growthbook.io/api/ExperimentResults_model.md)
- [Experiment Snapshot](https://docs.growthbook.io/api/ExperimentSnapshot_model.md)
- [Experiment Template](https://docs.growthbook.io/api/ExperimentTemplate_model.md)
- [Experiment With Enhanced Status](https://docs.growthbook.io/api/ExperimentWithEnhancedStatus_model.md)
- [Fact Metric](https://docs.growthbook.io/api/FactMetric_model.md)
- [Fact Table](https://docs.growthbook.io/api/FactTable_model.md)
- [Fact Table Column](https://docs.growthbook.io/api/FactTableColumn_model.md)
- [Fact Table Filter](https://docs.growthbook.io/api/FactTableFilter_model.md)
- [Feature Base Rule](https://docs.growthbook.io/api/FeatureBaseRule_model.md)
- [Feature Contextual Bandit Ref Rule](https://docs.growthbook.io/api/FeatureContextualBanditRefRule_model.md)
- [Feature Definition](https://docs.growthbook.io/api/FeatureDefinition_model.md)
- [Feature Environment V1](https://docs.growthbook.io/api/FeatureEnvironmentV1_model.md)
- [Feature Environment V2](https://docs.growthbook.io/api/FeatureEnvironmentV2_model.md)
- [Feature Experiment Ref Rule](https://docs.growthbook.io/api/FeatureExperimentRefRule_model.md)
- [Feature Experiment Rule](https://docs.growthbook.io/api/FeatureExperimentRule_model.md)
- [Feature Force Rule](https://docs.growthbook.io/api/FeatureForceRule_model.md)
- [Feature Revision Ref](https://docs.growthbook.io/api/FeatureRevisionRef_model.md)
- [Feature Revision Summary](https://docs.growthbook.io/api/FeatureRevisionSummary_model.md)
- [Feature Revision V1](https://docs.growthbook.io/api/FeatureRevisionV1_model.md)
- [Feature Revision V2](https://docs.growthbook.io/api/FeatureRevisionV2_model.md)
- [Feature Rollout Rule](https://docs.growthbook.io/api/FeatureRolloutRule_model.md)
- [Feature Rule V1](https://docs.growthbook.io/api/FeatureRuleV1_model.md)
- [Feature Rule V2](https://docs.growthbook.io/api/FeatureRuleV2_model.md)
- [Feature Safe Rollout Rule](https://docs.growthbook.io/api/FeatureSafeRolloutRule_model.md)
- [Feature V1](https://docs.growthbook.io/api/FeatureV1_model.md)
- [Feature V2](https://docs.growthbook.io/api/FeatureV2_model.md)
- [Feature With Revisions V1](https://docs.growthbook.io/api/FeatureWithRevisionsV1_model.md)
- [Feature With Revisions V2](https://docs.growthbook.io/api/FeatureWithRevisionsV2_model.md)
- [Holdout](https://docs.growthbook.io/api/Holdout_model.md)
- [Information Schema](https://docs.growthbook.io/api/InformationSchema_model.md)
- [Information Schema Table](https://docs.growthbook.io/api/InformationSchemaTable_model.md)
- [Learning](https://docs.growthbook.io/api/Learning_model.md)
- [Lookback Override](https://docs.growthbook.io/api/LookbackOverride_model.md)
- [Member](https://docs.growthbook.io/api/Member_model.md)
- [Metric](https://docs.growthbook.io/api/Metric_model.md)
- [Metric Analysis](https://docs.growthbook.io/api/MetricAnalysis_model.md)
- [Metric Group](https://docs.growthbook.io/api/MetricGroup_model.md)
- [Metric Usage](https://docs.growthbook.io/api/MetricUsage_model.md)
- [Namespace](https://docs.growthbook.io/api/Namespace_model.md)
- [Namespace Experiment Member](https://docs.growthbook.io/api/NamespaceExperimentMember_model.md)
- [Organization](https://docs.growthbook.io/api/Organization_model.md)
- [Pagination Fields](https://docs.growthbook.io/api/PaginationFields_model.md)
- [Project](https://docs.growthbook.io/api/Project_model.md)
- [Query](https://docs.growthbook.io/api/Query_model.md)
- [Ramp Schedule](https://docs.growthbook.io/api/RampSchedule_model.md)
- [Ramp Schedule Template](https://docs.growthbook.io/api/RampScheduleTemplate_model.md)
- [Report](https://docs.growthbook.io/api/Report_model.md)
- [Require Review Rule](https://docs.growthbook.io/api/RequireReviewRule_model.md)
- [Require Review Rule Input](https://docs.growthbook.io/api/RequireReviewRuleInput_model.md)
- [Revision Id Ref](https://docs.growthbook.io/api/RevisionIdRef_model.md)
- [Safe Rollout Rule](https://docs.growthbook.io/api/Safe Rollout Rule_model.md)
- [Saved Group](https://docs.growthbook.io/api/SavedGroup_model.md)
- [Saved Group Approval Rule](https://docs.growthbook.io/api/SavedGroupApprovalRule_model.md)
- [Saved Group References](https://docs.growthbook.io/api/SavedGroupReferences_model.md)
- [Saved Group Revision](https://docs.growthbook.io/api/SavedGroupRevision_model.md)
- [Saved Group Revision Activity Log Entry](https://docs.growthbook.io/api/SavedGroupRevisionActivityLogEntry_model.md)
- [Saved Group Revision Ref](https://docs.growthbook.io/api/SavedGroupRevisionRef_model.md)
- [Saved Group Revision Review](https://docs.growthbook.io/api/SavedGroupRevisionReview_model.md)
- [Schedule Rule](https://docs.growthbook.io/api/ScheduleRule_model.md)
- [Scheduled Stop Plan](https://docs.growthbook.io/api/ScheduledStopPlan_model.md)
- [Sdk Connection](https://docs.growthbook.io/api/SdkConnection_model.md)
- [Segment](https://docs.growthbook.io/api/Segment_model.md)
- [Settings](https://docs.growthbook.io/api/Settings_model.md)
- [Targeting Rule](https://docs.growthbook.io/api/Targeting Rule_model.md)
- [Team](https://docs.growthbook.io/api/Team_model.md)
- [Visual Change](https://docs.growthbook.io/api/VisualChange_model.md)
- [Visual Changeset](https://docs.growthbook.io/api/VisualChangeset_model.md)

## OpenAPI Specs

- [openapi](/openapi.yaml)
