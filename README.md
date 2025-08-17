# GenAi Code Analyzer
This repository is a guide for flattening entire codebases and analyzing them with LLMs. 

## Flatterning Codebases
Repo2txt is a simple Python module that can take a local directory and flatten all of its content into a single text file for appending to a prompt.  https://github.com/donoceidon/repo2txt/tree/main

## Local
You will want a small model for local use, probably less than 10B parameters.
Meta's ollama has a 7B model suitable for local use and a great CLI.
https://ollama.com/library/codellama

Following the docs, you can prompt the model with a question like:
```bash
ollama run codellama "Write me a function that outputs the fibonacci sequence"
```

### Example
You can tokenize the sample code in this repo with the following command:
```bash
repo2txt -r /path/to/this/repo/sample_code -o output.txt
```
And interrogate the codebase with:
```bash
ollama run codellama "Can you tell me what this code is doing?  $(<output.txt)"
```

```bash
ollama run codellama "Can you find nay bugs in the code?  $(<output.txt)"
```

## Cloud (Bedrock)
TO DO
