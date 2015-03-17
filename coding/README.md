## Editors

We enforce consistency in editor defaults using an **[`.editorconfig`](http://editorconfig.org/)**. The contents of our preferred editorconfig settings are:

```
indent_style = space
indent_size = 2
charset = utf-8
end_of_line = lf
insert_final_newline = true
```

### Enforcing editor defaults

Automated enforcement of `.editorconfig` is enabled for you by default in boxen if you use Atom or Sublime Text.

Everyone (unless you're an exception, and you'll know if that is the case) has an available `.editorconfig` in their user directory for consumption by editors.

If you use a different editor, check to see if your editor has support for, or a package/plugin that supports, editorconfig and install/enable it.

It is known that BBEdit, for some inexplicable reason, does not support editorconfig. It's probably possible to replicate the editorconfig settings by adjusting preferences. Shrug. 
