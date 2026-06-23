# Bash/Shell Script Template

**Script Name:** [FILL]

**Purpose:** [FILL — What does this script do?]

**Author:** [FILL]

**Version:** [FILL]

**Last Updated:** [FILL]

## Script

```bash
#!/bin/bash

################################################################################
# [FILL — Script Title]
################################################################################
#
# Description:
#   [FILL — Detailed description of what this script does]
#
# Usage:
#   $0 [FILL — arguments and options]
#   Example: $0 --option value --flag
#
# Requirements:
#   [FILL — Required commands/tools]
#   - bash >= 4.0
#   - [FILL]
#   - [FILL]
#
# Author: [FILL]
# Date: [FILL]
# Version: [FILL]
#
################################################################################

set -euo pipefail  # Exit on error, undefined vars, pipe failures

################################################################################
# Configuration
################################################################################

# Script directory
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

# Color codes for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
NC='\033[0m'  # No Color

# Logging
LOG_LEVEL="INFO"  # DEBUG, INFO, WARN, ERROR
LOG_FILE="${SCRIPT_DIR}/$(basename "$0" .sh).log"

################################################################################
# Functions
################################################################################

# Logging functions
log_debug() {
    if [[ "$LOG_LEVEL" =~ ^(DEBUG)$ ]]; then
        echo -e "${BLUE}[DEBUG]${NC} $*" | tee -a "$LOG_FILE"
    fi
}

log_info() {
    echo -e "${GREEN}[INFO]${NC} $*" | tee -a "$LOG_FILE"
}

log_warn() {
    echo -e "${YELLOW}[WARN]${NC} $*" | tee -a "$LOG_FILE" >&2
}

log_error() {
    echo -e "${RED}[ERROR]${NC} $*" | tee -a "$LOG_FILE" >&2
}

# Error handler
error_exit() {
    log_error "$1"
    exit "${2:-1}"
}

# Print usage
usage() {
    cat << EOF
Usage: $0 [FILL — options]

Options:
    -h, --help          Show this help message
    -v, --verbose       Enable debug logging
    [FILL]              [FILL — option description]

Example:
    $0 [FILL]

EOF
}

# [FILL — Function 1]
[FILL]() {
    log_info "Starting [FILL]"
    
    # [FILL] Add function body
    
    log_info "Completed [FILL]"
}

# [FILL — Function 2]
[FILL]() {
    log_info "Starting [FILL]"
    
    # [FILL] Add function body
    
    log_info "Completed [FILL]"
}

################################################################################
# Main
################################################################################

main() {
    log_info "Starting script: $(basename "$0")"
    
    # [FILL] Add main logic
    
    log_info "Script completed successfully"
}

# Parse arguments
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            usage
            exit 0
            ;;
        -v|--verbose)
            LOG_LEVEL="DEBUG"
            shift
            ;;
        [FILL])
            [FILL]="$2"
            shift 2
            ;;
        *)
            log_error "Unknown option: $1"
            usage
            exit 1
            ;;
    esac
done

# Run main function
main "$@"
```

## Documentation

**Purpose:** [FILL]

**When to use:** [FILL]

**Dependencies:** [FILL]

**Environment Variables:**
- `[FILL]` — [Description]
- `[FILL]` — [Description]

**Exit Codes:**
- `0` — Success
- `1` — General error
- `2` — Misuse of shell command

## Testing Checklist

- [ ] Script runs without errors
- [ ] Help message displays correctly
- [ ] All functions work as expected
- [ ] Error handling works properly
- [ ] Logging captures expected output
- [ ] Script handles edge cases
- [ ] Documentation is accurate

## Notes

[FILL]
