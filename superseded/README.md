# Superseded evaluation data

## Status

The files in this directory correspond to an earlier evaluation of the γµS implementation. They are retained only for transparency and traceability: these data are superseded and **do not correspond to the quantitative results reported in the camera-ready paper**.

The corrected evaluation data are available in the parent evaluation directory.

## Reason for supersession

### MCP server implementation error
The original evaluation was conducted with an implementation affected by a bug in the MCP server.

This bug concerned successive calls to the mutation script well-formedness checker through the MCP server. The model used by the checker was not systematically reloaded between calls: as a consequence, some checks could be performed against a model on which previous mutation scripts were already applied. This issue could affect the feedback returned to the LLM and therefore the quality of generated mutation scripts.

### Scoring error
Moreover, during the review of the original evaluation artifacts, we identified model regressions in five runs of the oceanographic-buoy case study. These regressions had not been detected during the initial manual scoring.

In those runs, the state machine diagram of the `Controller` block was reduced to its initial state after mutation application. This occurred because, for this class of syntactically invalid input models, the graphical model-to-memory translation used by TTool omitted parts of the state machine, which were consequently lost when the graphical model was reconstructed. Although the added elements addressed part of the omission identified by the executable suggestion, the resulting model had lost the pre-existing controller behavior.

These five models had initially received high model improvement scores because this regression had not been noticed. These scores and the aggregated results derived from them are therefore not considered valid.

## Corrective actions

The implementation bug was fixed by ensuring that the model is reloaded appropriately in the MCP server for each separate invocation of the mutation verification mechanisms, and the complete evaluation was then rerun from scratch. The corrected evaluation:
- contains 35 independent runs;
- includes a new manual inspection of every resulting model;
- records the scoring rationale directly in notes attached to the block diagrams;
- is the unique source of the quantitative results reported in the camera-ready paper.

## Impact on the results

The correction naturally changes several numerical values. However, interestingly **the main qualitative observations remain unchanged from one evaluation to another**:
- well-formed executable suggestions are associated with substantially better model improvement quality;
- well-formed executable suggestions require less computation time on average;
- model modification remains to appear less efficient than completion or deletion in the evaluated sample;
- deletion suggestions remain consistently well formed in the corrected evaluation.