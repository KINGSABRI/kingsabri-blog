# Executing C\# Assembly in Memory Using Assembly.Load\(\)

Here is a simple code to load a C\# assembly \(exe or dll\) in memory from C\#/

{% tabs %}
{% tab title="C\#" %}
```csharp
using System;
using System.IO;
using System.Reflection;

namespace AssemblyLoader
{
    class Program
    {
        static void Main(string[] args)
        {

            Byte[] fileBytes = File.ReadAllBytes("C:\\Tools\\JustACommandWithArgs.exe");

            string[] fileArgs = { "arg1", "arg2", "argX" };

            ExecuteAssembly(fileBytes, fileArgs);
        }

        public static void ExecuteAssembly(Byte[] assemblyBytes, string[] param)
        {
            // Load the assembly
            Assembly assembly = Assembly.Load(assemblyBytes);
            // Find the Entrypoint or "Main" method
            MethodInfo method = assembly.EntryPoint;
            // Get the parameters
            object[] parameters = new[] { param };
            // Invoke the method with its parameters
            object execute = method.Invoke(null, parameters);
        }
    }
}
```
{% endtab %}

{% tab title="Result" %}
```
PS C:\Users\KING> AssemblyLoader.exe
Hi arg1!
Hi arg2!
Hi argX!
```
{% endtab %}
{% endtabs %}



## References

{% embed url="https://www.csharpcodi.com/csharp-examples/System.Reflection.Assembly.Load\(byte\[\]\)/" %}

{% embed url="https://www.csharpcodi.com/vs2/3972/hanzoInjection/src/Program.cs/" %}

{% embed url="https://exord66.github.io/csharp-in-memory-assemblies" %}



