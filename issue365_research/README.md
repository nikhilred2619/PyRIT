# Issue #365: existing PyRIT benchmark demonstration

This is **research support material**, not a new PyRIT API and not a replacement for Microsoft's existing documentation.

* [Notebook](pyrit_issue365_existing_benchmark.ipynb): register one generator at temperature 0.2 / 0.7 / 1.2, configure PyRIT's existing `AdversarialBenchmark`, verify isolation, and optionally run a paid pilot.
* [Findings and scope](findings.md): offline findings and constraints, based on the external Cloud report supplied on 2026-10-25.

**Default: no live attack calls.** A live run requires `PYRIT_ISSUE365_MODE=live` and `PYRIT_ISSUE365_CONFIRM_LIVE=yes`, configured credentials, and the pinned HarmBench dataset. Do not enable live mode until costs and model choices have been approved. The online notebook is a compact example adapted from the separately validated Cloud report; Cloud's reported offline tests have **not** been rerun against this compact notebook.

Corresponds to [Issue #365](https://github.com/microsoft/PyRIT/issues/365) and the maintainer's [review on PR #3349](https://github.com/microsoft/PyRIT/pull/3349#issuecomment-6395084595). This dedicated branch intentionally does **not** modify PR #3349.
