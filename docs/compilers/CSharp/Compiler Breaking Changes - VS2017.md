**This document lists known breaking changes in Roslyn 2.0 *(VS2017*) from Roslyn 1\*. *(VS2015)* and native C# compiler *(VS2013 and previous)*.**

<!--
*Breaking changes are formatted with a numerically delineated list so as to allow shorthand numerical references (e.g., "known break #1").

Each entry should include a short description of the breaking change, followed by either a link to the issue describing the full details of the change or the full details inline.*
-->

1. Previously, we would not find a best type among multiple types (for ternary expressions and method type inference) when the types differed only in dynamic-ness and would involve some nesting. For example, we could not find a best type between `KeyValuePair<dynamic, object>` and `KeyValuePair<object, dynamic>`. Starting with VS 2017, we can find a best type (we merge dynamic-ness). In this example, `KeyValuePair<dynamic, dynamic>` is the best type. This can affect overload resolution. For instance, allowing a better overload to be picked, which was previously discarded.   See issues [#12585](https://github.com/dotnet/roslyn/issues/12585), [#14247](https://github.com/dotnet/roslyn/issues/14247), [#14213](https://github.com/dotnet/roslyn/issues/14213), and their corresponding PRs for more details.
