# Securing MCP: Threats, Trust and What You Can Actually Do About It

Workshop materials, vulnerability catalog, and resource index for the MCP security talk at [MCP Dev Summit North America](https://mcpdevsummitna26.sched.com/) (April 1-3, 2026, New York).

This is a fast-moving area. The MCP specification itself is evolving, the security guidance in the spec is being actively developed, and new tooling appears regularly. This document collects what exists today so you can evaluate it yourself. None of these materials are exhaustive. The landscape changes weekly, and new tools, vulnerabilities, and mitigations appear faster than any single resource can track.

**Disclaimer:** Inclusion of any project, product, or link here is not an endorsement. This is a landscape index. Evaluate everything independently.

**Browse this content online:** [sammorrowdrums.github.io/mcp-security-workshop](https://sammorrowdrums.github.io/mcp-security-workshop/)

---

## Workshop Materials

- [WALKTHROUGH.md](WALKTHROUGH.md) - Practical demonstration of MCP server attack vectors: six attacks implemented in ~250 lines against a fork of `github/github-mcp-server`, all passing tests
- [mcp-vulnerability-catalog.md](mcp-vulnerability-catalog.md) - Catalog of documented MCP vulnerabilities (40+ entries across 10 categories including context-layer attacks, DNS rebinding, command injection, auth flaws, and supply chain)
- [diagrams/mcp-security-layers.svg](diagrams/mcp-security-layers.svg) - MCP security surface diagram showing trust boundaries from discovery through to the LLM context window

The walkthrough covers practical attack implementation. The vulnerability catalog covers the broader documented landscape. They are complementary: the walkthrough shows how easy it is to build attacks, the catalog shows the breadth of what has been found in the wild.

---

## MCP Dev Summit North America: Security Track

This workshop is part of [MCP Dev Summit NA 2026](https://mcpdevsummitna26.sched.com/) (April 1-3, New York). The conference has a dedicated Security and Operations track running across all three days. Several of the projects, companies, and researchers referenced in this resource index are presenting at the summit.

Notable: Obot AI is both a conference sponsor and presenter, with a keynote, a workshop on enterprise auth and governance, and talks on supply chain attacks and workflow engines.

### Security and Operations Track Talks

**April 1 (Workshops)**

| Time | Talk | Speaker |
|---|---|---|
| 1:00-4:00pm | Enabling MCP at Enterprise Scale: Navigating Authentication and Governance Challenges | Bill Maxwell and Shannon Williams, Obot AI |
| 1:00-4:00pm | Securing MCP: Threats, Trust and What You Can Actually Do About It | Sam Morrow, GitHub |

**April 2 (Thursday)**

| Time | Talk | Speaker |
|---|---|---|
| 11:50am | Securing MCP at Scale: From Principles To Production | Peter Smulovics, Morgan Stanley |
| 12:20pm | When MCP Becomes a Product | Gautam Baghel, HashiCorp and Roy Derks, IBM |
| 12:50pm | Golem To Murderbot: Challenges With Agentic Security Delegation Via MCP | Michael Schwartz, Gluu |
| 12:50pm | Who's Driving? Delegation and the Confused Deputy Problem for AI Agents | Vitor Balocco and Alvaro Inckot, Runlayer |
| 2:35pm | From Scopes To Intent: Reimagining Authorization for Autonomous Agents | Andres Aguiar and Abhishek Hingnikar, Okta |
| 3:05pm | Deploying MCP at Scale Without Skipping Compliance | Becky Brooks, MCP Manager by Usercentrics |
| 3:35pm | Shadow MCP: Finding the MCPs Nobody Approved | Tal Peretz and Alexander Frazer, Runlayer |
| 4:30pm | If You Can Secure It Here, You Can Secure It Anywhere | Milan Williams and Katrina Liu, Semgrep |
| 5:00pm | Towards Building Safe and Secure Agentic AI | Dawn Song, UC Berkeley and Matt White, Linux Foundation |
| 5:30pm | MCP Traffic Handling at Scale: Stateless Design, Proxies, and the Road Ahead | Erica Hughberg, Tetrate and Boteng Yao, Google |

**April 3 (Friday)**

| Time | Talk | Speaker |
|---|---|---|
| 11:30am | Demistifying Client ID Metadata Documents in MCP | Den Delimarsky, Anthropic |
| 12:00pm | Threat Modeling Authorization in MCP | Sarah Cecchetti, OpenID Foundation |
| 12:30pm | Mix-Up Attacks in MCP: Multi-Issuer Confusion and Mitigations | Emily Lauber, Microsoft |
| 2:25pm | Putting the Single Back in Single Sign-On: Cross-App Access for MCP | Paul Carleton, Anthropic and Max Gerber, Twilio |
| 2:55pm | The Boring Attack That Will Actually Get You | Craig Jellick, Obot AI |
| 3:25pm | Beyond the Sandbox: Security at the Host Layer | Lorenzo Verna and Pietro Valfre, Denied |
| 3:25pm | MCPwned: Hacking MCP Servers With One Skeleton Key Vulnerability | Jonathan Leitschuh, Independent |
| 4:20pm | From Chaos To Clarity: How MCP Transforms Incident Response | Sebastian Villanelo and Rocio Bayon, PagerDuty |
| 4:20pm | Securing the MCP Ecosystem: Production Patterns for Transparency and Trust | Lisa Tagliaferri and Trevor Dunlap, Chainguard |
| 4:50pm | Enterprise-Ready MCP: Security Patterns and the "4-Legged" Identity Challenge | Paulina Xu, Agentic Fabriq |
| 4:50pm | Kubernetes-Native Agent Discovery: A Unified Registry for MCP Servers and Skills | Carlos Santana, AWS |
| 5:20pm | Context Middleware for MCP: From Enterprise Needs To Protocol Extension | Peder Holdgaard Pedersen, Saxo Bank |
| 5:20pm | Hooks, Not Hacks: Modular Enforcement for MCP Agents | Fred Araujo and Ian Molloy, IBM |

### Other Security-Relevant Talks (Non-Security Track)

| Time | Talk | Speaker | Track |
|---|---|---|---|
| Apr 2 12:20pm | Evolution, Not Revolution: How MCP Is Reshaping OAuth | Aaron Parecki, Okta | Protocol |
| Apr 2 3:35pm | OCI Images as MCP Packaging: Supply Chain Security for AI Tools | Juan Antonio Osorio, Stacklok | Best Practices |
| Apr 2 4:30pm | Safer AI Integration Using Mock MCP Servers for Your 3rd-Party APIs | Kin Lane, Naftiko | Best Practices |
| Apr 3 12:30pm | The Anatomy of a Meltdown: A Deep-Dive into MCP via Selective Sabotage | Joey Stout, Spacelift | Protocol |
| Apr 3 2:55pm | The MCP Gateway Pattern: Aggregation, Composition, and Beyond | Juan Antonio Osorio, Stacklok | Best Practices |
| Apr 3 5:20pm | MCP Elicitation: Balancing Convenience With Security | Kay James, Gravitee | Protocol |

---

## MCP Specification and Official Security Resources

The protocol has gone through three major stable revisions in 2025, each adding security surface:

- [Model Context Protocol Specification](https://spec.modelcontextprotocol.io/) - The current spec
- [MCP Security Best Practices](https://modelcontextprotocol.io/specification/2025-11-25/security) - Official security guidance (added 2025-06-18, updated 2025-11-25)
- [MCP Authorization Specification](https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization) - OAuth 2.1 framework for MCP
- [MCP Roadmap](https://modelcontextprotocol.io/roadmap) - Security and Authorization listed as "On the Horizon" work
- [MCP Working Groups](https://modelcontextprotocol.io/community/working-interest-groups) - See below for details
- [MCP Changelog: 2025-03-26](https://modelcontextprotocol.io/specification/2025-03-26) - OAuth framework, Streamable HTTP, tool annotations
- [MCP Changelog: 2025-06-18](https://modelcontextprotocol.io/specification/2025-06-18) - Protected Resource Metadata, Resource Indicators, security best practices page
- [MCP Changelog: 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25) - OIDC discovery, incremental scope consent, Origin validation, governance

### MCP Working Groups and Interest Groups

There are many planned improvements in the pipeline. The security posture of MCP should continue to change for the better as these groups produce output.

**Interest Groups** (research and discussion):

- Security in MCP
- Auth in MCP

**Working Groups** (producing spec changes):

- Server Identity
- Tool Filtering
- Registry
- Inspector

**Auth Working Groups** (focused on specific auth improvements):

- Client Registration
- Fine-Grained Authorization
- Improve Developer Experience
- Mix-Up Protection
- Profiles
- Tool Scopes

The Auth working groups are particularly relevant. Fine-grained authorization and tool scopes would allow more precise control over what each server and tool can access. Mix-up protection addresses the OAuth multi-issuer confusion attacks documented in RFC 9207. These are active efforts, not aspirational.

### Related Standards

- [RFC 9700 - OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/html/rfc9700) (Jan 2025)
- [RFC 9728 - OAuth Protected Resource Metadata](https://datatracker.ietf.org/doc/html/rfc9728) (Apr 2025)
- [RFC 8707 - Resource Indicators for OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc8707)
- [RFC 9207 - OAuth Authorization Server Issuer Identification](https://datatracker.ietf.org/doc/html/rfc9207) - Mix-up attack countermeasure
- [OWASP MCP Top 10](https://owasp.org/www-project-mcp-top-10/) - OWASP's MCP-specific risk catalog

---

## Vulnerability Research and Catalogs

See also the [vulnerability catalog](mcp-vulnerability-catalog.md) in this repository for detailed entries with MCP-specific enablers and mitigation analysis.

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

The [vulnerability catalog](mcp-vulnerability-catalog.md) documents several MCP supply chain incidents:

- **postmark-mcp** (Sep 2025): First confirmed malicious MCP package in the wild. Published to npm, appeared benign at install, then changed tool descriptions to inject prompt injection
- **Phantom Repos**: Wiz documented ~100 registry entries pointing to nonexistent GitHub repositories (Apr 2025)
- **Docker MCP Hub Trust Misattribution**: "Verified" and "official" labels on container registries do not necessarily prove author affiliation
- **Registry Hijacking Study**: Academic study of 67,000+ MCP servers cataloging systemic registry trust issues
- **53% of 5,000+ Servers**: Study finding that over half of sampled MCP servers used hardcoded secrets in their configurations

These are the same classes of problems that package ecosystems have faced for years (typosquatting, account takeover, dependency confusion, abandoned package hijacking), now appearing in agent and MCP server registries.

### GitHub Security Features

GitHub provides a set of security features that compose together to address supply chain risks. These are free for all public repositories:

- [Dependabot](https://docs.github.com/en/code-security/dependabot) - Automated dependency updates and vulnerability alerts. Monitors dependencies for known CVEs and opens PRs to update them
- [Secret Scanning](https://docs.github.com/en/code-security/secret-scanning) - Detects tokens, keys, and credentials committed to repositories. Supports partner patterns to auto-revoke leaked secrets. GitHub's own MCP server uses secret scanning under the hood to prevent token exfiltration, because many users store tokens in plaintext alongside their MCP server configurations
- [Code Scanning](https://docs.github.com/en/code-security/code-scanning) - Static analysis (powered by CodeQL and third-party tools) that finds vulnerabilities in source code
- [Security Advisories](https://docs.github.com/en/code-security/security-advisories) - Private vulnerability reporting and coordinated disclosure for maintainers
- [GitHub Advisory Database](https://github.com/advisories) - Community-sourced vulnerability database covering npm, PyPI, Go, Rust, and more

These features work together: Dependabot pulls from the Advisory Database, secret scanning catches credentials that should never be in source, code scanning finds the bugs before they ship. For MCP server authors and consumers, this is baseline hygiene.

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

AI-driven offensive testing is now a practical reality. Autonomous reconnaissance, vulnerability identification, and exploit execution operate at a scale and speed that manual testing cannot match. The same capabilities inform the threat model for any agent-connected system.

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

If you know of relevant tools, research, or resources that should be listed here, open an issue or PR. The goal is a useful, current index of the MCP security landscape. This list is not exhaustive and will never be. Additions, corrections, and updates are welcome.
