# CODEX RHS_NS Update Report

## A) Repo status
- Repo path: `/home/jaguir26/local/src/Q-DESN---Theory-for-implementation`
- Branch: `main`
- Git status at report time:
  - modified: `main.tex`
- Key RHS-relevant files audited: `main.tex`
- Reference anchor used for RHS claims: `/home/jaguir26/local/src/RHS---Implementations/main.tex` and `/home/jaguir26/local/src/RHS---Implementations/CODEX_VALIDATION_REPORT.md`

## B) What was changed and why
1. Reworked the theory document to make `rhs_ns` the explicit default framework.
   - Replaced legacy direct-`c^2` default exposition with NS-style joint construction and `\zeta` notation.
   - Retained legacy PV prior only as a short contextual note (non-default).
2. Added a full posterior section under the pseudo-data/product representation.
3. Added implementation-ready MCMC derivations with explicit block structure and full conditionals.
4. Added VB-CAVI section with clear factorization and update equations under `rhs_ns`.
5. Added ELBO decomposition with explicit tagging of exact closed-form vs approximate pieces.
6. Added explicit section separating:
   - conditional equivalence,
   - joint-prior non-equivalence,
   - algorithmic implications for Gibbs updates.
7. Added in-document bibliography (theory references tied to the new derivations).

## C) Derivation / claim validation summary
Validated and encoded in derivations:
- Shared conditional law:
  - `\beta_j\mid\lambda_j,\tau,\zeta` uses
    `V_j=(\zeta^{-2}+\tau^{-2}\lambda_j^{-2})^{-1}`.
- Conditional-vs-joint distinction:
  - NS and PV share conditional regularized Gaussian form,
  - NS is not PV at the joint-prior level.
- MCMC block implications:
  - Under `rhs_ns`, ordinary global-local block preservation is expressed at the full-conditional level given `\beta`.
- Random slab compatibility:
  - With IG prior on `\zeta^2`, update is conjugate under pseudo-data/product representation.
- VB separation:
  - exact closed-form factors for conjugate blocks,
  - Laplace/Delta approximation only where non-conjugacy remains (`(\sigma,\gamma)`).

## D) Citation / bibliography updates
- Added theory citations directly in the document bibliography:
  - Piironen & Vehtari (2017)
  - Nishimura & Suchard (2023)
  - Makalic & Schmidt (2016)
  - Bhattacharya, Khare & Pal (2021)
  - Fan et al. (2025)
  - Yan, Zheng & Kottas (2025)
- Kept citation usage aligned with mathematical claims introduced in the rewrite.

## E) Compile / check status
Command run:
- `pdflatex -interaction=nonstopmode -halt-on-error main.tex` (two passes)

Results:
- Final compile: success.
- Resolved environment issue: removed unavailable package `bbm` and replaced indicator notation with `\mathbf{1}`.
- Remaining non-fatal warning:
  - one overfull hbox in the ELBO section formatting.

## F) Remaining uncertainties and next steps
- The prior on `(\sigma,\gamma)` remains intentionally non-conjugate; approximation strategy is explicit, but model-specific sampler tuning (proposal scales / optimizer settings) is implementation-dependent.
- If strict journal style is needed, we can add a compact symbol table and theorem/lemma numbering around key derivations.
- If desired, an additional appendix can map every equation one-to-one to concrete code variables for a reference implementation.
