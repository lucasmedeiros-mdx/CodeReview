## Pull Requests

- **DO** give PRs short-but-descriptive names (e.g. "Improve code coverage for System.Console by 10%", not "Fix #1234")
- **DO** refer to any related TFS Items or relevant issues.
- **DO** tag any users that should know about and/or review the change.
- **DO** ensure each commit successfully builds. The entire PR must pass all tests in the Continuous Integration (CI) system before it'll be merged.
- **DO** address PR feedback in an additional commit(s) rather than ammending the existing commits, and only rebase/squash them when necessary. This makes it easier for reviewers to track changes. If necessary, squashing should be handled by the merger using the "squash and merge" feature, and should only be done by the contributor upon request.
- **DO NOT** fix merge conflicts using a merge commit. Prefer *git rebase*.
- **DO NOT** mix independent, unrelated changes in one PR. Separate real product/test code changes from larger code formatting/dead code removal changes. Separate unrelated fixes into separate PRs, especially if they are in different assemblies.

Based on [.NET Core Contributing Guide](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/contributing.md)
