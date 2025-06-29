# jinja2-fsloader TODO List

## Infrastructure Modernization
- [ ] Remove Python 2.7 compatibility code from `__init__.py`
- [ ] Update setup.cfg to require Python >= 3.8
- [ ] Create `.github/workflows/tests.yml` for GitHub Actions CI
- [ ] Create `.github/workflows/release.yml` for automated releases
- [ ] Remove `.travis.yml` file
- [ ] Create `pyproject.toml` with modern packaging configuration
- [ ] Migrate metadata from setup.cfg to pyproject.toml

## Code Quality
- [ ] Add type hints to FSLoader class and all public methods
- [ ] Create `py.typed` marker file for PEP 561 compliance
- [ ] Set up black for code formatting
- [ ] Set up isort for import sorting
- [ ] Configure flake8 for linting
- [ ] Add pre-commit configuration
- [ ] Format entire codebase with black
- [ ] Add mypy for type checking
- [ ] Create custom exception classes for better error handling

## Feature Enhancements
- [ ] Implement LRU cache for compiled templates
- [ ] Add cache configuration options
- [ ] Create AsyncFSLoader class for async support
- [ ] Implement async versions of get_source and list_templates
- [ ] Add template preprocessor support
- [ ] Implement common preprocessors (whitespace removal, comment stripping)

## Documentation
- [ ] Convert README.rst to README.md
- [ ] Create examples/ directory with usage examples
- [ ] Add API reference documentation
- [ ] Create CONTRIBUTING.md
- [ ] Create CODE_OF_CONDUCT.md
- [ ] Add GitHub issue templates
- [ ] Add pull request template
- [ ] Set up documentation site (Sphinx or MkDocs)

## Testing
- [ ] Add tests for edge cases and error conditions
- [ ] Add integration tests with real filesystem backends
- [ ] Add performance benchmarks
- [ ] Achieve >95% code coverage
- [ ] Add security tests for path traversal
- [ ] Set up CodeQL security scanning
- [ ] Add mutation testing with mutmut

## Dependencies and Tools
- [ ] Update minimum PyFilesystem2 version
- [ ] Add development dependencies group in pyproject.toml
- [ ] Configure dependabot for automatic updates
- [ ] Add tools configuration (black, isort, flake8, mypy) to pyproject.toml
- [ ] Set up automated dependency vulnerability scanning

## Release Preparation
- [ ] Update version to 0.4.0-dev
- [ ] Create migration guide for breaking changes
- [ ] Update CHANGELOG.rst with planned changes
- [ ] Tag and release version 0.4.0 after all improvements