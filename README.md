# oracle-rman

A collection of Oracle RMAN operational documentation covering archive log maintenance and point-in-time database recovery procedures, across Oracle Database versions 11g, 12c, and 19c, on both Microsoft Windows and Oracle Linux.

> **Note:** All host names, SIDs, paths, dates, and credentials shown in these documents are placeholders. Replace them with your actual environment values before use.

---

## Contents

### Archive Log Maintenance

Automated procedures to synchronize RMAN archive log metadata with physical files on disk, clean up expired metadata, and remove archive log files older than a configurable retention period.

| Document | Database | Platform |
|---|---|---|
| [oracle-11g-maintenance-archivelog-script-windows.md](oracle-11g-maintenance-archivelog-script-windows.md) | Oracle 11g | Microsoft Windows |
| [oracle-11g-maintenance-archivelog-script-ol6.md](oracle-11g-maintenance-archivelog-script-ol6.md) | Oracle 11g | Oracle Linux 6 |
| [oracle-12c-maintenance-archivelog-script-windows.md](oracle-12c-maintenance-archivelog-script-windows.md) | Oracle 12c (CDB) | Microsoft Windows |
| [oracle-12c-maintenance-archivelog-script-ol7.md](oracle-12c-maintenance-archivelog-script-ol7.md) | Oracle 12c (CDB) | Oracle Linux 7 |
| [oracle-19c-maintenance-archivelog-script-windows.md](oracle-19c-maintenance-archivelog-script-windows.md) | Oracle 19c (CDB) | Microsoft Windows |
| [oracle-19c-maintenance-archivelog-script-ol8.md](oracle-19c-maintenance-archivelog-script-ol8.md) | Oracle 19c (CDB) | Oracle Linux 8 |

### Recovery Database Before Crash

Step-by-step incomplete (point-in-time) recovery procedures to restore a database to the moment just before a crash or user error (e.g., accidental `DROP TABLE` / `DELETE`), using a pre-incident backup/snapshot plus archive logs.

| Document | Database | Platform |
|---|---|---|
| [oracle-11g-recovery-database-before-crash-windows.md](oracle-11g-recovery-database-before-crash-windows.md) | Oracle 11g | Microsoft Windows |
| [oracle-11g-recovery-database-before-crash-ol6.md](oracle-11g-recovery-database-before-crash-ol6.md) | Oracle 11g | Oracle Linux 6 |
| [oracle-12c-recovery-database-before-crash-windows.md](oracle-12c-recovery-database-before-crash-windows.md) | Oracle 12c (CDB) | Microsoft Windows |
| [oracle-12c-recovery-database-before-crash-ol7.md](oracle-12c-recovery-database-before-crash-ol7.md) | Oracle 12c (CDB) | Oracle Linux 7 |
| [oracle-19c-recovery-database-before-crash-windows.md](oracle-19c-recovery-database-before-crash-windows.md) | Oracle 19c (CDB) | Microsoft Windows |
| [oracle-19c-recovery-database-before-crash-ol8.md](oracle-19c-recovery-database-before-crash-ol8.md) | Oracle 19c (CDB) | Oracle Linux 8 |

---

## Version-Specific Differences

These documents are not identical copies across versions — each reflects real differences in Oracle's architecture and tooling conventions:

- **11g** — single-instance (non-CDB) architecture. Windows procedures use SQL*Plus with manual archive log prompts (`RECOVER DATABASE UNTIL CANCEL`); Linux procedures use a minimal RMAN environment setup with no explicit `rman` binary check.
- **12c / 19c** — multitenant (CDB/PDB) architecture. Recovery and maintenance operations run against the CDB root (`CDB$ROOT`); after `ALTER DATABASE OPEN RESETLOGS`, the affected pluggable database must be opened explicitly with `ALTER PLUGGABLE DATABASE ... OPEN`. Linux procedures use a fuller environment setup (`ORACLE_BASE`, `LD_LIBRARY_PATH`, `CLASSPATH`) and include an explicit `rman` executable check.
- **19c** — adds enhanced Fast Recovery Area (FRA) monitoring (space used/limit/reclaimable, archive log distribution by day) on top of the 12c procedures, for both maintenance and post-recovery verification.

---

## Disclaimer

All environment details (host names, SIDs, paths, dates, and credentials) in these documents are illustrative placeholders. Review and adapt every script and query to your own environment, and test in a non-production environment before applying any destructive operation (archive log deletion, `RESETLOGS`, etc.).

---

*Author: Kusnandar R*
