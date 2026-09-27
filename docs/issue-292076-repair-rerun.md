# Kibana #292076 — repair and focused reruns

- Issue: https://github.com/elastic/kibana/issues/292076
- Upstream base: `8cd6f5919c443e3b14dbb8e460b699a637b52e17`.
- Original frozen test commit: `0bc84601033504bb0dbdde2fa34c9457b213582f`.
- First Red: https://github.com/ahcrm-core/kibana/actions/runs/36358319372 — **3 failed / 3 total**; dependency bootstrap completed; all failed on `index_not_found_exception`.
- Limited production repair: `88cc0acff2013c83380fe809ad9dcf4580510bb1`, affecting only `indices_stats_helpers.ts`. `indices.stats` and `indices.get` now use `ignore_unavailable: true`. ILM explain does not support that option, so only its absent-index error returns an empty lifecycle map; other errors propagate.
- Same frozen tests rerun: https://github.com/ahcrm-core/kibana/actions/runs/36358797150 — **3 passed / 3 total**.
- Additional safeguard tests (without editing the three original tests): `ce047a11b45409f6d1682d44869a4895531d3956`; confirm unrelated ILM errors propagate and existing lifecycle data remains intact.
- Expanded focused run: https://github.com/ahcrm-core/kibana/actions/runs/36358961306 — **5 passed / 5 total**.
- Scope: Jest unit tests with mocks emulating Elasticsearch's missing-index response. No live Elasticsearch, full Storage Explorer route, browser UI, repository-wide tests, or type-check gate has been run. These remain **NO_VERDICT**.
- Status: repair is on a fork branch only; no upstream pull request or merge.
