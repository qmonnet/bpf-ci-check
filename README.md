# bpf-ci-check

## Run the BPF CI on your own Linux repository

Want to check your BPF patches through the CI on your own repository, without
sending your patches just yet to the mailing list? This script is here to help.

## How it works

1. The script creates a new branch `ci-test/<branch>` based on your development
   branch to test.
2. It pulls the files for the BPF CI from
   https://github.com/kernel-patches/vmtest and adds them to your repository,
   and commits the change on that new branch.
3. It pushes the branch and creates a new pull request from this branch against
   a base branch, on a given repository.
4. The GitHub Action starts, builds the kernel, and runs the BPF selftests.

## Requirements

- curl
- [gh](https://cli.github.com/) (GitHub command line)
- git
- rsync
- unzip

## Usage

Make sure your base branch is up-to-date (if you intend to create the PR
against `bpf-next` from your own repository, make sure you have updated your
`bpf-next` branch on your Linux fork on GitHub).

Then just run the script:

```
$ ./bpf-ci-check -h
Usage: ./bpf-ci-check [options]
Test in CI - Open a GitHub PR for 'ci-test/<branch>' against <base> on <repo>
Options:
        -h              display this help
        -n              dry run (create branch, but do not push or create a PR)
        -d branch       development branch to test in CI (default: current)
        -b base         base branch to use (default: 'bpf-next')
        -r repo         GitHub repository to use, for both branches and for PR
                        (default: gh-resolved base or first remote found)
```
