# resource-pack-deploy
This is a GitHub Action designed for Minecraft resource packs which will zip up your repository and automatically create a release on commit. This means you can use one universal link in the Spigot setResourcePack function, and merely have to commit to the repository for players to start using your new pack.

Whilst the ideal would be to simply serve the latest version of the repository through using the "Download ZIP" feature, for some reason GitHub decides to put your repository files inside a folder inside of a .zip, which is not a valid resource pack. The flow ensures that so long as your files are at the root of your repository then it will serve a valid resource pack.

Action steps:
- **Trigger on Push to Master Branch:** Initiates the workflow whenever changes are pushed to the master branch.
- **Checkout Code:** Pulls the latest code from the master branch into the workflow environment.
- **Create ZIP File:** Packages the codebase into a ZIP file, including the short commit ID in the file's name for version tracking.
- **Upload ZIP Artifact:** Uploads the created ZIP file as an artifact to the workflow run for later access or download.
- **Create Release:** Automatically generates a new GitHub release, tagged with the current commit SHA, making the ZIP file available in the repository's releases.
- **Upload Release Artifact:** Attaches the ZIP file to the corresponding GitHub release, making it accessible for users to download the latest version.

Setup steps:
1. Create a Personal Access Token (PAT) which has permissions for your repository
2. Add your PAT as a secret variable in the repository with the name "RESOURCE_ZIPPER"

After the first run, your resource pack can then be accessed at this link:
`https://github.com/<username>/<repository>/releases/latest/download/RP.zip`

This will automatically download the latest release which you can serve to players using the setResourcePack function.

For an example of a repository successfully using this flow, see https://github.com/flytegg/ls-christmas-rp.
