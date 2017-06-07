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

### Layout Guidelines

The general rule to follow is "use Visual Studio defaults".
1. If a file happens to differ in style from these guidelines (e.g. private members are named `m_member` rather than `_member`), the existing style in that file takes precedence.
1. **DO** use Allman style braces, where each brace begins on a new line. A single line statement block can go without braces but the block must be properly indented on its own line and it must not be nested in other statement blocks that use braces.
1. **DO** use four spaces of indentation (no tabs).
1. **DO** always specify the visibility, even if it's the default (i.e. `private string _foo` not `string _foo`). Visibility should be the first modifier (i.e. `public abstract` not `abstract public`).
1. **DO** specify Namespace imports at the top of the file, outside of namespace declarations and sorted alphabetically. Per [StyleCop rule](http://stylecop.soyuz5.com/SA1210.html), *System* namespaces should be placed before other namespaces.
1. **DO NOT** use more than one empty line at any time. For example, do not have two blank lines between members of a type.
1. **DO NOT** use extra spaces. For example avoid `if (someVar == 0)...`, where the dots mark the spurious extra spaces. Consider enabling "View White Space (Ctrl+E, S)" if using Visual Studio, to aid detection.
1. **DO NOT** comment out code. It's the tracking system responsibility to keep track of the changes.
1. **AVOID** using *regions*.
1. **DO** place the members in (well-defined order)[http://stylecop.soyuz5.com/Ordering%20Rules.html]. 
   1. Constant fields / Fields
   1. Constructors / Destructors
   1. Delegates / Events
   1. Properties
   1. Methods

Within each of these groups order by access: `public, internal, protected internal, protected, private`. Within each of the    access groups, order by `static`, then `non-static`.

### Naming Guidelines

1. **DO** use `_camelCase` for internal and private fields and use readonly where possible. 
1. **DO** use *PascalCasing* for all public member, type, and namespace names consisting of multiple words. A special case is made for two-letter acronyms in which both letters are capitalized: `IOStream`.
1. **DO** use *camelCasing* for parameter names (`ioStream`).
1. **DO** group extension methods in a class suffixed with *Extensions*.
1. **DO** post-fix asynchronous methods with `Async` or `TaskAsync`. The general convention for methods that return a `Task` or `Task<TResult>` is to post-fix them with `Async`.
1. **DO** provide a meaningful and rich name to methods and classes. This can be tricky.
1. **DO NOT** use abbreviations. For example, use `OnButtonClick` instead of `OnBtnClick`.

### Design Guidelines

1. **DO** use language keywords instead of BCL types (i.e. `int, string, float` instead of `Int32, String, Single`) for both type references as well as method calls (i.e. `int.Parse` instead of `Int32.Parse`)
1. **DO** use `nameof(...)` instead of `"..."` whenever possible and relevant.
1. **DO** use the `var` when the variable type can be implied (`var name = "Lucas"` instead of `string name = "Lucas"` and `var names = new List<string>()` instead of `List<string> names = new List<string>()`).
1. **DO** ensure that each type is a well-defined set of related members, not just a random collection of unrelated functionality.
1. **DO** return an `ICollection<T>` or `IReadOnlyCollection<T>` instead of a concrete collection class.
1. **DO** define parameters as specific as possible. If your member needs a specific piece of data, define the parameters as specific as that and don't take a container object instead.
1. **DO** throw the most specific exception that is appropriate. For example, if a method receives a `null` argument, it should throw `ArgumentNullException` instead of its base type `ArgumentException`.
1. **DO** use using statements instead of fully qualified type names. If you need to prevent name clashing, use a `using` directive to assign an alias.
1. **DO** prefer single (conditional) assignments instead of if-else statements.
1. **DO** use `.Any()` instead of `.Count()` when feasible.
1. **DO** implement classes or interfaces with a single responsibility. If you can't assign a single design pattern to a class, chances are that it is doing more than one thing.
1. **DO** provide at least one type that is an implementation of an interface.
1. **DO** use an interface instead of a base class to support multiple implementations. 
1. **DO** implement methods with a single responsibility.
1. **DO NOT** use this. unless absolutely necessary.
1. **DO NOT** use marker interfaces (interfaces with no members). If you need to mark a class as having a specific characteristic (marker), in general, use a custom attribute rather than an interface.
1. **DO NOT** combine many vaguely related members on the same interface. Separate the members by responsibility, so that callers only need to call or implement the interface related to a particular task.
1. **DO NOT** swallow errors by catching generic exception. Unless you're in a last-change exception handler, avoid catching non specific exception such as `Exception` or `SystemException`.
1. **DO NOT** make explicit comparisons to *true* or *false*.
1. **CONSIDER** defining a struct instead of a class if instances of the type are small and commonly short-lived or are commonly embedded in other objects. `Structs` should be immutable and should not be boxed frequently.
1. **CONSIDER** using object and collection initializer over separated statements.
1. **AVOID** static classes. With the exception of extension method containers, static classes very often lead to badly designed code. They're also very difficult to test in isolation.
1. **AVOID** using named arguments. If you need named arguments to improve the readability of the call to a method, that method is probably doing too much and should be refactored. The exception is when calling a method of some code base you don't control that has a `bool` parameter.
1. **AVOID** code duplication. If the code is used in more than one place, it should probably be extracted to a common place.

### Miscellaneous Guideline

1. **DO** apply a single space before single line comments ([StyleCop](http://stylecop.soyuz5.com/SA1005.html): `// A single-line comment.`).

## Unit Tests

TBD.

## Code Review Checklist

- [ ] **DO** ensure it follows [Pull Request](#pull-requests) standards.
- [ ] **DO** ensure the implementation covers the TFS acceptance criteria or fixes the issue.
- [ ] **DO** verify if it follows [Commit Message's](#commit-messages) convention.
- [ ] **DO** verify if the code is covered by appropriate [Unit Tests](#unit-tests).
- [ ] **DO** ensure the code is compliant with security tools (such as Fortify).
- [ ] **DO** ensure it follows [C# Coding Style](#c-coding-style) guidelines.

### How to not review
- **DO NOT** get emotional.
- **DO NOT** focus on blame.
- **DO NOT** focus on how you would have coded it, instead verify if the code is maintanable/scalable and proficient.
- **AVOID** redesigning the code. Unless that's the specific goal of the PR, the code review is about finding nuggets of information in the code, not about revisiting design decisions.
