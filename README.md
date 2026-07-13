# macOS ComboBox Navigation Fix

A lightweight Python utility that works around a macOS UI issue affecting combo boxes in applications such as DaVinci Resolve (and potentially other software).

## Problem

On macOS, some applications do not properly update a combo box when navigating its dropdown menu using keyboard shortcuts. The highlighted item changes, but the actual selection is not committed until the combo box receives a mouse click.

This issue does **not** occur on Windows or Linux.

This script automates the missing interaction.

## How It Works

When you:

1. Move your mouse cursor over the combo box title (or the combo box itself).
2. Hold **Shift**.
3. Press **Up** or **Down**.

The script automatically:

1. Temporarily releases the Shift key.
2. Performs a mouse click to commit/focus the combo box.
3. Sends the Up or Down key.
4. Presses Enter to confirm the new selection.
5. Restores the Shift key state.

This makes navigating combo boxes behave as expected without manually clicking every time.

## Requirements

* macOS
* Python 3.8+
* Accessibility permissions enabled for Terminal (or the application running the script)

### Python Dependencies

Install the required packages:

```bash
pip install pyautogui pynput
```

## macOS Permissions

Because the script controls the mouse and keyboard, macOS requires Accessibility permissions.

Go to:

```
System Settings
→ Privacy & Security
→ Accessibility
```

Enable access for:

* Terminal
* iTerm (if applicable)
* PyCharm / VS Code (if running from an IDE)
* Any other application used to launch the script

Without these permissions, simulated mouse and keyboard events will not work.

## Usage

Start the script:

```bash
python dvr-combobox.py
```

When the script is running:

1. Open the application's combo box.
2. Position the mouse cursor over the combo box title (or directly over the combo box).
3. Hold **Shift**.
4. Press:

   * **Shift + Up** → previous item
   * **Shift + Down** → next item

Repeat as needed.

## Why Is This Needed?

Some macOS applications fail to update the selected value when navigating dropdown menus via keyboard alone.

The script simulates the missing mouse click that normally commits the selection, making keyboard navigation reliable.

## Tested With

* DaVinci Resolve
* Other macOS applications exhibiting the same combo box behavior

If another application has the same issue, this script will likely work there as well.

## Dependencies

* `pyautogui` — mouse and keyboard automation
* `pynput` — global keyboard listener

## Notes

* This utility is intended only for macOS.
* Windows and Linux do not require this workaround because the combo box behavior works correctly there.
* The cursor must remain over the target combo box for the click to activate the correct control.

## License

MIT License
