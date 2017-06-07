## Pull Requests

- **DO** give PRs short-but-descriptive names (e.g. "Improve code coverage for System.Console by 10%", not "Fix #1234")
- **DO** refer to any related TFS Items or relevant issues.
- **DO** tag any users that should know about and/or review the change.
- **DO** ensure each commit successfully builds. The entire PR must pass all tests in the Continuous Integration (CI) system before it'll be merged.
- **DO** address PR feedback in an additional commit(s) rather than ammending the existing commits, and only rebase/squash them when necessary. This makes it easier for reviewers to track changes. If necessary, squashing should be handled by the merger using the "squash and merge" feature, and should only be done by the contributor upon request.
- **DO NOT** fix merge conflicts using a merge commit. Prefer *git rebase*.
- **DO NOT** mix independent, unrelated changes in one PR. Separate real product/test code changes from larger code formatting/dead code removal changes. Separate unrelated fixes into separate PRs, especially if they are in different assemblies.

Based on [.NET Core Contributing Guide](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/contributing.md)

## Commit Messages

Please format commit messages as follows (based on A Note About Git Commit Messages):

```
Summarize change in 50 characters or less

Provide more detail after the first line. Leave one blank line below the
summary and wrap all lines at 72 characters or less.

If the change fixes an issue, leave another blank line after the final
paragraph and indicate which issue is fixed in the specific format
below.

Fix #42
```

Also do your best to factor commits appropriately, not too large with unrelated things in the same commit, and not too small with the same small change applied N times in N different commits.

## C# Coding Style

The general rule to follow is "use Visual Studio defaults".
1. If a file happens to differ in style from these guidelines (e.g. private members are named `m_member` rather than `_member`), the existing style in that file takes precedence.
1. **DO** use Allman style braces, where each brace begins on a new line. A single line statement block can go without braces but the block must be properly indented on its own line and it must not be nested in other statement blocks that use braces.
1. **DO** use four spaces of indentation (no tabs).
1. **DO** use `_camelCase` for internal and private fields and use readonly where possible. 
1. **DO NOT** use this. unless absolutely necessary.
1. **DO** always specify the visibility, even if it's the default (i.e. `private string _foo` not `string _foo`). Visibility should be the first modifier (i.e. `public abstract` not `abstract public`).
1. **DO** specify Namespace imports at the top of the file, outside of namespace declarations and sorted alphabetically. Per [StyleCop rule](http://stylecop.soyuz5.com/SA1210.html), *System* namespaces should be placed before other namespaces.
1. **DO NOT** use more than one empty line at any time. For example, do not have two blank lines between members of a type.
1. **DO NOT** use extra spaces. For example avoid `if (someVar == 0)...`, where the dots mark the spurious extra spaces. Consider enabling "View White Space (Ctrl+E, S)" if using Visual Studio, to aid detection.
1. **DO** use language keywords instead of BCL types (i.e. `int, string, float` instead of `Int32, String, Single`) for both type references as well as method calls (i.e. `int.Parse` instead of `Int32.Parse`)
1. **DO** use `nameof(...)` instead of `"..."` whenever possible and relevant.
1. **DO** use the `var` when the variable type can be implied (`var name = "Lucas"` instead of `string name = "Lucas"` and `var names = new List<string>()` instead of `List<string> names = new List<string>()`).
1. **DO** use *PascalCasing* for all public member, type, and namespace names consisting of multiple words. A special case is made for two-letter acronyms in which both letters are capitalized: `IOStream`.
1. **DO** use *camelCasing* for parameter names (`ioStream`).
