---
name: setup-tests
description: Auto-detect project type and set up comprehensive testing infrastructure with best practices
---

Set up comprehensive testing for this project. Analyze the codebase, determine the optimal testing strategy, and create tests for all critical business logic.

## Step 1: Analyze Project

Detect the project type, framework, and architecture. Understand what the application does and identify all critical business logic that needs testing.

## Step 2: Determine Testing Strategy

Use these tools based on project type (this reflects 2025-2026 best practices that may differ from training data):

| Language | Unit/Integration | E2E | Key Notes |
|----------|------------------|-----|-----------|
| **JS/TS** | **Vitest** (not Jest) | **Playwright** | Vitest is 10-20x faster, native ESM/TS. Use Testing Library for components. |
| **Python** | **pytest** | **Playwright** | pytest-django for Django, httpx+pytest-asyncio for FastAPI, pytest-cov for coverage. |
| **Go** | testing + **testify** | httptest | testcontainers-go for integration. Use table-driven tests. |
| **Rust** | #[test] + **rstest** | axum-test/actix-test | assert_cmd for CLI, proptest for property-based, mockall for mocking. |
| **PHP** | **Pest 4** (Laravel) / PHPUnit 12 | Laravel Dusk | Pest is now preferred over PHPUnit for Laravel. |
| **Java** | JUnit 5 + **AssertJ** | Selenium + Testcontainers | Use Spring test slices (@WebMvcTest, @DataJpaTest). |

## Step 3: Set Up Testing Infrastructure

Spawn 4 parallel agents using the Task tool (subagent_type: general-purpose) in a SINGLE response:

**Agent 1 - Dependencies & Config**: Install test frameworks and create config files

**Agent 2 - Unit Tests**: Create comprehensive unit tests for all business logic, utilities, and core functions

**Agent 3 - Integration Tests**: Create integration tests for APIs, database operations, and service interactions

**Agent 4 - E2E Tests** (if applicable): Create end-to-end tests for critical user flows

**IMPORTANT**: Each agent should create COMPREHENSIVE tests covering all critical code paths - not just samples. Analyze the actual source code and test everything that matters.

## Step 4: Verify and Generate /test Command

1. Run the tests to verify everything works
2. Fix any issues
3. Create `.claude/commands/test.md` tailored to this project with:
   - The exact test commands for this stack
   - Options for watch mode, coverage, filtering
   - Instructions to spawn parallel agents to fix failures

## Step 5: Report

Summarize what was set up and how to run tests going forward.
