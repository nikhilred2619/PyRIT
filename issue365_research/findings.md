# Existing-API feasibility findings — PyRIT Issue #365

**Source:** external Cloud validation report dated 2026-10-25, reported against upstream PyRIT `246b659e`. These results are attributed to the report rather than independently rerun in this GitHub publishing session.

## Feasibility

**Yes:** existing `OpenAIChatTarget(temperature=...)`, `TargetRegistry.instances.register`, and `AdversarialBenchmark(adversarial_targets=[...])` cover the three-temperature comparison. The objective target, scorer, dataset and technique can remain fixed. `compute_scenario_statistics` supplies per-variant ASR. Repetitions and intervals do not justify a dedicated sweep API.

## Reported validation

* Existing relevant PyRIT unit tests: **1,651 passed**, no failures.
* New external offline tests: **9 passed, 1 strict expected failure**.
* External notebook: dry-run and fake-HTTP offline simulation completed, no endpoint calls.
* **No real AI model inference, live ASR or empirical temperature optimization** has been measured.

## Narrow issues observed

1. **Simulated-technique cache identity:** changing target temperature while re-registering the **same registry name** may reuse completed results when `use_cached=True`. The report reproduces this with `crescendo_simulated`; `red_teaming` was a control. A focused regression test and maintainer-selected cache-key fix may be appropriate as separate work.
2. **TAP scorer coupling:** TAP can fall back to a scorer that uses the swept generator, so the judge changes with temperature. Avoid TAP for this experiment.
3. **Dataset sampling correction:** `AdversarialBenchmark._select_stable_sample` uses deterministic ordering; the earlier PR's comment alleging nondeterministic benchmark sampling was incorrect.

## Recommendation

Do not merge the 1,400+ lines of new sweep/analysis API simply to run this comparison. Consider (a) concise documentation for the existing registry-based workflow, (b) a separate focused cache regression, and (c) a small live pilot with maintainer-approved generator/target/judge choices and explicit cost approval.

The compact notebook in this branch **demonstrates configuration, not the complete Cloud fake-HTTP test suite**. To inspect the full suite, use the original Cloud report and its separate companion package. This research branch leaves the original PR unchanged.
