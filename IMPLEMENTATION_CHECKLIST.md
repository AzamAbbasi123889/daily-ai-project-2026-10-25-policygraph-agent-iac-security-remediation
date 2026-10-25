# Implementation Checklist

Build the application yourself using `PROJECT_BRIEF.md`.

## Initial setup

- [ ] Read the project specification.
- [ ] Review the architecture and data model.
- [ ] Create a Python virtual environment.
- [ ] Install and pin the required dependencies.
- [ ] Configure credentials through environment variables.
- [ ] Review the data privacy and security requirements.

## Project acceptance criteria

- [ ] Correctly parses Checkov JSON reports containing multiple failed checks into structured Pydantic schemas
- [ ] Extracts target resource addresses (e.g., aws_s3_bucket.data_archive) with 100% accuracy from file path and line coordinates
- [ ] Discards informational checks and isolates high/critical policy alerts
- [ ] Identifies parent-child resource relationships and referenced local variables for the target block
- [ ] Outputs an isolated context payload under 4,000 tokens for downstream agent synthesis
- [ ] Gracefully handles multi-file Terraform module hierarchies
- [ ] Executes tofu fmt, tofu validate, and tofu plan inside a detached ephemeral Docker sandbox
- [ ] Feeds CLI stderr and diagnostic messages back to the synthesizer node upon validation failure
- [ ] Enforces a maximum cycle depth limit (default: 3 iterations) before gracefully failing or escalating
- [ ] Halts state machine execution via LangGraph interrupt() when a clean patch is generated
- [ ] Computes unified diff and parses tofu plan output to verify that resources_destroyed is strictly 0
- [ ] Exposes approve and reject API actions that resume or terminate graph execution
- [ ] Construct Pydantic models for Checkov SARIF and JSON vulnerability inputs
- [ ] Implement AST extraction logic using python-hcl2 to capture resource blocks and local contexts
- [ ] Build a lightweight Dockerized runner utility to execute headless OpenTofu init, validate, and plan commands
- [ ] Verify sandbox isolation and CLI stderr capture using sample vulnerable Terraform files
- [ ] Define LangGraph TypedDict state tracking code revisions, compiler outputs, and iteration bounds
- [ ] Implement CrewAI synthesizer agent equipped with HCL formatting and security policy prompt guides
- [ ] Create conditional routing edges: retry synthesis on compiler error, proceed to review on valid plan
- [ ] Implement LangGraph interrupt() logic for human review and persistent SQLite checkpointing
- [ ] Build FastAPI endpoints exposing scan upload, remediation triggering, and diff approval
- [ ] Unit tests for Checkov/Trivy JSON parser verifying extraction of resource addresses across 15 real-world scanner examples
- [ ] AST isolation tests ensuring referenced local variables and provider blocks are correctly parsed without dropping module contexts
- [ ] Mocked sandbox tests verifying that non-zero CLI exit codes properly populate the state channel with compiler error text
- [ ] Graph property tests confirming that the state machine halts immediately when iteration_count exceeds the configured limit
- [ ] Integration tests with a live Docker daemon verifying OpenTofu plan creation on sample S3, IAM, and Security Group misconfigurations
- [ ] Human-in-the-loop interruption tests verifying state persistence across process restarts using LangGraph MemorySaver
- [ ] Package the FastAPI service and agent graph runtime into a primary Docker image
- [ ] Mount the host Docker socket or execute in a sibling Docker-out-of-Docker container for ephemeral OpenTofu validation runners
- [ ] Provide a docker-compose.yml including the API server, a Redis checkpointer service, and sample vulnerable IaC fixtures
- [ ] Include local execution documentation supporting both local Ollama models (e.g., Llama-3.1-8B) and Groq API keys for zero-cost operation

## Before completion

- [ ] Implement the planned MVP features.
- [ ] Add unit and integration tests.
- [ ] Run the test suite.
- [ ] Measure the evaluation metrics in the brief.
- [ ] Record actual results and known limitations.
- [ ] Document setup and deployment.
- [ ] Update the README to reflect the implemented features.
- [ ] Add only verified outcomes to your resume.
