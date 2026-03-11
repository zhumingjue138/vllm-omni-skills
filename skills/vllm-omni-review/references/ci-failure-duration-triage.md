## CI Failure & Duration Triage

## Quick Start

When a user reports CI is **failing (red) / flaky / noticeably slower** and provides logs:

1. Focus only on the **first error** (the earliest fatal signal). Don’t get distracted by cascading follow-up errors.
2. Extract: job name/level, the stage/step where the first error occurs, exit code/exception stack, whether it’s a timeout, and per-stage durations (if available).
3. Classify into one of five categories: **build/install/deps**, **test failure**, **infrastructure/resources**, **timeout/performance regression**, **config/permissions/credentials**.
4. Provide **1–3** root-cause hypotheses. Each must include an **exact log evidence excerpt**, and hypotheses must be ordered **from lowest verification cost to highest**.
5. Provide a **≤5-minute** minimal verification for **Hypothesis 1** only. Specify **environment + commands + expected result** (must not require running the full pipeline).

## Required inputs (list what’s missing if not provided)

- Job name and type (deploy / L1–L5 / other)
- Logs: **50–100 lines before and after the first error** (or the full log)
- Change: PR link or commit SHA (if unknown, explicitly mark as “unknown”)
- CI environment info (runner/image/Python/CUDA, etc.; cite from logs if present)

## Decision tree (branch on the first error)

- **Compile / build / dependency install failures**
  - Common signals: `SyntaxError`, compiler `error:`, `ld:`/`linker`, `undefined reference`, `CMake Error`, `nvcc fatal`, `ModuleNotFoundError`, `ImportError`, `pip install` failures, `Failed building wheel`, `No matching distribution found`
- **Test failures (assertions or exceptions inside tests)**
  - Common signals: pytest `FAILED`, `AssertionError`, `E   assert ...`, traceback pointing to a `tests/...` line, or still failing after flaky retries
- **Infrastructure / resource issues (non-product logic)**
  - Common signals: `Timeout`/`timed out`, `Killed`/`SIGKILL`, `OOM`/`Out of memory`, `No space left on device`, `Disk quota exceeded`, `Connection reset`, `TLS handshake`, `503`/`429`, image pull failures
- **Duration / performance regressions (job doesn’t fail but is clearly slower)**
  - Common signals: a stage/step duration increases significantly in logs/summary; approaches timeout threshold; or long periods with no output
- **Config / permissions / credentials / environment variables**
  - Common signals: `Permission denied`, `AccessDenied`, `401/403`, `missing required env`, `KeyError: <ENV>`, secrets/tokens not injected, `could not read credentials`

## Output (must use this template)

Rules:

- Hypotheses must be grounded in log facts. If there’s no evidence, write “cannot attribute from current logs” and list what additional info is needed.
- For duration issues, explicitly state: **stage name + baseline vs current run**.
- If there are multiple hypotheses, mark priority (usually ordered by verification cost from low to high).

```markdown
## CI Triage Report

- **Job**: <job name> / <L1|L2|…> / <trigger>
- **Change**: <PR or SHA or unknown>
- **Classification**: <build/install | test failure | infrastructure | config/environment | timeout/perf regression | other>

### First error

- **Location**: <stage or step name>
- **Excerpt**:
```
<verbatim log lines>
```

### Duration (if relevant)

- **Anomalous stage**: <stage name>
- **Baseline vs current**: <e.g., 2min → 10min> or <multiplier>
- **Notes**: <log-based only: serialized waiting/retries/cache misses, etc.>

### Root-cause hypotheses (ordered by verification priority)

**Hypothesis 1 (verify first)**
- **Description**: <one sentence>
- **Evidence**:
```
<log excerpt>
```

**Hypothesis 2**
- **Description**: …
- **Evidence**: …

(Optional hypothesis 3)

### Minimal verification plan (for Hypothesis 1)

- **Environment**: <local / specific container image / minimal CI workflow name>
- **Steps**:
  1. `<command or action A>`
  2. `<command or action B>`
- **Expected result**: <success | reproduce an error | duration within a range>

### Recommended actions

- If verification **confirms**: <fix direction or recommend reverting the change>
- If verification **does not confirm**: <move to next hypothesis or expand logs/contact infra>
- If it’s **infra/environment**: <adjust parallelism/timeouts/resources or include key points for an ops ticket>
```

## Additional resources

- L1–L5 levels and directory conventions: `https://github.com/vllm-project/vllm-omni/blob/main/docs/contributing/ci/CI_5levels.md`
