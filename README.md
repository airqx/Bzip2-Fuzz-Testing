## Fuzzing Results and Analysis

### Decompression Campaign (24 hours)

The decompression campaign produced the most interesting results.

- The fuzzer explored many execution paths
- Multiple crashes and hangs were discovered
- Complex behaviors appeared when processing malformed inputs

**Analysis:**
The decompression pipeline is highly sensitive to input structure. Since it parses compressed data, small corruptions can break internal assumptions and lead to unstable states. This makes it more vulnerable and a better target for fuzzing.

---

### Compression Campaign (24 hours)

The compression campaign was more stable.

- No real crashes or hangs were found
- Many execution paths were still explored
- The system handled random inputs reliably

**Analysis:**
Compression is more controlled because it generates structured output rather than interpreting it. This reduces the chance of invalid states and explains the overall stability.

---

### Coverage and Graph Analysis

- Core loops in both compression and decompression were well covered
- CFGs showed that main execution paths are heavily exercised
- Call graph mapping confirmed that frequently used functions were covered

**Analysis:**
Most normal execution paths are easy to reach, but rare branches (especially error handling and edge cases) remain uncovered. This is expected due to strict conditions required to trigger them.

---

### Seed Effectiveness

- Simple seeds resulted in very limited exploration
- Diverse and structured seeds significantly improved coverage and path discovery

**Analysis:**
Seed quality has a major impact on fuzzing. Structured inputs help the fuzzer reach deeper logic that random mutations alone cannot discover.

---

### Crash Behavior

- Some crashes were real memory-related issues (e.g., pointer corruption)
- Others were valid error-handling cases (false positives)

**Analysis:**
Fuzzing is effective at exposing both real vulnerabilities and edge-case behaviors. However, manual triage is required to distinguish between actual bugs and expected failures.

---

### Overall Insight

- Main program logic is well tested through fuzzing
- Rare and defensive paths remain difficult to reach
- Combining fuzzing with coverage graphs gives a deeper understanding of test completeness
