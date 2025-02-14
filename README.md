# UV example

An application using a library, built with uv.

To recreate:

run these commands
```
uv init
uv venv --python 3.12
source .venv/bin/activate
mkdir -p foo bar
cd bar
uv init --lib
cd ..
cd foo
uv init --app
uv add bar
```

Add to foo pyproject.toml

```toml
[tool.uv]
package = true

[project.scripts]
hello = "hello:main"
```

update foo hello.py with the bar function

```python
from bar import hello

print(hello())
```

run commands
```
cd ..
uv lock
uv sync --all-packages
```


run foo app

The following are equivalent here:
- `uv run hello`
- `uv run foo/hello.py`
- `uv run -m hello --package foo`

```
Hello from foo!
Hello from bar!
```