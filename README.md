# gh-merge-base-next Action

A GitHub Action that automatically finds the next commit on the first-parent path from merge-base.

## Overview

This action calculates the merge-base from specified base and head refs, then returns the SHA and depth of the next commit on the first-parent path from that merge-base.

## Usage

### Basic Usage

```yaml
- name: Find next commit from merge-base
  id: merge-base-next
  uses: srz-zumix/merge-base-next-action@v1
  with:
    base: 'main'
    head: 'feature/branch'

- name: Use the result
  run: |
    echo "Next commit SHA: ${{ steps.merge-base-next.outputs.sha }}"
    echo "Depth from merge-base: ${{ steps.merge-base-next.outputs.depth }}"
```

### Specifying a Different Repository

```yaml
- name: Find next commit from merge-base in another repo
  id: merge-base-next
  uses: srz-zumix/merge-base-next-action@v1
  with:
    repository: 'owner/repo'
    repo-token: ${{ secrets.GITHUB_TOKEN }}
    base: 'main'
    head: 'develop'
```

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `repo-token` | The GitHub token used to manage labels | No | `${{ github.token }}` |
| `repository` | The repository in the format owner/repo. If not provided, the repository of the workflow run is used | No | `''` |
| `base` | The base ref (branch or commit SHA) to find the merge base from | Yes | - |
| `head` | The head ref (branch or commit SHA) to find the merge base to | Yes | - |

## Outputs

| Name | Description |
|------|-------------|
| `sha` | The SHA of the next commit on the first-parent path from the merge-base |
| `depth` | The number of commits between the merge-base and the next commit on the first-parent path |

## License

This project is licensed under the [MIT License](LICENSE).

## Author

[srz-zumix](https://github.com/srz-zumix)
