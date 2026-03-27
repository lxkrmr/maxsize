# CONTRIBUTOR.md

## Commit messages

Use **Conventional Commits** and include a **scope** in every commit message.

Format:

```text
<type>(<scope>): <description>
```

Examples:

```text
feat(cli): add --max-width flag
fix(resize): preserve aspect ratio when only one limit is set
docs(readme): add shell alias example
refactor(resize): extract targetSize function
test(resize): add table-driven tests for targetSize
chore(deps): upgrade golang.org/x/image
build(go): add go.mod and go.sum
docs(adr): add decision record for Go rewrite
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
