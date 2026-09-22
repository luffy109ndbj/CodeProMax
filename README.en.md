# Code ProMax

[Tiếng Việt](README.md) · [English](README.en.md)

Code ProMax is a proprietary desktop application that connects a local Codex workflow with ChatGPT Web while keeping the Codex task, project context, tool lifecycle, and local workspace on your computer.

> **Unofficial third-party software.** Code ProMax is not affiliated with, endorsed by, or sponsored by OpenAI.

## Demo

<p align="center">
  <img src="media/demo.gif" alt="Code ProMax demo" width="960">
</p>

## Main features

- **Chat Long — long-running work through ChatGPT Web.** Chat Long runs models through ChatGPT Web using the capabilities of the signed-in ChatGPT account instead of consuming **Native Work/Codex quota**. Models are exposed according to the account's real capabilities: for Plus accounts, the current code supports **GPT-5.6 Sol Instant, Medium, and High** Web routes; higher tiers such as Extra High/Pro appear only when that account is actually entitled to them. Because Chat Long travels through the browser/Web route, it can be slower than Native Work, but it is well suited to long tasks while preserving Work quota for cases where faster native execution matters more.
- **Chat Long can continue context and recover connections.** A Chat Long thread keeps a durable conversation across turns. When the backing conversation exhausts its context, the launcher can roll over/continue into a fresh Web chat and carry the task forward instead of forcing the user to restart manually. The runtime also contains reconnect/recovery paths for bridge/model interruptions. This is a long-running continuity mechanism, **not a promise of unlimited context or any fixed token ceiling**; effective limits still depend on the model, account, and OpenAI-side changes.
- **Native Work — faster native path using Work quota.** Work runs project tasks through the native Codex backend and uses the signed-in account's Work quota. Its model list comes directly from the account-gated native catalog, so available models may differ from Chat Long and can change with account entitlements. Work is the better fit when native responsiveness is the priority and consuming Work quota is acceptable.
- **Embedded ChatGPT sign-in** — authentication stays inside the launcher-owned browser profile.
- **Quick Chat** — a lighter standalone chat path for fast questions that do not need project access.
- **Project folder management** — projects can be moved to a new folder while preserving historical path aliases and previous threads.
- **Images and rich task context** — images and compiled Codex context can travel with the active task.
- **MCP / local tools** — supported configurations can connect ChatGPT back to the active local Codex tool harness.
- **Secure MCP Tunnel support** — Code ProMax can use OpenAI's Secure MCP Tunnel flow for private/local MCP connectivity where the account/workspace supports it.
- **Local diagnostics** — runtime health checks, logs, smoke tests, cancellation controls, and explicit errors when a required capability is unavailable.
- **Multiple model tiers** — the launcher exposes the ChatGPT model/mode choices actually available to the signed-in account.

The MCP tunnel portion uses OpenAI's documented Secure MCP Tunnel model, where the customer-run tunnel client keeps an outbound connection and the private MCP server does not need a public inbound port. See the official OpenAI `tunnel-client` documentation for the current platform requirements and availability.

## Installation

### Windows

1. When a production-signed build is available, open this repository's **Releases** page.
2. Download the latest production-signed Windows installer named similar to:

   ```text
   code-promax-<version>-win-x64.exe
   ```

3. Run the installer.
4. Start **Code ProMax**.
5. Sign in to ChatGPT inside the embedded browser using your own account.
6. Run the browser/runtime verification shown by the app.
7. Install/enable the Codex integration when prompted.
8. Restart Codex if the app asks you to, then select the ChatGPT Web model exposed by Code ProMax.

If Windows SmartScreen or another security product blocks an installer, verify that you downloaded it from this repository's official Releases page and check the published file/signature before continuing. Do not download builds from mirrors you do not trust.

## Basic usage

1. Open Code ProMax and confirm your ChatGPT session is signed in.
2. Open or select the project you want to work on.
3. Choose the workflow that matches the task:
   - **Quick Chat** for short questions without project access.
   - **Chat Long** for long-running tasks through ChatGPT Web without consuming Work/Codex quota, while still being subject to ChatGPT Web account limits.
   - **Work** for tasks through the native backend; often faster, but it consumes the account's Work quota.
4. Choose a model/mode that the current surface and your account are actually entitled to use.
5. Start the task from Codex normally. Code ProMax handles the browser/model bridge and streams the result back into the Codex task.

Your available models, limits, UI, and connector capabilities depend on the ChatGPT account/workspace you sign in with and may change when OpenAI changes its products.

## Recommended workflow: Chat Long + Work

Code ProMax is designed so **Chat Long and Work complement each other** instead of forcing one mode to handle every kind of task.

- **Use Chat Long for long-running planning and builds.** It is a strong fit when you want the AI to inspect a project, produce a plan, implement a large sequence of changes, or run multiple connected tasks over a long session without consuming Work/Codex quota. Persistent conversation, continuation, and recovery make Chat Long suitable for extended work.
- **Use Work for review, alignment, and detail passes.** After Chat Long completes most of an implementation, Work is well suited to reviewing changes, correcting small details, running a focused native task with higher responsiveness, or handling work where speed matters more than preserving Work quota.
- **Switch between them as the project phase changes.** A practical pattern is: let Chat Long analyze and build most of the work → use Work to review and refine the remaining details → return to Chat Long when another long implementation branch is needed.

### The same Harness is available in both modes

Chat Long and Work both execute through Code ProMax's **CodexChatHost Harness** machinery. Harness provides a structured lifecycle for larger tasks: the AI can produce a **Plan**, you approve it to **Build**, then **Continue** through subsequent tasks; when a recoverable step needs another attempt, Harness also has a **Retry** path instead of forcing the entire job to restart.

The difference is the **model route and quota**, not whether Harness exists: Chat Long uses the ChatGPT Web route while Work uses the native Codex route, but both retain plan/build/continue/retry behavior so longer work stays organized and resumable.

## Optional: MCP / local tool access

Both Chat Long and Work can use **MCP/local tools**. Work keeps user MCP configuration in the account's native profile; Chat Long synchronizes user MCP servers into its separate Web/bridge profile while preserving Code ProMax-managed workers. MCP is therefore not limited to Work: both modes can use project MCP servers according to the configuration and permissions you provide.

## Advanced features

- **Multiple accounts with fast switching.** You can add multiple accounts; each managed account has its own isolated browser partition and `CODEX_HOME`, then switch accounts directly from the launcher. This keeps ChatGPT/Work sessions separated instead of overwriting another account's profile.
- **AI Models / custom providers.** Code ProMax has a generic provider layer supporting three current protocols: `openai-responses`, `openai-chat`, and `anthropic-messages`. External providers/models can be configured when their endpoint is compatible with one of those protocols. For example, **9router can be used if the endpoint you configure is compatible with a protocol supported by Code ProMax**; there is no dedicated built-in 9router integration.
- **Agent Customization with `AGENTS.md` and Skills.** You can manage persistent `AGENTS.md` instructions at global or project scope, create/import skill packages, and reuse workflows on demand. Project resources use the standard `AGENTS.md` and `.agents/skills` locations, while global resources are synchronized into Code ProMax's isolated profiles so Chat Long, Work, and Harness can share them.
- **MCP for both Chat Long and Work.** User MCP servers can live in Work profiles and are synchronized into Chat Long. Code ProMax preserves its own managed MCP workers during synchronization, so the same project MCP/tool setup can be available from both surfaces rather than only from Work.

<p align="center">
  <img src="media/mcp-create-tunnel.gif" alt="Create a Secure MCP Tunnel" width="900">
</p>

<p align="center">
  <img src="media/mcp-connect-connector.gif" alt="Connect the MCP connector" width="900">
</p>

OpenAI documents Developer Mode / MCP apps and its Secure MCP Tunnel client separately. Those platform features, account eligibility, permissions, and UI can change independently of Code ProMax.

Useful official references:

- OpenAI Secure MCP Tunnel client: https://github.com/openai/tunnel-client
- ChatGPT Developer Mode and MCP apps: https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt

## Account risk and responsibility

Code ProMax interacts with ChatGPT through your own account. There is **no guarantee that using any third-party automation or integration is risk-free for an account**.

The developer's own experience is that Code ProMax has been used for months, on multiple computers, with ChatGPT Plus accounts without those accounts being disabled as a result of that testing. **That is only an anecdotal experience, not a guarantee that the same outcome will apply to every user, account, usage pattern, region, workspace, or future OpenAI policy.**

A ChatGPT account can encounter restrictions, verification requests, temporary limitations, suspension, or other problems for many different reasons. Depending on the situation, those reasons may relate to account security, billing, policy enforcement, unusual activity, usage patterns, workspace rules, product changes, or other factors. If an account issue happens while Code ProMax is installed, that timing alone does not prove that Code ProMax caused it.

Parts of Code ProMax integrate with capabilities documented by OpenAI, including MCP-related functionality and Secure MCP Tunnel where available. However, the ChatGPT Web bridge itself is an **unofficial third-party integration** and is not an OpenAI-supported guarantee of account safety or continued compatibility.

By using Code ProMax, you are responsible for:

- complying with the OpenAI terms, policies, and workspace rules that apply to your account;
- choosing how aggressively and how frequently you automate tasks;
- reviewing tool permissions before allowing local write/modify actions;
- protecting your own ChatGPT account and credentials;
- keeping backups of important project files before allowing automated code changes; and
- deciding whether the operational/account risk is acceptable for your use case.

**Code ProMax and its developer are not responsible for suspension, restriction, loss of access, rate limits, account review, billing issues, or other ChatGPT account problems where the cause may depend on OpenAI systems, user behavior, account state, policy enforcement, or other circumstances outside the application's control.** Nothing in this notice overrides rights or liabilities that cannot legally be excluded.

## Privacy and security notes

- ChatGPT prompts are still processed by OpenAI; Code ProMax is not local AI inference.
- Do not treat Temporary Chat or an embedded browser session as anonymity.
- Keep your operating system and Code ProMax installation updated.
- Install only builds from the official repository/release source you trust.
- Review MCP/tool permissions carefully before enabling write or modify actions.
- The application should never require you to publish private project source code to this GitHub repository in order to use the desktop app.

## Troubleshooting

If setup fails:

1. Confirm ChatGPT opens and is signed in inside Code ProMax.
2. Run the app's runtime/browser verification or doctor check.
3. Restart Code ProMax and Codex after changing integration settings.
4. If using MCP, verify that the tunnel/connector is available to the same OpenAI/ChatGPT environment you configured.
5. Check local logs for an explicit capability, permission, browser-UI, or network error before retrying repeatedly.

Because ChatGPT's web UI and platform capabilities can change, a future OpenAI update can temporarily break browser automation or connector behavior even when Code ProMax itself has not changed.

## Releases and updates

Production-signed binaries are distributed through this repository's **Releases** section when a release is published. The source code for Code ProMax is not published here.

Before installing an update, prefer the production-signed installer and any checksum/signature information supplied with that release.

## License

Code ProMax itself is proprietary software. See [LICENSE](LICENSE).

The application includes third-party open-source components distributed under their own licenses. Their notices and attribution are provided in:

- [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt)
- [Bun.md](Bun.md)

Third-party components keep their original license rights and are not relicensed under the Code ProMax proprietary license.

## Trademark notice

Code ProMax is an independent third-party application and is not affiliated with, endorsed by, or sponsored by OpenAI. OpenAI, ChatGPT, GPT, Codex, and related marks belong to their respective owners.
