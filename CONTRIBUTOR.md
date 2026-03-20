# CONTRIBUTOR.md

## Commit messages

Use **Conventional Commits** and include a **scope** in every commit message.

Format:

```text
<type>(<scope>): <description>
```

Examples:

```text
feat(cli): add doctor command
feat(config): support profile selection
fix(resize): skip images already within bounds
docs(readme): clarify uv installation
refactor(output): normalize json result schema
test(doctor): cover missing config handling
```

## Commit style

Prefer small, meaningful commits.

A good commit should:
- represent one coherent change
- have a message that explains the change clearly
- be easy to review and easy to revert

## References

Conventional Commits specification:
- https://www.conventionalcommits.org/en/v1.0.0/
