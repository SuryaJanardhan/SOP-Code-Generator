# Multi-Agents :


- SOP Agent → understands the bug, instructions, conditions, expected fix.
- Repository Agent → understands the structure of the massive repository.
- Code Localization Agent → finds the exact relevant file/function.
- Planning Agent → decides what change should be made.
- Code Modification Agent → applies the patch.
- Validation Agent → runs tests/build/static checks.
- Debug Agent → analyzes failures and feeds the information back into the fixing loop.
- Supervisor → maintains state and decides what should happen next.





# Proposed Agents

## 1. SOP Agent

### Responsibility

The SOP Agent is responsible for reading, understanding, and analyzing the SOP document.

It extracts and interprets:

- The reported error or issue
- Conditions under which the issue occurs
- The affected component or area, if specified
- Step-by-step instructions provided in the SOP
- Expected behavior after the fix
- Constraints or requirements that must be maintained

### Goal

Convert the natural language information present in the SOP into a structured understanding of the problem.

### Output

The agent produces a structured understanding of:

- What is currently failing
- Under what conditions the failure occurs
- Which area of the system is affected
- What behavior is expected after the fix
- What resolution instructions or requirements are provided by the SOP

---

## 2. Repository Agent

### Responsibility

The Repository Agent is responsible for understanding the overall structure of the codebase.

Since the repository may contain a large number of files and a significant amount of code, the agent first develops a high-level understanding of the repository instead of immediately analyzing every line.

The Repository Agent analyzes:

- Repository structure
- Important directories
- Modules and packages
- Programming languages used
- Frameworks and dependencies
- README files and available documentation
- Application entry points
- Major components
- Relationships between different modules

### Goal

Create an initial understanding of how the repository is organized so that other agents can efficiently navigate the codebase.

### Output

A structured representation or summary of the repository, including the important modules, components, and relationships relevant to the task.

---

## 3. Code Localization Agent

### Responsibility

The Code Localization Agent is responsible for identifying the exact location in the codebase related to the issue described in the SOP.

A large repository may contain thousands of files and hundreds of thousands of lines of code. The agent must progressively narrow down the search to identify the relevant implementation.

The localization process may involve identifying:

- The relevant module
- The relevant directory
- The relevant file
- The relevant class or component
- The exact function or implementation responsible for the issue

The agent uses information from:

- SOP analysis
- Repository analysis
- Code search
- Function and symbol references
- Imports and dependencies
- Related files and components
- Relevant surrounding code

### Goal

Find the most relevant file, class, function, or implementation point where the required modification should be applied.

### Output

The agent returns:

- Relevant module
- Relevant file or files
- Relevant class or component
- Exact target function or implementation
- Supporting code context
- Reasoning for why the identified location is relevant

---

## 4. Planning Agent

### Responsibility

The Planning Agent determines how the identified code should be modified before any changes are made.

It analyzes:

- The current implementation
- The requirements extracted from the SOP
- Dependencies and related components
- Potential impact on other parts of the codebase
- Possible edge cases
- The minimum changes required to resolve the issue

### Goal

Create a clear modification strategy before changing the repository.

### Output

A structured plan describing:

- What needs to change
- Where the change should be made
- Why the change is necessary
- How the change addresses the issue described in the SOP
- Potential dependencies or risks
- What validation should be performed after the modification

---

## 5. Code Modification Agent

### Responsibility

The Code Modification Agent is responsible for applying the required changes to the codebase based on the plan.

Before modifying the code, the agent reads and understands:

- The target implementation
- Relevant surrounding code
- Related functions or classes
- Dependencies required for the change

The agent then applies the required modification.

### Goal

Produce the smallest correct change required to resolve the issue while avoiding unnecessary modifications to unrelated parts of the repository.

### Output

The result may include:

- Modified source code
- Updated files
- A code patch or diff
- An alternative implementation, if required

---

## 6. Validation Agent

### Responsibility

The Validation Agent verifies whether the modification works correctly and does not break the existing codebase.

Depending on the repository and available tooling, validation may include:

- Build or compilation checks
- Unit tests
- Integration tests
- Existing test suites
- Static analysis
- Linting
- Type checking
- SOP-specific validation scenarios

### Goal

Determine whether the modification successfully resolves the issue while maintaining the correctness of the affected codebase.

### Output

The agent returns a validation result indicating either:

- `PASS` — the modification successfully passes the required validation checks.
- `FAIL` — one or more validation checks failed.

If validation fails, the agent provides relevant information such as:

- Error messages
- Failed test cases
- Build or compilation failures
- Stack traces
- Static analysis results
- Other information required for debugging

---

## 7. Debug Agent

### Responsibility

The Debug Agent is invoked when the Validation Agent reports a failure.

It analyzes the validation results to understand why the modification did not succeed.

The Debug Agent investigates:

- Error messages
- Failed test cases
- Compilation failures
- Runtime failures
- Incorrect assumptions in the previous plan
- Missing dependencies
- Incomplete or incorrect code changes

### Goal

Determine what went wrong and provide the necessary information for the system to make another attempt at resolving the issue.

### Output

The Debug Agent provides:

- Failure analysis
- Likely root cause
- Relevant debugging information
- Recommendations for the next iteration

Depending on the cause of the failure, the workflow may return to:

- **Code Localization Agent** — if the wrong location was identified
- **Planning Agent** — if the modification strategy was incorrect
- **Code Modification Agent** — if the implementation needs adjustment

---

## 8. Supervisor

### Responsibility

The Supervisor is responsible for orchestrating the complete workflow and maintaining the overall state of the task.

The Supervisor:

- Receives the Git repository URL and SOP document
- Manages the overall task state
- Invokes the required agents
- Passes relevant outputs between agents
- Tracks the progress of the task
- Decides which agent should be invoked next
- Controls the validation and retry loop
- Determines when the task has been successfully completed
- Handles controlled termination if the issue cannot be resolved

### Goal

Coordinate the specialized agents and dynamically control the workflow based on the current state of the task.

### Dynamic Execution

Not every issue will require the exact same sequence of agents.

Depending on:

- SOP complexity
- Repository structure
- Current findings
- Agent outputs
- Validation results
- Errors encountered during execution

the Supervisor can dynamically determine which specialized agent should be invoked next.

### Output

The Supervisor produces the final task outcome, which may include:

- Successfully modified and validated code
- Generated patch or code changes
- Validation results
- Relevant explanation of the completed fix
- Controlled failure information if the system is unable to resolve the issue

---


### Proposed Tech Stack

- **Python** → Main backend language; runs agents and project logic.
- **LangGraph** → Manages agent workflow, state, routing, and retry loops.
- **LLM (OpenAI / Claude / Gemini)** → Provides reasoning and understanding to agents.
- **PyMuPDF / python-docx** → Reads and extracts text from SOP documents.
- **GitPython / Git CLI** → Clones and interacts with the target Git repository.
- **ripgrep** → Quickly searches huge codebases for relevant code.
- **Docker** → Safely runs the repository, builds, and tests in an isolated environment.
- **pytest / Maven / npm** → Validates the modified code depending on the project's tech stack.
- **FAISS / ChromaDB** → Performs semantic search to find code relevant to the SOP. [For Large Repositories]

### Optional
- **Tree-sitter / AST Tools** → Understands code structure, functions, classes, and dependencies.
- **FastAPI** → Backend API connecting the frontend to the agent system.
- **PostgreSQL** → Stores persistent task and project data if required.
- **Redis** → Handles caching or background task/state management if required.
- **Streamlit / React** → Provides the user interface for uploading the SOP and entering the Git URL.
