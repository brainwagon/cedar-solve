# Update: Modern Dependency Compatibility

This library is a **private fork** of the original [smroid/cedar-solve](https://github.com/smroid/cedar-solve.git). It has been **minimally modified** to ensure compatibility with the most recent versions of its major dependencies, specifically addressing breaking changes and deprecations introduced in NumPy 2.x and recent SciPy releases.

## Changes

- **Dependency Constraints:** Updated `pyproject.toml` to remove upper bounds for `numpy`, `scipy`, and `Pillow`.
- **Pillow Upgrade:** Set minimum `Pillow` version to `>= 10.0.0` to ensure compatibility with modern image processing standards.
- **SciPy Deprecations:** Fixed all occurrences of `scipy.ndimage.filters` (which is deprecated and removed in SciPy 2.0). Replaced with their modern equivalents in the `scipy.ndimage` namespace:
  - `scipy.ndimage.filters.uniform_filter` -> `scipy.ndimage.uniform_filter`
  - `scipy.ndimage.filters.median_filter` -> `scipy.ndimage.median_filter`
- **NumPy 2.0 Compatibility:** Verified compatibility with NumPy 2.x.
- **Internal Cleanup:** Fixed minor comment typos in the source code.

## Test Environment

The changes were verified by running the full test suite (`pytest`) in a clean virtual environment using the following package versions:

| Package | Tested Version |
| :--- | :--- |
| **NumPy** | 2.2.6 |
| **SciPy** | 1.15.3 |
| **Pillow** | 12.1.1 |

All tests passed (with the exception of gRPC-related tests which require a running Cedar-Detect server).
