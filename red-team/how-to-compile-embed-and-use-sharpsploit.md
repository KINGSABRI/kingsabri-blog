# How to compile, embed and use SharpSploit

[SharpSploit](https://github.com/cobbr/SharpSploit) is a .NET C\# post-exploitation library written by [@cobbr\_io](https://twitter.com/cobbr_io) that tend to be used to facilitate developing many Windows attack surface and makes an easy to understand APIs \(even for none C\# coders\) to deal with Windows APIs. So first, don't expect an `exe` binary; instead, we are going to compile it to a DLL library to be embedded in our simple binary. Also, I'm expecting that you have already installed Visual Studio 2017, I'm using CommandoVM.

## Compiling SharpSploit to DLL

### Step \#1 \| Clone the repository

```text
git clone https://github.com/cobbr/SharpSploit
```

### Step \#2 \| Open the project from VS2017

Go to **File &gt;&gt; Open** and select `SharpSploit.sln`

![Import SharpSploit project](../.gitbook/assets/image%20%2818%29.png)

### Step \#3 \| Prepare your build

Change the build type to by _release_ instead of _debug_ to avoid exposing metadata and other information about your machine \(e.g. your system path that may include your username\)

![](../.gitbook/assets/image%20%2814%29.png)

Also, SharpSploit is configured to be compiled with .Net version 4.0+, in my case, only .Net 3.5 was installed, so I've changed the project configurations as the following

**Project &gt;&gt; Edit SharpSploit.csproj**

![](../.gitbook/assets/image%20%284%29.png)

Then change `net40` to `net35` in the configuration file and then Press **Ctrl+S** to save

![](../.gitbook/assets/image%20%282%29.png)

### Step \#4 \| Compile the library

Now go to **Build &gt;&gt; Build SharpSploit**

![](../.gitbook/assets/image%20%2819%29.png)

Once this done, you will fine the DLL file under the repository directory in `bin\Release\net35\SharpSploit.dll`

![](../.gitbook/assets/image%20%286%29.png)

## Embedding SharpSploit in a Binary

One of the APIs that SharpSploit provides is `WhoAmI` API which is exactly what you expect. Let's build our console application.

### Step \#1 \| Create a new Project

From **File &gt;&gt; New &gt;&gt; Select Console App \(.Net Framework\)**

![](../.gitbook/assets/image%20%283%29.png)

Our code will be as the follows

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using SharpSploit;


namespace SharpSploitWhoAmI
{
    class Program
    {
        static void Main(string[] args)
        {
            SharpSploit.Credentials.Tokens tokens = new SharpSploit.Credentials.Tokens();
            string whoami = tokens.WhoAmI();
            Console.WriteLine(whoami);
        }
    }
}
```

&gt; NuGet Package Manager &gt;&gt; Package Manager Console"\]\]\]\]}'&gt;

### Step \#2 \| Embedding SharpSploit in our project

Now let's install the library from the NuGet package manager

**Tools &gt;&gt; NuGet Package Manager &gt;&gt; Package Manager Console**

![](../.gitbook/assets/image%20%2813%29.png)

You will see a console similar to the following

![](../.gitbook/assets/image%20%2811%29.png)

Execute the following line.

PM&gt; Install-Package costura.fody -Version 3.3.3

{% hint style="info" %}
**Note:** 

For compatibility, you need this version of `msbuild.exe` v15 in Visual Studio 2017. If you are using VS2019 then use the last version of _costura_ and _fody_.
{% endhint %}

And Now, add the library reference to the project

![](../.gitbook/assets/image%20%2817%29.png)

Browse to the compiled DLL path

```text
C:\Users\KING\Desktop\csarps\SharpSploit\SharpSploit\bin\Release\net35
```

Select it and add

![](../.gitbook/assets/image%20%2812%29.png)

### Step \#3 \| Compile the application

Now you will do exactly as you've done with the DLL compilation. 

Change the build type to _Release_ and go to  **Build &gt;&gt; Build WhoAmI**. You will find the executable file under your project page under `bin\Release` directory.

![](../.gitbook/assets/image%20%288%29.png)

## Finally

This library is an intuitive APIs for red teamers on Windows. However, it's a big one, meaning, the size of the DLL after compilation is +1Mb which will get even bigger when you embed it in your binary. Therefore, you can inject it into memory and execute  using something like `execute-assembly` in CobaltStrike.

