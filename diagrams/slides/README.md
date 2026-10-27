# MCP Security Surface: slide-sized sections

These are static, **2:1 SVG companions** to the [original detailed chart](../mcp-security-layers.svg). The original is unchanged. Insert each SVG as a picture in your presentation; each has a **1600 x 800** canvas and remains sharp when scaled. Keep the aspect ratio locked and place the image above your existing slide footer. At full slide width on a 16:9 slide, the image occupies 800 of the equivalent 900 height units, leaving the bottom **100 units (about 11%)** free. Do not stretch it to fill the slide height.

Use the overview, then the six sections in the order below. Keep the detailed chart and your existing QR code as the reference or closing slide. There is no new animation or interactive tour.

The colours use the supplied Universe palette: **Green 1 `#5FED83`** for server/content concerns and the active section, **Purple 1 `#AE85FF`** for connection/host concerns, and **Orange 1 `#FFABA8`** for action/risk paths. Text uses white `#FFFFFF` and light grey `#B0BAC2`. The flat **`#101411`** background was sampled from the supplied deck screenshots, including the actual footer; this matches the slide background rather than the palette's separate pure-black swatch. Boxes use the same background to avoid mismatched dark panels. The overview has no "Detailed chart online" label or embedded link.

Arrows show only the relationship being discussed, not every protocol exchange. The overview rows are areas of concern, not literal containment boundaries.

## Overview

[00-overview.svg](00-overview.svg)

**On screen:** the six areas from the original chart, without the per-box threat lists.

**Speaker notes:**

The full chart is a mess, and that is kind of the point. But you do not need to read all of it at once. To understand MCP security, you need a mental model of the parts involved, how they interact, and the risks at each boundary. Most of these are familiar software security problems; some arise from putting a model into the loop. I am going to take these six areas one at a time.

## 1. Discovery and supply chain

[01-discovery-supply-chain.svg](01-discovery-supply-chain.svg)

**On screen:** manual installation, public and organisation registries, the server, and its dependencies.

**Speaker notes:**

Before a tool is called, we have already chosen software to run or an operator to connect to. That choice might come from a registry, an organisation allowlist, or a command copied from a web page. We are trusting the publisher, its dependencies, and its update path. A registry listing or an official-looking name is not proof of what the code does. For a local server, launching it already runs code on the machine.

## 2. Transport and auth

[02-transport-auth.svg](02-transport-auth.svg)

**On screen:** local stdio and remote HTTP as two alternative paths.

**Speaker notes:**

Local and remote connections have different security concerns. With stdio, the host starts or connects to a process; that process has operating-system permissions and may receive credentials through its environment. With HTTP, we need to identify the endpoint and handle authorization, tokens, and scopes correctly. These are alternatives, not steps in a sequence. If a gateway is present, it can only enforce policy on traffic that actually passes through it.

## 3. MCP servers

[03-mcp-servers.svg](03-mcp-servers.svg)

**On screen:** local and remote servers reaching files, processes, APIs, databases, and services.

**Speaker notes:**

An MCP server is still software executing with permissions. A small, innocent-looking tool can sit in front of broad filesystem access or a powerful service account. The examples here are not exclusive: a local server can call a remote API, and a remote server has a filesystem too. Input validation, isolation, least privilege, and authorization still matter. The protocol does not replace those controls.

## 4. Context flow

[04-context-flow.svg](04-context-flow.svg)

**On screen:** content moving towards the model; proposed calls and actual MCP calls moving back through the host.

**Speaker notes:**

The server sends more than tool results. Descriptions, prompts, and resources are also content surfaces. The host chooses which of that content reaches the model. In the other direction, the model proposes a call, and the host decides whether to send it. That distinction matters: server-supplied text can influence what the model proposes next. Tool definitions and returned content can also change after the initial connection.

## 5. Host and client

[05-host-client.svg](05-host-client.svg)

**On screen:** MCP clients, context assembly, and tool-use policy inside the host; the model outside that application boundary.

**Speaker notes:**

The host is the application coordinating this: an IDE, desktop application, or custom agent. It manages MCP clients, assembles context, and applies tool-use policy. Depending on the host, that can mean allowing, denying, or asking a user to approve an action. The model proposing a call is not the same as permission to execute it. The server must still authorize the operation; user approval and tool annotations do not replace that check. Model deployment varies; the boundary here distinguishes application responsibilities, not physical machines.

## 6. Multi-server composition

[06-multi-server-composition.svg](06-multi-server-composition.svg)

**On screen:** content from server A influencing an agent's use of server B.

**Speaker notes:**

Now connect the agent to more than one server. One server supplies text, while another supplies access or a capability. For example, text in an issue could influence the agent to send information through a messaging tool. The second server does not have to be compromised. The dashed arrow is a possible path, not a guaranteed outcome: host policy, permissions, and server authorization can still restrict the action. This is why looking at each server in isolation is not enough.

## Return to the detailed chart

Show the [original SVG](../mcp-security-layers.svg) with the QR code already in your deck. Its small text is reference material rather than something the audience needs to read from the back of the room.

**Speaker notes:**

Those are the layers. This is the full chart with the examples and risks filled back in. You do not need to read every box now; the linked version is there for that. As we go through the demonstrations, we can place each one back on this map.
