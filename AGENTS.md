# AGENTS.md

Agent guidance for this repository lives in [CLAUDE.md](./CLAUDE.md). Everything there applies to any coding agent, not just Claude Code.

The short version before you edit anything:

1. This is a documentation-only repo — no build, lint, or test commands. The two top-level directories demo two knowledge-base formats (Karpathy's llm-wiki pattern and Google's OKF v0.1) over the same knowledge, and edits must conform to each format's own conventions.
2. `karpathy-llm-wiki/CLAUDE.md` is both demo content and the binding rules for that subtree: `sources/` is read-only, wiki pages carry frontmatter and `[[wikilinks]]`, and `wiki/log.md` is append-only.
3. `google-okf/bundle/` must remain a conformant OKF v0.1 bundle (required `type` frontmatter, reserved `index.md`/`log.md`, relative links) — see `google-okf/README.md` for the spec summary.
