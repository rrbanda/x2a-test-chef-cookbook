# MIGRATION FROM CHEF TO ANSIBLE

This document outlines the migration plan for the `hello_world` Chef cookbook to a corresponding Ansible role. The repository contains a single, simple cookbook whose only purpose is to log a "Hello, World!" message. The migration is considered low-complexity and low-risk, with an estimated timeline of a few hours for a single engineer.

## Module Migration Plan

This repository contains a single Chef cookbook that requires migration.

### MODULE INVENTORY
- **hello_world**:
    - Description: Logs the static message "Hello, World!" to the Chef log output during a Chef client run.
    - Path: `/`
    - Technology: Chef
    - Key Features: Uses the built-in `log` resource.

### Infrastructure Files

- `metadata.rb`: Contains cookbook metadata like name, version, and description. This will be migrated to the `meta/main.yml` file in the new Ansible role.
- `recipes/default.rb`: The main recipe file containing the `log "Hello, World!"` resource. This logic will be migrated to `tasks/main.yml` using the `ansible.builtin.debug` module.
- `Vagrantfile`: Defines a Vagrant environment for testing the cookbook. This file can be modified to use the Ansible provisioner instead of the Chef provisioner to test the new role.
- `Gemfile` / `Gemfile.lock`: Ruby dependency management files. These are not needed for Ansible and can be replaced with a `requirements.txt` for any Python-based tooling if necessary.
- `chefignore`: Specifies files to be ignored by the Chef toolchain. This can be replaced with an `.ansible-ignore` file.
- `Thorfile`: A Ruby-based task runner. Any tasks within can be migrated to a `Makefile` or simple shell scripts.
- `LICENSE` / `README.md`: Standard project files that can be carried over to the new Ansible role repository.

### Target Details

- **Operating System**: The source cookbook does not specify a target OS, as the `log` resource is platform-agnostic. The new Ansible role will be developed to be OS-agnostic as well, but testing will default to Red Hat Enterprise Linux 9.
- **Virtual Machine Technology**: Vagrant is used for local testing, as specified in the `Vagrantfile`.
- **Cloud Platform**: Not specified.

## Migration Approach

### Key Dependencies to Address
The `metadata.rb` file does not declare any cookbook dependencies. Therefore, there are no external dependencies to address.

### Security Considerations
- **Secrets Management**: The cookbook does not handle any secrets, credentials, or sensitive data. No secrets management migration is required.
- **Security Practices**: The functionality is limited to logging a message and has no security impact.

### Technical Challenges
- **Functionality Mapping**: The primary task is to map the Chef `log` resource to its Ansible equivalent. The `ansible.builtin.debug` module provides the same functionality. This is a straightforward, one-to-one mapping.
- **Tooling**: The development environment will shift from Ruby-based tools (Bundler, Thor) to Python-based tools (pip, Ansible-lint). This is a minor change in local development setup.

### Migration Order
As there is only one simple component, the migration can be done in a single phase:
1.  **Initialize Ansible Role**: Create a new directory structure for the `hello_world` Ansible role using `ansible-galaxy init hello_world`.
2.  **Migrate Logic**: Translate the `log "Hello, World!"` resource from `recipes/default.rb` into a task in `tasks/main.yml` using the `ansible.builtin.debug` module.
3.  **Migrate Metadata**: Copy the relevant information from `metadata.rb` into the `meta/main.yml` file.
4.  **Update Test Environment**: Modify the `Vagrantfile` to use the `ansible` provisioner to apply the new role.
5.  **Cleanup**: Remove old Chef-specific files (`metadata.rb`, `recipes/`, `chefignore`, `Gemfile`, etc.).

### Assumptions
- The objective is to create an Ansible role with the exact same functionality as the Chef cookbook: logging a "Hello, World!" message.
- The existing `Vagrantfile` is the desired testing platform and should be updated for use with Ansible.
- No new functionality is required as part of this migration.
