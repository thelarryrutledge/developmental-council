# Extension Guide

To add a new domain package, create four profile files and one package file.

## 1. Create a council

Add `councils/<domain>.md` with 4–7 advisors representing competing concerns.

Good advisors are not generic experts. They should pull in different directions.

## 2. Create a chair

Add `chairs/<chair-name>.md`.

The Chair embodies the convergence personality: what gets weighted, protected, ignored, escalated, or recommended.

## 3. Create an executor

Add `executors/<executor-name>.md`.

The Executor creates domain artifacts from the Chair's recommendation.

## 4. Create a reviewer

Add `reviewers/<reviewer-name>.md`.

The Reviewer verifies alignment, correctness, and risk.

## 5. Create a package

Add `packages/<domain>/package.md` that references the four components.

Example:

```text
- Council: councils/writing.md
- Chair: chairs/editor-in-chief.md
- Executor: executors/writing-executor.md
- Reviewer: reviewers/copy-editor.md
```

## Design advice

Do not overload the core skill. Put domain assumptions in packages.

Do not make the Chair neutral. A Chair always has values and priorities. Make them explicit.

Do not let the Executor re-run the whole council. Its job is artifact creation.

Do not skip the Reviewer when the Executor creates something consequential.
