# gnome-eg
Store gome eg (a git wrapper in perl) at github.

## eg original

The original eg project is available here:


 - main page: https://people.gnome.org/~newren/eg/
 - downloads:  https://people.gnome.org/~newren/eg/download/
 - online docs: https://people.gnome.org/~newren/eg/documentation/


The gitorious repo (https://gitorious.org/projects/eg) unfotunately ceased to work.

This repo picks the last version (1.7.5.2) of eg, and tries to keep it

 - as simple as it was (i don't expect feature upgrades)
 - correct smaller problems if arised

## List of changes

 1. "Unescaped left brace in regex is deprecat..."

With newer perl versions eg gives annoying warnings:

```
[xxx@yyy ~]$ eg version
Unescaped left brace in regex is deprecated, passed through in regex; marked by <-- HERE in m/^stash\@{ <-- HERE [^{]+}$/ at ./eg line 5861.
Unescaped left brace in regex is deprecated, passed through in regex; marked by <-- HERE in m/(stash\@{ <-- HERE [^}]+}): (?:WIP )?[Oo]n [^:]*: (?:[0-9a-f]+\.\.\. )?/ at ./eg line 5926.
eg version 1.7.5.2
git version 2.5.5
```

This can be corrected with two pairs of backslash:

```
5861c5861
<     if ($stash_description =~ m#^stash\@{[^{]+}$# ||
---
>     if ($stash_description =~ m#^stash\@\{[^{]+\}$# ||
5926c5926
<       qr#(stash\@{[^}]+}): (?:WIP )?[Oo]n [^:]*: (?:[0-9a-f]+\.\.\. )?#;
---
>       qr#(stash\@\{[^}]+\}): (?:WIP )?[Oo]n [^:]*: (?:[0-9a-f]+\.\.\. )?#;
```

We give it a version number 1.7.5.3, too.
