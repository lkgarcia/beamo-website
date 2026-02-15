### Overview
I would like to request the creation of a GitHub Actions workflow that automates the deployment of our website to GitHub Pages. This will improve our deployment process and make it more efficient.

### Workflow Details
- **Trigger:** The workflow should be automatically triggered when a pull request is merged into the `main` branch.
- **Steps:**
  1. Checkout the repository.
  2. Set up Node.js.
  3. Install dependencies using the existing `deploy` script in the `package.json` file.
  4. Execute `npm run deploy`.

### Permissions
Ensure that GitHub Actions has the necessary permissions:
- **Read and write permissions** under Repository Settings > Actions > General.

### GitHub Pages Settings
Confirm that GitHub Pages is enabled and serving from the `gh-pages` branch in the repository settings.

### Additional Notes
This workflow will streamline our deployment process and help maintain consistency across our releases.