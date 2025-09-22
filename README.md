# gear-update-submodules

## Description

This script recursively traverses all **git submodules**, identifies the pinned commits,  
and creates **git tags** for each of them, including nested submodules. Then, it performs  
a `git merge` of these tags and generates helper strings for `gear-rules` and the spec file.

## Dependencies

- **bash**
- **git** (with submodule support)
- Standard utilities: `sed`, `awk`, `basename`, `xargs`, `pushd`, `popd`

## Usage

```bash
gear-update-submodules <version>
```

**Important!**

The `<version>` parameter is the version itself, **not** a tag.

## What the script does

1. Switches to the root of the repository  
2. Initializes all submodules (including nested ones)  
3. Recursively iterates through each submodule  
4. Retrieves:
   - Path  
   - URL  
   - Commit hash  
5. Tags each submodule with `<relpath>-<version>`  
6. Performs a `git merge` of all these tags (with `--allow-unrelated-histories` and the `ours` strategy)  
7. Outputs:
   - List of tags  
   - List of `tar:` rules for `.gear/rules`  
   - List of `SourceN:` entries

## License

MIT
