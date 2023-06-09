# ✨ OpenAI GitHub Action - Completions + Chat

Github Action to easily integrate OpenAI's API (Chat+Completions) into workflows. Empower your project with OpenAI's language model for intelligent response generation in just a few steps.

This project is a wrapper around the [OpenAI's NodeJS SDK](https://github.com/openai/openai-node).

## Usage

In your Github Actions workflow, add the following YAML code to utilize the action:

```yaml
- name: OpenAI
  uses: Just-Moh-it/openai@v0.0.1
  with:
    openai-api-key: ${{ secrets.OPENAI_API_KEY }}
    openai-mode: "completion"
    openai-params: '{"prompt":"Repeat after me, Hello World: }}", "model": "text-davinci-003"}'
  id: openai
```

## Inputs

The action requires the following inputs:

- `openai-api-key`: Your OpenAI API key. This should be stored as a secret in your GitHub repository. \[**Required: Yes**\]
- `openai-mode`: The mode of the OpenAI API to use. Can be `completion` or `chat`. \[**Required: Yes**\]
- `openai-params`: A JSON string with parameters to send to the OpenAI API \[**Required: Yes**\]. Check out the params here:
  - `completion` mode: [OpenAI API documentation](https://beta.openai.com/docs/api-reference/completions/create) for more information.
  - `chat` mode: [OpenAI API documentation](https://beta.openai.com/docs/api-reference/chat/create) for more information.

## Outputs

The output of the action is a response generated by OpenAI API. You can access the response by logging the output of the action.

```yaml
${{ steps.openai.outputs.completion }}
```

## Quick start

1. Create a new Github repository or navigate to an existing one.
2. Go to the "Actions" tab and click on "Set up a workflow yourself".
3. Copy and paste the code below into the workflow file.

```yml
name: Test output of OpenAI on Push
on:
  push:
    branches:
      - main
jobs:
  openai-chat:
    name: OpenAI Chat Completion
    runs-on: ubuntu-latest
    environment: Production
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v1
        with:
          node-version: 16
      - name: OpenAI
        uses: Just-Moh-it/openai@v0.0.1
        with:
          openai-api-key: ${{ secrets.OPENAI_API_KEY }}
          openai-mode: "completion"
          openai-params: '{"prompt":"Repeat after me, Hello World: }}", "model": "text-davinci-003"}'
        id: openai
      - name: Print
        run: |
          echo  "${{ steps.openai.outputs.completion }}"
```

4. Go to the "Settings" tab and click on "Secrets".
5. Add a new secret named `OPENAI_API_KEY` with your OpenAI API key.
6. Use the following code to access the response generated by OpenAI API.
7. Commit the changes to your repository.

## Limitations

The action is limited by the usage limits of your OpenAI API key.

## Support

If you have any questions or need help with this Github Action, please open an issue/discussion in the repository.

## Contributing

If you find any bugs or have suggestions for improvements, feel free to open an issue or create a pull request.

## Credits

The project is a fork of [riccardolinares/openai-commit](https://github.com/riccardolinares/openai-commit). We thank the author for their work.
