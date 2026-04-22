# Contributing to Vestigo

Thank you for your interest in contributing. Vestigo is an open source project and contributions of all kinds are welcome -- bug reports, documentation improvements, code, and feature ideas.

---

## Code Style

**Rust**
- Run `cargo fmt` before committing. The project uses default rustfmt settings.
- Run `cargo clippy` and address any warnings before submitting a PR.
- Unsafe code must be documented with a comment explaining why it is necessary.

**TypeScript / React**
- Prettier is configured for the frontend. Run `npm run format` before committing.
- Components live in `src/components/`. Keep them small and single-purpose.
- Avoid `any` types. If you need to work around a type, add a comment explaining why.

---

## Pull Request Guidelines

- Keep PRs focused. One feature or fix per PR.
- Write a clear description of what the PR does and why.
- Reference any related issues with `Fixes #123` or `Closes #123` in the PR description.
- If the PR adds a new integration or external API call, document the required API key/scope in the PR description and update the README if applicable.
- PRs that add dependencies must include a brief justification for the new crate or package.

---

## Reporting Bugs

Open an issue on GitHub with:
- A clear description of the problem
- Steps to reproduce
- Expected behaviour vs actual behaviour
- Your OS and Vestigo version
- Any relevant error output from the terminal or the Tauri console

---

## Security Issues

If you discover a security vulnerability in Vestigo, please do not open a public issue. Contact the maintainers directly via the email listed on the GitHub profile. We will respond as quickly as possible and coordinate a fix before any public disclosure.

---

## Feature Requests

Open an issue with the label `enhancement`. Describe the use case, not just the feature -- it helps to understand the problem being solved. Check the [ROADMAP.md](ROADMAP.md) first to see if it is already planned.

---

## License

By contributing to Vestigo, you agree that your contributions will be licensed under the MIT License.
