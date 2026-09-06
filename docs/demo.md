# Demo Script

## Target Interaction

### Step 1: Case Import

Drop a patient folder into the Copilot panel.

**Detected:**
- CT DICOM series
- liver.nii.gz
- tumor.nii.gz
- liver.vtk
- vessels.vtk

### Step 2: Prepare Case

User: "Prepare this case for review."

Copilot imports and organizes the available data.

### Step 3: Show Structures

User: "Show only the tumor and surrounding vessels."

Copilot shows Tumor, Portal Vein, Vena Cava and hides everything else.

### Step 4: Adjust Display

User: "Make the liver transparent."

Copilot sets Liver opacity to 0.3.

### Step 5: Navigate

User: "Zoom to the tumor."

Copilot centers the 3D camera on the tumor.

### Step 6: Query

User: "What structures are currently visible?"

Copilot reads the actual scene and responds.

## What This Demonstrates

- IMPORT: Detect and load medical imaging data
- UNDERSTAND: Interpret natural language commands
- CONTROL: Safely modify the Slicer scene
- VISUALIZE: Apply display properties
- VERIFY: Confirm every action succeeded
