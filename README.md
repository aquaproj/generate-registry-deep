# generate-registry-deep

Run `aqua-registry gr --deep` by GitHub Actions

`--deep` option may cause GitHub API rate limiting, so we created this repository only for running `aqua-registry gr --deep`.

https://docs.github.com/en/rest/overview/resources-in-the-rest-api?apiVersion=2022-11-28

> When using `GITHUB_TOKEN`, the rate limit is 1,000 requests per hour per repository.

`GITHUB_TOKEN`'s rate limit is set per repository, so even if the rate limit occurs in this repository, it doesn't affect other repositories and users.

## How to use

[Run the GitHub Actions Workflow](https://github.com/aquaproj/generate-registry-deep/actions/workflows/generate.yaml).

e.g.

```console
$ gh workflow run generate.yaml -f package=suzuki-shunsuke/tfcmt [-r <branch>]
```

## Reference

- [aquaproj/aqua#1662](https://github.com/aquaproj/aqua/pull/1662)
- [aquaproj/registry-tool#307](https://github.com/aquaproj/registry-tool/pull/307)

## LICENSE

[MIT](LICENSE)
