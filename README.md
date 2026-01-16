<h1 align="center">Logic Injection Payloads</h1>
<p align="center">
  🇺🇸 <a href="README.md"><b>English</b></a> |
  🇪🇸 <a href="README_ES.md">Español</a>
</p>
<h3 align="center">A curated collection of logic injection, type confusion, and edge-case payloads designed to break unsafe assumptions in application logic.</h3>


This repository focuses on scenarios where inputs are technically valid, but semantically unexpected, leading to authentication bypasses, authorization issues, feature abuse, or broken business logic.

Unlike classic injection payloads (SQLi, XSS, etc.), these payloads target **how code *thinks*** rather than how it parses.

---

## Purpose

Modern applications often rely on:

* Implicit type coercion
* Truthy / falsy checks
* Weak comparisons (`==`)
* Incomplete validation
* Assumptions about input shape or state

This repository exists to help:

* Identify logic flaws
* Test unsafe conditionals
* Explore edge cases that bypass intended restrictions
* Demonstrate why strict validation matters

---

## Repository Structure

The payloads are grouped by **logic category**, not by vulnerability class.

```
logic-injection-payloads/
├── arrays-objects/
├── auth/
├── booleans/
├── edge-cases/
├── null-state/
└── numbers/
```

Each folder contains:

* `cases.txt` – Realistic logic scenarios with expected vs broken behavior
* `variants.txt` – Reusable payload values to inject and test

---

## Categories Overview

### Arrays & Objects

Payloads that exploit assumptions about input type and structure.

Common targets:

* Role checks
* Permission flags
* Object comparisons
* Array existence checks

Focuses on:

* Arrays vs strings
* Objects vs primitives
* Constructor checks
* Empty vs non-empty containers

---

### Authentication & Authorization

Payloads designed to bypass or confuse auth logic.

Common targets:

* Login checks
* Session validation
* Role enforcement
* Authentication flags

Highlights issues with:

* Non-empty strings
* Loose equality
* Truthy values accepted as authenticated
* Missing strict type checks

---

### Booleans

Targets logic that relies on boolean assumptions.

Common problems:

* `"false"` being truthy
* `1 == true`
* Arrays and objects passing boolean checks
* Negation logic behaving unexpectedly

Useful for:

* Feature flags
* Admin toggles
* Access gates

---

### Edge Cases

Payloads that exploit invisible or uncommon values.

Includes:

* Null bytes
* Zero-width characters
* BOM characters
* Trailing whitespace
* Scientific notation
* Parsing quirks

These values often bypass:

* Trimming logic
* Case normalization
* Numeric parsing

---

### Null & State Confusion

Focuses on missing, undefined, or unexpected states.

Targets logic such as:

* `if (value)`
* `if (!value)`
* `value != "banned"`
* `data && data.id`

Common impacts:

* TypeErrors
* Incorrect access grants
* Invalid state acceptance

---

### Numbers

Payloads that abuse numeric logic and comparisons.

Includes:

* Zero edge cases (`-0`, `0.0`)
* Floating point precision
* `NaN` and `Infinity`
* Integer overflow boundaries
* Type coercion with strings and booleans

Often affects:

* Pricing
* Limits
* Cooldowns
* Counters
* Quotas

---

## Where This Is Useful (Summary)

These payloads are applicable in many real-world scenarios, including:

* **Web application input points**
  Forms, query parameters, JSON bodies, headers, cookies, and JWT claims.

* **HTTP request tampering**
  Modifying valid requests using tools like Burp Suite, ZAP, or mitmproxy to inject unexpected types or states.

* **API logic testing**
  Finding broken assumptions in REST or GraphQL APIs that lack strict schema enforcement.

* **Authentication & authorization bypass testing**
  Exploiting weak checks based on truthiness, loose equality, or missing validation.

* **Business logic abuse**
  Breaking flows related to payments, limits, cooldowns, feature flags, or access control.

* **Edge-case fuzzing (logic-focused)**
  Semantic fuzzing aimed at logic errors rather than crashes.

* **Client ↔ server trust boundary testing**
  When frontend validation exists but backend validation is incomplete or missing.

* **CTFs, wargames, and labs**
  Ideal for challenges focused on logic flaws instead of classic injection vulnerabilities.

* **Code review & secure development**
  Identifying dangerous conditionals and improving defensive programming practices.

---

## Usage Philosophy

This repository is not meant to be:

* A drop-in exploit kit
* An automated attack framework

It *is* meant to be:

* A testing reference
* A thinking tool
* A logic-breaking checklist

Use the payloads to:

1. Identify assumptions in code
2. Challenge those assumptions
3. Observe unintended behavior
4. Fix the root logic flaw

---

## Disclaimer

This repository is provided for **educational, defensive, and authorized security testing purposes only**.

Do not use these payloads against systems you do not own or have explicit permission to test.

The author assumes no responsibility for misuse.

---
Made with <3 by URDev.
