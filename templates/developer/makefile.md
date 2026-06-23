# Makefile Template

**Project Name:** [FILL]

**Description:** [FILL]

**Version:** [FILL]

## Makefile

```makefile
# [FILL — Project Name]
# Purpose: [FILL]
# Author: [FILL]

.PHONY: help build install test clean run setup dev prod
.DEFAULT_GOAL := help
SHELL := /bin/bash

# Variables
PROJECT_NAME := [FILL]
PROJECT_DIR := $(shell pwd)
PYTHON := python3
PIP := pip3

# Color output
RED := \033[0;31m
GREEN := \033[0;32m
YELLOW := \033[1;33m
NC := \033[0m # No Color

################################################################################
# Help
################################################################################

.PHONY: help
help:
	@echo "$(GREEN)Available targets:$(NC)"
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "  $(YELLOW)%-15s$(NC) %s\n", $$1, $$2}'

################################################################################
# Setup & Installation
################################################################################

.PHONY: setup
setup: ## Initialize development environment
	@echo "$(GREEN)Setting up development environment...$(NC)"
	$(PYTHON) -m venv venv
	source venv/bin/activate && $(PIP) install --upgrade pip
	$(MAKE) install

.PHONY: install
install: ## Install dependencies
	@echo "$(GREEN)Installing dependencies...$(NC)"
	$(PIP) install -r requirements.txt

.PHONY: install-dev
install-dev: install ## Install dev dependencies
	@echo "$(GREEN)Installing dev dependencies...$(NC)"
	$(PIP) install -r requirements-dev.txt

################################################################################
# Build & Compilation
################################################################################

.PHONY: build
build: ## Build project
	@echo "$(GREEN)Building project...$(NC)"
	[FILL — build commands]

.PHONY: clean
clean: ## Clean build artifacts
	@echo "$(YELLOW)Cleaning build artifacts...$(NC)"
	find . -type d -name __pycache__ -exec rm -rf {} + 2>/dev/null || true
	find . -type d -name .pytest_cache -exec rm -rf {} + 2>/dev/null || true
	find . -type f -name '*.pyc' -delete
	find . -type f -name '*.egg-info' -exec rm -rf {} + 2>/dev/null || true
	[FILL — additional clean commands]

################################################################################
# Testing
################################################################################

.PHONY: test
test: ## Run all tests
	@echo "$(GREEN)Running tests...$(NC)"
	$(PYTHON) -m pytest -v

.PHONY: test-fast
test-fast: ## Run tests without coverage
	@echo "$(GREEN)Running fast tests...$(NC)"
	$(PYTHON) -m pytest -v --tb=short

.PHONY: test-coverage
test-coverage: ## Run tests with coverage report
	@echo "$(GREEN)Running tests with coverage...$(NC)"
	$(PYTHON) -m pytest --cov --cov-report=html --cov-report=term

.PHONY: lint
lint: ## Run linters
	@echo "$(GREEN)Running linters...$(NC)"
	flake8 .
	pylint [FILL]

.PHONY: format
format: ## Format code
	@echo "$(GREEN)Formatting code...$(NC)"
	black .
	isort .

################################################################################
# Development
################################################################################

.PHONY: run
run: ## Run application
	@echo "$(GREEN)Running application...$(NC)"
	$(PYTHON) -m [FILL]

.PHONY: dev
dev: ## Run in development mode with auto-reload
	@echo "$(GREEN)Running in dev mode...$(NC)"
	[FILL — dev command]

.PHONY: shell
shell: ## Start interactive shell
	@echo "$(GREEN)Starting interactive shell...$(NC)"
	$(PYTHON)

################################################################################
# Docker
################################################################################

.PHONY: docker-build
docker-build: ## Build Docker image
	@echo "$(GREEN)Building Docker image...$(NC)"
	docker build -t $(PROJECT_NAME):latest .

.PHONY: docker-run
docker-run: ## Run Docker container
	@echo "$(GREEN)Running Docker container...$(NC)"
	docker run -it $(PROJECT_NAME):latest

.PHONY: docker-compose-up
docker-compose-up: ## Start Docker Compose services
	@echo "$(GREEN)Starting Docker Compose...$(NC)"
	docker-compose up -d

.PHONY: docker-compose-down
docker-compose-down: ## Stop Docker Compose services
	@echo "$(GREEN)Stopping Docker Compose...$(NC)"
	docker-compose down

################################################################################
# Documentation
################################################################################

.PHONY: docs
docs: ## Generate documentation
	@echo "$(GREEN)Generating documentation...$(NC)"
	[FILL — documentation command]

.PHONY: docs-serve
docs-serve: ## Serve documentation locally
	@echo "$(GREEN)Serving documentation...$(NC)"
	[FILL — docs server command]

################################################################################
# Utilities
################################################################################

.PHONY: status
status: ## Show project status
	@echo "$(GREEN)Project Status:$(NC)"
	@echo "  Name: $(PROJECT_NAME)"
	@echo "  Dir: $(PROJECT_DIR)"
	@echo "  Python: $$($(PYTHON) --version)"
	@echo "  Pip: $$($(PIP) --version)"

.PHONY: info
info: status ## Show project information

.PHONY: check
check: lint test ## Run all checks
	@echo "$(GREEN)All checks passed!$(NC)"

.PHONY: all
all: clean install build test ## Run full build pipeline

# [FILL — Custom targets]

.PHONY: [FILL]
[FILL]: ## [FILL — Description]
	@echo "$(GREEN)[FILL]...$(NC)"
	[FILL — commands]
```

## Usage

**View available targets:**
```bash
make help
```

**Setup development environment:**
```bash
make setup
```

**Run tests:**
```bash
make test
```

**Build and test:**
```bash
make check
```

## Common Patterns

### Variable Definition
```makefile
VAR_NAME := value
VAR_NAME ?= default_if_not_set
```

### Conditional Execution
```makefile
ifeq ($(ENV),production)
    @echo "Production build"
else
    @echo "Development build"
endif
```

### Phony Targets
```makefile
.PHONY: target-name
target-name: dependency1 dependency2
	@echo "Running target"
	command here
```

## Notes

[FILL]
