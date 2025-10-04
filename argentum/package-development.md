---
description: Argentum documentation for those who want to develop packages
icon: code
---

# Package development

_NOTE: This is for Argentum 2. Everything written here is incompatible with the original Argentum._

## Repository setup

To create a package for Argentum, you must either use an existing repository that you have access to or you must create a new one. When creating a repository for Argentum, it's recommended to use GitHub for reasons that will be explained later. However, anything can be used, including a mounted filesystem on the OpenComputer accessing the package.

After your package is made, if you want it to be in the main package registry, you must submit a pull request to `/ag2/registry.json` in the Halyde repo and add your repo indexed by the name of each package you want to make public. For example, if you wanted to publish 2 packages, `package1` and `package2` in the repo `https://myrepository.net`, you would have to add these 2 lines to `/ag2/registry.json`:

```json
"package1": "https://myrepository.net",
"package2": "https://myrepository.net"
```

## Configuration

In the root of the repository, there must be an `ag2.json` file. This is what directs Argentum to each package, lists its files, directories, dependencies, etc. The format must be like this:

{% code title="ag2.json" %}
```json
{
  "packageName": {
    "version": "vX.X.X",
    "description": "Your package description goes here.",
    "dependencies": [
      "dependency1",
      "dependency2"
    ],
    "conflicts": [
      "conflict1",
      "conflict2"
    ],
    "mainDirectory": "packages/packageName",
    "files": [
      "file1",
      "halyde/apps/file2",
    ],
    "directories": [
      "packageDir",
      "packageDir/something"
    ],
    "scripts": {
      "pre-install": "extra/pre-install.lua",
      "post-install": "extra/post-install.lua"
    }
  }
}
```
{% endcode %}

* `packageName` is your package's name;
* `version` is your package's version;
* `description` is a brief description of your package;
* `dependencies` is a list of packages your package depends on (this is optional);
* `conflicts` is a list of packages your package conflicts with and cannot be installed alongside (this is optional);
* `mainDirectory` is the directory in which all of your package's files are contained in the repository. For example, when downloading `file1.txt` for a package that has `mainDirectory` set to `some/directory`, the file will be downloaded from `some/directory/file1.txt`, but it will be placed in `/file1.txt` in the user's system. This is useful for multi-package repositories where two packages can provide different files in the same location (this is optional);
* `files` is a list of files that will be downloaded when installing your package (this is optional);
* `directories` is a list of directories that will be created when installing your package (this is optional);
* `scripts` is for scripts that will be run before/after installation of your package (this is optional):
  * `pre-install` is the path of the script that will be run before installing your package (this is optional);
  * `post-install` is the path of the script that will be run after installing your package (this is optional).

## Versioning

All past versions of any package should always be kept available. This is done with some directories in your repository. For each package, there has to be a `packageName-versions/` directory in your repository's root. If this is not present, only the latest version of your package will be available, and packages that depend on older versions may break.

Inside the `packageName-versions/` directory, for each version there is another directory (for example, `packageName-versions/vX.X.X`) which has all the files needed for the package and its configuration (`ag2.json`). That configuration is structured the same way, however it only has the one package. There is also no `mainDirectory` option, as `packageName-versions/vX.X.X` is already the main directory.

Every time a new version is released, the corresponding directory in `packageName-versions` should be made and all the package's files and its config copied into it. If you use GitHub to host your repository, you can use this [nifty GitHub Action I've made](https://github.com/WahPlus/ArgentumPackages/tree/main/.github/workflows) to automate the process.
