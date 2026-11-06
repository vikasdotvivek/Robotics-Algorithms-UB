# Code improvement triage

**Automated first pass, not a complete manual code audit or a safety certification.**

Repository: `vikasdotvivek/Robotics-Algorithms-UB`
Snapshot: `f6594a1702a7faf753a3388093e51667314eaa4f`

- Tracked paths: 70; source files inspected: 8.
- Findings: 5; retained: 5; omitted by cap: 0.
- Priority counts in retained findings: {'P1': 3, 'P2': 2}.
- No repository code, tests, builds or hardware were executed.

## Scope and limitations

Python findings use AST parsing under the runner Python 3. C/C++/C# findings are lexical review candidates, not compiler-verified defects. Files over 1 MB, designer files, generated/vendor paths, binaries, notebooks, PDFs and other non-source formats are excluded and enumerated in the JSON report. No findings does not establish correctness.

## Build and test follow-up

Build/dependency entry points detected:
- `Project 1/CMakeLists.txt`
- `Project 1/package.xml`
- `Project 2/CMakeLists.txt`
- `Project 2/package.xml`
- `Project 4/CMakeLists.txt`
- `Project 4/package.xml`

No conventional test paths were detected. Add regression fixtures for the critical calculations and input boundaries; notebook/manual tests may still exist.

## Potential improvements

### 1. P1: Does not parse with the audit runner Python 3
Source: [Project 1/scripts/evader_bot.py:36](https://github.com/vikasdotvivek/Robotics-Algorithms-UB/blob/f6594a1702a7faf753a3388093e51667314eaa4f/Project%201/scripts/evader_bot.py#L36)
Confirm the intended Python version. This may be legacy Python 2 rather than an unintended syntax error; compile with the supported interpreter.

### 2. P1: Does not parse with the audit runner Python 3
Source: [Project 1/scripts/evader_pursuer_bot.py:36](https://github.com/vikasdotvivek/Robotics-Algorithms-UB/blob/f6594a1702a7faf753a3388093e51667314eaa4f/Project%201/scripts/evader_pursuer_bot.py#L36)
Confirm the intended Python version. This may be legacy Python 2 rather than an unintended syntax error; compile with the supported interpreter.

### 3. P1: Does not parse with the audit runner Python 3
Source: [Project 1/scripts/pursuer_bot.py:48](https://github.com/vikasdotvivek/Robotics-Algorithms-UB/blob/f6594a1702a7faf753a3388093e51667314eaa4f/Project%201/scripts/pursuer_bot.py#L48)
Confirm the intended Python version. This may be legacy Python 2 rather than an unintended syntax error; compile with the supported interpreter.

### 4. P2: Exception handler only passes
Source: [Project 2/scripts/percept.py:140](https://github.com/vikasdotvivek/Robotics-Algorithms-UB/blob/f6594a1702a7faf753a3388093e51667314eaa4f/Project%202/scripts/percept.py#L140)
Decide whether the error is recoverable; surface nonrecoverable failures instead of silently continuing.

### 5. P2: Exception handler only passes
Source: [Project 4/scripts/main.py:152](https://github.com/vikasdotvivek/Robotics-Algorithms-UB/blob/f6594a1702a7faf753a3388093e51667314eaa4f/Project%204/scripts/main.py#L152)
Decide whether the error is recoverable; surface nonrecoverable failures instead of silently continuing.

## Acceptance gate

Confirm each candidate in its calling context. Add a regression test, make one focused change, and build using the actual target dependencies. For robotics/actuator firmware, verify safe outputs, limit handling, sensor failure and timing on a controlled test rig. Do not merge or deploy a blanket rewrite based on these pattern matches.

Machine-readable scope, exclusions and findings: `static-review.json`.
