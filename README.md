# generate-registry-deep

Run `aqua gr --deep` by GitHub Actions

`--deep` option may cause GitHub API rate limiting, so we created this repository only for running `aqua gr --deep`.

https://docs.github.com/en/rest/overview/resources-in-the-rest-api?apiVersion=2022-11-28

> When using `GITHUB_TOKEN`, the rate limit is 1,000 requests per hour per repository.

`GITHUB_TOKEN`'s rate limit is set per repository, so even if the rate limit occurs in this repository, it doesn't affect other repositories and users.

## How to use

[Run the GitHub Actions Workflow](https://github.com/aquaproj/generate-registry-deep/actions/workflows/generate.yaml).

e.g.

```console
$ gh workflow run generate.yaml -f package=suzuki-shunsuke/tfcmt [-r <branch>]
```

Then the result would be outputted to GITHUB_STEP_SUMMARY.
Please see the summary.

e.g.

https://github.com/aquaproj/generate-registry-deep/actions/runs/4263618160

registry.yaml

```yaml
packages:
  - type: github_release
    repo_owner: cloudspannerecosystem
    repo_name: wrench
    description: wrench - Schema management tool for Cloud Spanner -
    asset: wrench_{{trimV .Version}}_{{.OS}}_{{.Arch}}.tar.gz
    checksum:
      type: github_release
      asset: wrench_{{trimV .Version}}_checksums.txt
      file_format: regexp
      algorithm: sha256
      pattern:
        checksum: "^(\\b[A-Fa-f0-9]{64}\\b)"
        file: "^\\b[A-Fa-f0-9]{64}\\b\\s+(\\S+)$"
    version_constraint: semver(">= 1.3.3")
    version_overrides:
      - version_constraint: semver(">= 1.3.0")
        supported_envs:
          - linux
          - darwin
      - version_constraint: semver(">= 1.1.0")
        asset: wrench_{{.OS}}_{{.Arch}}
        format: raw
        supported_envs:
          - linux
          - darwin
        checksum:
          enabled: false
      - version_constraint: semver("< 1.1.0")
        asset: wrench_{{.OS}}_{{.Arch}}
        format: raw
        supported_envs:
          - linux/amd64
          - darwin
        rosetta2: true
        checksum:
          enabled: false
```

testdata

```yaml
packages:
  - name: cloudspannerecosystem/wrench@v1.3.3
  - name: cloudspannerecosystem/wrench
    version: v1.3.0
  - name: cloudspannerecosystem/wrench
    version: v1.1.0
  - name: cloudspannerecosystem/wrench
    version: v1.0.0
```

### :rocket: Fork this repository

If you want to run the workflow, please [fork this repository](https://github.com/aquaproj/generate-registry-deep/fork) and run the workflow!
No GitHub Secrets or something are needed. You only have to fork this repository.

## Reference

- [aquaproj/aqua#1662](https://github.com/aquaproj/aqua/pull/1662)

## LICENSE

[MIT](LICENSE)
