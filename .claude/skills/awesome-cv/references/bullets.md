# Writing experience bullets

The `examples/resume/experience.tex` sample shows the pattern this template rewards. Match it.

## Shape

- One sentence per `\item`. If a thought needs two sentences, split it into two items.
- Start with a strong verb: Led, Designed, Built, Migrated, Provisioned, Introduced, Automated, Reduced, Saved, Established.
- Past tense for prior roles; present tense only if the role is current.
- Prefer concrete over abstract: name the tool, the scale, the outcome.
- Keep to one line at rendered width when you can — the layout is tight.

## Impact + how

Aim for `<what changed> + <how / with what>` in each bullet. Numbers when honest, no invented metrics.

**Good**

- Saved over 30% of overall AWS costs by establishing a quarterly RI/SP purchasing strategy and introducing Graviton instances.
- Migrated orchestration from DC/OS to AWS EKS (3 clusters, 300+ pods) with all manifests declaratively managed via Kustomize and ArgoCD.
- Provisioned an ES cluster (9 nodes, 1B+ documents/month) via a reusable Terraform module.

**Weak**

- Worked on infrastructure.
- Responsible for AWS.
- Helped with cost savings.

## When tailoring to a job posting

- Lead each `\cventry` with the bullet closest to the role's must-haves.
- Drop bullets that are clearly off-topic — a 6-bullet role is fine, a 12-bullet role is noise.
- Rewrite phrasing to use the posting's own vocabulary when it means the same thing (`observability` vs `monitoring`, `platform team` vs `infrastructure team`), never to claim something the source CV doesn't back up.
- If the posting mentions a stack the person hasn't used, don't add it. Note the gap for the user.

## LaTeX gotchas inside bullets

- Percent signs: `30\%`, not `30%`.
- Ampersands in company names: `Danggeun Pay Inc.` → keep as-is; `AT\&T` → escape.
- Version numbers with underscores: escape (`node\_modules`) or wrap in `\texttt{}`.
- Avoid smart quotes copied from job postings — replace `“` `”` with `` `` `` and `''`.

## Length

- Résumé (one-page): 3–5 bullets per current/recent role, 1–3 for older roles, none for very old or short stints.
- CV (long form): as many as the truth supports; still one sentence each.
