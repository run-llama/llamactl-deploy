# llamactl-deploy

## Update LlamaAgent Deployments

Update a LlamaAgent deployment on LlamaCloud

## Usage

### Inputs

| Name | Desscription | Required | Default |
|------|--------------|----------|---------|
| `llama-cloud-api-key` | API key for LlamaCloud | true | `''` |
| `llama-cloud-project-id` | Project ID for LlamaCloud | true | `''` |
| `deployment-id` | ID of the deployed LlamaAgent | true | `''` |
| `git-reference` | Git reference for deployment update | false | `''` |

### Output

This action does not produce outputs.

### Example Usage

```yml
name: Update LlamaAgent Deployment

on:
  push:
    branches:
        - main

jobs:
  update-deployment:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Update deployment
        uses: run-llama/llamactl-deploy@a883f44eb9512d33714db4b0c545a099b93577ec
        with:
          llama-cloud-api-key: ${{ secrets.LLAMA_CLOUD_API_KEY }}
          llama-cloud-project-id: ${{ secrets.LLAMA_CLOUD_PROJECT_ID }}
          deployment-id: "your-deployment-id"
          git-reference: ${{ github.sha }} # not required
```

## How does it work

This action works by:

- Setting up uv (through `astral-sh/setup-uv`)
- Running `llamactl auth` for token-based authentication to LlamaCloud
- Running `llamactl deployments update <your_deployment_id>` (with the optional `--git-ref <your_git_reference>` if `git-reference` is provided as input)

## References

Get to know more about `llamactl` and LlamaAgents in [the dedicated documentation](https://developers.llamaindex.ai/python/cloud/llamaagents/getting-started/)

## Contributing

Contributions (both for the blog and for the source code) are more than welcome! You can find a detail contribution guide [here](./CONTRIBUTING.md).

## License

The code is provided under the [MIT License](./LICENSE)
