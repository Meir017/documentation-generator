# Documentation Generator

Generate code examples for your C# API using your C# code, this will ensure that your code examples in your documentation comments are valid.

⚠️ This is an idea for a tool, no implementation yet, Please share your feedback here https://github.com/Meir017/documentation-generator/discussions/1 ⚠️

## Example

for example - 

`ICalculator.cs`:

```csharp
namespace MyService;

public class MyClass
{
    /// <summary>
    /// method summary
    /// <example>
    /// this-will-be-generated
    /// </example>
    /// </summary>
    /// <param name="a">...</param>
    /// <returns
    public int MyMethod(int a, int b);
}
```

`CalculatorDocs.cs`:

```csharp
public class CalculatorDocs
{
    public void TheMethodAdd()
    {
        var theClass = new MyClass();
#region M:MyService.MyClass.MyMethod(System.Int32,System.Int32);
        var result = theClass.MyMethod(1, 2);
        Assert.Equal(result, 42);
#endregion
    }
}
```

The idea is to wrap the example code with `#region ID` and `#endregion`.
where the ID follows the format https://github.com/dotnet/csharpstandard/blob/standard-v6/standard/documentation-comments.md#d42-id-string-format  

will modify the source code's comment:

```csharp
namespace MyService;

public class MyClass
{
    /// <summary>
    /// method summary
    /// <example>
    /// var result = theClass.MyMethod(1, 2);
    /// Assert.Equal(42, result);
    /// </example>
    /// </summary>
    /// <param name="a">...</param>
    /// <returns
    public int MyMethod(int a, int b);
}
```

## Installation

```bash
dotnet tool install DocumentationGenerator.Tool --global
```

## Usage:

using the dotnet tool `documentation-generator`

```bash
dotnet documentation-generator --source-code ./src/Component --documentation ./docs/Component.Docs
```

## Sample project structure

- src
  - Component
- docs
  - Component.Docs
