# Security

## Privilege boundary

The QML plugin runs with normal user permissions. Telemetry is read from sysfs,
and no privileged background helper or passwordless policy is installed.

Saving a fan curve launches the repository's `t2fan-control` helper through
`pkexec`. PolicyKit therefore asks the user to authenticate each change. The
helper validates every argument before writing, backs up `/etc/t2fand.conf`,
uses an atomic temporary file with root ownership and mode 0644, and restores
the previous configuration if `t2fanrd` cannot restart.

Because plugins execute unsandboxed and their source is user-writable, users
should review updates before installing them, as recommended by Omarchy.

## Reporting a vulnerability

Please use GitHub's private vulnerability reporting for this repository rather
than opening a public issue for exploitable behavior.
