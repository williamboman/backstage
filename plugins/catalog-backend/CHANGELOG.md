# @backstage/plugin-catalog-backend

## 0.2.0
### Minor Changes

- e0be86b6f: Entirely case insensitive read path of entities
- 12b5fe940: Add ApiDefinitionAtLocationProcessor that allows to load a API definition from another location
- 57d555eb2: This feature works the same as \$secret does in config - it allows programmatic substitution of values into a document.
  
  This is particularly useful e.g. for API type entities where you do not want to repeat your entire API spec document inside the catalog-info.yaml file. For those cases, you can instead do something like
  
  ```
  apiVersion: backstage.io/v1alpha1
  kind: API
  metadata:
    name: my-federated-service
  spec:
    type: graphql
    definition:
      $text: ./schema.graphql
  ```
  
  The textual content of that file will be injected as the value of definition, during each refresh loop. Both relative and absolute paths are supported, as well as any HTTP/HTTPS URL pointing to a service that returns the relevant data.
  
  The initial version supports injection of text file data, and structured data from JSON and YAML files. You can add any handler of your own in addition to these.
- 61db1ddc6: Allow node v14 and add to master build matrix
  
  - Upgrade sqlite3@^5.0.0 in @backstage/plugin-catalog-backend
  - Add Node 14 to engines in @backstage/create-app
- 81cb94379: Simplify the read function in processors
- a768a07fb: Add the ability to import users from GitHub Organization into the catalog.
  
  The token needs to have the scopes `user:email`, `read:user`, and `read:org`.
- ce1f55398: Use the new `UrlReader` in `PlaceholderProcessor`.
  This allows to use the placeholder processor to include API definitions in API entities.
  Previously it was only possible to do this if the definition comes from the same location type as the entity itself.
- e6b00e3af: Remove the backstage.io/definition-at-location annotation.
  The annotation was superseded by the placeholder processor.
  
  ```yaml
  apiVersion: backstage.io/v1alpha1
  kind: API
  metadata:
    name: spotify
    description: The Spotify web API
    tags:
      - spotify
      - rest
    annotations:
      # Don't use this annotation, but the placeholder $text instead (see below).
      backstage.io/definition-at-location: 'url:https://raw.githubusercontent.com/APIs-guru/openapi-directory/master/APIs/spotify.com/v1/swagger.yaml'
  spec:
    type: openapi
    lifecycle: production
    owner: spotify@example.com
    definition:
      $text: https://raw.githubusercontent.com/APIs-guru/openapi-directory/master/APIs/spotify.com/v1/swagger.yaml
  ```
- 512d70973: Use the new `UrlReader` in the `CodeOwnersProcessor`.
- 49d70ccab: Remove the `read` argument of `LocationProcessor.processEntity`.
  Instead, pass the `UrlReader` into the constructor of your `LocationProcessor`.
- 440a17b39: The catalog backend UrlReaderProcessor now uses a UrlReader from @backstage/backend-common, which must now be supplied to the constructor.

### Patch Changes

- 3472c8be7: Add codeowners processor
  
  - Add `codeowners-utils@^1.0.2` as a dependency
  - Add `core-js@^3.6.5` as a dependency
  - Added new CodeOwnersProcessor
- Updated dependencies [3a4236570]
- Updated dependencies [e0be86b6f]
- Updated dependencies [f70a52868]
- Updated dependencies [12b5fe940]
- Updated dependencies [5249594c5]
- Updated dependencies [56e4eb589]
- Updated dependencies [e37c0a005]
- Updated dependencies [a768a07fb]
- Updated dependencies [f00ca3cb8]
- Updated dependencies [440a17b39]
  - @backstage/catalog-model@0.2.0
  - @backstage/backend-common@0.2.0
