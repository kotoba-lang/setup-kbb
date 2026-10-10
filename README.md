# setup-kbb

A GitHub Action that installs **kbb**, the JVM-free runner for Kotoba and
Clojure-shaped `.cljk` code, with its pinned engine
([kotoba-lang/org-babashka-nbb](https://github.com/kotoba-lang/org-babashka-nbb)),
and puts it on `PATH`. It replaces `clojure -M:test` in CI (root
ADR-2610100200): the cognitect runner does not look for `.cljk` and reported
"Ran 0 tests" as success.

```yaml
- uses: actions/checkout@v4
- uses: kotoba-lang/setup-kbb@<commit>
- run: kbb -M:test
```

`kbb` comes from [kotoba-lang/kotoba](https://github.com/kotoba-lang/kotoba)
(`bin/kbb`). Both repositories are fetched at pinned commits (`kotoba-ref`,
`engine-ref`) into `RUNNER_TEMP`, outside the workspace. It lives in its own
repository because kotoba-lang/kotoba's tree carries a symlink GitHub cannot
download as an action.
