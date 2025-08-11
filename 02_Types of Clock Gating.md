# Static Clock Gating
- Clock gating decisions are made at design time and fixed in hardware.
- Enable signal is derived from known design condition (e.g., a control register or mode signal).
- **No runtime analysis of workload or switching activity** it's based on pre-determined logic.
- **ADvantages**:
  - Simple to implement.
  - Low area overhead.
  - Predictable behavior.
- **Disadvantages**:
  - Not workload-aware; might miss opportunities for extra savings.
- **Example**:
  - Gating a UART block's clock whenever a configuration bit `uart_enable` is 0.
  - If a GPU block is never used in a certain SoC variant, its clock is permanently gated.

# Dynamic Clock Gating
- Clock gating is controlled **at runtime** based on current activity or signal toggling inside the block.
- Enable signal often comes from combinational logic that detects when the block is idle.
- **Advantages**:
  - Reacts to real-time conditions.
  - Can save more power for irregular worloads.
- **Disadvantages**:
  - Needs careful timing to avoid glitches.
  - Slightly more control logic and verification complexity.
- **Examples**:
  - In an ALU, clock is disabled for multiplier registers whenever `mul_enable = 0`.
  - FIFO logic clock is stopped when both `write_enable = 0` and `read_enable = 0`.
 
# Adaptive Clocking Gating
- Clock gating decisions are **adjusted dynamically** using feedback from performance counters, workload monitors, or power management firmware.
- Can **switch between coarse and fine-grained gating** based on real-time performance/power needs.
- Sometimes uses **machine learning or heuristics** to predict idle times.
- **Advantages**:
  - Can balance **performance vs. power** intelligently.
  - Works well in SoCs with varying wrokloads (smartphones, AI accelerators).
- **Disadvantages**:
  - Most complex to design and verify.
  - Requires monitoring infrastructure and possibly software co-ordination.
- **Example**:
  - CPU core clock gating aggressiveness changes depending on battery level and thermal state.
  - If workload is bursty, use fine-grained gating; if idle for long, use coarse-grained gating.
