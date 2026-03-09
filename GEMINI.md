# Cedar-Solve (Tetra3 Fork)

Cedar-Solve is a fast, lost-in-space plate solver for star trackers, forked from [esa/tetra3](https://github.com/esa/tetra3). It identifies stars in images and determines the camera's pointing direction (Right Ascension, Declination, and Roll) and Field of View (FOV).

## Project Overview

- **Purpose:** High-performance star identification and plate solving.
- **Main Technologies:** Python, NumPy, SciPy, Pillow.
- **Optional Integrations:** [Cedar Detect](https://github.com/smroid/cedar-detect) via gRPC for high-performance star detection.
- **Architecture:** 
  - `Tetra3` class handles database management and solving logic.
  - Hashing-based geometric matching for fast lookups.
  - Supports multiple star catalogs (BSC5, Hipparcos, Tycho).

## Building and Running

### Installation
```bash
# Basic installation
pip install .

# Installation with optional cedar-detect support
pip install .[cedar-detect]

# Development installation (includes pytest)
pip install -e .[dev]
```

### Testing
Tests are located in the `tests/` directory and use `pytest`.
```bash
pytest
```

### Database Generation
The project includes a CLI tool to generate custom star databases.
```bash
# Example: Generate a database for a 30-degree FOV
tetra3-gen-db --max_fov 30 --save_as my_database
```

### Basic Usage
```python
import tetra3
from PIL import Image

# Initialize with default database
t3 = tetra3.Tetra3()

# Solve from an image file
with Image.open('path/to/image.jpg') as img:
    result = t3.solve_from_image(img)
    if result['status'] == tetra3.MATCH_FOUND:
        print(f"RA: {result['RA']}, Dec: {result['Dec']}, Roll: {result['Roll']}")
```

## Development Conventions

- **Coding Style:** Follows standard Python conventions (PEP 8).
- **Testing:** New features or bug fixes should include tests in `tests/`. Large datasets for testing are stored in `tests/data/`.
- **Database Catalogs:** If generating new databases, star catalog files (e.g., `bsc5`, `hip_main`) should be placed in the `tetra3/` directory or specified via path.
- **Compatibility:** Maintain compatibility with the original `tetra3` API where possible.
- **Protobuf:** gRPC/Protobuf files are located in `tetra3/proto/` and can be compiled using `scripts/compile_proto.py`.

## Key Files
- `tetra3/tetra3.py`: Core logic for the solver and database generation.
- `tetra3/cli/generate_database.py`: Implementation of the database generation CLI.
- `tetra3/cedar_detect_client.py`: Client for interacting with Cedar Detect.
- `pyproject.toml`: Project metadata and dependency definitions.
