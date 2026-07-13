# Requirements

The artifact can be used in two ways:

1. **Inspecting the archived results**, which does not require re-running the LLM-based workflow.
2. **Recomputing suggestions with the TTool-based implementation of γμS**, which requires installing TTool and configuring access to an LLM backend.

## Hardware Requirements

We recommend a standard laptop or desktop computer with:

* a 64-bit processor,
* at least 8 GB of RAM,
* at least 2 GB of free disk space for TTool, its build artifacts, and the artifact files,
* an Internet connection if a remote LLM provider is used.

No GPU is required.

## Operating System

TTool is compatible with macOS, Linux and Windows. In our tests, we used two computers, running macOS and Ubuntu 24.04.4 LTS.

## Software Requirements for Installing TTool

### Standard installation from TTool's website

Only a Java Runtime Environment 11 (or later) is required, with `java` available in the execution path.

### Installation from TTool's GitLab

To install TTool from the public GitLab repository, the following tools must be installed and available in the execution path:

* `git`,
* Gradle 7 or 8,
* `make`,
* `javac` 11 or later,
* `java` 11 or later.

## Software Requirements for Re-running the TTool-based implementation of γμS

Re-running the TTool-based implementation of γμS requires the AI-assisted modeling features of TTool. In addition to the TTool installation requirements listed above, one needs:

* access to an LLM backend supported by TTool,
* the corresponding API key or authentication mechanism,
* a configured TTool AI setup,
* a configured MCP setup if using Codex as in our experiments.

Our experiments used OpenAI Codex through TTool's AI/MCP support.

TTool-AI can also be configured with other AI providers or with a self-hosted backend compatible with the OpenAI-style JSON interface.

## OpenAI / Codex Requirements

To reproduce the γμS execution setup used in the paper, one should configure Codex in TTool.

This requires:

* installing the Codex command-line interface,
* logging into the relevant OpenAI or ChatGPT account from the command line (no API key is needed, but a ChatGPT account is needed),
* adding the Codex path to the TTool configuration file,
* selecting Codex as the AI model in TTool,
* configuring TTool as an MCP server for Codex.

A typical TTool configuration includes entries of the following form, adapted to the local installation:

```xml
<CustomAIModel data="codex ..." />
<CodexPath data="/path/to/codex" />
```
See the [example TTool configuration file](./configuration/config.xml.example) for more details.

A typical Codex MCP configuration includes entries of the following form, adapted to the local installation:

```toml
[mcp_servers.ttool]
command = "java"
args = ["-jar", "/path/to/TTool/bin/ttool-cli.jar", "-mcpcodex"]

[mcp_servers.ttool_suggestion]
command = "java"
args = ["-jar", "/path/to/TTool/bin/ttool-cli.jar", "-mcpcodex-suggestion"]

[mcp_servers.ttool_mutation]
command = "java"
args = ["-jar", "/path/to/TTool/bin/ttool-cli.jar", "-mcpcodex-mutation"]
```
See the [example Codex configuration file](./configuration/config.toml.example) for more details.
