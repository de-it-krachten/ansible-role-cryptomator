[![CI](https://github.com/de-it-krachten/ansible-role-cryptomator/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-cryptomator/actions?query=workflow%3ACI)


# ansible-role-cryptomator

Installs Cryptomator - Cloud Storage Encryption Utility<br>
https://cryptomator.org<br>
https://github.com/cryptomator/cryptomator<br>



## Dependencies

#### Roles
None

#### Collections
None

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- Red Hat Enterprise Linux 10<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- RockyLinux 10
- OracleLinux 8
- OracleLinux 9
- OracleLinux 10
- AlmaLinux 8
- AlmaLinux 9
- AlmaLinux 10
- SUSE Linux Enterprise 15<sup>1</sup>
- openSUSE Leap 15
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Debian 13 (Trixie)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS
- Fedora 41
- Fedora 42

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Github CLI - API
cryptomator_api: https://api.github.com/repos/cryptomator/cryptomator

# Github CLI - repo
cryptomator_repo: https://github.com/cryptomator/cryptomator

# Lookup table for architecture
cryptomator:
  architecture:
    x86_64: amd64
    i386: i386
    armv6l: arm
    armv7l: arm
    aarch64: arm64
  system:
    Linux: linux
    Darwin: darwin

# Construct filename based on the system & architecture
cryptomator_file: "cryptomator-{{ cryptomator_version | regex_replace('^v') }}-{{ ansible_architecture }}.AppImage"

cryptomator_version_command: >-
  {{ cryptomator_path }} --version | awk '/Cryptomator version/ {print $3}'

# Version of the CLI to install
cryptomator_version: latest

# Location/ownership/permissions of the binary
cryptomator_path: /usr/local/bin/cryptomator
cryptomator_owner: root
cryptomator_group: root
cryptomator_mode: '0755'
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'cryptomator' pre playbook
  ansible.builtin.import_playbook: converge-pre.yml
  when: molecule_converge_pre is undefined or molecule_converge_pre | bool
- name: sample playbook for role 'cryptomator'
  hosts: all
  become: 'yes'
  vars:
    cryptomator_version: 1.9.3
  tasks:
    - name: Include role 'cryptomator'
      ansible.builtin.include_role:
        name: cryptomator
</pre></code>
