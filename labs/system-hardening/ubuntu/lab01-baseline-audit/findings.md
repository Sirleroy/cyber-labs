# Baseline Findings — Ubuntu System

## 1. User and Privilege Review
Observations: 
- The system is being accessed using a standard user account (ezinna). This reduces risk of accidental system wide changes.
- The primary user is a member of the sudo group grabting full administrative privileges.
- Only one user is assinged administrative privileges despite the presence of multiple services and application accounts.
Potential risks:
- Security breach via the primary user account would result in a full system takeover.
- Service accounts increase attack surface and must be restricted.

## 2. Authentication and Access Control
Observations:
- Only one user (ezinna) has sudo privileges.
- No evidence of widespread privileges among service and application accounts.
- Password lifetime extremely long.
- SSH password authentication is enabled.
- SSH on default port.
Potential risks:
- Potential breach could be catastrophic due to infinite usage of passwords.

## 3. Running Services
Observations:
- SSH running
- MariaDB running.
- PostgreSQL running
- Multiple background daemons
Potential risks:
- Increase in attack surface due to multiple service running.
## 4. Network Exposure
Observations:
- The system is connected to a private network (172.24.250.47.)
- SSH is listening on all interfaces (0.0.0.0:22 and :: :22).
- MySQL and PostgresSQL are running and bound to localhost only.
- DNS resolver services are active.
Potential risks:
- SSH running on all interfaces makes it a primary remote attck surface.
- SSH credentials compromise would enable direct system access.
- Multiple active services increase overall attack surface and must be justified.

## 5. Firewall Status
Observations:
- UFW is enabled with a default deny policy for incoming traffic.
- The only allowed inbound service is SSH (22/tcp).
- iptables show a default drop policy for inbound traffic.
Potential risks:
- SSH exposure remains a crictical access point.
- Firewall rules may require tightening and monitoring improvements.

## Summary
This baseline audit showed that the system is actively networked with SSH sxposed as the primary external point.
While a host-based firewall is enables with a default deny posture, SSH password authentication, long password lifetime and
multiple services running increase the attack sureface. These findings are a basis for structured system hardening.
