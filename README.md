# AutoCAD MCP Server

A Python Model Context Protocol server that exposes AutoCAD drawing operations to MCP clients through a stdio interface.

## Repository origin

This repository is a fork of [ahmetcemkaraca/AutoCAD_MCP_archive](https://github.com/ahmetcemkaraca/AutoCAD_MCP_archive). The project retains the upstream [MIT license](LICENSE), copyright Barry Adams, 2025.

## Core tools

The entry point in [src/server.py](src/server.py) registers these tools:

| Tool | Purpose |
| --- | --- |
| `draw_line` | Create a line between two 3D points |
| `draw_circle` | Create a circle from a center and radius |
| `extrude_profile` | Extrude a profile into a solid |
| `revolve_profile` | Revolve a profile around an axis |
| `list_entities` | Inspect drawing entities |
| `get_entity_info` | Read details of an entity |
| `server_status` | Check the server and AutoCAD connection |

Additional modules explore geometry processing, code generation, and development tooling. These modules are separate from the seven tools registered by the stdio entry point.

## Requirements

- Windows with AutoCAD installed and an active drawing.
- Python 3.12 or later.
- Poetry for the dependency configuration in [pyproject.toml](pyproject.toml).
- An MCP client that can launch a local stdio server.

The project targets AutoCAD 2025 through its Windows COM interface.

## Local setup

```powershell
git clone https://github.com/Salema0x/AutoCAD_MCP.git
cd AutoCAD_MCP
poetry install
poetry run python -m src.server
```

Run the module from the repository root so the `src` package can be imported. The server communicates over stdio and logs to stderr; it is intended to be launched by an MCP client rather than used as a normal terminal prompt.

Configure the client to launch the project's Python environment with arguments `-m src.server` and the repository root as its working directory. Client-specific configuration formats vary.

Start with `server_status`, then a simple drawing operation in a test drawing. Runtime compatibility depends on the installed AutoCAD version and COM environment.

## Development

```powershell
poetry run pytest
```

Tests are under [tests](tests/). Operations that connect to AutoCAD require the Windows application and a suitable drawing session. The package metadata classifies this project as alpha.

## License

[MIT](LICENSE). Original copyright and license notices are retained.
