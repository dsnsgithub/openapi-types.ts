# @octokit/openapi-types

> [!NOTE]
> `@octokit/openapi-types` is currently outdated because Octokit lacks maintainers for the official Octokit JS repositories.
> This is my attempt at creating a working package.
>
> Issue: https://github.com/dsnsgithub/dsns.dev/issues/6


## Usage

Add to `package.json`:
```json
"overrides": {
    "@octokit/openapi-types": "github:dsnsgithub/openapi-types.ts#main"
},
```

```ts
import { components } from "@octokit/openapi-types";

type Repository = components["schemas"]["full-repository"];
```

## License

[MIT](LICENSE)
