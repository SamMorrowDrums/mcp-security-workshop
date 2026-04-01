# Securing MCP: Threats, Trust and What You Can Actually Do About It

Workshop materials, vulnerability catalog, and resource index for the MCP security talk.

This is a fast-moving area. The MCP specification itself is evolving, the security guidance in the spec is being actively developed, and new tooling appears regularly. This document collects what exists today so you can evaluate it yourself.

**Disclaimer:** Inclusion of any project, product, or link here is not an endorsement. This is a landscape index. Evaluate everything independently.

---

## Workshop Materials

- [WALKTHROUGH.md](WALKTHROUGH.md) - Practical demonstration of MCP server attack vectors, six attacks implemented in ~250 lines
- [mcp-vulnerability-catalog.md](mcp-vulnerability-catalog.md) - Comprehensive catalog of documented MCP vulnerabilities (40+ entries across 10 categories)
- [diagrams/mcp-security-layers.svg](diagrams/mcp-security-layers.svg) - MCP security surface diagram

---

## MCP Specification and Official Security Resources

The protocol has gone through three major stable revisions in 2025, each adding security surface:

- [Model Context Protocol Specification](https://spec.modelcontextprotocol.io/) - The current spec
- [MCP Security Best Practices](https://modelcontextprotocol.io/specification/2025-11-25/security) - Official security guidance (added 2025-06-18, updated 2025-11-25)
- [MCP Authorization Specification](https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization) - OAuth 2.1 framework for MCP
- [MCP Roadmap](https://modelcontextprotocol.io/roadmap) - Security and Authorization listed as "On the Horizon" work
- [MCP Working Groups](https://modelcontextprotocol.io/community/working-interest-groups) - Includes Security in MCP, Auth in MCP, Server Identity, Tool Filtering, and Registry groups
- [MCP Changelog: 2025-03-26](https://modelcontextprotocol.io/specification/2025-03-26) - OAuth framework, Streamable HTTP, tool annotations
- [MCP Changelog: 2025-06-18](https://modelcontextprotocol.io/specification/2025-06-18) - Protected Resource Metadata, Resource Indicators, security best practices page
- [MCP Changelog: 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25) - OIDC discovery, incremental scope consent, Origin validation, governance

### Related Standards

- [RFC 9700 - OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/html/rfc9700) (Jan 2025)
- [RFC 9728 - OAuth Protected Resource Metadata](https://datatracker.ietf.org/doc/html/rfc9728) (Apr 2025)
- [RFC 8707 - Resource Indicators for OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc8707)
- [RFC 9207 - OAuth Authorization Server Issuer Identification](https://datatracker.ietf.org/doc/html/rfc9207) - Mix-up attack countermeasure
- [OWASP MCP Top 10](https://owasp.org/www-project-mcp-top-10/) - OWASP's MCP-specific risk catalog

---

## Vulnerability Research and Catalogs

### Vulnerability Databases

- [Vulnerable MCP Project](https://vulnerablemcp.info/) - Tracking 50 MCP vulnerabilities from 32 researchers. Organized by severity, category, and timeline. Maintained by [Vineeth Sai](https://vineethsai.com)
- [mcpsec.dev](https://mcpsec.dev/) - MCP security advisories

### Key Research

- [Invariant Labs - Tool Poisoning Attacks](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks) - Hidden instructions in tool descriptions exfiltrating SSH keys and config files (Apr 2025)
- [Invariant Labs - WhatsApp MCP Exploit](https://invariantlabs.ai/blog/whatsapp-mcp-exploited) - Cross-server shadowing: a malicious server steering a trusted WhatsApp server to exfiltrate chat history (Apr 2025)
- [Invariant Labs - GitHub MCP Vulnerability](https://invariantlabs.ai/blog/mcp-github-vulnerability) - Private repository data exfiltration via public issue prompt injection (May 2025)
- [Trail of Bits - Line Jumping](https://blog.trailofbits.com/2025/04/21/jumping-the-line-how-mcp-servers-can-attack-you-before-you-ever-use-them/) - Attacks that happen before a tool is ever invoked (Apr 2025)
- [Trail of Bits - ANSI Terminal Code Deception](https://blog.trailofbits.com/2025/04/29/deceiving-users-with-ansi-terminal-codes-in-mcp/) - Invisible instructions via terminal escape sequences (Apr 2025)
- [Trail of Bits - Insecure Credential Storage](https://blog.trailofbits.com/2025/04/30/) - Plaintext credential handling across MCP environments (Apr 2025)
- [CyberArk - Universal Output Poisoning](https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe) - Prompt injection through every MCP output channel (Jul 2025)
- [HiddenLayer - Tool Parameter Abuse](https://hiddenlayer.com/innovation-hub/exploiting-mcp-tool-parameters/) - Exfiltrating system prompts and context via parameter naming (May 2025)
- [Lakera AI - Zero-Click RCE via Google Docs MCP](https://www.lakera.ai/blog/zero-click-remote-code-execution-exploiting-mcp-agentic-ides) - Hidden prompt injection in shared documents chains through to code execution (Sep 2025)
- [Palo Alto Unit 42 - MCP Sampling Exploitation](https://unit42.paloaltonetworks.com/model-context-protocol-attack-vectors/) - Three attack classes exploiting bidirectional sampling (Dec 2025)
- [Snyk Labs - Cursor + Jira Zero-Click](https://labs.snyk.io/resources/cursor-jira-mcp-vulnerability-explained/) - Credential exfiltration via malicious Jira ticket content (Aug 2025)
- [Simon Willison - MCP Prompt Injection Analysis](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/) - "Mixing tools with untrusted instructions is inherently dangerous"

### Industry Assessments

- [Rapid7 - MCP Security Fundamentals](https://www.rapid7.com/) - Measured exposure analysis: "The schema is the enforcement point" (Feb 2026)
- [Wiz - MCP Security Research Briefing](https://www.wiz.io/) - Early ecosystem analysis including registry risk, ~3,500 listed servers, ~100 pointing to nonexistent repos (Apr 2025)
- [Microsoft - Indirect Prompt Injection in MCP](https://devblogs.microsoft.com/) - Framing MCP risks as AI-era supply chain security (Apr 2025)
- [Aaron Parecki - OAuth for MCP](https://aaronparecki.com/) - "Let's not overthink auth in MCP" - influenced the 2025-06-18 spec changes (Apr 2025)
- [Acuvity - Cross-Server Tool Shadowing](https://acuvity.ai/cross-server-tool-shadowing-hijacking-calls-between-servers/) - Detailed analysis of cross-server attack mechanics
- [Acuvity - Rug Pulls](https://acuvity.ai/rug-pulls-silent-redefinition-when-tools-turn-malicious-over-time/) - Silent tool redefinition after user trust is established
- [Adversa AI - Top 25 MCP Vulnerabilities](https://adversa.ai/) - Ranked vulnerability index

---

## MCP Security Scanners and Analysis Tools

Tools for scanning MCP server configurations, tool definitions, and agent setups for known risks.

| Project | Description | Link |
|---|---|---|
| **Snyk Agent Scan** (formerly Invariant Labs mcp-scan) | Scans agent configs across Claude, Cursor, VS Code, Windsurf, Gemini CLI, and more. Detects prompt injection, tool poisoning, tool shadowing, toxic flows, hardcoded secrets | [github.com/snyk/agent-scan](https://github.com/snyk/agent-scan) |
| **Cisco AI Defense MCP Scanner** | Scans MCP servers for security threats. Python-based | [github.com/cisco-ai-defense/mcp-scanner](https://github.com/cisco-ai-defense/mcp-scanner) |
| **Trail of Bits mcp-context-protector** | Security proxy between client and MCP servers. TOFU pinning of tool definitions, guardrail scanning, ANSI sanitization, quarantine for suspicious responses | [github.com/trailofbits/mcp-context-protector](https://github.com/trailofbits/mcp-context-protector) |
| **MCPSafetyScanner** | Safety scanning for MCP server configurations | [vulnerablemcp.info](https://vulnerablemcp.info/) (referenced in catalog) |

---

## Runtime Protection and Sandboxing

Running AI agents with unrestricted access to your machine is running arbitrary code on your machine. These projects provide isolation at different levels.

| Project | Description | Platform | Link |
|---|---|---|---|
| **NVIDIA OpenShell** | Sandboxed execution environments for AI agents. Declarative YAML policies control filesystem, network, process, and inference access. Runs agents (Claude Code, Codex, Copilot, OpenCode) inside policy-enforced containers. L7 proxy enforces HTTP method and path-level egress rules | Linux (Docker/K8s) | [github.com/NVIDIA/OpenShell](https://github.com/NVIDIA/OpenShell) |
| **SandVault** | Lightweight sandbox using macOS user account isolation and sandbox-exec. No VM overhead. Designed for running Claude Code, Codex, and Gemini with their "skip permissions" flags in a limited user account | macOS | [github.com/webcoyote/sandvault](https://github.com/webcoyote/sandvault) |
| **jai** (Stanford SCS) | Casual sandbox for AI agents on Linux. Prefix any command with `jai` to get a copy-on-write overlay on your home directory. Working directory stays writable, home is protected. Three isolation modes (casual, strict, hidden). Not a hardened container - reduces blast radius for everyday use | Linux | [jai.scs.stanford.edu](https://jai.scs.stanford.edu/) |
| **ToolHive** (Stacklok) | Enterprise platform for running MCP servers in isolated containers with secrets management, policy enforcement, OIDC/OAuth SSO, and audit logging. Includes a registry server, runtime, gateway, and portal | Linux (Docker/K8s) | [github.com/stacklok/toolhive](https://github.com/stacklok/toolhive) |

See also: Docker containers, Podman, bubblewrap, firejail, and VMs for general-purpose isolation.

---

## MCP Platforms and Gateways

Enterprise-oriented platforms for hosting, managing, and governing MCP servers across an organization.

| Project | Description | Link |
|---|---|---|
| **Obot** | Open-source MCP platform: hosting (Docker/K8s with OAuth 2.1), registry (curated catalog with shared credentials), gateway (access rules, logging, request filtering), and chat client. Self-hosted, MIT-licensed | [github.com/obot-platform/obot](https://github.com/obot-platform/obot) |
| **ToolHive** (Stacklok) | See Runtime Protection above. Also provides registry and gateway functionality | [github.com/stacklok/toolhive](https://github.com/stacklok/toolhive) |
| **Cloudflare Agents SDK** | Remote MCP client support with built-in OAuth, automatic tool namespacing, and third-party auth provider integration | [developers.cloudflare.com](https://developers.cloudflare.com/) |

---

## Agent Configuration and Supply Chain Management

As agent configurations (skills, prompts, instructions, MCP server references) proliferate, managing and securing them becomes a supply chain problem.

| Project | Description | Link |
|---|---|---|
| **Microsoft APM (Agent Package Manager)** | Open-source dependency manager for AI agent configuration. Declares skills, prompts, instructions, hooks, plugins, and MCP servers in `apm.yml`. Resolves transitive dependencies. Scans packages before deployment. Works across Copilot, Claude Code, Cursor, OpenCode, Codex. MIT-licensed | [microsoft.github.io/apm](https://microsoft.github.io/apm/) |
| **Tessl** | Package manager and registry for agent skills and context. Evaluates skills against structured benchmarks (measurable accuracy impact). Security scores powered by Snyk. Used by Cisco, HashiCorp/IBM | [tessl.io](https://tessl.io/) |

---

## Supply Chain Security: A Growing Challenge

Supply chain attacks against software ecosystems are not new, but the scale and speed are increasing. AI agent configurations, MCP server registries, and skill/plugin ecosystems introduce new supply chain surfaces that mirror problems seen in npm, PyPI, and container registries.

### The axios Incident (March 31, 2026)

The npm maintainer account for [axios](https://github.com/axios/axios) was hijacked. Malicious versions `1.14.1` and `0.30.4` were published with a hidden dependency (`plain-crypto-js`) that dropped a cross-platform Remote Access Trojan. The malicious versions were live for approximately three hours. Platform-specific payloads targeted macOS, Windows, and Linux. This was part of a broader campaign ("TeamPCP") that also targeted Trivy, Telnyx, and LiteLLM.

- [StepSecurity - axios compromised on npm](https://www.stepsecurity.io/blog/axios-compromised-on-npm-malicious-versions-drop-remote-access-trojan)
- [Socket.dev - axios npm package compromised](https://socket.dev/blog/axios-npm-package-compromised)
- [GitHub Issue: axios/axios#10604](https://github.com/axios/axios/issues/10604)

### MCP-Specific Supply Chain Risks

The vulnerability catalog documents several MCP supply chain incidents:

- **postmark-mcp** (Sep 2025): First confirmed malicious MCP package in the wild. Published to npm, appeared benign at install, then changed tool descriptions to inject prompt injection
- **Phantom Repos**: Wiz documented ~100 registry entries pointing to nonexistent GitHub repositories (Apr 2025)
- **Docker MCP Hub Trust Misattribution**: "Verified" and "official" labels on container registries do not necessarily prove author affiliation
- **Registry Hijacking Study**: Academic study of 67,000+ MCP servers cataloging systemic registry trust issues
- **53% of 5,000+ Servers**: Study finding that over half of sampled MCP servers used hardcoded secrets in their configurations

These are the same classes of problems that package ecosystems have faced for years (typosquatting, account takeover, dependency confusion, abandoned package hijacking), now appearing in agent and MCP server registries.

### Relevant Supply Chain Security Tools

- [Socket.dev](https://socket.dev/) - Package supply chain security (npm, PyPI, and others)
- [StepSecurity](https://www.stepsecurity.io/) - GitHub Actions and CI/CD supply chain hardening
- [Sigstore](https://www.sigstore.dev/) - Keyless code signing for open source
- [SLSA Framework](https://slsa.dev/) - Supply chain Levels for Software Artifacts

---

## AI-Powered Offensive Security

AI is increasingly used on the offensive side of security testing. This changes the economics of both attack and defense.

| Project | Description | Link |
|---|---|---|
| **XBOW** | Autonomous offensive security platform. Executes penetration tests at machine scale with exploit-validated findings (not theoretical risk). Validated on HackerOne finding real vulnerabilities in production applications. $120M Series C | [xbow.com](https://xbow.com/) |

XBOW is relevant context for this workshop because it demonstrates that AI-driven offensive testing is a practical reality, not a research concept. The same capabilities that make autonomous pentesting effective also inform the threat model for agent-connected systems: automated reconnaissance, vulnerability identification, and exploit execution are now available at scale.

---

## Data Protection and Cyber Resilience

As AI agents gain access to production data and infrastructure through MCP, the consequences of compromise extend beyond code execution into data integrity and recovery.

- [The AI-Native Data Protection Stack](https://solutionsreview.com/backup-disaster-recovery/the-ai-native-data-protection-stack-how-cyber-resilience-is-evolving-in-real-time/) - How cyber resilience is evolving with AI on both sides of the attack/defense equation (Solutions Review, Mar 2026)

---

## Further Reading

### Proposals and Extensions

- [ETDI - Enhanced Tool Definition Interface](https://arxiv.org/abs/2506.01333) - Proposed cryptographic signatures and immutable versioned tool definitions for MCP. PR #845 to official SDK was closed without merge (Jul 2025). Notable as evidence the ecosystem agrees on the problem but has not converged on a protocol-native solution

### Community and Standards

- [AGENTS.md](https://agents.md/) - Emerging standard for agent instructions in repositories
- [Agent Skills](https://agentskills.io/) - Specification for portable agent skills
- [MCP Community Working Groups](https://modelcontextprotocol.io/community/working-interest-groups) - Active groups on Security, Auth, Server Identity, Tool Filtering, Registry

---

## Contributing

If you know of relevant tools, research, or resources that should be listed here, open an issue or PR. The goal is a useful, current index of the MCP security landscape.
