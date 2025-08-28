# Run Python in the Browser (Pyodide template)

This is a minimal, production-friendly template that runs your **prewritten Python** directly in the browser using [Pyodide](https://pyodide.org). No backend servers are needed.

## How to use
1. Open `index.html` and find the `const code = \\`...\\`;` section.
2. Replace the Python in that string with your script’s logic (don’t accept arbitrary user code).
3. Adjust the input fields in the HTML and read them in JS before calling `runPythonAsync`.

## Install extra packages
You can install **pure-Python** packages from PyPI using `micropip`. (Packages with C extensions usually won’t work.) Example:
```js
await pyodide.loadPackage("micropip");
await pyodide.runPythonAsync(`
import micropip
await micropip.install("markdown")  # pure-Python example
`);
```

## Local preview
Just double-click `index.html` to open it in your browser. Because Pyodide is loaded from a CDN, no local server is required.

If you prefer a local server:
```bash
python -m http.server 8000
# then open http://localhost:8000/
```

## Deploy options
- **GitHub Pages** (static): push this folder to a repo and enable Pages.
- **Netlify**: drag-and-drop the folder at https://app.netlify.com/drop or connect to your Git repo.
- **Vercel**: create a new project from your repo; framework preset “Other”.

## Tips
- First page load downloads the Pyodide runtime (~10–20MB). Subsequent loads are faster thanks to browser cache.
- Keep your Python **pure-Python**; avoid packages that need native binaries.
- Add UI elements to collect typed inputs (text, numbers, file upload) and pass them to your Python code via string interpolation or the [Pyodide JS ↔ Python API](https://pyodide.org/en/stable/usage/type_conversions.html).

## Security
- Do **not** evaluate arbitrary user-provided Python code.
- Treat this as a fixed-function tool that calls your known Python function with validated inputs.
