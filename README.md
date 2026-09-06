# Slicer AI Copilot

Natural-language AI assistant embedded in 3D Slicer for medical imaging workflow automation.

## Features

- **Natural Language Control**: Control Slicer through chat commands
- **Scene Awareness**: Understands current MRML scene (volumes, models, segmentations, markups)
- **Verified Actions**: All operations validated before execution, verified after
- **Case Import**: Drag-and-drop folder import for DICOM, NIfTI, NRRD, models
- **Safety First**: No arbitrary code execution, strict action allowlist

## Commands

| Category | Examples |
|----------|----------|
| Visibility | "Show the tumor", "Hide the skin", "Show only tumor and vessels" |
| Display | "Make liver transparent", "Set tumor opacity to 80%", "Make tumor red" |
| Navigation | "Zoom to tumor", "Show axial view", "Switch to 3D" |
| Queries | "What is loaded?", "What structures are visible?" |
| Case Prep | "Prepare this case for review" |

## Installation

1. Clone this repository
2. In 3D Slicer: `Modules → Add Module Path` → select this folder
3. Restart Slicer
4. Open **Slicer AI Copilot** from Modules menu

## Configuration

Set environment variables:

```bash
export LLM_PROVIDER=modelscope
export LLM_API_KEY=your_modelscope_token
export LLM_BASE_URL=https://api-inference.modelscope.ai/v1
export LLM_MODEL=Qwen-Ambassador/Qwen3.7-Max
```

## Architecture

```
User → Chat UI → LLM Client → Validator → Action Engine → Scene Manager → Slicer API
                                    ↓
                              Verification
```

## Project Structure

```
SlicerAICopilot/
├── SlicerAICopilot/          # Main Python package
│   ├── SlicerAICopilot.py    # Module entry point
│   ├── chat_ui.py            # Qt chat panel
│   ├── llm_client.py         # ModelScope/OpenAI client
│   ├── scene_manager.py      # MRML scene inspection
│   ├── action_engine.py      # Action execution
│   ├── validator.py          # Action validation
│   ├── verification.py       # Result verification
│   ├── file_manager.py       # Folder scanning/import
│   ├── schemas.py            # Pydantic schemas
│   └── utils.py              # Utilities
├── prompts/                  # LLM prompts
├── knowledge/                # Action definitions & examples
├── tests/                    # Unit tests
└── docs/                     # Documentation
```

## Development

Run tests inside Slicer:
```bash
Slicer --python-script -m pytest tests/
```
DEMO: https://youtu.be/-SVpAnDcjaw 

## Safety

- LLM never executes arbitrary Python
- All actions go through validator allowlist
- Target objects must exist in scene
- Destructive operations require confirmation (future)
- No patient data sent to LLM (only scene metadata)

## License

MIT
