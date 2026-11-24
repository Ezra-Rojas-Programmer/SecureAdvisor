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

## License
MIT License

Copyright (c) 2026 Ezra Isaac Rojas

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
