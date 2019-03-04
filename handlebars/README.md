# Handlebars Guide

## Handlebars files with Markdown frontmatter get improperly indented in VSCode

If you use Visual Studio Code and edit a handlebars file with markdown frontmatter (as you'll commonly find in our pattern libraries), and you have `formatOnSave` enabled, you may find that the frontmatter is improperly indented. You can fix this by setting `html.format.indentHandlebars` to `true`.
