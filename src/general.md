
# Coding Conventions

## Files

### File Newlines

Files should use Unix-style newlines, LF (Line Feed). Do not use CR+LF (Carriage Return + Line Feed).

### File Encoding

Files must be encoded with UTF-8.
They must not include a *Byte Order Mark* (**BOM**), represented as `U+FEFF`.

<details>
<summary><em>Code editors and BOMs</em></summary>

* **Microsoft Notepad**: Most versions of Microsoft Notepad will always insert a BOM. This no longer happens in the Windows 10 May 2019 Update (Version 1903, build 10.0.18362).[^so-windows-10-notepad-bom] *However*, we do not support Microsoft Notepad as a suggested code editor for writing software.
* **Visual Studio Code**: Visual Studio Code supports [saving files with different encodings](https://code.visualstudio.com/docs/editor/codebasics#_file-encoding-support).
  * To set the default file encoding:
    * Go to "Settings" (`Ctrl + ,` / `Cmd + ,`)
    * Text Editor → Files → Files: Encoding → "UTF-8"
  * To change a file's current encoding:
    * Open Command Palette (`Ctrl + Shift + P` / `Command + Shift + P`)
    * "Change File Encoding" then "Save with Encoding"
    * Select "UTF-8 without BOM (`utf8bom`)"

</details>

## File Structure

Generally, the structure of a software project should **at least** contain the following files and folders:

```txt
.
└── software/
    ├── .devcontainer/
    │   ├── devcontainer.json
    │   └── Dockerfile
    ├── .github/
    │   ├── workflows/
    │   │   └── ci.yml
    │   └── renovate.json
    ├── .idea/
    ├── docs/
    ├── src/
    ├── tests/
    ├── .editorconfig
    ├── .gitattributes
    ├── .gitignore
    ├── LICENSE
    ├── README.md
    └── CHANGELOG.md
```

* `{software}`: The name of the software library or application.
* `.devcontainer/`: Folder to allow editing the project in a development container, like [GitHub Codespaces](https://docs.github.com/en/codespaces).
  * `devcontainer.json`: File to configure the development container.
  * `Dockerfile`: Dockerfile to build the development container.
* `.github/`: Meta-folder for a GitHub project.
  * `renovate.json`: File to configure [Renovatebot](https://docs.renovatebot.com/) for automating dependency management
  * `workflows/`: Folder to configure GitHub Actions.
    * `ci.yml`: The main GitHub workflow for continuous integration
* `.idea/`: Meta-folder for containing IntelliJ configuration.
* `docs/`: Documentation of the software.
* `src/`: Source code.
* `tests/`: Unit tests and integration tests.
* `.editorconfig`: File to configure the code editor and maintain code style across IDEs ([official docs](https://editorconfig.org/))
* `.gitattributes`: file that contains attributes for file paths ([official docs](https://git-scm.com/docs/gitattributes))
* `.gitignore`: a file that lists files and folders to ignore when committing to a git repository. ([official docs](https://git-scm.com/docs/gitignore))
* `LICENSE`: The license the software is released under.
* `README.md`: A meta-file that describes what the software is about.
* `CHANGELOG.md`: A meta-file that describes what changes have been made to the software for each release/version.

## Indentation

Code should use tabs (`U+0009`) for indentation. This allows developers to configure their editor to show the amount of spaces per tab: 2, 4, or 8 spaces per tab.

Use the "One True Brace Style" (OTBS or 1TBS for short) to indent every braces. An example:

```rust
fn main() {
    if(x > 0) {
        println!("x is positive");
    } else {
        println!("x is non-positive");
    }
}
```
