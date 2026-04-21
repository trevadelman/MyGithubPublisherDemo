# xs.demo.publisher

A minimal xetolib used to exercise the **`xs.git` publisher
roundtrip** — `gitInitLib` → `gitPublishLib` → `gitLibStatus`, plus
consumer-side `gitInstallLib` against the resulting GitHub repo.

Layout: flat (one lib per repo, `lib.xeto` at root). This matches the
publisher convention in `xs.git::ROADMAP.md`.

## Roundtrip

```axon
// publisher side (this xbd)
gitInitLib("xs.demo.publisher")          // .git/ created, tag v0.0.1
gitLibStatus("xs.demo.publisher")        // published: true, drift: false

// bump version in lib.xeto to "0.0.2" and add a change
gitPublishLib("xs.demo.publisher")       // new commit + tag v0.0.2
gitLibStatus("xs.demo.publisher")

// ... push to GitHub via gh / git push --tags ...

// consumer side (another xbd)
gitInstallLib(
  "https://github.com/trevadelman/MyGithubPublisherDemo",
  "v0.0.2"
)
libAdd("xs.demo.publisher")
```
