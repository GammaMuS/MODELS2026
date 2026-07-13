# Welcome to the γμS Companion Material!

This repository contains the companion material used to evaluate the TTool-based implementation of **γμS**, reported in the camera-ready version of the paper accepted at **MODELS 2026**.

The artifact contains the models, specifications, prompts, and detailed evaluation results used in the paper. The reported results can be inspected directly from the archived files, without re-running the LLM-based workflow, just by opening the `.xml` files in TTool.

## Public Archive

* The artifact is publicly archived on Zenodo: https://doi.org/10.5281/zenodo.20848789
* The Zenodo record includes a source snapshot of the exact TTool version used for the corrected evaluation.
* The source code of the latest version of TTool is publicly available from Télécom Paris' GitLab: https://gitlab.telecom-paris.fr/mbe-tools/TTool

## Repository Contents

### `./models/`

This directory contains the base variants of the two case studies and the 35 run-specific results. When an executable suggestion was applicable, the corresponding tab contains the model obtained after applying it; otherwise, it preserves the available output of the run for inspection.

#### Oceanographic Buoy

##### `oceanographicBuoy_incompleteVariant.xml`

[This file](./models/oceanographicBuoy_incompleteVariant.xml) contains the base models and 10 run-specific results relative to the oceanographic buoy case-study, incomplete variants. When opened in TTool, it contains the following tabs:

* **`FullDesign`**: the initial complete design model, including one block diagram and 8 state machines.
* **`IncompleteDesign`**: the first variant, in which the `Barometer` block is missing.
* **`IncompleteDesignVariant`**: a factorized version of the incomplete variant, in which the data acquisition is modeled in the `Controller` SMD through a single transition from `readingIMUData` to `computingDerivedMeasurements` with six consecutive input signal receptions.
* For each *i* in `[1; 5]` and each *X* in {`IncompleteDesign`, `IncompleteDesignVariant`}:

  * **`X_Testi`**: the model produced for run *i* of γμS on `X`. Each tab includes, in a note displayed in the block diagram panel:
    * the computed suggestion,
    * the resulting model, when the executable suggestion was applicable,
    * the score assigned by LLM#3,
    * our own scores,
    * a justification of our scores.

##### `oceanographicBuoy_overspecifiedVariant.xml`

[This file](./models/oceanographicBuoy_overspecifiedVariant.xml) contains the base models and 10 run-specific results relative to the oceanographic buoy case-study, overspecified variants. When opened in TTool, it contains the following tabs:

* **`FullDesign`**: the initial complete design model, including one block diagram and 8 state machines.
* **`OverspecifiedDesign`**: the second variant, in which a `SatelliteTransmitter` block has been added, together with a connection between this block and `Controller`, and a corresponding signal in the block `Controller`.
* **`Design2`**: a factorized version of the overspecified variant, in which the data acquisition is modeled in the `Controller` SMD through a single transition from `readingIMUData` to `computingDerivedMeasurements` with six consecutive input signal receptions.
* For each *i* in `[1; 5]` and each *X* in {`OverspecifiedDesign`, `OverspecifiedDesignVariant`}:

  * **`X_Testi`**: the model produced for run *i* of γμS on `X`. Each tab includes, in a note displayed in the block diagram panel:
    * the computed suggestion,
    * the resulting model, when the executable suggestion was applicable,
    * the score assigned by LLM#3,
    * our own scores,
    * a justification of our scores.

#### Coffee Machine

##### `coffeeMachine_incompleteAndtimingVariants.xml`

[This file](./models/coffeeMachine_incompleteAndtimingVariants.xml) contains the base models and 10 run-specific results relative to the coffee machine case-study, for the incomplete variant and the variant with timing errors. When opened in TTool, it contains the following tabs:

* **`AVATAR Requirements`**: a requirement diagram. It is not required for γμS.
* **`FullDesign`**: the initial complete design model, including one block diagram and 4 state machines.
* **`IncompleteDesign`**: the first variant, in which the `TeaButton` block is missing, and where the initial values of attributes and transitions are inconsistent with temporal constraints.
* **`TimingErrors`**: the second variant, where the initial values of attributes and transitions are inconsistent with temporal constraints.
* For each *i* in `[1; 5]` and each *X* in {`IncompleteDesign`, `TimingErrors`}:

  * **`X_Testi`**: the model produced for run *i* of γμS on `X`. Each tab includes:
    * the computed suggestion,
    * the resulting model, when the executable suggestion was applicable,
    * the score assigned by LLM#3,
    * our own scores,
    * a justification of our scores.

##### `coffeeMachine_overspecifiedVariant.xml`

[This file](./models/coffeeMachine_overspecifiedVariant.xml) contains the base models and 5 run-specific results relative to the coffee machine case-study, for the overspecified variant. When opened in TTool, it contains the following tabs:

* **`AVATAR Requirements`**: a requirement diagram. It is not required for γμS.
* **`FullDesign`**: the third variant, which includes an additional `CappuccinoButton` block connected to the `CoffeeMachine` block.
* For each *i* in `[1; 5]`:

  * **`Overspecification_Testi`**: the model produced for run *i* of γμS. Each tab includes:
    * the computed suggestion,
    * the resulting model, when the executable suggestion was applicable,
    * the score assigned by LLM#3,
    * our own scores,
    * a justification of our scores.

### `./specifications/`

[This directory](./specifications) provides the complete system specifications for both case studies, in Markdown format.

### `./evaluationResults/`

[This directory](./evaluationResults) contains an `.ods` [spreadsheet](./evaluationResults/FullEvaluationTable.ods) gathering our detailed evaluation results for each of the 35 runs of the TTool-based implementation of γμS.

### `./prompts/`

[This directory](./prompts) contains a Markdown file gathering the predefined prompts used by our implementation to drive the three LLMs.

### `./superseded/`

[This directory](./superseded) contains [the models](./superseded/models) and [the evaluation scores](./superseded/evaluationResults) of a first evaluation of the SysML implementation of γμS. These results were obtained with an implementation affected by a bug in one of the MCP tools and contain a manual scoring error identified a posteriori. It is kept only for transparency and traceability: the data it contains are **superseded** and must not be used to reproduce the quantitative results reported in the camera-ready paper.

[This file](./superseded/README.md) gives more details about this initial evaluation.



## Inspecting the Reported Results

The results reported in the paper can be inspected without re-running the SysML implementation of γμS. You just need to:
1. Open the relevant `.xml` model file in TTool.
2. Navigate to the tab corresponding to the run of interest.
3. Inspect the computed suggestion, the modified model, the score assigned by LLM#3, and our scoring and evaluation.
4. Compare these results with the detailed table provided in `./evaluationResults/`.



## Reproducing Suggestion Computation with the TTool-based implementation of γμS

### Version note

The evaluation was conducted with:

- TTool version: 5.0 alpha
- Build: 14889
- Git commit: cf4760ec80a029fc4aee1314213cfb43e7461a7e (For artifact reproduction, we provide revision 29d32f99a9fbe617cd72f838436b5246d03b371c, which differs only in that Codex sandbox and approval policies are now delegated to the selected config.toml profile).

### Installing TTool

The following procedure has been validated on both **macOS** and **Linux (Ubuntu 24.04 LTS)**. The following tools are required to install and run TTool:

* Gradle 7 or 8
* `make`
* `javac` 11
* `java` 11 or higher

First, install TTool:

```bash
git clone https://gitlab.telecom-paris.fr/mbe-tools/TTool.git
cd TTool
git checkout 29d32f99a9fbe617cd72f838436b5246d03b371c
make ttool-cli && make ttoolnotest
```


### Configuring Codex and the MCP server

A complete sanitized version of the configuration used for the evaluation is provided in [`configuration/`](./configuration/).

1. Copy [`config.xml.example`](./configuration/config.xml.example) to `TTool/bin/config.xml`.
2. Replace the codex binary placeholder path with the path of your local installation.
3. Copy [`config.toml.example`](./configuration/config.toml.example) to `~/.codex/config.toml`.
4. Replace every placeholder path in `config.toml` with the absolute path of the corresponding file in your local TTool installation.
5. Run `codex` and complete the authentication procedure displayed by the CLI. Since Codex can access files located in its working directory, we recommend launching it from an isolated directory containing no confidential data. Note that Codex **does not** require an OpenAI API key when authenticated through a ChatGPT account. Running `codex` without authentication options opens the ChatGPT sign-in flow in your web browser.
6. Start TTool and verify the configuration by selecting `AI` > `Set AI model`. If you see `codex` in the list, select it.

Additional information is available in the [TTool AI documentation](https://ttool.telecom-paris.fr/ttoolai.html).


### Computing Suggestions with the TTool-based implementation of γμS

Once TTool is installed, launch it:

```bash
./ttool.exe
```

Open a model, for example **[`coffeeMachine_incompleteAndtimingVariants.xml`](./models/coffeeMachine_incompleteAndtimingVariants.xml)**, and navigate to the **`IncompleteDesign`** tab.

In the left panel, scroll to **`Suggestions by AI`**. Right-click on it and select **`Advanced suggestions for Avatar Design`** to start the implementation of γμS.

During execution, the console displays the interaction trace between TTool and the LLMs.

When the implementation of γμS completes, a suggestion appears in the tree. If the suggestion is well-formed, you can execute it by right-clicking on it and selecting **`Apply on current model`**.

After execution, the modified model is opened in a new tab.

### Note on LLM-Based Reproduction

Re-running this TTool-based implementation of γμS requires access to the configured LLM backend, in particular OpenAI Codex in our setup. Since the workflow relies on LLM calls, newly generated suggestions may differ from the archived ones.

The archived models and evaluation results correspond to the runs reported in the paper and should be used as the reference material for artifact evaluation.

## Current implementation limitation

Although the generic γµS framework is defined over models that may initially be syntactically incorrect, the current TTool-based implementation assumes syntactically well-formed input models. The reference evaluation only considers models within this supported input domain.

In TTool, input-model well-formedness can easily be checked using the `Syntax analysis` button in the main toolbar. Its icon is a red arrow with white dots.




Enjoy!