# Overview

Enabling this action on your repository will automatically generate Binary.com production App IDs for any PRs opened to your target branch (specified in your workflow, see `.github/workflows/example.yml`).

**Please ensure you're using a dedicated Binary API token for this**

- To generate a new token, visit https://www.binary.com/en/user/security/api_tokenws.html.

## How it works

The action retrieves all open PRs for the installed repository, it will then compare this list with the created apps on Binary. If any of the apps has a `github_url` which no longer points to an open PR, it will be recycled.

- You may find an example workflow in the `.github/workflows` folder.

### Inputs

- `BINARY_API_TOKEN`: The Binary token to be used to generate App IDs. Please use a dedicated token. See https://www.binary.com/en/user/security/api_tokenws.html (pass as GitHub secret!)
- `BINARY_APP_ID`: The App ID to be used with Binary API to identify the API connection to Binary.
- `GITHUB_TOKEN`: The GitHub token to be used with Octokit to identify the API connection to GitHub.
- `max_retries` (optional): Amount of times to retry in case of error(s) (default: `5`).

### Outputs

- `pr_url`: The URL of the GitHub pull request.
- `pr_number`: The number of the GitHub pull request.
- `app_id`: The newly created or updated Binary App ID.
- `new_branch_name`: The branch name to publish via gh-pages.
- `should_post_comment`: Signals the next step whether to post a comment or not.

## Development

All of the logic is in a single file (`index.js`). After making changes to the file run `npm run build` to compile `dist/index.js` and all `node_modules` into a single JS file (it'll be placed in `dist/index.js`).