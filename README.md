# SourceBuilder

A wrapper around `StringBuilder` to make it easier to build source code in source generators.

Supports indentation and code blocks.

## Examples

### Example #1 (using indentation)

Input:
```csharp
var builder = new SourceBuilder();
builder.AppendLine("pubic class User");
builder.AppendLine("{");
builder.AddIndent();
builder.AppendLine("public required int Id { get; set; }");
builder.AppendLine("public required string Name { get; set; }");
builder.RemoveIndent();
builder.AppendLine("}");
```

Output:
```csharp
pubic class User
{
    public required int Id { get; set; }
    public required string Name { get; set; }
}
```

### Example #2 (using code blocks)

Input:
```csharp
var builder = new SourceBuilder();
builder.AppendLine("using System;");
builder.AppendLine();
builder.AppendLine("namespace MyNamespace");
builder.AddCodeBlock(_ =>
{
    builder.AppendLine("public class MyClass");
    builder.AddCodeBlock(_ =>
    {
        builder.AppendLine("public void MyMethod()");
        builder.AddCodeBlock(_ =>
        {
            builder.AppendLine("Console.WriteLine(\"Hello, world!\");");
        });
    });
});
```

Output:
```csharp
using System;

namespace MyNamespace
{
    public class MyClass
    {
        public void MyMethod()
        {
            Console.WriteLine("Hello, world!");
        }
    }
}
```