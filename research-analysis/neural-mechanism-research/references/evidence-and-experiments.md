# Evidence and experiment guide

Read this for substantial neural-mechanism research. It guides judgment, not a mandatory visible report format.

## 1. Make competing explanations explicit

Preserve the user's hypothesis and turn it into something falsifiable. For example:

| Proposed explanation | A discriminating check |
| --- | --- |
| Smaller matrices receive more precise gradients | Partition an unchanged operation and compare its output and gradients; then separately change normalization or routing. |
| More dimensions contain more information | Compare linear rank, intrinsic dimension, task-accessible information, and stored parameter capacity. |
| One neuron stores one fact | Check polysemanticity, distributed features, redundancy, paraphrase behavior, and causal intervention. |
| A deeper model always learns better | Separate representational existence results from actual training under matched compute and tuned hyperparameters. |
| A default value is mathematically necessary | Trace its original ablation, later models that change it, and hardware constraints. |

Consider more than one explanation when the evidence permits it. Do not assign invented probabilities. Rank hypotheses by the strength of evidence and name an observation that would distinguish them.

## 2. Historical comparison

Build a small internal evidence ledger with:

```text
claim and scope
source / first publication / inspected version
original motivation versus later interpretation
dataset / objective / architecture / size / training budget
comparison baseline and what was held fixed
reported result and statistical support
theorem assumptions or intervention semantics
counterevidence / variants / unresolved gap
```

The historical search should locate relevant stages rather than an arbitrary number of papers:

- mathematical or computational precursors;
- the initial architecture and actual ablations;
- later pruning, scaling, replacement, or replication studies;
- explanations proposed after the design became successful;
- successful variants that retain some parts and remove others;
- recent evidence that changes the interpretation.

Do not call an early result “wrong” just because its optimum moved. Ask whether its claim was local and accurate, or whether later work refuted a claimed general law.

When broad scaling laws conflict, inspect the experimental frontier, token budget, stopping rule, learning-rate schedule, and extrapolation regime. Hardware limitations and incomplete search are plausible limitations; do not invent the authors' motives or undocumented experiments.

## 3. Exact computation first

State the tensor convention: row or column vectors, sequence axis, feature axis, and batch axis. Distinguish trainable weights from activations and caches. Mark when normalization, bias, position encoding, or a residual path is omitted from a teaching equation.

For a linear map, inspect rank, null space, image, scaling, basis change, and the task that becomes easier downstream. Increasing output coordinates does not itself add independent information. A nonlinear feature lift can improve what a simple readout can express without adding information to a fixed input.

For a residual update, distinguish:

```text
inference: state changes using fixed learned parameters
training: parameters change using error signals
```

A state update can promote, suppress, overwrite, or re-express features. It is not automatically monotonic knowledge accumulation.

For attention, locate the actual normalization and mixing axes. Separate query-head count, KV-head count, Q/K width, V width, residual width, and sequence length. Shared K/V does not imply one attention distribution.

## 4. Gradient meaning

Write the simplest useful chain-rule expression, starting from the true loss. Explain the sign and direction in ordinary language. Identify where examples, tokens, features, and heads contribute to shared parameters.

Ask whether a claimed learning improvement is about:

- a new function family or routing structure;
- parameter sharing and gradient interference;
- initialization or symmetry breaking;
- saturation, conditioning, or unstable scales;
- the optimizer's parameterization and learning-rate scaling;
- sample efficiency, generalization, or convergence speed.

Gradient magnitude is coordinate dependent. Reparameterizations can preserve the same function while changing gradient norms. Compare the induced change in outputs or loss, not raw norms alone. There is no conserved budget of semantic information divided evenly among weight entries.

An analytical or automatic-differentiation check should state the seed, precision, shapes, objective, and numerical tolerance. Distinguish floating-point roundoff from a change of function.

## 5. Geometry and dynamics without mysticism

High-dimensional coordinates are generally not individually named semantic axes. Check relevant reparameterization symmetries before claiming a unique geometric interpretation.

If using an energy analogy, define the state variable, energy function, update rule, constraints, and whether descent is actually guaranteed. The inference trajectory through untied layers is different from optimizer steps through parameter space. “Temperature” in a softmax has a precise mathematical role but need not be a thermodynamic temperature.

For feature superposition, distinguish a toy construction from evidence in trained models. Sparse features may share coordinates with interference; this does not let a finite representation store arbitrary independent dense variables losslessly.

## 6. Causal evidence

Use each method for the claim it supports:

| Method | Main evidence | Important limitation |
| --- | --- | --- |
| Attention or activation visualization | Correlation with input patterns | Not proof of causal importance or exclusive storage. |
| Linear probe / logit lens | Decodability under a chosen readout | Information can be decodable without being used; intermediate readouts can mislead. |
| Ablation / pruning | Dependence on a component in that intervention | Distribution shift and compensation affect conclusions; dispensable after training is not dispensable during training. |
| Activation patching / causal tracing | Effect of restoring a chosen state after corruption | Result depends on corruption, baseline, location, and what remains fixed. |
| Weight editing | A change there can modify behavior | An effective edit site is not necessarily the unique site where the fact was stored. |
| Sparse feature decomposition | A useful candidate feature basis | Dictionary learning, reconstruction error, and feature splitting affect interpretation. |
| Controlled training / counterfactual data | Dependence on a controlled data or architecture factor | Synthetic tasks and finite scales limit external validity. |

Where possible, use converging methods rather than overinterpreting one visualization or intervention.

## 7. Fair alternatives and costs

Keep these comparisons separate:

- matched parameters versus matched active parameters;
- matched training FLOPs versus matched inference latency;
- same token count versus same convergence level;
- a pruned pretrained network versus a smaller network trained from scratch;
- same optimizer settings versus appropriately tuned settings;
- observed benchmark gains versus general expressive power.

Do not infer equal runtime from equal arithmetic counts. For architectures, include memory traffic, serial operations, kernel shapes, cache size, and hardware utilization when they affect the proposed choice.

For capacity claims, define the knowledge distribution, retrieval criterion, reliability, precision, redundancy, and number of exposures. An empirical bits-per-parameter estimate is not a universal law for arbitrary natural-language knowledge.

## 8. Report limits constructively

State where the explanation is exact, where evidence converges, and where more than one mechanism may contribute. Leave the reader with a usable model even when the science is incomplete.

If a question remains open, propose the smallest discriminating check: a parameter-matched ablation, a head-count/width sweep, a tuned learning-rate comparison, a held-out compositional task, or an intervention that separates storage from retrieval. Label unrun experiments as proposed, never as completed.
