# VERIFICATION.md — The Non-Negotiable Checklist

> Run this **in full** on every new tool, and re-run the affected sections after **every** edit — human or AI. An AI asked to "make the table wider" can silently rewrite a formula three functions away. Diff the file (`git diff`) after every AI edit and read what actually changed.

Print this page and initial each line. Keep the initialed copy in the project file. If a line doesn't apply, write N/A and why.

## A. Hand-calc match (the big one)

- [ ] **A1.** Pick a realistic input set. Work the entire calculation **by hand** (or in a previously-validated reference: textbook example, validated spreadsheet, commercial software).
- [ ] **A2.** Enter the same inputs into the tool. Every intermediate value shown in the report's calc steps matches the hand calc **digit-for-digit** at displayed precision. Not "close" — matching. A 2% mystery discrepancy is a unit bug you haven't found yet.
- [ ] **A3.** Repeat A1–A2 with a **second, dissimilar** input set (different governing limit state if possible — e.g., one deflection-governed case and one strength-governed case).

## B. Units audit

- [ ] **B1.** Read every formula in the JS calc engine. Annotate the units of every variable in a comment if the AI hasn't. Confirm every multiplication/division is dimensionally consistent.
- [ ] **B2.** Check the classic traps: psf↔psi, plf↔lb/in, ft↔in in deflection terms (L⁴ amplifies the error 20,000×), kips↔lb, ASD↔LRFD/strength↔service level wind pressures, nominal vs actual lumber dimensions.
- [ ] **B3.** Confirm displayed units in the report match the units actually computed.

## C. Code references

- [ ] **C1.** Open the actual code/standard (ASCE 7, NDS, ACI, AISC, ADM, FBC, local amendments…) next to the tool. Verify **every cited section number** exists and says what the tool uses it for.
- [ ] **C2.** Verify edition consistency — a tool citing ASCE 7-22 must not use 7-16 coefficients (and vice versa).
- [ ] **C3.** Verify every tabulated coefficient (Kz, GCp, Cd, CD, adjustment factors…) against the printed table, at three points including both ends of the range.

## D. Boundary conditions & sanity behavior

- [ ] **D1.** Zero / blank / negative inputs: the tool warns or clamps — it never renders a confident wrong answer.
- [ ] **D2.** Absurd inputs (100-ft span 2×4, 500 mph wind): results are absurd in the right direction and FAIL flags trip.
- [ ] **D3.** Interpolation ranges: inputs just below, inside, and just above every table/interpolation range behave correctly.
- [ ] **D4.** Toggle every dropdown/checkbox once and confirm each visibly changes the result it should (a control wired to nothing is a latent bug).

## E. The deliverable itself

- [ ] **E1.** Print preview: pages break correctly, nothing clipped, footer/branding on every page, no orphaned headings.
- [ ] **E2.** The printed report contains everything a reviewer needs to check it **without the tool**: all inputs, all assumptions, code editions, load combinations, and step-by-step substituted numbers — not just final answers.
- [ ] **E3.** Version number in the file name, on the report, and bumped from the previous revision. Revision notes state what changed.
- [ ] **E4.** The draft watermark is ON for anything not yet verified, and only removed after this checklist is complete.

## F. Ongoing discipline

- [ ] **F1.** The tool is in version control (git) or, at minimum, dated copies are archived per project.
- [ ] **F2.** After any AI edit: diff reviewed line-by-line, then re-run section A with one input set and all of section D.
- [ ] **F3.** Gut check, signed: *"The governing result is consistent with my experience for this kind of member/condition."* If your gut disagrees with the tool, the tool is guilty until proven innocent.

---

**Verified by:** ______________________  **License #:** ____________  **Date:** ____________

**Tool:** ______________________________  **Version:** ____________
