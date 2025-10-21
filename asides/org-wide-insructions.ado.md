
Step 1: Create a centralized instruction template repository.
Create one repository that holds your standard instructions as markdown templates. This becomes your source of truth for coding standards.

Step 2: Document standard instructions as markdown templates.
In this repository, create templates for different types of projects:
copilot-instructions-python.md
copilot-instructions-javascript.md
copilot-instructions-dotnet.md
etc.

Step 3: Have teams copy templates to their repo .github/ folders.
When a team starts a new project or wants to add Copilot instructions, they copy the relevant template from your central repository into their .github folder.

Step 4: Use pull request templates to enforce inclusion.
In your ADO pull request templates, include a checklist item: "Copilot instructions are present and up to date." This reminds teams to maintain their instructions.

Step 5: Run regular audits to ensure consistency.
Periodically, audit your repositories to make sure they have instructions and that they match your standards. You can automate this with an Azure Pipeline.

Optional: Create an Azure Pipeline to sync instructions across repos automatically.
Here's a simple example:
# Example Azure Pipeline to sync instructions
trigger: none  # Manual or scheduled only

steps:
- checkout: self

- script: |
    curl https://raw.githubusercontent.com/yourorg/copilot-standards/main/copilot-instructions.md \
      -o .github/copilot-instructions.md

- task: GitCommit
  # Commit updated instructions

This pipeline pulls the latest instructions from your central repository and updates each project's instructions automatically. You can schedule this to run monthly or trigger it manually when you update your standards.

It's more work than GitHub Enterprise's organization instructions, but it achieves the same goal: consistent Copilot behavior across all your projects.
