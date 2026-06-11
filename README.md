# stack-trace-cleaner

Strip framework noise from stack traces. Paste a trace from Node, Python, Rust, Java, Ruby, or Go, get only the frames in your code, with the option to expand framework frames if you need them. Browser only.

**Live demo:** https://0xelitesystem.github.io/stack-trace-cleaner/

## Use

Open [`index.html`](./index.html). Paste a trace. Click Clean.

The tool:

- Detects the language (Node, Python, Rust, Java, Ruby, Go, or unknown)
- Marks frames as user-code or framework noise
- Hides noise by default, with a toggle to show it
- Collapses runs of consecutive noise frames into `[N framework frames hidden]` summaries

## What's noise

Per-language patterns the tool filters:

- **Node**: `node_modules/`, `node:internal/`, `webpack-internal`, Next.js internals, `<anonymous>` frames
- **Python**: `site-packages/`, `dist-packages/`, asyncio internals, threading, Django/Flask/FastAPI internals, frozen modules
- **Rust**: `~/.cargo/registry/`, `library/`, tokio internals, `core::panicking`, `std::panicking`
- **Java**: `java.base/`, `jdk.internal.`, `org.springframework.`, Tomcat, JUnit, Gradle, Netty
- **Ruby**: `gems/`, Rails, ActiveSupport, ActionPack, Bundler
- **Go**: `runtime/`, `pkg/mod/`, package-level `runtime.` calls

## Why

A stack trace from a vibe-coded project often has 30 frames where 3 are yours. The 27 noise frames make the actual problem harder to see. Cleaning surfaces the user-code frames immediately.

## What this is not

- Not a debugger
- Not a stack trace analyzer (it doesn't tell you what's wrong, just what's important)
- Not connected to any service

## Privacy

Pure browser, no upload, no analytics.

## Run locally

```
git clone https://github.com/0xelitesystem/stack-trace-cleaner
cd stack-trace-cleaner
```

Open `index.html` in a browser.

## Contribute

PRs welcome:

- More language support (Elixir, Clojure, Haskell, Swift, Kotlin)
- Better detection for unknown formats
- Per-project framework patterns (configurable)
- Source map support (resolve minified Node traces)

Don't add: external scripts, npm dependencies, telemetry. Single file.

## Build

No build. Single HTML file.

## License

MIT.

## Related

- [agent-diff-reviewer](https://github.com/0xelitesystem/agent-diff-reviewer) - review agent-generated diffs
- [vibe-coding-anti-patterns](https://github.com/0xelitesystem/vibe-coding-anti-patterns) - failures that produce noisy traces
