[![npm version](https://img.shields.io/npm/v/@itrocks/action-pack?logo=npm)](https://www.npmjs.org/package/@itrocks/action-pack)
[![npm downloads](https://img.shields.io/npm/dm/@itrocks/action-pack)](https://www.npmjs.org/package/@itrocks/action-pack)
[![GitHub](https://img.shields.io/github/last-commit/itrocks-ts/action-pack?color=2dba4e&label=commit&logo=github)](https://github.com/itrocks-ts/action-pack)
[![issues](https://img.shields.io/github/issues/itrocks-ts/action-pack)](https://github.com/itrocks-ts/action-pack/issues)
[![discord](https://img.shields.io/discord/1314141024020467782?color=7289da&label=discord&logo=discord&logoColor=white)](https://25.re/ditr)

# action-pack

Bundle to define actions and render views for business objects.

## Installation

```bash
npm i @itrocks/action-pack
```

This single dependency pulls in a coherent stack of packages used to
build action‑based UIs for your domain objects:

- [@itrocks/action](https://github.com/itrocks-ts/action):
  An abstract class for applying actions in your framework, with `@actions` and `@need` decorators for assignment,
- [@itrocks/action-bar](https://github.com/itrocks-ts/action-bar):
  CSS for action button bars with flexible layout and basic styling,
- [@itrocks/action-request](https://github.com/itrocks-ts/action-request):
  Domain-oriented action request with path decoding, business object preloading, and action extracting,
- [@itrocks/data-to-object](https://github.com/itrocks-ts/data-to-object):
  Transforms raw string-based data into a business object with type-safe values,
- [@itrocks/route](https://github.com/itrocks-ts/route):
  Domain-driven route manager with automatic generation, decorators, and static routes,
- [@itrocks/storage](https://github.com/itrocks-ts/storage):
  Transforms model objects to and from storage systems,
- [@itrocks/ux-core](https://github.com/itrocks-ts/ux-core):
  UI component providing a basic it.rocks app container with navigation, title bar, and logout support.

`@itrocks/action-pack` itself does **not** expose additional runtime
APIs. It is a convenience bundle that:

- groups these dependencies under a single versioned package,
- defines a common baseline for building action-based features that wire
  domain objects, routes, and views together.

## Usage

You typically use `@itrocks/action-pack` in a project or library that
defines **actions and views for one or more business objects**.

Instead of depending on each low‑level package individually, add a
single dependency on `@itrocks/action-pack`, then import the concrete
building blocks you need from their dedicated packages.

### Example: code a new action for the [User](https://github.com/itrocks-ts/user) entity

**package.json**:
```json
{
  "dependencies": {
    "@itrocks/action-pack": "latest",
    "@itrocks/user": "latest"
  }
}
```

**src/play-together.ts**:
```ts
import { Action }  from '@itrocks/action'
import { Request } from '@itrocks/action-request'
import { Route }   from '@itrocks/route'
import { User }    from '@itrocks/user'

@Route('/play-together')
export class ListUsers extends Action<User>
{

	async html (request: Request<User>) {
		// Make users play together
		// Build and return an HtmlResponse to display the resulting state
	}

}
```

The only direct dependency of your project is `@itrocks/action-pack`,
yet you can freely use [@itrocks/action](https://github.com/itrocks-ts/action),
[@itrocks/route](https://github.com/itrocks-ts/route),
[@itrocks/action-request](https://github.com/itrocks-ts/action-request), etc. inside your pack.
