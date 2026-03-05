# 🔧 Oh My hsh — Pipes

Community pipes for the [hsh](https://github.com/takakix2/hsh) shell ecosystem.

All pipes follow the **Flux Protocol v1** — they read and/or write NDJSON on stdin/stdout, making them composable with each other and standard Unix tools.

## Installation

```bash
hsh pipe install flux-render
hsh pipe install filter-json
```

Or install directly from this repository:

```bash
hsh pipe install oh-my-hsh/pipes
```

## Available Pipes

| Pipe | Description | Runtime |
|------|-------------|---------|
| [flux-eye](./flux-eye/) | High-speed filesystem scanner | Binary |
| [flux-grep](./flux-grep/) | Fast signal extraction from NDJSON streams | Binary |
| [flux-render](./flux-render/) | Universal format converter (NDJSON ↔ Markdown/CSV/YAML) | Python 3 |
| [filter-json](./filter-json/) | Filter NDJSON streams by keyword | Python 3 |
| [json-to-table](./json-to-table/) | Render NDJSON as ASCII tables | Python 3 |

## Writing Your Own Pipe

Any executable that reads/writes NDJSON can be a Flux pipe. Here's a minimal example in Python:

```python
#!/usr/bin/env python3
import json, sys
for line in sys.stdin:
    record = json.loads(line)
    record["processed"] = True
    print(json.dumps(record), flush=True)
```

Save it, `chmod +x`, and pipe it: `flux-eye -p . | ./my-pipe`

## License

MIT
