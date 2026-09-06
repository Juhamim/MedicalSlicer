# 🧠 MedicalSlicer AI Copilot

> **A natural-language AI assistant for 3D Slicer that simplifies medical imaging workflows through intelligent, validated, and safe automation.**

![3D Slicer](https://img.shields.io/badge/Platform-3D%20Slicer-blue)
![Python](https://img.shields.io/badge/Language-Python-yellow)
![License](https://img.shields.io/badge/License-MIT-green)
![AI](https://img.shields.io/badge/AI-LLM%20Powered-purple)

---

## 📌 Overview

**MedicalSlicer AI Copilot** is an AI-powered assistant integrated with **3D Slicer** that enables users to control and interact with medical imaging workflows using natural language.

Instead of manually navigating complex menus and tools, users can simply describe what they want to do.

For example:

> 💬 "Show the tumor and hide the skin."

> 💬 "Make the liver transparent."

> 💬 "Zoom to the tumor."

> 💬 "What structures are currently loaded?"

The AI Copilot interprets the request, analyzes the current **MRML scene**, validates the requested action, executes only approved operations, and verifies the result.

The project is designed with a strong focus on **safety, scene awareness, and controlled AI execution**.

---

## ✨ Key Features

### 💬 Natural Language Control

Control 3D Slicer using simple conversational commands.

Examples:

* Show the tumor
* Hide the skin
* Show only the tumor and vessels
* Make the liver transparent
* Change tumor opacity to 80%
* Make the tumor red
* Zoom to the tumor

---

### 🧠 Scene Awareness

The assistant understands the current **MRML scene** and can inspect:

* Medical image volumes
* Segmentation nodes
* 3D models
* Markups
* Anatomical structures
* Visibility states
* Scene objects

This allows the assistant to perform actions based on the actual data currently loaded in 3D Slicer.

---

### 🛡️ Verified and Safe Actions

The AI model does **not directly execute arbitrary Python code**.

Every user request follows a controlled execution pipeline:

```text
User
  ↓
Chat Interface
  ↓
LLM Client
  ↓
Action Parser
  ↓
Validator
  ↓
Action Engine
  ↓
Scene Manager
  ↓
3D Slicer API
  ↓
Verification
```

All actions are validated before execution and verified afterward.

---

### 📂 Medical Case Import

The system supports importing medical imaging data from folders, including:

* DICOM
* NIfTI
* NRRD
* 3D Models

This makes it easier to prepare medical cases for review and visualization.

---

### 🔍 Scene Queries

Users can ask questions about the currently loaded scene.

Examples:

```text
What is loaded?

What structures are visible?

Show all available segmentations.

Which models are currently hidden?
```

---

## 🏗️ System Architecture

```text
                 ┌──────────────────┐
                 │      User        │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │     Chat UI      │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │    LLM Client    │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │    Validator     │
                 │  Action Allowlist│
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │  Action Engine   │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │  Scene Manager   │
                 │   MRML Analysis  │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │   3D Slicer API  │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │   Verification   │
                 └──────────────────┘
```

---

## 🛠️ Technology Stack

| Technology                             | Purpose                        |
| -------------------------------------- | ------------------------------ |
| 🐍 Python                              | Core application development   |
| 🧠 LLM                                 | Natural language understanding |
| 🩻 3D Slicer                           | Medical imaging platform       |
| 🧬 MRML                                | Medical scene management       |
| 🖥️ Qt                                 | Chat interface                 |
| 📦 Pydantic                            | Data validation and schemas    |
| 🔌 ModelScope / OpenAI-compatible APIs | LLM integration                |

---

## 💬 Supported Commands

### 👁️ Visibility Control

```text
Show the tumor
Hide the skin
Show only tumor and vessels
```

---

### 🎨 Display Control

```text
Make the liver transparent
Set tumor opacity to 80%
Make the tumor red
```

---

### 🧭 Navigation

```text
Zoom to tumor
Show axial view
Switch to 3D view
```

---

### 🔍 Scene Queries

```text
What is loaded?
What structures are visible?
```

---

### 📁 Case Preparation

```text
Prepare this case for review
```

---

## 📂 Project Structure

```text
MedicalSlicer/
│
├── SlicerAICopilot/
│   │
│   ├── SlicerAICopilot/
│   │   ├── SlicerAICopilot.py      # Main module entry point
│   │   ├── chat_ui.py              # Qt-based chat interface
│   │   ├── llm_client.py           # LLM integration
│   │   ├── scene_manager.py        # MRML scene inspection
│   │   ├── action_engine.py        # Action execution engine
│   │   ├── validator.py            # Action validation
│   │   ├── verification.py         # Result verification
│   │   ├── file_manager.py         # Medical file import
│   │   ├── schemas.py              # Pydantic schemas
│   │   └── utils.py                # Utility functions
│
├── prompts/                        # LLM system prompts
│
├── knowledge/                      # Action definitions and examples
│
├── tests/                          # Unit tests
│
├── docs/                           # Documentation
│
├── Agents.md                       # Agent instructions
│
├── requirements.txt                # Python dependencies
│
└── README.md
```

---

## 🚀 Installation

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/Shafah0717/MedicalSlicer.git
```

```bash
cd MedicalSlicer
```

---

### 2️⃣ Install Dependencies

Install the required Python packages:

```bash
pip install -r requirements.txt
```

---

### 3️⃣ Add the Module to 3D Slicer

Open **3D Slicer** and navigate to:

```text
Edit → Application Settings → Modules
```

Add the project module directory to the additional module paths.

Alternatively:

```text
Modules → Add Module Path
```

Select the project module folder.

---

### 4️⃣ Restart 3D Slicer

Restart the application.

Then open:

```text
Modules → Slicer AI Copilot
```

---

## ⚙️ Configuration

Configure the LLM provider using environment variables.

Example:

```bash
export LLM_PROVIDER=modelscope
export LLM_API_KEY=your_modelscope_token
export LLM_BASE_URL=https://api-inference.modelscope.ai/v1
export LLM_MODEL=Qwen-Ambassador/Qwen3.7-Max
```

### Windows PowerShell

```powershell
$env:LLM_PROVIDER="modelscope"
$env:LLM_API_KEY="your_modelscope_token"
$env:LLM_BASE_URL="https://api-inference.modelscope.ai/v1"
$env:LLM_MODEL="Qwen-Ambassador/Qwen3.7-Max"
```

> ⚠️ Never commit your API keys or credentials to GitHub.

---

## 🛡️ Safety and Security

MedicalSlicer AI Copilot is designed with a controlled execution architecture.

### Security Principles

* 🚫 No arbitrary Python code execution from the LLM
* ✅ Strict action allowlist
* 🔍 All actions validated before execution
* 🎯 Target objects must exist in the MRML scene
* ✔️ Results verified after execution
* 🔒 Only scene metadata is intended to be processed for AI interaction
* ⚠️ Destructive operations can require user confirmation

The AI model acts as an **intent interpretation layer**, while the application retains control over what operations can actually be executed.

---

## 🧪 Testing

Run tests from within the 3D Slicer environment:

```bash
Slicer --python-script -m pytest tests/
```

The test suite is intended to validate:

* Action parsing
* Schema validation
* Scene inspection
* Action execution
* Verification logic
* File handling

---

## 🎥 Demo

Watch the project demonstration:

[▶️ Watch MedicalSlicer AI Copilot Demo](https://youtu.be/-SVpAnDcjaw)

---

## 🎯 Use Cases

MedicalSlicer AI Copilot can assist with workflows such as:

* 🩻 Medical image visualization
* 🧠 Surgical planning workflows
* 🫁 Anatomy exploration
* 🧬 Segmentation visualization
* 🔬 Medical research workflows
* 📊 Clinical case review
* 🎓 Medical imaging education

---

## 🗺️ Future Roadmap

* [ ] Voice-based interaction
* [ ] Multi-step workflow planning
* [ ] Advanced scene reasoning
* [ ] Confirmation system for destructive actions
* [ ] Workflow history and audit logs
* [ ] Support for additional LLM providers
* [ ] Improved medical terminology understanding
* [ ] Context-aware workflow recommendations
* [ ] Advanced DICOM case preparation
* [ ] Multi-agent medical imaging assistance

---

## 🤝 Contributing

Contributions are welcome!

To contribute:

1. Fork the repository
2. Create a new branch

```bash
git checkout -b feature/your-feature-name
```

3. Make your changes
4. Commit your changes

```bash
git commit -m "Add your feature"
```

5. Push to your branch

```bash
git push origin feature/your-feature-name
```

6. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License**.

See the `LICENSE` file for more information.

---

## 👨‍💻 Project

**MedicalSlicer AI Copilot**

An intelligent natural-language interface designed to make medical imaging workflows in 3D Slicer more accessible, efficient, and safe.

---

### ⭐ Support the Project

If you find this project useful, consider giving the repository a **star ⭐**.

It helps support the project and encourages further development.
