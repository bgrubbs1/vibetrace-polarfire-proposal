# VibeTrace Vibration Event Recorder

PolarFire FPGA Design Contest 2026
Track 1: Compact Edge Systems Using PolarFire SoC Discovery Kit

## Project Overview

VibeTrace is a proposed vibration event recorder for reproducible condition-monitoring research. A maintenance alert is difficult to evaluate when its underlying waveform is missing or incomplete. VibeTrace will associate each accepted trigger with raw samples, feature values, configuration and integrity status so an engineer can inspect both the signal change and data quality.

On the PolarFire SoC Discovery Kit, an existing PC preloads signed 16-bit traces into on-chip memory. A hardware timer drives deterministic replay through four 64-tap fixed-point FIR bands per channel. The pipeline calculates band and raw mean-square energy and raw peak magnitude in nonoverlapping 1,024-sample windows. Configurable thresholds, persistence and hysteresis govern triggers. After history is primed, each accepted capture retains 4,096 samples before the trigger anchor and 4,096 beginning at it; the anchor is the qualifying window’s final sample. Sequence identifiers, overflow flags and busy-event counters expose missing or unrecorded evidence. USB-UART handles setup and post-run export; bare-metal RISC-V firmware manages configuration and an equivalent C baseline.

The minimum design target is one channel at 48 ksample/s, scaling to four channels if timing and memory placement permit. The four-channel plan budgets 192 KiB for replay and capture samples, plus state and queues. No external sensor or ADC is required; PC compatibility and adequate USB-C power must be confirmed.

Expected outputs are a reproducible RTL/firmware design, bit-accurate model, verification tests, waveform viewer and measured hardware/software comparison. Synthetic tests and appropriately licensed public bearing recordings will assess correctness and limits. Throughput, latency, speedup and power savings are unmeasured; live-sensor performance and field fault accuracy are outside the demonstrator’s claims.

## Innovation & Expected Impact

VibeTrace’s contribution is a complete, auditable event-recording path around FPGA signal processing. Each accepted event connects a configurable decision to an exact waveform range and explicit completeness status. This lets reviewers distinguish a vibration change from clipping, arithmetic saturation, incomplete history, overflow or an event that could not be recorded while capture was busy.

The FPGA establishes the sample schedule and combines filtering, feature extraction, trigger decisions and waveform retention. Bare-metal RISC-V firmware handles orchestration and a matched software baseline. This division creates a focused test of hardware/software co-design without requiring Linux, a neural network or additional acquisition hardware.

The evaluation will use identical inputs, arithmetic, windows and triggers in the FPGA and optimized C implementations. It will report throughput and latency, distinguish compute time from transfer overhead, and publish failures and operating limits. A proposed decision-processing target is at most 100 microseconds after the qualifying window ends; window acquisition, filter and persistence delays will be reported separately.

The potential impact is a reusable foundation for trustworthy condition-monitoring prototypes and an accessible teaching example of deterministic acquisition, fixed-point design and evidence-based benchmarking. Compact routine features reduce exported payload while event waveforms preserve inspection detail. The goal is reproducible engineering evidence; any deployment benefits, fault accuracy or power savings remain to be established.

## AI Assistance Disclosure

OpenAI's dot assistant assisted with developing and editing this proposal, including the proposed architecture, numerical targets, verification plan and block diagram. This proposal claims no measured performance results. This disclosure describes assistance with proposal development and does not represent completed implementation or engineering validation.

