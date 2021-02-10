# Executing C\# Assembly in Memory Using Assembly.LoadFile\(\)



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

            string filePath = "C:\\Tools\\JustACommandWithArgs.exe";

            string[] fileArgs = { "arg1", "arg2", "argX" };

            ExecuteAssemblyLoadFile(filePath, fileArgs);
        }

        // Load and execute assembly from path
        //   - Accept only local file path
        public static void ExecuteAssemblyLoadFile(string assemblyPath, string[] param)
        {
            Console.WriteLine("[*] Using Assembly.LoadFile:");

            try
            {
                // Load the assembly
                Assembly assembly = Assembly.LoadFile(assemblyPath);
                // Find the Entrypoint or "Main" method
                MethodInfo method = assembly.EntryPoint;
                // Get the parameters
                object[] parameters = new[] { param };
                // Invoke the method with its parameters
                object execute = method.Invoke(null, parameters);
            } 
            catch (Exception e)
            {
                Console.WriteLine(e);
            }
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

