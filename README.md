# glap

![Python package](https://github.com/Mountlex/glap/workflows/Python%20package/badge.svg)

A GitLab Artifact Puller / Downloader

## Quick Start

`glap` is a convenience tool to download artifacts of your frequently used GitLab repositories. Install via

```bash
pip install glap
```

Before you can use `glap`, you have to setup your configuration file located at `~/.config/glap/glap.toml` (if such a file cannot be found, it will also search for a local `glap.toml` file). It contains the following information.

* Remotes with corresponding `url`s and access-tokens:

```toml
[remotes.myremote]
url = "https://gitlab.com"
private_token = "<my-private-token>"
oauth_token = "<my-oauth-token>"
job_token = "<my-job-token>"
```

Note that there must be exactly one token specified.

* Shortcuts for specific repositories. For example, the following shortcut points at the `PDFs` job of the `main` branch of `https://gitlab.com/name/repo`.

```toml
[shortcuts.myshortcut]
remote = "myremote"
namespace = "name"
repository = "repo"
branch = "main"
job = "PDFs"
```

Any configured shortcut will appear as a subcommand, i.e. you can use it as follows

```bash
glap myshortcut
```

Alternatively, you can specify the namespace and repository directly

```bash
glap download <namespace> <repository>
```

If no remote is given, `glap` will use the first one in the configuration file. Otherwise, you can use

```bash
glap download <namespace> <repository> -r myremote
```

where `myremote` is the name of the remote in the configuration file.

### Options

* `--job` (`-j`) specifies the job's name.
* `--branch` (`-b`) specifies the branch's name.
* `--output` (`-o`) specifies the download location.
* `--temp` (`-t`) downloads the artifact to a temporary location and opens the directory.
* `--silent` (`-s`) enables silent mode (exceptions only).
* `--verbose` (`-v`) enables verbose mode (e.g. print file list).
  