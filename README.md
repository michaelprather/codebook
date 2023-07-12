# Codebook
An opinionated coding guide

Contents:
- [Formatting](#formatting)
- [Code Structure](#code-structure)
- [Dev Ops](#dev-ops)

## Formatting

### Linting

- Use single quotes because they are faster to write

### Casing

- Name constants using uppercase snake case
- Name classes using PascalCase
- Be consistent with casing for everything else with preference towards snake case because it's easiest to replace underscores.

### File naming

- Frontend apps: Names of views should always be appended with "View"
- Components that are one word or that share the same name as a native HTML element should be prefixed (ex. prefix Vue components with "V")
- Singleton component names should be prefixed with "App" or "The"

## Code structure

### Orthogonality (self-containment)

- Frontend apps: Whenever possible, the following should always be done in views and not in components.
  - Abstracted (API) calls
  - Page routing
  - Reading/writing to state

### RESTful APIs

- Use consistent nomenclature when referring to methods. The nomenclature below is borrowed from Django Rest Framework.

| Method    | Name     |
| --------- | -------- |
| `POST`    | create   |
| `GET` 1   | retrieve |
| `GET` *n* | list     |
| `DELETE`  | destroy  |
| `PATCH`   | update   |
| `PUT`     | replace  |

- Frontend apps: API calls should never be made directly from components or views.
- Use functions to set/unset tokens instead of injecting tokens for each call.

### State

- Frontend apps: use a store only when either: 1) data must persist across views, or 2) as a global event listener (ex. toasts)

### Composables

- Use composable when logic, not data, is shared across components.

### Errors

- Frontend apps: Never display raw error messages to users. It's likely too technical and may contain sensitive details.
- Backend apps: Never return error messages containing potentially sensitive information as it is exposed by the browser.

## Dev Ops

### Environment variables

- Maintain a list of supported environment variables (without values) in a `.env.sample` file
- For security reasons, never store environment variable values in version control

### Continuous development

- Use a tool like Dependabot to keep project dependencies up-to-date
- Frontend apps: console log the app version for troubleshooting purposes

### Branching

- Branches for new features and bug fixes should be branched off of `main`
- Hotfixes should be branched off of `production` but merged into both `main` and `production`.
- Dev and/or staging code should live in `dev` and `staging` branches.

### Testing

- Frontend apps: store unit test files in the same directory as the file it tests.
- Frontend apps: exclude test and other dev-only files and dependencies from production builds.
- Standardize mocking of app data types using randomized data from tools like Faker whenever possible.

### Releases

- Tag each release
- Track meaningful changes, most especially breaking changes, in a `CHANGELOG.md` file.
