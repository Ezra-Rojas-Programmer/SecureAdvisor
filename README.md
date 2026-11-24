# &lt;SecureAdvisor&gt;

Reads AWS CloudTrail events (JSON lines) and uses a Qwen model hosted on a
GPUStack server to classify each event as BENIGN, SUSPICIOUS, MALICIOUS,
or UNKNOWN, with a 1-5 severity score and a one-sentence reason.


## What it does
- Classifies each log entry (BENIGN / SUSPICIOUS / MALICIOUS) with a 1&ndash;5 severity and a reason.
- Returns validated JSON, and processes a whole log file in batch.
- Generates a detection rule (for example a Sigma rule) from the suspicious and malicious findings.
- Treats log text as untrusted input and uses a hardened prompt to resist prompt injection.

## Requirements
- Python 3.9 or newer
- The `openai` package (`pip install openai`)
- Access to an OpenAI-compatible model endpoint (a vLLM server, the class Qwen Coder server, etc.)

## Setup
Install the one dependency:

```
pip install openai
```

Set your model endpoint and key as environment variables (never hard-code them):

```
export QWEN_BASE_URL="http://your-server:8000/v1"
export QWEN_API_KEY="your-api-key"
```

## Usage
Open the notebook and run the cells top to bottom, or import the functions into
your own script. Point `LOG_FILE` at a log file (`.txt` or `.csv`) of log lines,
and the tool will assess them and save the results.

## Security notes
- The API key is read at runtime (`getpass`) or from an environment variable; it is never stored in the notebook.
- Log data is treated as untrusted; the tool uses a hardened prompt to resist instructions hidden in the input.
