# Code availability

## Manuscript-ready statement

The complete analysis code is publicly available in this GitHub repository. The repository contains a self-contained Jupyter notebook that retrieves the public municipality-week surveillance inputs from the InfoDengue API; reconstructs the prespecified municipal panels; fits, calibrates, and evaluates all forecasting models; estimates cross-municipality dependence; reproduces the primary and secondary scoring analyses; runs the hypothetical preparedness scenarios; and exports all tables, figures, diagnostics, provenance records, and file hashes. Package requirements and step-by-step execution instructions are provided in the repository README. Because InfoDengue surveillance records are revised retrospectively, later API retrievals may not exactly reproduce the study snapshot; completed runs preserve raw-file hashes and retrieval metadata to support auditing.

## Short journal version

Analysis code, environment requirements, and reproduction instructions are available in this public GitHub repository. Inputs are retrieved from the InfoDengue API during execution. Because the source surveillance records are revised retrospectively, reruns using later API snapshots may differ; the workflow records retrieval metadata and SHA-256 hashes for all downloaded files.

Before manuscript submission, replace “this public GitHub repository” with the final repository URL and, if archived, add the permanent DOI.
