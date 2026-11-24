# eSim Winter Internship 2026 - Task 4
## eSim Upgradation on Ubuntu 25.04

### 1. Objective

The objective was to identify installation and dependency-related problems encountered while installing eSim 2.5 on Ubuntu 25.04, investigate their causes, and fix the identified issues.

### 2. Environment and Technologies

- Operating System: Ubuntu 25.04
- Application: eSim 2.5
- Scripting Language: Bash
- Version Control: Git and GitHub
- Repository: FOSSEE/eSim (forked repository)
- Working Branch: installer

### 3. Installation Issues Identified and Fixed

#### Issue 1: Syntax Error in the Main Installer

File: Ubuntu/install-eSim.sh

Function: run_version_script()

Problem:
The function had an incorrect structure. A closing brace was missing, and unrelated configuration lines were placed inside the function. This caused a Bash syntax error.

Investigation and Fix:
1. Inspected the main installer script.
2. Examined the run_version_script() function.
3. Identified the missing function closure and misplaced configuration lines.
4. Corrected the function structure and moved the unrelated lines outside it.

Result:
The syntax issue was corrected.

#### Issue 2: KiCad Installation Terminates the Entire Installer

File: Ubuntu/install-eSim-scripts/install-eSim-25.04.sh

Function: installKicad()

Problem:
When KiCad 8.0 was already installed, the script executed exit 0. This terminated the entire installer instead of allowing the remaining eSim installation functions to execute.

Original code:

    echo "KiCad 8.0 is already installed."
    exit 0

Fix:
Replaced exit 0 with return 0.

Corrected code:

    echo "KiCad 8.0 is already installed."
    return 0

Result:
The function now returns successfully without terminating the complete installer, allowing the main installation process to continue.

### 4. Additional Issues Observed

#### Issue 3: Insufficient Disk Space

An earlier installation attempt encountered the error "No space left on device". Disk usage was approximately 96%.

Observation:
Insufficient disk space can interrupt package downloads, extraction, and installation.

Status:
Identified and documented. A separate fix was not implemented.

#### Issue 4: KiCad Library Archive Not Found

An earlier attempt reported that library/kicadLibrary.tar.xz could not be opened. A later repository checkout contained a kicadLibrary directory.

Observation:
There was a difference between the expected archive and the available repository contents.

Status:
Investigated and documented. The exact cause remains unverified.

#### Issue 5: Working Directory and Relative Paths

The installer uses pwd to determine eSim_Home and uses relative paths.

Observation:
Executing the installer from an unexpected working directory may cause path-related problems.

Status:
Identified and documented as a potential issue. A separate fix was not implemented.

### 5. Validation

Bash syntax validation was performed on both modified scripts.

Commands:

    bash -n Ubuntu/install-eSim.sh
    bash -n Ubuntu/install-eSim-scripts/install-eSim-25.04.sh

Both scripts passed Bash syntax validation.

A complete end-to-end installation test after the modifications was not performed.

### 6. Modified Files

1. Ubuntu/install-eSim.sh
   - Corrected the structure of run_version_script().

2. Ubuntu/install-eSim-scripts/install-eSim-25.04.sh
   - Replaced exit 0 with return 0 in installKicad().

### 7. Summary of Issues

| No. | Issue | Status |
|---|---|---|
| 1 | Syntax error in main installer | Fixed |
| 2 | KiCad function terminates entire installer | Fixed |
| 3 | Insufficient disk space | Observed |
| 4 | KiCad library archive not found | Unresolved |
| 5 | Working directory and relative paths | Observed |

### 8. Conclusion

During this task, two issues in the eSim installation scripts were corrected. The first involved the structure of the main installer function, while the second involved premature termination of the installer when KiCad was already installed.

Three additional installation-related problems or potential problems were documented for further investigation.

Both modified scripts passed Bash syntax validation. A complete installation test remains pending.

This task provided practical experience with Bash scripting, debugging, Linux installation processes, and Git-based version control.
