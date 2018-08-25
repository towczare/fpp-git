# Git config
Before you start using GIT, cofig your local user settings using following command
```
git config --global <key> <value>
```

| KEY           | Example value |
| ------------- | ------------- |
| `user.name`   | "Jan Kowalski"|
| `user.email`  | jan.kowalski@kowalski.io  |
| `core.editor`  | vim  |
| `color.ui`  | auto |
| `merge.tool`  | meld |
to see full list use `git config --list` This also shows what are current values.
# Exercises
Configure following settings:
 - `user.name` as value use your name and surname
 - `user.email` as value use your email
 - `merge.tool` use `meld` or `kdiff3` and install this tool