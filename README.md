# jinjainc - incremental evaluation in a Jinja2 template.

Given a template like

```markdown
    Once {{ _.a }}, twice {{ _.a }}, thrice {{ _.a }}.
    ```python
    a = 9
    b = 3.2
    ```
    But now {{ _.a }} ({{ _.a }}).
    ```python
    a = 10
    ```
    And then {{ _.a }}.
    ```python
    a *= b
    ```
    Finally {{ _.a }} ({{ _.a }}).
```

rendered with `template.render(_=Incer(template_text))`,
yield

```markdown
    Once ???, twice ???, thrice  ???.
    ```python
    a = 9
    b = 3.2
    ```
    But now 9 (9).
    ```python
    a = 10
    ```
    And then 10.
    ```python
    a *= b
    ```
    Finally 32.0 (32.0).

```

or, after rendering through pandoc or whatever:

Once ???, twice ???, thrice  ???.
```python
a = 9
b = 3.2
```
But now 9 (9).
```python
a = 10
```
And then 10.
```python
a *= b
```
Finally 32.0 (32.0).


