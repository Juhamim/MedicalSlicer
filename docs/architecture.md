# Architecture

Slicer AI Copilot is a natural-language AI assistant embedded directly inside 3D Slicer.

## Pipeline

```
User Input (chat_ui.py)
    → LLM (llm_client.py via ModelScope/Qwen API)
    → JSON Response Parsing
    → Validation (validator.py) — safety boundary
    → Action Execution (action_engine.py)
    → Scene Modification (scene_manager.py → Slicer API)
    → Verification (verification.py)
    → UI Feedback (chat_ui.py)
```

## Components

### chat_ui.py
Qt-based chat panel embedded in 3D Slicer. Handles user input, message display, folder drag-and-drop, and orchestrates the full request/response cycle.

### llm_client.py
OpenAI-compatible client targeting ModelScope/Qwen. Supports sync, async, and streaming completions. Configured via environment variables (`LLM_API_KEY`, `LLM_BASE_URL`, `LLM_MODEL`).

### scene_manager.py
Inspects the MRML scene: reads volumes, models, segmentations, markups, transforms. Provides visibility, opacity, and color controls. Resolves natural-language object names via fuzzy matching.

### schemas.py
Pydantic models for all 19 action types, `ActionPlan`, `SceneObject`, `SceneSummary`. Defines `ALLOWED_ACTIONS` allowlist.

### validator.py
Mandatory safety boundary. Validates action type allowlist, target existence, parameter ranges, and detects malicious content. Rejects arbitrary Python code.

### action_engine.py
The only layer allowed to modify the Slicer scene. Executes validated actions through trusted Python functions that call Slicer APIs.

### verification.py
Post-execution verification. Re-reads actual scene state to confirm actions produced expected results.

### file_manager.py
Scans folders for DICOM, NIfTI, NRRD, and model files. Groups DICOM series. Imports selected files through Slicer APIs.

### utils.py
Fuzzy matching, target resolution, file type detection, folder scanning, scene formatting.

## Safety Model

```
LLM = Understand and plan
    ↓
Validator = Decide what is allowed
    ↓
Action Engine = Execute trusted operations
    ↓
Slicer = Perform the actual work
    ↓
Verification = Confirm what actually happened
```

The LLM never receives unrestricted execution privileges. Every operation passes through a controlled action layer and verification step.
