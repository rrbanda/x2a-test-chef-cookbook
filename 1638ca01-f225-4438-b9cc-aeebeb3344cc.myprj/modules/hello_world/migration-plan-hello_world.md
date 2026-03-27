# Migration Plan: hello_world

**TLDR**: The Chef cookbook `hello_world` is empty and appears to be a placeholder or non-existent. It does not contain any recipes, templates, or attributes. Consequently, it performs no actions, installs no software, and configures no services. The Ansible equivalent would be an empty role with no tasks.

## Service Type and Instances

**Service Type**: Other

**Configured Instances**:
- There are no configured instances. The cookbook is empty and does not define any resources, attributes, or configurations.

## File Structure

**MANDATORY: Preserve this section from the original plan.**

```
(No recipe files found)
(No provider files found)
(No template files found)
(No attribute files found)
```

## Module Explanation

The cookbook is empty and performs no operations. The analysis did not find an entry point recipe (`recipes/default.rb`) or any other executable files. Therefore, there are no steps to document.

## Dependencies

**External cookbook dependencies**: None
**System package dependencies**: None
**Service dependencies**: None

## Checks for the Migration

**Files to verify**:
*   None, as no files are created or modified.

**Service endpoints to check**:
*   None, as no services are installed or configured.

**Templates rendered**:
*   None.

## Pre-flight checks:
```bash
# Verify no unexpected services are running
systemctl list-units --type=service --state=running

# Verify there are no unexpected open ports
ss -tulpn

# Confirm no files related to a "hello_world" application exist
find /etc /opt /var -name "hello_world*"
```