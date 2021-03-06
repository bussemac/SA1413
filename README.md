SA1413 https://github.com/DotNetAnalyzers/StyleCopAnalyzers rule as a stand-alone Roslyn Analyzer.

[![Build status](https://ci.appveyor.com/api/projects/status/qoqatl4nj8ekq61u?svg=true)](https://ci.appveyor.com/project/krk/sa1413)
[![NuGet](https://img.shields.io/nuget/v/RoslynAnalyzers.SA1413.svg?style=plastic)]()

# SA1413

<table>
<tr>
  <td>TypeName</td>
  <td>SA1413UseTrailingCommasInMultiLineInitializers</td>
</tr>
<tr>
  <td>CheckId</td>
  <td>SA1413</td>
</tr>
<tr>
  <td>Category</td>
  <td>Maintainability Rules</td>
</tr>
</table>

:memo: This rule is new for StyleCop Analyzers, and was not present in StyleCop Classic.

## Cause

The last statement in a multi-line C# initializer or list is missing a trailing comma.

### Rationale

This rule is specifically designed to work well with the most widely used source control systems as an aid to long-term
code review. By placing a comma on the last line of a multi-line sequence, developers who append an item to the list or
reorder the list at some point in the future will not need to modify any more lines than absolutely necessary for the
change. As a result, the size of the subsequent code review is minimized and focused, and tools like **git blame**
continue to show the original author and commit for the item that was previously last in the list.

## Rule description

A violation of this rule occurs when the last statement of a C# initializer or list is missing a trailing comma.

For example, the following code would generate one instance of this violation:

```csharp
var x = new Barnacle
{
    Age = 100,
    Height = 0.2M,
    Weight = 0.88M
};
```

The following code would not produce any violations:

```csharp
var x = new Barnacle
{
    Age = 100,
    Height = 0.2M,
    Weight = 0.88M,
};
```

This diagnostic is also reported for other forms of comma-separated list, such as enum members.

## How to fix violations

To fix a violation of this rule, add a trailing comma to the last statement in the initializer.

## How to suppress violations

```csharp
[SuppressMessage("StyleCop.CSharp.MaintainabilityRules", "SA1413:UseTrailingCommasInMultiLineInitializers", Justification = "Reviewed.")]
```

```csharp
#pragma warning disable SA1413 // UseTrailingCommasInMultiLineInitializers
#pragma warning restore SA1413 // UseTrailingCommasInMultiLineInitializers
```
