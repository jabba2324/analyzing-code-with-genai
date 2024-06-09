# GenAi Code Analyzer
This repository is a guide for tokenizing entire codebases and analyzing them with LLM models.

## Tokenizing Codebases
Repo2txt is a simple python mobule that can take a local directory and flattern all of it's content into a single text file for appending to a prompt.  https://github.com/donoceidon/repo2txt/tree/main

## Local
For local use, you will want a small model, probably less than 10B parameters.
Meta's ollama has a 7B model that is suitable for local use and a great CLI.
https://ollama.com/library/codellama

Following the docs you can prompt the model with a question like:
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

## Cloud (AWS)
For cloud AWS development, we can run some larger models with 30B+ parameters. CodeWizard has a high ranking 33B model that is suitable for cloud use.

CPU accelerated:
https://github.com/nlpxucan/WizardLM
https://huggingface.co/WizardLMTeam/WizardCoder-33B-V1.1

GPU accelerated (Linux/CUDA):
https://huggingface.co/TheBloke/WizardCoder-33B-V1.1-GPTQ
Consider creating a local virtual pyenv

Setup a python virtual environment with pyenv and install the required packages:
```bash
pyenv virtualenv 3.11 genaica

pyenv activate genaica
```

```bash
pip install boto3 sagemaker
```
Run the sagemaker.py example to deploy the model and run a prompt, using python to read the output.txt and append to the prompt.
