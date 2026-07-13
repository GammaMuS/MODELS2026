# Superseded evaluation data

## Status

The files in this directory correspond to an earlier evaluation of the γµS implementation. They are retained only for transparency and traceability: these data are **superseded** and must not be used to reproduce the quantitative results reported in the camera-ready paper.

The corrected evaluation data are available in the parent evaluation directory.

## Reason for supersession

### MCP server implementation error
The original evaluation was conducted with an implementation affected by a bug in the MCP server.

The bug concerned successive calls to the mutation-script well-formedness checker through the MCP server. The model used by the checker was not systematically refreshed between calls. Consequently, some checks could be performed against a model on which previous mutation scripts were already applied.

This issue could affect the feedback returned to the LLM, and therefore the quality of generated mutation scripts.

### Scoring error
Moreover, during the review of the original evaluation artifacts, we identified substantial regressions that had not been detected during the initial manual scoring.

In particular, in several completion runs of the oceanographic-buoy case study, the state machine diagram of the `Controller` block was reduced to its initial state after mutation application. This occurred because, for this class of syntactically invalid input models, the graphical-model-to-memory translation used by the current implementation omitted parts of the state machine, which were consequently lost when the graphical model was reconstructed. Although the added elements addressed part of the identified omission, the resulting model had lost the pre-existing controller behavior.

Some of these models had initially received high final-model-quality scores because this regression had not been noticed. These scores and the aggregated results derived from them are therefore not considered valid.

This also illustrates the distinction between syntactic well-formedness and semantic model quality: a state machine containing only an initial state may satisfy the implemented syntactic checks while representing a major semantic regression.

## Corrective actions

The implementation bug was fixed by ensuring that the model is refreshed appropriately in the MCP server for each separate invocation of the mutation verification mechanisms.

The complete evaluation was then rerun from clean model states. The corrected evaluation:
- contains 35 independent runs;
- uses the corrected implementation;
- includes a new manual inspection of every resulting model;
- records the scoring rationale directly in notes attached to the block diagrams;
- is the unique source of the quantitative results reported in the camera-ready paper.

## Impact on the results

The correction naturally changes several numerical results; however, **the main qualitative observations remain unchanged**:
- well-formed executable suggestions are associated with substantially better final-model quality;
- well-formed suggestions require less computation time on average;
- model modification remains more error-prone than completion or deletion in the evaluated sample;
- deletion suggestions remain consistently well formed in the corrected evaluation.

