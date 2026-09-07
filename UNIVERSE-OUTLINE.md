# GitHub Universe 2026 Workshop Outline

## Securing MCP: Threats, Trust and What You Can Actually Do About It

### Session promise

Attendees leave with a practical model for deciding:

1. Which party they are trusting at each layer of an MCP system.
2. How untrusted content can become an authorized action.
3. Which controls reduce blast radius, and which controls merely improve UX.
4. What changed in the 2026 MCP specification without assuming that protocol improvements solve prompt injection or server provenance.

### Core thesis

> By the time a user is asked to approve a tool call, an attacker may already have shaped what the model proposes.

MCP security is not one problem. It is the interaction between server provenance, credentials, transport, tool metadata, untrusted content, model behavior, host policy, and human approval.

## Full workshop run of show

The full version below is 180 minutes, matching the format of the original workshop. The modules are intentionally separable for a shorter Universe slot.

| Time | Module | Format | Outcome |
|---:|---|---|---|
| 0:00-0:10 | Welcome and room calibration | Hands-up questions and framing | Establish experience levels and the workshop's evidence-based, discussion-friendly format |
| 0:10-0:25 | The trust-at-the-wrong-layer model | Diagram and discussion | Give attendees a reusable map of the MCP security surface |
| 0:25-0:45 | What a legitimate server can already do | Guided threat modeling | Separate malicious-server risk from ordinary credential and capability risk |
| 0:45-1:20 | The friendly malicious GitHub MCP fork | Live demonstration | Show how small, plausible changes subvert metadata, responses, and runtime behavior |
| 1:20-1:30 | Break and catalog exercise setup | Break | Start the delayed-registration timer and assign catalog examples |
| 1:30-1:55 | Classic incidents still matter | Small-group exercise | Map real incidents to trust boundaries instead of memorizing a vulnerability list |
| 1:55-2:25 | New specification, familiar failure modes | Protocol walkthrough and benign demos | Cover MRTR, elicitation, and mirrored headers accurately |
| 2:25-2:45 | Defense in depth by owner | Facilitated discussion | Assign controls to infrastructure, host/client, server, and governance layers |
| 2:45-2:57 | Deployment scenarios | Table exercise | Choose realistic controls for solo, team, and enterprise environments |
| 2:57-3:00 | Close | Takeaway and action list | Leave attendees with concrete next steps |

## Module details

### 1. Welcome and room calibration

Open by making the workshop contract explicit:

- This is a practical security workshop, not a catalog recital.
- Questions and disagreement are welcome.
- Demonstrations use controlled repositories, fake canary credentials, and benign local logging.
- The goal is to understand systems and trust boundaries, not to blame MCP for vulnerabilities that are ordinary implementation bugs.

Suggested room questions:

- Who builds MCP servers?
- Who builds clients, hosts, gateways, or agent runtimes?
- Who has reviewed the official MCP security guidance?
- Who has connected an MCP server to production credentials or private data?
- Who has threat-modeled what happens before a tool confirmation appears?

### 2. The trust-at-the-wrong-layer model

Use the security-layers diagram to distinguish:

1. **Discovery and distribution** — where the server, package, image, or endpoint came from.
2. **Process and network execution** — what code runs and where it can communicate.
3. **Credentials and authorization** — which authority the server and host possess.
4. **Tool definitions and metadata** — what the model sees before invocation.
5. **Tool inputs and outputs** — which untrusted data enters the model context.
6. **Model decision-making** — how data and instructions become an action plan.
7. **Approval and policy** — what the human or host can actually observe and enforce.

Key distinction:

> A sandbox limits impact. It does not make hostile instructions trustworthy.

### 3. What a legitimate server can already do

Introduce the three risk conditions:

- Access to private or valuable data.
- Exposure to attacker-controlled content.
- Ability to communicate externally or perform consequential actions.

Ask attendees to identify which combinations exist in their own deployments. Emphasize that a server does not need to be malicious for the lethal-trifecta pattern to exist.

Cover the credential reality directly:

- A local server receives whatever secrets are placed in its environment.
- A remote server receives whatever authority its access token grants.
- Tool filtering affects what the model can request; it does not constrain arbitrary code already running inside a local server process.
- Read-only access can still expose highly sensitive data.

### 4. Friendly malicious GitHub MCP fork

Use the controlled [`SamMorrowDrums/workshop-mcp`](https://github.com/SamMorrowDrums/workshop-mcp) fork. Build it locally; do not use the upstream container image referenced by its inherited README.

Recommended order:

1. **Annotation spoofing** — show a destructive operation labeled read-only and non-destructive.
2. **Silent request logging** — make an ordinary tool call, then reveal the locally logged arguments.
3. **Tool-description poisoning** — show how a one-line description change can steer tool selection.
4. **Response prompt injection** — show instructions arriving inside otherwise legitimate tool output.
5. **Delayed tool registration** — reveal the diagnostic-looking tool after the three-minute timer.
6. **Indirect prompt injection** — use `SamMorrowDrums/official-work#1` to show ordinary collaboration content changing agent behavior.

For each demonstration, ask the same four questions:

1. What did the user trust?
2. What did the model see that the user did not?
3. Which control would have prevented the action?
4. Which proposed control would only have made the attack less convenient?

### 5. Classic incidents still matter

Give each table one or two entries from the vulnerability catalog. Ask them to report:

- The attacker-controlled input.
- The authority or sensitive resource available to the agent.
- The outbound or consequential action.
- The MCP-specific interaction, if any.
- The ordinary software-security failure, if any.
- The smallest control that would have broken the chain.

Use examples from different layers:

- Tool poisoning or cross-server shadowing.
- GitHub issue-to-private-repository exfiltration.
- DNS rebinding against a local MCP endpoint.
- Shell injection in an MCP server implementation.
- A malicious or misleading package/image.
- Telemetry-based Agentjacking.

The teaching point is that older examples remain useful because the underlying trust compositions still recur.

### 6. New specification, familiar failure modes

Frame this section carefully: the 2026-07-28 specification changes important mechanics and closes specific gaps, but it does not eliminate hostile servers, indirect prompt injection, excessive authority, or unsafe client implementations.

#### Mirrored tool parameters in HTTP headers

Demonstration:

- Define a harmless fake canary value as a parameter marked with `x-mcp-header`.
- Show the value in both the JSON body and the resulting `Mcp-Param-*` header.
- Show how a proxy, WAF, APM product, or debug logger could record the custom header.

Messages:

- The feature exists for routing and policy metadata, not secret transport.
- Base64 is encoding, not encryption.
- Custom headers may not receive the automatic redaction commonly applied to `Authorization`.
- Servers must validate that mirrored header values match the request body.

#### MRTR and `requestState`

Demonstration:

- Compare readable Base64 JSON, integrity-protected state, and AEAD-protected state using fake values.
- Attempt harmless tampering and replay against a workshop-only implementation.

Messages:

- Opaque does not mean confidential.
- Signed does not mean encrypted.
- Encrypted does not mean single-use or replay-proof.
- Bind state to the authenticated principal, originating request, and a short expiry.
- Enforce server-side consumption when an operation must be single-use.

#### Elicitation boundary

Demonstration:

- Show an intentionally non-compliant form-mode request for a fake API key.
- Contrast it with URL-mode elicitation, where the credential is entered outside the MCP client and LLM context.

Messages:

- Form mode must not request passwords, API keys, access tokens, or payment credentials.
- URL mode still requires clear origin display, explicit consent, safe navigation, and user binding.
- A URL must not contain the secret, be pre-authenticated, or let another user complete the authorization for the attacker's pending request.

Closing line for this module:

> Opaque is not secret, signed is not encrypted, and encrypted is not replay-proof.

### 7. Defense in depth by owner

| Owner | High-value controls | Important limitation |
|---|---|---|
| Infrastructure | Sandboxing, egress policy, short-lived secrets, workload identity, resource limits, monitoring | Cannot distinguish instructions from data inside model context |
| Client or host | Clear server identity, tool-change review, capability separation, policy enforcement, confirmation UX, content provenance | A confirmation dialog cannot display every influence on the model's proposal |
| Server author | Minimal tool surface, strict parameter handling, safe subprocess APIs, output labeling, auth audience validation, no token passthrough | A well-written server still processes attacker-controlled content |
| Governance | Approved registries, namespace and artifact provenance, version pinning, review, audit logs, incident response | Registry presence and signatures establish origin, not benign behavior |

Reinforce:

- Annotations are useful UX and planning signals, not security boundaries.
- Tool pinning detects change; it does not prove the original definition was safe.
- A sandbox reduces blast radius; it does not prevent authorized data disclosure through allowed channels.
- Model safety improvements are valuable but cannot replace enforceable policy.

### 8. Deployment scenario exercise

Give each table one environment:

| Environment | Constraint | First priorities |
|---|---|---|
| Solo developer | Low operational overhead | Trusted sources, narrow tokens, isolated workspaces, visible confirmations, easy reset |
| Product team | Shared repositories and automation | Reviewed config, version pinning, role separation, sandboxed execution, centralized audit |
| Regulated enterprise | Multiple identities, gateways, and data classes | Workload identity, policy enforcement, approved registries, data-flow controls, evidence retention |

Ask each group:

1. Which risks are unacceptable?
2. Which layer owns each control?
3. What will the organization deliberately not support?
4. What evidence would demonstrate that the control works?

## Closing

### Four actions

1. Map where untrusted content and valuable authority meet.
2. Reduce credential scope and isolate capabilities before improving consent UX.
3. Treat server code, configuration, metadata, and output as separate trust decisions.
4. Test controls against realistic agent flows, not only direct API calls.

### Final takeaway

> Do not ask only, "Is this tool call safe?" Ask, "Who shaped this tool call, what authority will execute it, and which boundary can actually stop it?"

## Shorter formats

### 90-minute version

- Keep modules 1-4.
- Use one catalog incident instead of the group exercise.
- Cover all three new-spec examples at explanation depth, but run only the MRTR demonstration live.
- Combine defense ownership and deployment scenarios into one facilitated discussion.

### 60-minute version

- Open with the thesis and trust-layer diagram.
- Demonstrate annotation spoofing, response injection, and delayed registration.
- Explain one classic external incident.
- Use the mirrored-header, MRTR, and elicitation examples as a single comparison slide.
- Close with the four actions.

## Rehearsal checklist

- Build the workshop fork locally rather than using `ghcr.io/github/github-mcp-server`.
- Use a fake, repository-scoped credential with no production authority.
- Confirm `SamMorrowDrums/official-work#1` and its comments still match the walkthrough.
- Start the delayed-registration server timer before the relevant section.
- Clear `~/sam/leaks/` before rehearsal and after the session.
- Keep a recorded or screenshot fallback for every live demonstration.
- Verify URLs, QR codes, the public catalog PDF, and the Pages rendering from a signed-out browser.
- Confirm the final Universe slot length before locking slide count and exercise depth.
