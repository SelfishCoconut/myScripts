# gscrub

Remove a string from a git repo's **entire history**: text files and commit
messages are rewritten, documents/archives containing it are deleted from
history. A backup bundle is written first. Companion to [gsearch](../gsearch).

Deps (Arch): `git git-filter-repo ripgrep-all poppler pandoc-cli`.
Run `gscrub -h` for options. It rewrites every commit hash, so you must
force-push afterwards.
