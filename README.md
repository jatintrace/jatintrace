# Hi, I'm Jatin Gupta

**Aspiring SOC Analyst · Hands-on Security Labs · Python Security Tools**

I'm working toward an entry-level Security Operations Center role.
I learn by building controlled labs, investigating security events,
and developing tools that support evidence-based analysis.

My focus is understanding what the evidence shows, how detections work,
and where their limitations are.

## Featured Projects

### [SOC Lab](https://github.com/jatintrace/soc-lab)
A hands-on security operations lab using Wazuh, Sysmon, Ubuntu Server,
and Windows Server.

- Documented detection scenarios and investigation reports
- Windows and Linux security-event analysis
- Detection-gap investigation and troubleshooting

### [TriageAI](https://github.com/jatintrace/triageai)
An offline-first, human-in-the-loop SOC triage assistant built in Python.

- Deterministic event processing, correlation, and detection rules
- Evidence-based timelines and analyst reports
- Redaction and validation boundaries for mock-AI explanations

**Scope:** A portfolio and learning release using sanitized or synthetic
events. The current AI provider is a deterministic mock, not a connected
language model. It is not a production SIEM or autonomous-response tool.

### [SecureGuard](https://github.com/jatintrace/secureguard)
A local static-analysis CLI for identifying possible security issues
in Python and PHP source code.

- Checks for possible hardcoded credentials, unsafe SQL construction,
  and unsafe command execution
- Terminal, JSON, HTML, and SARIF reporting
- Baseline comparison and inline suppressions

**Scope:** Findings identify patterns for human review, not confirmed
vulnerabilities. Scanned code is not executed.

### [ProofSentinel](https://github.com/jatintrace/proofsentinel)
An early-development security testing and evidence harness for
authorized local Python projects.

- Focused on deterministic checks and reviewable evidence
- Designed around explicit safety boundaries and documented limitations
- Developed incrementally with tests and development tooling

**Status:** In development. Planned capabilities are not claims of
currently working features. The harness is not a sandbox.

## Additional Projects

| Project | Focus |
| --- | --- |
| [SOC-IQ](https://github.com/jatintrace/SOC-IQ) | A desktop investigation tool for report analysis, IOC extraction, threat-intelligence enrichment, and reporting. |
| [Portfolio](https://github.com/jatintrace/Portfolio) | Source code for my personal cybersecurity portfolio website. |

## Tools & Technologies

Technologies used across my labs and projects—not a claim of mastery:

- **Security monitoring:** Wazuh, Sysmon
- **Systems:** Ubuntu Server, Windows Server, VirtualBox
- **Development:** Python, Git, GitHub
- **Testing & code quality:** pytest, Ruff, mypy, GitHub Actions

## Current Learning Focus

- Networking fundamentals and Linux administration
- Windows security events and endpoint telemetry
- Alert triage and incident investigation
- Detection logic and MITRE ATT&CK mapping
- Secure Python development and automated testing
- Clear documentation and evidence handling

## How I Work

- **Authorized environments:** Keep testing within controlled,
  explicitly authorized scope.
- **Evidence before conclusions:** Separate observed facts from
  assumptions and investigation questions.
- **Honest limitations:** Document false positives, detection gaps,
  and unsupported capabilities.
- **Reproducible work:** Include setup instructions, sample inputs,
  and verification steps where available.
- **Human judgment:** Treat tools as support for an analyst,
  not a replacement for one.

---

These repositories document my learning and portfolio work.
They are not claims of professional SOC experience, security
certification, or production readiness.
