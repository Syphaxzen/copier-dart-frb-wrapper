# Changelog

All notable changes to this template will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2025-01-28

### Added

#### Core Features
- Copier template for Flutter Rust Bridge (FRB) projects
- Flutter Rust Bridge integration for type-safe Dart-Rust bindings
- Dart Native Assets build hook for automatic library download
- SHA256 checksum verification for supply chain security
- Retry logic for network operations with exponential backoff

#### Cross-Platform Support
- Android (arm64-v8a, armeabi-v7a, x86_64)
- iOS (arm64 device, arm64/x86_64 simulator)
- macOS (arm64, x86_64)
- Linux (x64, arm64)
- Windows (x64)
- Web/WASM (optional via `enable_web`)

#### GitHub Actions Workflows
- `test.yml` / `test-reusable.yml` - Multi-platform testing with coverage
- `build-<package>.yml` - Native library builds for all platforms
- `publish.yml` - pub.dev publishing with OIDC + GitHub Release creation
- `check-<package>-updates.yml` - Automated upstream version checking
- Rust security audit via `cargo-audit`
- Coverage badge support via GitHub Gist

#### Template Variables
- Required: `package_name`, `description`, `native_library_name`, `github_repo`, `native_repo`
- Rust config: `crate_name`, `rust_edition`, `rust_version`, `frb_version`
- Upstream crate: `upstream_crate`, `upstream_version`, `strip_version_prefix`
- Flutter/Dart: `flutter_version`, `dart_sdk_version`, `flutter_sdk_version`
- Android: `android_min_sdk`, `android_compile_sdk`, `android_ndk_version`
- Feature flags: `enable_web`, `enable_claude`
- Metadata: `license`, `topics`

#### Developer Experience
- FVM (Flutter Version Manager) integration with Windows support
- Makefile with common commands (setup, codegen, build, test, coverage)
- Claude Code skills for generated projects (optional via `enable_claude`)
- Comprehensive documentation templates (README, CONTRIBUTING, SECURITY, CHANGELOG, CLAUDE.md)
- Automatic example app creation (Flutter GUI + CLI)
- Variable validators with helpful error messages
- Jinja2 templating with case conversion filters (jinja2-strcase)

#### Generated Project Features
- Pre-configured `analysis_options.yaml` with recommended lints
- GitHub Actions setup instructions in README
- Coverage badge setup guide
- Security policy template
- Git hooks for pre-commit checks

[Unreleased]: https://github.com/djx-y-z/copier-dart-frb-wrapper/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/djx-y-z/copier-dart-frb-wrapper/releases/tag/v1.0.0
