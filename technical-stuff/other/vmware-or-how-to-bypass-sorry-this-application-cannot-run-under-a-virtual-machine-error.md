# VMWare \| How to Bypass Sorry, this application cannot run under a Virtual Machine error

Some applications might restrict running on VM machine for various reasons, such as licenses. I've faced this issue with Acunetix web scanner.  


Here is a quick fix.

1. Close the VM machine "not suspend".
2. find the VM's file ends with \`vmx\`.
3. Edit the file with your favorite text editor and add, then save `monitor_control.restrict_backdoor = "true"` 
4. Run your vm.

