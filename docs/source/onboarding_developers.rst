.. _onboarding_developers:

================================================
Onboarding Tutorial: Using Claude Code with Smarter
================================================

Welcome to the Northern Aurora Power & Light (NAPL) custom programming onboarding guide. This tutorial outlines how to configure and utilize **Claude Code** as your AI coding assistant, leveraging **Smarter** as our centralized on-premise LLM host and authoring platform.

Goal
====
We will use Claude Code with Smarter to accelerate software development, streamline code refactoring, and automate technical workflows directly from your local development environment.

Prerequisites
=============
Before beginning this guide, ensure you have:
* An active **Smarter** platform account and login credentials.
* **Node.js** (v18 or higher) and **npm** installed on your local machine (required for running the Claude Code CLI).
* A code editor (such as VS Code) installed and configured.
* Basic familiarity with command-line interfaces (Terminal, PowerShell, or Bash) and Git workflows.

Setup
=====
Complete the following initialization steps to connect your local development environment to the Smarter platform:

1. **Obtain Your Smarter API Token:**
   Log into your Smarter web dashboard, navigate to your user profile settings, and generate a personal API access token.
2. **Configure Environment Variables:**
   Set the required environment variables in your local shell profile (e.g., `~/.bashrc`, `~/.zshrc`, or PowerShell profile) so that Claude Code routes requests through Smarter:

   .. code-block:: bash

      export ANTHROPIC_BASE_URL="https://smarter.napl.internal/v1"
      export ANTHROPIC_API_KEY="your-smarter-api-token-here"

3. **Install Claude Code CLI:**
   Install the Claude Code command-line interface globally via npm:

   .. code-block:: bash

      npm install -g @anthropic-ai/claude-code

Concept Overview
================
Understanding how components interact within the NAPL infrastructure ensures smooth daily usage:

* **Smarter Platform:** Acts as our centralized, secure on-premise gateway. It intercepts LLM requests, handles enterprise authentication, and logs token consumption for accounting codes.
* **Claude Code CLI:** Runs directly inside your repository workspace in your terminal, allowing you to ask questions, generate code snippets, and execute safe automated edits across multiple files.
* **Routing:** By pointing your environment variables to Smarter's endpoint, all prompts and code context flow securely through corporate infrastructure without leaving our network boundaries.

Step-by-Step Workflow
=====================

1. **Navigate to Your Project Directory:**
   Open your terminal and change directory to any active Git repository you are working on:

   .. code-block:: bash

      cd /path/to/your/project

2. **Launch Claude Code:**
   Initialize Claude Code in your workspace by running:

   .. code-block:: bash

      claude

3. **Execute Your First Prompt:**
   Once the interactive interface loads, type a natural language prompt to test code generation or review:

   > "Analyze this repository structure and summarize the main Python modules."

4. **Review and Apply Changes:**
   Claude Code will propose file edits or run terminal commands. Review the proposed changes carefully before approving them in the prompt interface.

Proof of Concept
================
To verify your setup is fully functional, run a quick self-test. Inside your project root, invoke Claude Code to generate a unit test template:

.. code-block:: bash

   claude -p "Generate a basic pytest skeleton for a utility function that validates user email strings."

**Expected Result:** Claude Code should successfully query the Smarter platform, output a clean, syntax-valid Python test file snippet directly in your terminal, and confirm token usage within acceptable response times.

Troubleshooting
===============
If you encounter issues during setup or execution, check the following common pitfalls:

* **Authentication Errors (401 / 403):** 
  * *Cause:* Invalid or expired Smarter API token, or missing header configuration.
  * *Solution:* Regenerate your token in the Smarter dashboard and verify that your `ANTHROPIC_API_KEY` environment variable is exported correctly.
* **Connection Timeout / DNS Resolution Failure:**
  * *Cause:* Working off-network without an active NAPL VPN connection.
  * *Solution:* Ensure you are connected to the corporate VPN so your machine can reach the on-premise Smarter gateway (`smarter.napl.internal`).
* **Model Not Found Error:**
  * *Cause:* Requesting a model identifier that hasn't been enabled by administrators.
  * *Solution:* Confirm with your team lead that the default Claude model identifier matches what is registered in the Smarter provider configuration.