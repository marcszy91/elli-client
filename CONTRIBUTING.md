# Contributing to Elli Client

Thank you for your interest in contributing!

## Development Setup

1. Clone the repository:
```bash
git clone https://github.com/marcszy91/elli-client
cd elli-client
```

2. Create a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

3. Install development dependencies:
```bash
pip install -e ".[dev]"
```

4. Set up environment variables:
```bash
# Copy template and add your credentials
cp .env.template .env
# Edit .env and add your ELLI_EMAIL and ELLI_PASSWORD
```

5. Install pre-commit hooks:
```bash
pre-commit install --install-hooks
```

## Code Quality

This project uses:
- **Black** for code formatting
- **isort** for import sorting
- **Flake8** for linting

Run checks before committing:

```bash
# Format code
black src/
isort src/

# Lint
flake8 src/
```

Or use pre-commit:

```bash
pre-commit run --all-files
```

## Commit Message Convention

This project uses [Conventional Commits](https://www.conventionalcommits.org/).

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- **feat**: New feature (triggers minor version bump)
- **fix**: Bug fix (triggers patch version bump)
- **docs**: Documentation only
- **style**: Code style changes (formatting, etc.)
- **refactor**: Code refactoring (triggers patch version bump)
- **perf**: Performance improvements (triggers patch version bump)
- **test**: Adding or updating tests
- **build**: Build system changes
- **ci**: CI configuration changes
- **chore**: Other changes (dependencies, etc.)
- **revert**: Revert a previous commit

### Examples

```bash
# New feature
feat: add support for scheduled charging

# Bug fix
fix: handle timeout errors correctly

# Documentation
docs: update API reference

# Breaking change (triggers major version bump)
feat!: change authentication method

BREAKING CHANGE: The login method now requires an API key
```

### Scope (Optional)

You can add a scope to provide more context:

```bash
feat(api): add new endpoint for charging history
fix(auth): resolve token refresh issue
docs(readme): update installation instructions
```

## Pull Request Process

1. Create a feature branch from `main`:
```bash
git checkout -b feature/my-new-feature
```

2. Make your changes and commit using conventional commits

3. Push your branch:
```bash
git push origin feature/my-new-feature
```

4. Create a Pull Request on GitHub

5. Wait for CI checks to pass:
   - Code formatting (Black, isort)
   - Linting (Flake8)
   - Commit message validation
   - Tests (when implemented)

6. Request review

## Automated Releases

Releases are fully automated using semantic-release:

- Merging to `main` triggers the release workflow
- Commit messages determine the version bump:
  - `feat:` → minor version (1.0.0 → 1.1.0)
  - `fix:`, `refactor:`, `perf:` → patch version (1.0.0 → 1.0.1)
  - `feat!:` or `BREAKING CHANGE:` → major version (1.0.0 → 2.0.0)
  - `docs:`, `chore:`, `ci:` → no release

- CHANGELOG is automatically generated
- GitHub Release is automatically created
- Package is automatically published to PyPI

## Questions?

Open an issue on [GitHub](https://github.com/marcszy91/elli-client/issues).
