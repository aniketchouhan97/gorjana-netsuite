# NetSuite GitHub Actions Deployment Guide

This repository is configured to automatically deploy SuiteCloud projects to NetSuite using GitHub Actions and M2M (Machine-to-Machine) OAuth 2.0.

## 1. Setting up GitHub Secrets

To allow GitHub to authenticate with your NetSuite account, you need to add the following **Repository Secrets**:

1. Go to your GitHub Repo -> **Settings** -> **Secrets and variables** -> **Actions**
2. Click **New repository secret** and add the following:

| Secret Name | Description |
| --- | --- |
| `NS_ACCOUNT_ID` | Your NetSuite Account ID (e.g., `1234567_SB1` for sandbox, `1234567` for production). |
| `NS_CERTIFICATE_ID` | The Certificate ID generated in NetSuite (this corresponds to the `KEY_ID` in your `clientId.js`). |
| `NS_PRIVATE_KEY` | The full contents of your `private.pem` file. **Make sure to include `-----BEGIN RSA PRIVATE KEY-----` and the end tags!** |

---

## 2. How to Deploy

The deployment workflow (`.github/workflows/deploy.yml`) is configured to run automatically in two ways:

### Method A: Pushing to the Main Branch (Default)
Anytime you push code or merge a Pull Request into the `main` branch, GitHub Actions will automatically start a deployment.

```bash
git add .
git commit -m "Your commit message"
git push origin main
```

### Method B: Pushing a Tag (For New Versions)
When you are ready to cut a new release or version, you can create a Git tag (e.g., `v1.0.0`) and push it. This will also trigger the deployment script.

```bash
# 1. Create a tag for your release
git tag v1.0.0

# 2. Push the tag to GitHub
git push origin v1.0.0
```

### Method C: Manual Dispatch
You can manually trigger the deployment from the GitHub website at any time without committing new code.

1. Go to the **Actions** tab in your GitHub repository.
2. Under "Workflows" on the left, click **Deploy to NetSuite**.
3. On the right side, click the **Run workflow** dropdown.
4. Select the branch (usually `main`) and click **Run workflow**.
