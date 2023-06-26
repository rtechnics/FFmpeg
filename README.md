# FFmpeg Windows/NuGet build system powered by GitHub Actions

## About
- `.github/workflows/build.yml` - Builds the FFmpeg git submodule every time a tag is added.
- `.github/workflows/update-ffmpeg.yml` - Checks for a new FFmpeg release tag daily and updates the submodule and adds a new release tag, triggering the Build workflow.

## How to configure
1. Enable the GitHub Actions workflows
2. A personal GitHub user token is used for the workflows to trigger each other. You will need to create a personal access token in the GitHub Developer Settings menu with the `repo` permissions. Then, add this token in your repo's Secrets and variables Settings menu as a secret with the name `PUSH_TOKEN`.
3. Update `ffmpeg.csproj` to the values that you want
4. In `.github/workflows/build.yml`, modify the `Download prebuilt OpenSSL binaries` step to your OpenSSL build repo (if the repo is private, ensure that in its GitHub Actions settings, Access is set to Accessible.

## How to use the NuGet package
1. In your account's Developer Settings menu, create a personal access token with the `read:packages` permission
2. Add your GitHub NuGet repo to your dotnet project - `https://nuget.pkg.github.com/rtechnics/index.json` - and log in using the access token. You can do this using the Visual Studio GUI or the command line:
`dotnet nuget add source --username <your-github-username-here> --password <your-github-access-token-here> --store-password-in-clear-text --name github "https://nuget.pkg.github.com/rtechnics/index.json"`
3. Download the package either using Visual Studio or `dotnet add package ffmpeg`
