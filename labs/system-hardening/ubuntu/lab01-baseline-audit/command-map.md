# Lab 01 - Baseline System Audit
# All commands executed during assessment

##Command 1: Identify current user

Purpose:
To determine the active user context and privilege level.

Command:

whoami


Output (summary):
ezinna

Observation:
Confirms the session is running under a non-root user account.

##Command 2: Check sudo privileges

Purpose:
To verify whether the current user has administrative privileges.

Command:

sudo -l


Output (summary):
User ezinna may run all commands.

Observation:
The user has full sudo privileges, meaning compromise of this account results in full system control.

##Command 3: Enumerate local users

Purpose:
To identify system and human user accounts.

Command:

cut -d: -f1 /etc/passwd


Output (summary):
List of system accounts and user account ezinna.

Observation:
Only one human user account identified. Reduces internal attack surface.

##Command 4: Check password policy

Purpose:
To inspect password aging and expiration policy.

Command:

sudo chage -l ezinna


Output (summary):
Password expires: never

Observation:
Passwords do not expire, increasing long-term credential exposure risk.

##Command 5: Identify active network interfaces

Purpose:
To determine network connectivity and IP assignment.

Command:

ip a


Output (summary):
eth0 assigned 172.24.250.47

Observation:
System is network-connected and reachable within a private network.

##Command 6: Enumerate listening services

Purpose:
To identify open ports and exposed services.

Command:

ss -tulnp


Output (summary):
SSH on 0.0.0.0:22, MySQL 127.0.0.1:3306, PostgreSQL 127.0.0.1:5432

Observation:
SSH is remotely accessible. Databases are locally bound.

##Command 7: Confirm host IP

Purpose:
To verify system network identity.

Command:

hostname -I


Output (summary):
172.24.250.47

Observation:
Confirms internal network placement.

##Command 8: Check firewall status

Purpose:
To determine host firewall posture.

Command:

sudo ufw status verbose


Output (summary):
Firewall active. Default deny incoming. SSH allowed.

Observation:
Firewall is enabled but SSH remains exposed.

##Command 9: Inspect kernel firewall enforcement

Purpose:
To verify firewall is enforced at iptables level.

Command:

sudo iptables -L -n -v


Output (summary):
INPUT chain default DROP, UFW chains active.

Observation:
Firewall policies are actively enforced.

##Command 10: Check update status

Purpose:
To assess patch exposure.

Command:

apt list --upgradable


Output (summary):
Listing. . . Done

Observation:
No pending updates.

- Analyst Note

All commands were executed from a local Ubuntu terminal under a sudo-capable user account as part of a baseline security audit.
