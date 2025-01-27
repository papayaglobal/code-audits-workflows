# Code Audits Workflows

This repository is designed to run code audits for our internal projects at Papaya Global.

To perform an audit, go to **Actions -> Workflow "Parse selected codebase for LLM audits"** and run it on your repository to generate an audit for your project.

An example audit for the [wm-worker-onboarding](https://github.com/papayaglobal/wm-worker-onboarding/) service can be seen [here](https://code-audits-papaya.vercel.app/repo/b51e8c35-64ab-4033-950f-8bc782cbddce).
# About the App

The Code Audits app operates in two steps:

1. It generates a single markdown or text file containing an LLM prompt that describes the repository’s code.
2. Based on this file, the app generates audits using LLM services (currently Google Gemini, with plans to add ChatGPT, Claude, and others in the future).

# Ways of Running Code Audits

There are several ways to generate code audits. Each method begins with the app [codebase-dump](https://github.com/frogermcs/codebase-dump), an open-source Python project that parses a codebase and submits it to CodeAudits.

The easiest way to run an audit within Papaya Global is through this repository's GitHub Actions:

1. Go to the **Actions** tab.
2. Run the workflow **"Parse selected codebase for LLM audits"**.
3. Paste the URL of your repository. For example: `https://github.com/papayaglobal/wm-worker-onboarding/`.

To explore other methods of running Code Audits, visit the documentation at [https://codeaudits.ai/docs/](https://codeaudits.ai/docs/).

# Limitations

Currently, the parsed repository cannot exceed 4.5MB due to the request size limit of Vercel Functions. Submitting larger repositories will likely result in a 500 error during the data submission phase of the codebase-dump parser.

To overcome this limitation, you can add a `.cdigestignore` file at the root of your repository. This file works similarly to `.gitignore` and allows you to specify files and directories to exclude from the parsing process. This can be useful for ignoring large files or entire directory trees that aren’t essential for the code audit.

For example, to parse our [file-generator-engine](https://github.com/papayaglobal/file-generator-engine/) service, which contains large test files, you can add a `.cdigestignore` file with the following content:

```
# Files to ignore by codebase-dump  
**/src/test/resources
```

For a more detailed explanation and working examples, please check out [Code Audits - Quickstart Guide - Ignore Example](https://colab.research.google.com/drive/1ASFMYyngcmiZeijQ_78jqR7NfyxHI9Zf?usp=sharing).
