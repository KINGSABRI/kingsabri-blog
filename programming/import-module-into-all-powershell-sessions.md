# Import module into all PowerShell Sessions

While testing some stuff, I wanted to keep all PowerSploit modules that I need to be automatically loaded into powershell when I open a session\(window\). To do so, we need a profile file for PowerShell that acts like  `.bashrc` in Linux or `.bash_profile` in MacOS.

### Step \#1 \| Get Powershell profile path

In your powershell, print the `profile` a variable that stores the powershell profile default path.



{% tabs %}
{% tab title="Command" %}
```text
$profile
```
{% endtab %}

{% tab title="Result" %}
```
C:\Users\<USERNAME>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
```
{% endtab %}
{% endtabs %}

This file does not exist by default, so you have to create it manually.

```text
PS C:> mkdir $HOME\Documents\WindowsPowerShell
PS C:> notepad $profile
```

### Step \#2 \| Add Your modules

I keep my stuff in `Downloads` directory, so here I load all the modules I need

```text
$Downloads      = "$HOME\Downloads"

$PowerSploitDir = "$Downloads\PowerSploit"
$PSExclude      = Get-ChildItem -Path "$PowerSploitDir\Tests\"
$Files          = Get-ChildItem -Path $PowerSploitDir -Recurse -File -Include "*.ps1" -Exclude $PSExclude | %{$_.FullName}
Write-Host "[+] Import PowerSploit Modules."
foreach ($f in $Files){ Import-Module $f }
```

Save and close, duh!

### Step \#3 \| Load your Profile

Now, when you open a new powershell session \(window\), run the following

```text
.$Profile
```

## **Resources**

* [https://ss64.com/ps/syntax-profile.html](https://ss64.com/ps/syntax-profile.html)

