# Roast My Code

Roast My Code is a GitHub Action that uses OpenAI's GPT-4o mini model to rip your code to shreds.
Can't get enough of the mean, snarky comments you can get from Reddit or StackOverflow, or your favorite Senior Software Engineer? Have a bot do it instead.

:warning: WARNING :warning: devs who are currently experiencing impostor syndrome should not attempt to use this action

## Features

- Snarky
- Sarcastic
- Mean
- Vicious

## Setup

1. To use this GitHub Action, you need an OpenAI API key. If you don't have one, sign up for an API key
   at [OpenAI](https://platform.openai.com/signup).

2. Add the OpenAI API key as a GitHub Secret in your repository with the name `OPENAI_API_KEY`. You can find more
   information about GitHub Secrets [here](https://docs.github.com/en/actions/reference/encrypted-secrets).

3. Create a `.github/workflows/main.yml` file in your repository and add the following content:

```yaml
name: Roast My Code

on:
  pull_request:
    types:
      - opened
      - synchronize
permissions: write-all
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3

      - name: Roast My Code
        uses: your-username/roast-my-code@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # The GITHUB_TOKEN is there by default so you just need to keep it like it is and not necessarily need to add it as secret as it will throw an error. [More Details](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret)
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          OPENAI_API_MODEL: "gpt-4o-mini" # Optional: defaults to "gpt-4o-mini"
          exclude: "**/*.json, **/*.md" # Optional: exclude patterns separated by commas
```

4. Replace `your-username` with your GitHub username or organization name where the AI Code Reviewer repository is
   located.

5. Customize the `exclude` input if you want to ignore certain file patterns from being reviewed.

6. Commit the changes to your repository, and AI Code Reviewer will start working on your future pull requests.

## How It Works

The Roast My Code GitHub Action retrieves the pull request diff, filters out excluded files, and sends code chunks to
the OpenAI API. It then generates review comments based on the AI's response and adds them to the pull request.

This is a fork of [freeedcom/ai-codereviewer](https://github.com/freeedcom/ai-codereviewer) and I can't take any credit for how it works. My main contribution was some silly prompt engineering :)

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

Let the maintainer generate the final package (`yarn build` & `yarn package`).

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more information.
