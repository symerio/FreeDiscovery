# Release history


## Version 1.0

**In developpement**

### New features  

 * Ability to add / remove documents in an existing processed dataset using `/api/v0/feature-extraction/{dsid}/append` and `/api/v0/feature-extraction/{dsid}/delete` URL endpoints 
 * Pagination in search and document categorization with the `batch_id` and `batch_size` parameters.

### Enhancements

 * Better handling of data persistence, which leads to faster response time for all URL endpoints, and in particular semantic search and categorization. This breaks backward compatibility for the internal data format: datasets need to re-processed and models re-trained. 
 * Additional tests for categorization and semantic search 

### API Changes
 * The `nn_metric` parameter was renamed to `metric`; a new metric `cosine-positive` was added
 * Breaking change: by default, the `cosine` similarity score is used.
 * The `/email-parser/*` endpoints are removed and merged into the `/feature-extraction/` endpoint, thus unifying data ingestion.


## Version 0.9

**Jan 28, 2017**

### New features  

 * Support for multi-class categorization and non integer class labels (PR [#96](https://github.com/FreeDiscovery/FreeDiscovery/pull/96/files)) 
 * In the case of binary categorization, recall at 20 % of documents is computed as part of the list of default scores (PR [#106](https://github.com/FreeDiscovery/FreeDiscovery/pull/106))

### Enhancements

 * Categorization and semantic search support sorting and filtering of documents below a user provided threashold. (PR [#96](https://github.com/FreeDiscovery/FreeDiscovery/pull/96/files))
 * Categorization returns only `max_result_categories` categories with the highest score. 
 * The similarity and ML scores can now be scaled to [0, 1] range using `nn_metric` and `ml_output` input parameters (PR [#101](https://github.com/FreeDiscovery/FreeDiscovery/pull/100/files)).
 * The REST API documentation is generated automatically from the code (using an OpenAPI specification) which allows to enforce consistency between the code and the docs (PR [#85](https://github.com/FreeDiscovery/FreeDiscovery/pull/85))
 * Adapted clustering and duplicate detection API to return structured objects indexed by `document_id`( and optionally `rendering_id`)
 * Improved tests coverage and overall simplified the API


### API Changes
 
 * The following endpoints accepting a request body are modified from `GET` to `POST` method (PR [#94](https://github.com/FreeDiscovery/FreeDiscovery/pull/94)), in accordance with the HTTP/1.1 spec, section 4.3,
    - `/api/v0/metrics/categorization`
    - `/api/v0/metrics/clustering`
    - `/api/v0/metrics/duplicate-detection`
    - `/api/v0/feature-extraction/{dsid}/id-mapping/flat`
    - `/api/v0/feature-extraction/{dsid}/id-mapping/nested`
    - `/api/v0/email-parser/{dsid}/index`
 * Significant changes in the categorization REST API to accommodate for multi-class cases
 * The endpoint `/api/v0/feature-extraction/{dsid}/id-mapping/flat` is removed, while `/api/v0/feature-extraction/{dsid}/id-mapping/nested` is renamed to `/api/v0/feature-extraction/{dsid}/id-mapping`. 
 * Removed the `/categorization/<mid>/test` which is superseded by `/metrics/categorization`. 
 * The `internal_id` is no longer exposed in the public API

## Version 0.8

**Feb. 25, 2017**

### New features  

 * NearestNeighbor search now can perform categorization both with positive/negative training documents (supervised) as well as with only a list of positive documents (unsupervised) (PR [#50](https://github.com/FreeDiscovery/FreeDiscovery/pull/50))
 * Document search and semantic search (PR [#63](https://github.com/FreeDiscovery/FreeDiscovery/pull/63))


### Enhancements
 
 * In depth code reorganisation making each processing step a separate REST endpoint (PR [#57](https://github.com/FreeDiscovery/FreeDiscovery/pull/57))
 * More rubust default parameters (PR [#65](https://github.com/FreeDiscovery/FreeDiscovery/pull/65))

### API Changes
 
 * Ability to associate external `document_id`, `rendition_id` fields when ingesting documents; document categorization can now be used with these external ids. 
 * All the wrappers classes are made private in the Python API
 * The same categorization and clustering enpoints can operate ether in the document-term space or in the LSI space (PR [#57](https://github.com/FreeDiscovery/FreeDiscovery/pull/57))
