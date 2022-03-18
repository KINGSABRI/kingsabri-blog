---
description: Adding different fonts for different languages in Linux
---

# Change Default Font for a Specific Language in Linux



```
nano ~/.config/fontconfig/fonts.conf
```

Here is an example for adding the "**Amiri**" font family for Arabic "**ar**" keyboard layout.

```xml
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
 <match target="font">
  <test name="lang" compare="contains">
   <string>ar</string>
  </test>
  <alias>
   <family>sans-serif</family>
   <prefer>
    <family>Amiri</family>
   </prefer>
  </alias>
  <test name="family" compare="contains">
   <string>Song</string>
  </test>
  <!-- check to see if the font is just regular -->
  <test name="weight" compare="less_eq">
   <int>100</int>
  </test>
  <test name="weight" target="pattern" compare="more_eq">
   <int>180</int>
  </test>
  <edit name="embolden" mode="assign">
   <bool>true</bool>
  </edit>
 </match>
 <match target="font">
  <test name="family" compare="contains">
   <string>Sun</string>
  </test>
  <!-- check to see if the font is just regular -->
  <test name="weight" compare="less_eq">
   <int>100</int>
  </test>
  <test name="weight" target="pattern" compare="more_eq">
   <int>180</int>
  </test>
  <edit name="embolden" mode="assign">
   <bool>true</bool>
  </edit>
 </match>
 <match target="font">
  <test name="family" compare="contains">
   <string>Kai</string>
  </test>
  <!-- check to see if the font is just regular -->
  <test name="weight" compare="less_eq">
   <int>100</int>
  </test>
  <test name="weight" target="pattern" compare="more_eq">
   <int>180</int>
  </test>
  <edit name="embolden" mode="assign">
   <bool>true</bool>
  </edit>
 </match>
 <match target="font">
  <test name="family" compare="contains">
   <string>Ming</string>
  </test>
  <!-- check to see if the font is just regular -->
  <test name="weight" compare="less_eq">
   <int>100</int>
  </test>
  <test name="weight" target="pattern" compare="more_eq">
   <int>180</int>
  </test>
  <edit name="embolden" mode="assign">
   <bool>true</bool>
  </edit>
 </match>
 <dir>~/.fonts</dir>
 <match target="font">
  <edit name="rgba" mode="assign">
   <const>rgb</const>
  </edit>
 </match>
 <match target="font">
  <edit name="hinting" mode="assign">
   <bool>true</bool>
  </edit>
 </match>
 <match target="font">
  <edit name="hintstyle" mode="assign">
   <const>hintslight</const>
  </edit>
 </match>
 <match target="font">
  <edit name="antialias" mode="assign">
   <bool>true</bool>
  </edit>
 </match>
</fontconfig>
```



