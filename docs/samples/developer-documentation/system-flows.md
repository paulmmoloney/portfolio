# System flows

System flows are flows that run at node startup, before any services
flows or user flows. The only currently supported system flow is
automatic ledger recovery; that is, the flow
`net.corda.node.internal.aliasing.flows.EnterpriseLedgerRecoveryFlow`.

## Configuring nodes to run system flows

To configure a node to run system flows, including the automatic ledger
recovery flow:

1. Set the Boolean parameter `runSystemFlowsAtStartup` in the
   `enterpriseConfiguration` section of the node configuration to true.

   The node will now have a system flow phase after startup, during which
   system flows are run.

2. (Optional) A second parameter, `systemFlowsStuckSkipThreshold`, may
   also be configured (its default is 1m). This integer parameter
   specifies the duration that a system flow can be stuck on a
   suspension point during the system flow phase before it is skipped.
   Such a flow will skip up to two times: once in checkpoint system
   flows phase, then again in startup system flows phase.

If you specify `runSystemFlowsAtStartup`, then
EnterpriseLedgerRecoveryFlow will run at startup with default
parameters, which means recovery will be attempted from all the nodes in
the network map. It is possible to override this with your own system
flow that invokes the EnterpriseLedgerRecovery flow where you can then
specify your own parameters. This is done via the system flow `supersedes`
property. This is used with the fully qualified name of the flow we want
to replace at startup: then, the flow with the annotation will instead
run in its place.

For example, the following example shows how the existing system flow
EnterpriseLedgerRecoveryFlow could be superseded by
MyCustomEnterpriseLedgerRecoveryFlow:

```kotlin
@SystemFlow(supersedes=\"net.corda.node.internal.aliasing.flows.EnterpriseLedgerRecoveryFlow\")
@StartableByRpc
@InitiatingFlow
class MyCustomEnterpriseLedgerRecoveryFlow : FlowLogic\<Unit\>() {
  @Suspendable
  override fun call() {
  // does something else and/or call EnterpriseLedgerRecovery with specific parameters
  }
}
```

## System flow phase

Once a node is configured to run system flows at startup, the following
sequence of actions occurs during the system flow phase:

1. If there are system flows that were previously checkpointed, these
   checkpointed system flows will run before the startup system flows.
2. Once any checkpointed system flows have either completed or resulted
   in an exception, normal system flows then run.
3. If there are paused flows, unpausing flows during the system flow
   phase will only unpause system flows.
4. If a system flow gets stuck on a suspension point during the system
   flow phase for longer than the value (in seconds) of the
   `systemFlowsStuckSkipThreshold` configured in the node configuration,
   it will skip up to two times: once for checkpoint system flows and
   then again for startup system flows (each system flow is checked for
   being stuck every one minute).
5. If the node is configured with the "pause all flows" option
   (`smmStartMode="Safe"`) or flow draining mode is on, then system
   flows will not run at startup.
6. While system flows at startup are running, if a flow is started via
   RPC, it will be blocked until the system flows have finished.
7. Flows annotated with `@SystemFlow` can be started via RPC during the
   system flow phase.
8. Once system flows have finished, a `SystemFlowsPhaseCompleted` event
   is produced, and the metric `SystemFlows.Phase` is recorded, with
   values CHECKPOINT, STARTUP and USER in this order. Note that only
   the latest metric is recorded.
9. After the startup system flow phase ends and the
   `SystemFlowsPhaseCompleted` event is distributed, user and non-system
   checkpointed flows will run.
10. Resuming or retrying nodes after the system flow phase ends will
    resume/retry only user and non-system flows.
