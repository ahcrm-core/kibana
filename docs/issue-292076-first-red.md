# Kibana #292076 — First Red (frozen tests)

- Issue: https://github.com/elastic/kibana/issues/292076
- Upstream base commit: `8cd6f5919c443e3b14dbb8e460b699a637b52e17`
- Frozen test commit: `0bc84601033504bb0dbdde2fa34c9457b213582f`
- Runner configuration commit: `47af7c83a674403d98b3defb6ee08adb34ed89e2`
- Workflow run: https://github.com/ahcrm-core/kibana/actions/runs/36358319372
- Job: `108730356134`
- Result: **3 failed / 3 total** in `indices_stats_helpers.test.ts`; dependency bootstrap completed successfully; Jest itself ran.
- Failure: all three helper calls propagated `index_not_found_exception: no such index [traces-apm-missing]` instead of returning an empty result.
- Scope: these are unit tests using mocks that emulate Elasticsearch's absent-index response according to the `ignore_unavailable` request setting. This does not yet prove the full Storage Explorer route or UI works with a live Elasticsearch deployment.
- Candidate production code: **unchanged**. No repair, merge, or upstream PR has been made.
- Decision: `FIRST_RED_CONFIRMED_WITHIN_MOCKED_HELPER_SCOPE`; route-level and live-ES behavior remain `NO_VERDICT`.

Preserve the failing run and test definitions before any production-code repair. Subsequent repair must reuse these tests unchanged and add any necessary route-level evidence rather than expanding the conclusion from this run.
