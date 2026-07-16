# ⚠️ DISCLAIMER — READ IN FULL

## 1. Nothing here is engineering advice

This repository provides a **software framework** — a way of structuring HTML files. It does not provide engineering services, engineering advice, or engineering judgement. No file in this repository, and no file generated using this framework, constitutes the practice of engineering.

## 2. AI-generated calculations are unverified by default

Tools built with this framework are typically written wholly or partly by large language models. LLMs:

- confidently produce plausible-looking formulas that are **wrong**;
- silently mix unit systems (psf vs psi, feet vs inches, ASD vs LRFD);
- cite code sections that don't say what the tool claims they say;
- handle the happy path and break at boundary conditions (zero spans, negative loads, tributary edge cases).

**Assume every generated tool contains at least one error until your verification process proves otherwise.** The first few tools you build are you creating a calculator from scratch — treat them with exactly that level of suspicion.

## 3. The engineer of record is responsible. Full stop.

If you seal, sign, submit, or rely on output from a tool built with this framework, **you** — a licensed professional exercising independent judgement — are solely responsible for its correctness. Responsibility does not transfer to:

- this repository or its authors,
- the AI model that wrote the code,
- the AI vendor,
- anyone who shared a module with you.

## 4. Intended scope

This framework is intended **only** for simple, verifiable calculations where an experienced engineer can immediately sanity-check the result — the kind of checks common in single-family residential and light remodeling work. It is **not** intended for, and must not be used for, finite element analysis, dynamic or seismic response analysis, nonlinear behavior, complex or coupled systems, or any analysis you could not reasonably reproduce by hand.

## 5. Verification is mandatory, not optional

Before any tool is used on real work, run the complete checklist in [VERIFICATION.md](VERIFICATION.md), including at minimum one independent hand calculation matched digit-for-digit against the tool's output, and boundary-condition spot checks. Repeat relevant portions after **every** revision to the tool — a one-line AI edit can silently change a formula elsewhere.

## 6. The forward-looking bet (and why the caution stands anyway)

The authors believe AI code generation is on a trajectory toward extremely high reliability, and that engineers who adopt input-to-deliverable, AI-first workflows *now* — on small, verifiable problems — will be strongly positioned as that reliability arrives. That belief is a reason to **learn the framework carefully**, not a reason to skip verification. Until the day an AI-written calc is as trustworthy as a validated commercial package (that day is not today), the human check is the load path.

## 7. No warranty

All software in this repository is provided "AS IS", without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement — per the [MIT License](LICENSE). In this repository that clause is not boilerplate; it is the design philosophy.
