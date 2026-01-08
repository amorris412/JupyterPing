# JupyterPing

Desktop-level alerts for Jupyter notebooks that notify you when code execution completes or encounters errors.

Ideal for long-running notebooks where you need to be notified when execution finishes, even when VS Code is hidden or minimized.

![Platform](https://img.shields.io/badge/platform-macOS-lightgrey)
![Python](https://img.shields.io/badge/python-3.7+-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## Features

- Green flashing alerts for successful completion
- Red flashing alerts for errors (automatically detected)
- Desktop-level alerts visible even when VS Code is hidden
- System sounds and macOS notifications
- No kernel crashes - alerts run in separate process
- Zero configuration - works from any directory
- Automatic error detection - no try/except blocks needed

## Demo

When your notebook completes successfully:
- Green flashing window appears on top of all apps
- "Glass" sound plays
- macOS notification banner
- Auto-closes after 12 seconds

When an error occurs:
- Red flashing window appears automatically
- "Basso" alert sound
- Shows error type and message
- No need for try/except blocks

## Quick Start

### Installation

1. Download the files:
   ```bash
   curl -O https://raw.githubusercontent.com/amorris412/JupyterPing/main/notebook_auto_alert.py
   curl -O https://raw.githubusercontent.com/amorris412/JupyterPing/main/_show_alert.py
   ```

2. Place them in your project directory (or anywhere in your Python path)

### Usage

Add to your notebook:

```python
# Cell 1 - Import (enables automatic error detection)
from notebook_auto_alert import done

# Cell 2, 3, 4... - Your code
# Any errors here will automatically trigger red alert
import pandas as pd
df = pd.read_csv('data.csv')
# ... your analysis ...

# Last Cell - Trigger success alert
done("Analysis complete - processed 10,000 rows")
```

This setup provides:
- Automatic red alerts if any cell errors
- Green alert when `done()` is called
- Desktop notifications you cannot miss

## Detailed Usage

### Success Alerts

```python
from notebook_auto_alert import done

# Basic usage
done()

# With custom message
done("Training complete - Accuracy: 95%")

# After long computation
train_model()  # Takes 2 hours
done("Model training finished")
```

### Error Alerts (Automatic)

Errors are automatically detected - no try/except needed:

```python
from notebook_auto_alert import done

# Any error in any cell automatically triggers red alert
result = 100 / 0  # ZeroDivisionError → automatic red alert
```

### Manual Error Alerts

If you want to manually trigger error alerts:

```python
from notebook_auto_alert import error

if not validate_data():
    error("Data validation failed")
```

## Requirements

- **macOS** (uses macOS notification system)
- **Python 3.7+**
- **tkinter** (included with Python on macOS)

No additional dependencies needed. Works with:
- VS Code with Jupyter extension
- JupyterLab
- Jupyter Notebook

## Use Cases

Ideal for:
- Long-running ML training - get alerted when training completes
- Data processing pipelines - know when ETL jobs finish
- Scientific computations - avoid checking back every 5 minutes
- Multiple notebooks - work on other things while notebooks run
- Background execution - minimize VS Code and get notified when done

## How It Works

1. Import triggers auto-error detection by hooking into IPython exception handler
2. Errors automatically show red alerts without code changes
3. Call `done()` for success to trigger green alert
4. Alerts run in separate process to prevent kernel blocking or crashes
5. Desktop-level notifications are always visible

## Files

- `notebook_auto_alert.py` - Main module (import this in notebooks)
- `_show_alert.py` - Alert display script (do not call directly)
- `example.ipynb` - Example notebook with usage demonstrations

## Troubleshooting

**Alert does not appear:**
- Ensure both `notebook_auto_alert.py` and `_show_alert.py` are in the same directory
- Check console output for any warnings

**Kernel crashes:**
- This should not happen in the latest version (uses subprocess)
- If it does, please open an issue

**Not working in Jupyter Notebook/Lab:**
- Should work correctly - automatic error detection requires IPython/Jupyter
- Ensure you are importing the module in a code cell

## Contributing

Contributions are welcome. Feel free to:
- Report bugs
- Suggest features
- Submit pull requests

## License

MIT License - free to use in your projects.

## Acknowledgments

Built for data scientists and ML engineers who run long notebooks and want to know when they are done without constantly checking.

---

**Made for the Jupyter community**

If this tool saves you time, consider giving it a star.
