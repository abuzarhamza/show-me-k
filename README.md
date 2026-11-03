# show-me-k

Skills that help humans understand what agents changed.

> "As LLMs get better … a lot more of our work will rise up the abstractions into oversight and understanding."
> — [Andrej Karpathy](https://x.com/karpathy/status/2105819303471976479)

## Installation

```bash
npx skills add abuzarhamza/show-me-k --skill show-me-mr
```

Or as a Claude Code plugin:

```text
/plugin marketplace add abuzarhamza/show-me-k
/plugin install show-me-mr@show-me-k
```

## show-me-mr

Explains a merge request by working up the output-format ladder from Karpathy's post. It stops at the lowest level that makes the change clear:

| Level | Format | Output |
|---|---|---|
| 1 | **Text** in ~80% [ASD-STE100](https://www.asd-ste100.org/) | summary, warnings, review order |
| 2 | **Diagrams** in the style of [`show-me`](https://github.com/humanlayer/skills) | `diff`-style file, call, and type trees, plus Mermaid |
| 1–2 | **Markdown file** (always) | `.show-me/mr-{id}/explainer.md`: levels 1–2 in one file that renders on GitHub/GitLab; also the `--post` body |
| 3 | **HTML** | `.show-me/mr-{id}/index.html`: change map, step-by-step walkthrough, animated before/after, review checklist |
| 4 | **Video** (opt-in) | `.show-me/mr-{id}/explainer.mp4`: Manim animation with ElevenLabs or local narration |

Works with GitHub (`gh`), GitLab (`glab`), or a plain local branch.

```text
/show-me-mr                    # current branch, up to HTML
/show-me-mr 142                # PR/MR #142
/show-me-mr 142 diagram        # text and diagrams only
/show-me-mr 142 video          # all four levels
/show-me-mr 142 --post         # also post explainer.md as a PR/MR comment (asks first)
```

The skill never edits the PR/MR description, pushes, merges, or approves. It installs nothing and calls no paid API (such as ElevenLabs) without asking you first.

Video needs `manim` and `ffmpeg`. Without them, the skill makes an auto-advancing HTML slide deck instead.

## Credits

- [HumanLayer `show-me` / `visual-pr`](https://github.com/humanlayer/skills) (MIT), which this skill's diagram views are adapted from.
- [Andrej Karpathy's post](https://x.com/karpathy/status/2105819303471976479) on output formats for understanding: STE writing → diagrams → HTML → explainer videos.
