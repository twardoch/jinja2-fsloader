# jinja2-fsloader Improvement Plan

## Overview

This document outlines a comprehensive plan to modernize and improve the jinja2-fsloader codebase. The goal is to make the library more maintainable, feature-rich, and aligned with modern Python development practices.

## Current State Analysis

### Strengths
- Simple and focused implementation
- Good test coverage for core functionality
- Clear separation of concerns
- Supports various filesystem backends through PyFilesystem2

### Weaknesses
- Still supporting Python 2.7 (EOL since January 2020)
- Using deprecated Travis CI for continuous integration
- Lacking type hints for better IDE support and type safety
- Using legacy packaging configuration (setup.cfg instead of pyproject.toml)
- Limited documentation and examples
- No async support for modern web frameworks
- No built-in caching mechanism

## Detailed Improvement Steps

### Phase 1: Infrastructure Modernization

#### 1.1 Drop Python 2.7 Support
- **Rationale**: Python 2.7 reached end-of-life in January 2020. Maintaining compatibility adds complexity and prevents using modern Python features.
- **Steps**:
  1. Remove Python 2 compatibility code (e.g., `_to_unicode` function)
  2. Update setup.cfg to require Python >= 3.8
  3. Remove Python 2.7 from test matrix
  4. Update code to use Python 3 idioms (f-strings, pathlib, etc.)

#### 1.2 Migrate from Travis CI to GitHub Actions
- **Rationale**: Travis CI has become less reliable for open source projects, while GitHub Actions is well-integrated and free for public repositories.
- **Steps**:
  1. Create `.github/workflows/tests.yml` for running tests
  2. Create `.github/workflows/release.yml` for automated releases
  3. Set up matrix testing for Python 3.8, 3.9, 3.10, 3.11, 3.12
  4. Add OS matrix (Ubuntu, macOS, Windows)
  5. Remove `.travis.yml`

#### 1.3 Adopt Modern Packaging Standards
- **Rationale**: pyproject.toml is the modern standard for Python packaging, providing better dependency resolution and build isolation.
- **Steps**:
  1. Create `pyproject.toml` with build-system requirements
  2. Migrate metadata from setup.cfg to pyproject.toml
  3. Use setuptools with declarative configuration
  4. Add development dependencies group
  5. Configure tools (black, flake8, mypy, pytest) in pyproject.toml

### Phase 2: Code Quality Improvements

#### 2.1 Add Type Hints
- **Rationale**: Type hints improve code maintainability, enable better IDE support, and help catch bugs early.
- **Steps**:
  1. Add type hints to all public APIs in `__init__.py`
  2. Create `py.typed` marker file
  3. Add mypy to development dependencies
  4. Configure mypy for strict type checking
  5. Add type checking to CI pipeline

#### 2.2 Implement Comprehensive Linting and Formatting
- **Rationale**: Consistent code style reduces cognitive load and prevents style-related discussions in PRs.
- **Steps**:
  1. Add black for code formatting
  2. Add isort for import sorting
  3. Configure flake8 with appropriate plugins
  4. Add pre-commit hooks for automatic formatting
  5. Format entire codebase with black

#### 2.3 Enhance Error Handling
- **Rationale**: Better error messages help users debug issues more quickly.
- **Steps**:
  1. Create custom exception classes for different error scenarios
  2. Add validation for template paths
  3. Provide helpful error messages with context
  4. Add proper logging support

### Phase 3: Feature Enhancements

#### 3.1 Add Caching Support
- **Rationale**: Template compilation is expensive; caching can significantly improve performance.
- **Steps**:
  1. Implement LRU cache for compiled templates
  2. Add cache size configuration option
  3. Support cache invalidation based on file modification time
  4. Add cache statistics for monitoring

#### 3.2 Implement Async Support
- **Rationale**: Modern web frameworks like FastAPI use async/await; async template loading can improve performance.
- **Steps**:
  1. Create `AsyncFSLoader` class
  2. Implement async versions of `get_source` and `list_templates`
  3. Ensure compatibility with async filesystem operations
  4. Add comprehensive async tests

#### 3.3 Add Template Preprocessing
- **Rationale**: Allow users to transform templates before compilation (e.g., for i18n, minification).
- **Steps**:
  1. Add preprocessor callback parameter
  2. Implement common preprocessors (whitespace removal, comment stripping)
  3. Document preprocessing API
  4. Add examples for custom preprocessors

### Phase 4: Documentation and Community

#### 4.1 Improve Documentation
- **Rationale**: Good documentation reduces support burden and increases adoption.
- **Steps**:
  1. Convert README.rst to README.md for better GitHub rendering
  2. Add comprehensive examples directory
  3. Create documentation site using Sphinx or MkDocs
  4. Add API reference documentation
  5. Create cookbook with common patterns

#### 4.2 Add Contributing Guidelines
- **Rationale**: Clear contribution guidelines encourage community participation.
- **Steps**:
  1. Create CONTRIBUTING.md with development setup instructions
  2. Add CODE_OF_CONDUCT.md
  3. Create issue templates for bugs and features
  4. Add pull request template
  5. Document release process

### Phase 5: Testing and Quality Assurance

#### 5.1 Expand Test Coverage
- **Rationale**: Comprehensive tests prevent regressions and enable confident refactoring.
- **Steps**:
  1. Add tests for edge cases and error conditions
  2. Add integration tests with real filesystems
  3. Add performance benchmarks
  4. Achieve >95% code coverage
  5. Add mutation testing

#### 5.2 Security Improvements
- **Rationale**: Template engines can be vectors for security vulnerabilities.
- **Steps**:
  1. Add security scanning to CI (CodeQL, Bandit)
  2. Implement path traversal protection
  3. Add template sandboxing options
  4. Document security best practices
  5. Set up dependency vulnerability scanning

## Implementation Timeline

- **Week 1-2**: Phase 1 (Infrastructure Modernization)
- **Week 3-4**: Phase 2 (Code Quality Improvements)
- **Week 5-6**: Phase 3.1-3.2 (Caching and Async Support)
- **Week 7**: Phase 3.3 (Template Preprocessing)
- **Week 8**: Phase 4 (Documentation)
- **Week 9-10**: Phase 5 (Testing and Security)

## Success Metrics

1. All tests passing on Python 3.8-3.12
2. >95% code coverage
3. Type hints for 100% of public APIs
4. Performance improvement of >50% with caching enabled
5. Documentation site with >10 example use cases
6. Zero security vulnerabilities in dependencies

## Risks and Mitigation

1. **Breaking changes for existing users**: Provide migration guide and deprecation warnings
2. **Increased maintenance burden**: Set up automation and clear contribution guidelines
3. **Performance regression**: Add benchmarks to CI to catch regressions
4. **Scope creep**: Prioritize improvements based on user feedback

## Conclusion

This improvement plan will transform jinja2-fsloader into a modern, well-maintained library that meets the needs of contemporary Python developers. The phased approach ensures that improvements can be delivered incrementally while maintaining stability.