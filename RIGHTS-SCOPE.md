# Rights and deployment scope

The MIT grant covers only the ELUCENIA-authored adapters, parsers, schemas, labels, test harness, CLI, server and documentation in this package. It does not license any provider algorithm, model binary, logo, third-party annotation, or private ELUCENIA portal/dashboard. No such UI, authentication, database, patient data or credentials are included.

This is a bounded official-API client, not a reimplementation or validation of the complete named provider. The provider computes the prediction/enrichment; our tests check request/response contracts, source identities, numerical formatting and selected consistency assertions. Clinical approval and professional language review have not been performed.

Public/synthetic research inputs only. Requests go to the named provider, and result exports contain the query and attribution. Do not submit identifying, patient or confidential data. The CLI requires an explicit --live option for network use; tests and default offline mode never call providers.

A deterministic provider lock directory is shared by all packages and the website/dashboard under the same OS account on one host: os.homedir()/.elucenia/research-provider-locks. ELUCENIA_RESEARCH_LOCK_DIRECTORY is an optional absolute override; use the same directory for all apps. This is not cross-host distributed coordination. Active PIDs are never evicted only because a lease expired; interrupted uncertain IEDB requests retain a conservative five-minute cooldown.

The standalone server binds only to 127.0.0.1 and has no account/session system. A production proxy must provide separately reviewed authentication, authorization, transport and privacy controls. No private dashboard authentication source is distributed here.

## g:Profiler / Gene Ontology

The official g:Profiler FAQ offers academic and non-academic API use without a paid license. This workflow requests only GO:BP/GO:MF/GO:CC and excludes KEGG/TRANSFAC. GO material and the bundled GO response extract carry the Gene Ontology Consortium CC BY 4.0 attribution requirement separately from MIT software. Retain the release, annotation versions, DOI and source links. Raw GO term names remain their official English scientific text; the surrounding interface/documentation is localized. Provider adjusted p-values are not independently recalculated by the client.

CC BY 4.0: https://creativecommons.org/licenses/by/4.0/
Citation policy: https://geneontology.org/docs/go-citation-policy/
GO release2026-01-23, DOI10.5281/zenodo.18422732; g:Profiler e114_eg62_p19_27110d83.
Service use: https://biit.cs.ut.ee/gprofiler/page/faq
