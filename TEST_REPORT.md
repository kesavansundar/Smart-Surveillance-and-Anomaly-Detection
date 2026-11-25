# SmartSurveillance Testing Report

**Test date:** 2026-11-25  
**Python:** 3.12.10  
**Platform:** Windows  
**PyTorch:** 2.5.1+cpu  
**YOLO model:** yolov8n.pt

## Summary

- Python syntax compilation: passed
- Component tests: 11 passed
- Installation verification: passed
- Camera indexes 0 and 1: opened and returned frames
- YOLOv8 detector initialization: passed
- Console monitoring: passed; detections and alert-frame saving verified
- GUI startup: passed
- Source-module imports: passed

## Results by file

| Test/file | Result | Notes |
|---|---|---|
| `python -m compileall -q .` | Passed | Python files compiled successfully. |
| `python -m pytest tests/test_components.py -q` | Passed | 11 tests passed. |
| `verify_installation.py` | Passed | All dependency, structure, camera-access, and initialization checks passed. GPU was unavailable; CPU mode was used. |
| `test_camera.py` | Passed with warning | Camera indexes 0 and 1 read frames; index 2 was unavailable. |
| `test_detector.py` | Passed | `yolov8n.pt` loaded successfully. |
| `test_main_integration.py` | Partial | Menu check passed; hard-coded external image and folder paths were unavailable. |
| `test_whatsapp_image.py` | Blocked | Its hard-coded BMW image path was not present. |
| `api_examples.py` | Passed | Script started and printed usage guidance. |
| `main.py`, `gui_app.py` | Passed startup | GUI processes started. |
| `src/gui.py` | Passed after fix | Added project-root path setup for direct execution. |
| `console_example.py` | Passed | Initialized camera/model, detected people, and saved an alert frame. |
| `simple_detection.py` | Partial | Camera opened, but live frame read failed with a Windows MSMF error. |
| `image_detection.py` | Interactive | Menu displayed; automated run had no stdin input. |
| `detect_simple.py` | Blocked | Hard-coded image path was unavailable. |
| `detect_upload.py` | Blocked | `uploaded_image.jpg` was unavailable. |
| `batch_detect.py` | Blocked | Hard-coded Pictures folder was unavailable. |
| `quick_detect.py` | Usage check passed | Correctly requested an image-path argument. |
| Source-module import check | Passed | All `src` modules imported successfully. |

## Environment notes

- Some detection scripts use machine-specific input paths that are not present in this environment.
- Camera access is inconsistent: camera reads worked in the camera diagnostic and console test, but `simple_detection.py` received MSMF error `-1072875772`.
- The direct `python src/gui.py` import issue was fixed by adding the project root to `sys.path`.
- Console monitoring saved an alert frame under `alerts\` during testing.

## Overall

Core dependencies, component tests, installation checks, model loading, GUI startup, and console monitoring succeeded. The remaining blocked/partial scripts require local image/folder inputs or stable Windows camera frame reads.
