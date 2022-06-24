# Tanzu insight source vulnerabilities

Get source vulnerabilities.

## <a id='synopsis'></a>Synopsis

Get source vulnerabilities. You can specify either commit or repo.

```console
tanzu insight source vulnerabilities [--commit <commit-hash>] [--repo <repo-url>] [--format <format>] [flags]
```

## <a id='examples'></a>Examples

```console
tanzu insight sources vulnerabilities --commit eb55fc13
```

## <a id='options'></a>Options

```console
  -c, --commit string   commit hash
  -f, --format string   output format which can be in 'json' or 'text'. If not present, defaults to text. (default "text")
  -h, --help            help for vulnerabilities
  -r, --repo string     source repository url
```

## <a id='see-also'></a>See also

* [Tanzu insight source](insight-source.md)	 - Source commands
