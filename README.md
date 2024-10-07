# WordPress Theme Development Workflow

## Local Development:

### Install Global Dependencies:
Ensure DDEV is installed on your machine.

If you are a Windows user, it is highly recommended to use WSL2 for an optimal development experience. Please follow this [Windows WSL2 DDEV installation guide](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/#wsl2-docker-ce-inside-install-script).

For any other OS, the installation is straightforward. Follow the [DDEV installation guide](https://ddev.readthedocs.io/en/stable/).

### Clone the Repository:
```bash
git clone https://github.com/Repository/WordPressProject.git
```

### Setup DDEV for WordPress:
1. Navigate to the project directory where the *.ddev* directory is located.
   ```bash
   cd /path/to/your/project
   ```

2. Import the database:
   You should have a dump of the project database (e.g., database.sql). To import it:
   1. Place the database dump file in the root of your project (where *.ddev* directory is located).
   2. Run the following command to import the dump file:
   ```bash
   ddev import-db --file=database.sql
   ```

3. Start DDEV:
   ```bash
   ddev start
   ```

Your local development environment is now ready. Access it via `https://yourlocal.ddev.site`.

---

## Git Branching Workflow

We use three main types of branches:

- `main`: Represents the live (production) site.
- `pre-deploy`: A staging branch for final checks before merging into `main`.
- Feature branches: Named as `feature/xyz`, for individual tasks or features.

### Creating Branches:

#### 1. **Main Branch:**
This branch represents the **live site**. Only thoroughly tested and approved changes should be merged here.
```bash
git checkout main
```

#### 2. **Pre-Deploy Branch:**
This branch is used as a **staging environment**. All features or fixes should be merged here for final testing before going to production. **Ensure that `pre-deploy` is always kept up to date with the latest changes from `main` before creating pull requests.**
```bash
git checkout pre-deploy
git pull origin main
```

#### 3. **Feature Branches:**
These branches are created from `main`. They are named following the convention `feature/xyz` but can be used for any type of task, including bug fixes, documentation, refactors, etc.
```bash
git checkout -b feature/ABC-123/short-description
```

---

## Production Deployment:

#### Create a Branch for Your Changes:
Always create a branch from `main`, regardless of the type of task (feature, bugfix, etc.).
```bash
git checkout -b feature/ABC-123/add-new-feature
```

#### Make Changes and Commit:
Make the necessary changes, then commit following the commit-lint format:
```bash
git add .
git commit -m "feat: Add new feature

This feature allows users to do something new.

ABC-123"
```

#### Create a Pull Request:
Push your feature branch and create a pull request against the `pre-deploy` branch. **Ensure that `pre-deploy` is fully updated with the latest changes from `main` before merging your feature branch.**
```bash
git checkout pre-deploy
git pull origin main
```

Once your changes are reviewed and approved, they will be merged into `pre-deploy`.

Notify the team when your pull request is ready.

#### Merging to Main:
After successful testing on the `pre-deploy` branch, the changes can be merged into `main`.

---

<details>
<summary>Example Workflow:</summary>

1. **Create a Feature Branch from Main:**
```bash
git checkout -b feature/ABC-123/add-slider
```

2. **Make Your Changes:**

Edit the code, then commit using the following format:
```bash
git add .
git commit -m "feat: Add slider

Implemented a new slider on the homepage to enhance the user experience.

ABC-123"
```

3. **Push the Feature Branch:**
```bash
git push origin feature/ABC-123/add-slider
```

4. **Create a Pull Request:**
Ensure `pre-deploy` is up to date with `main`:
```bash
git checkout pre-deploy
git pull origin main
```

Then create a pull request to merge `feature/ABC-123/add-slider` into `pre-deploy`. After review and approval, it will be merged into `pre-deploy`.

5. **Merge into Main:**
Once testing is complete on the `pre-deploy` branch, create a pull request to merge your feature branch into `main`.

</details>

---

<details>
<summary>Task Abbreviations:</summary>

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Non-functional changes (formatting, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or correcting tests
- `chore`: Updates to build processes or auxiliary tools

</details>

---

With this structure, you ensure that `pre-deploy` is always synchronized with `main`, preventing any discrepancies during the staging process. This keeps the workflow stable and consistent for deployment.

---

This should work seamlessly with your WordPress and DDEV setup!
