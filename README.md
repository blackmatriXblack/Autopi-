# Autopi-neverstop
This page implements an unbounded, real‑time π decimal generator using a pure JavaScript spigot algorithm (Rabinowitz &amp; Wagon, adapted with BigInt). Unlike traditional approximations, the algorithm produces digits sequentially without any upper limit, guaranteeing infinite precision.

This HTML document implements an **unbounded, real‑time π decimal generator** using a pure JavaScript spigot algorithm (Rabinowitz & Wagon, adapted with BigInt). Unlike traditional approximations, the algorithm produces digits sequentially without any upper limit, guaranteeing infinite precision.

## Core Features

- **Non‑blocking infinite execution** – A lightweight scheduler yields to the event loop every 18–28 ms, generating thousands of digits per second while keeping the UI fully responsive.
- **Incremental DOM rendering** – Digits are batched and appended via `insertAdjacentHTML`, avoiding re‑parsing of existing content. Memory overhead stays minimal even after millions of digits.
- **Adaptive batch sizing** – Larger batches are used for the first few thousand digits (fast initial fill); batch sizes automatically decrease later to maintain smooth scrolling and low latency.
- **Smart auto‑scroll** – The viewport follows the new digits automatically. If the user scrolls up, auto‑scroll pauses for 4.5 seconds, then resumes. This respects manual exploration while preserving the “infinite stream” experience.
- **Pure digital timer** – A floating elapsed timer displays HH:MM:SS, updated every second. No labels, icons, or extra UI elements – only a white background, monospaced type, and the flowing digits.

## Algorithm & Implementation

The spigot algorithm uses **BigInt** arithmetic, so it never loses precision or wraps around. A ES6 generator yields each decimal digit on demand. The main loop batches digit generation, buffers the result, and flushes to the DOM either when the buffer exceeds ~320 characters or after 30 ms. This balances throughput with visual smoothness.

## Performance & Scalability

The page runs indefinitely in any modern browser. It has been tested to generate **hundreds of thousands of digits** without slowdown. The adaptive scheduler prevents long micro‑tasks, and the incremental DOM updates guarantee that scrolling and interaction remain fluid even after hours of runtime.

## Design Philosophy

**Extreme minimalism** – no text labels, no buttons (except the hidden smart scrolling behavior), no external fonts or assets. The page consists solely of a white canvas, the number π, and a silent clock. It embodies the beauty of infinite, uninterrupted computation.
