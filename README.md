# jinjainc - incremental evaluation in a Jinja2 template.

Given a template like

```markdown
    `a` is {{ _.a }}, twice {{ _.a }}, thrice {{ _.a }}.
    ```python
    a = 9
    b = 3.2
    ```
    But now `a` = {{ _.a }} ({{ _.a }}).
    ```python
    a = 10
    ```
    And then `a` is {{ _.a }}.
    ```python
    a *= b
    ```
    Finally a: {{ _.a }} ({{ _.a }}).
```

rendered with `template.render(_=Incer(template_text))`,
yield

```markdown
    `a` is ???, twice ???, thrice ???.
    ```python
    a = 9
    b = 3.2
    ```
    But now `a` = 9 (9).
    ```python
    a = 10
    ```
    And then `a` is 10.
    ```python
    a *= b
    ```
    Finally a: 32.0 (32.0).
```

or, after rendering through pandoc or whatever:

`a` is ???, twice ???, thrice ???.
```python
a = 9
b = 3.2
```
But now `a` = 9 (9).
```python
a = 10
```
And then `a` is 10.
```python
a *= b
```
Finally a: 32.0 (32.0).


