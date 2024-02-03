# comfyui-legacy
## PyPI custom node packages
- [ComfyUI_Ib_CustomNodes](https://pypi.org/project/ComfyUI_Ib_CustomNodes/)
- [comfyui-tooling-nodes](https://pypi.org/project/comfyui-tooling-nodes/)

## Making legacy custom nodes installable
Add a `pyproject.toml` file with the following content to the repository root, and then change all the values marked with `CHANGE`:

```toml
[project]
# CHANGE: The project name
name = "ComfyUI_Ib_CustomNodes"
version = "0.1.0"
# description = '...'
readme = "README.md"
# requires-python = ">=3.8"
# license = "MIT"
keywords = ["comfyui"]
dynamic = ["dependencies"]

[project.urls]
# CHANGE: Homepage, mostly the GitHub repository
Homepage = "https://github.com/Chaoses-Ib/ComfyUI_Ib_CustomNodes"
comfyui-legacy = "https://github.com/Chaoses-Ib/comfyui-legacy"

[build-system]
requires = ["hatchling", "hatch-requirements-txt"]
build-backend = "hatchling.build"

[tool.hatch.metadata.hooks.requirements_txt]
# CHANGE: Remove this section if there is no requirements.txt
files = ["requirements.txt"]

[tool.hatch.build.targets.sdist]
packages = ["."]

[tool.hatch.build.targets.wheel]
packages = ["."]
exclude = [
  "*.md",
  "/images",
  "/docs",
  "/examples",
  "/workflow_examples",
  "/tests",
]

[tool.hatch.build.targets.sdist.sources]
# CHANGE: Package name. Must be an valid Python id (no dashes)
"." = "ComfyUI_Ib_CustomNodes"

[tool.hatch.build.targets.wheel.sources]
# CHANGE: Same as above
"." = "ComfyUI_Ib_CustomNodes"

[project.entry-points."comfyui_legacy.custom_nodes"]
# CHANGE: Same as above
ComfyUI_Ib_CustomNodes = "ComfyUI_Ib_CustomNodes"
```

With this change, the custom nodes can be installed through `pip` and still keep compatibility with the legacy installation approach (cloning into the `custom_nodes` directory). For example:
```sh
pip install git+https://github.com/Chaoses-Ib/ComfyUI_Ib_CustomNodes.git
```