# eSim Winter Internship 2026 - Task 4

## Objective
Identify and fix installation issues in eSim on Ubuntu 25.04.

## Issue 1: KiCad installation terminates the complete installer

File: Ubuntu/install-eSim-scripts/install-eSim-25.04.sh

Function: installKicad()

Original code:
    echo "KiCad 8.0 is already installed."
    exit 0

Problem:
The exit command terminates the entire installer when KiCad 8 is already installed. This prevents subsequent eSim installation functions from executing.

Fix:
Replaced exit 0 with return 0.

Corrected code:
    echo "KiCad 8.0 is already installed."
    return 0

Reason:
return 0 exits only the current function and allows the main installation process to continue.

## Validation
Command:
    bash -n Ubuntu/install-eSim-scripts/install-eSim-25.04.sh

Result: SYNTAX OK

A complete installation test after this modification has not yet been performed.

## Additional Issues Observed

1. Disk space:
A previous installation attempt encountered "No space left on device". Disk usage was approximately 96%.

2. KiCad library:
A previous attempt reported that library/kicadLibrary.tar.xz could not be opened. A later repository checkout contained a kicadLibrary directory. The exact cause remains unverified.

3. Working directory:
The installer uses pwd to determine eSim_Home and uses relative paths. Running it from an unexpected directory may cause path-related errors.

## Modified File
Ubuntu/install-eSim-scripts/install-eSim-25.04.sh

## Conclusion
One control-flow issue in the KiCad installation function was corrected. Bash syntax validation passed. Additional observations are documented for further investigation.
