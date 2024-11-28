# Documentation Generator

Generate code examples for your C# API using your C# code, this will ensure that your code examples in your documentation comments are valid.

⚠️ This is an idea for a tool, no implementation yet ⚠️

Please share your feedback here https://github.com/Meir017/documentation-generator/discussions/1

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
#region public int MyService.MyClass.MyMethod(int a, int b);
        var result = theClass.MyMethod(1, 2);
        Assert.Equal(result, 42);
#endregion
    }
}
```

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
