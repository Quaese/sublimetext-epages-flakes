Flakes
=================

*A tasty treat for your epages6 development workflow.*

[Sublime Text 2](http://www.sublimetext.com/2) plugin that helps... a lot!...

---

- [Installation](#installation)
- [Configuration](#configuration)
  - [Windows](#windows)
  - [Unix](#unix)
- [Usage](#usage)
- [Features](#features)
- [Development](#development-todo)


Installation
------------
Follow [this readme](https://github.com/ePages-rnd/sublimetext-plugins).

To use the ctags functionality:

* Install the CTags plugin via the Package Control or grab the copy at [GitHub](https://github.com/SublimeText/CTags) and perform a manual install.
* Install the ctags command line program on your VMs. For CentOS a simple ```yum install ctags``` will do the job.
* Initialize via executing the "refresh ctags" command.
* **Don't use the commands provided by the CTags plugin!** Just update via the "refresh ctags" command.
* Test the installation. Ctrl+shift+leftmouse on a function/sub/constant name will cause Sublime to move to its definition. (Hit ctrl+shift+rightmouse to go back where you're from.)

Configuration
--------------
Edit User Settings:
* In Sublime Text.
* Click the **Preferences > Package Settings > Flakes > User - Settings User** menu entry.
* Edit the following **json** object and save it into your User Settings file.
### Windows
```js
{
      //
      // for local installation, windows-vms and linux-vms:
      //    
      "C": "C:\\epages\\",                            // "driveletter" : "Path to eproot on that drive"
      "AHEUMANN-VM1" : "\\\\AHEUMANN-VM1\\epages\\",  // windows-vm mounted as a network drive
      "X" : "X:\\",                                   // linux-vm mounted on X: drive via WinSCP
      "vms": [
        // ["Machine-name as above", "Some description"]
        ["C", "Lokale Installation"],
        ["AHEUMANN-VM1", "VM1"],
        ["X", "VM2"]
      ],
      
      //
      // only for linux-vms:
      //      
      "drive_letter_to_vm_name" : {
        "X" : "aheumann-vm2"  // "driveletter" : "name of the virtual machine on the nextwork"
      },
      "path_to_putty" : "C:\\Users\\username\\Programs\\putty"
}
```
### Unix
```js
{
      // "hostname of virtual machine" : "path to eproot on virtual machine on your file system"
      "jr-vm-lin-1" : "/Volumes/jr-vm-lin-1/srv/epages/eproot/",
      "jr-vm-lin-2" : "/Volumes/jr-vm-lin-2/srv/epages/eproot/",
      "jr-vm-lin-3" : "/Volumes/jr-vm-lin-3/srv/epages/eproot/",
      "vms" : [
        // ["hostname of virtual machine", "Some description"]
        ["jr-vm-lin-1", "VM1"],
        ["jr-vm-lin-2", "VM2"],
        ["jr-vm-lin-3", "VM3"]
      ],
      "filepath_to_vm" : "\\/Volumes\\/(.*)\\/srv\\/epages\\/.*$",
      // regex matching a filepath to the hostname of a virtual machine
      "filepath_to_eproot" : "\\/Volumes\\/.*\\/srv\\/epages\\/eproot/(.*)$",
      // regex matching a filepath to a relative filepath, i.e. relative to eproot.
      // used for exec_file_command_on_vm command.
}
```

Usage
--------
### Via Command Pallette
Bring up the Command Palette (`Command+Shift+P` on OS X, `Control+Shift+P` on Linux/Windows).
* Type `Epages` to select `Epages: Open error.log`, `Epages: Open file on vm from clipboard`,...
* or type `Choose VM` to select `Choose VM: Open error.log`, `ChooseVM: Open file on vm from clipboard`,...

What's the difference between `Epages: ...` and `Choose VM: ...`?

* `Epages: ...` commands try to infer the machine on which to run the command from the current file. E.g., when you are editing 
  `C:/epages/Cartridges/DE_EPAGES/SomeTemplate.html`, and run `Epages: Open error.log`, this is going to open the `error.log` on your local installation.
* `Choose VM: ...` commands will bring up a selection dialog with the machines defined in the `vms` key of your User - Settings (see above), and then run the command on the selected machine.

### Via Tools Menu
Some of the `Choose VM` commands are also available through the **Tools** menu.
 * **Tools > Flakes**
 * Click `Set debug 2`, `Open file from clipboard`,...

Features
--------

### Epages commands
Runs epages commands on virtual machine (or locally on windows, if applicable)
* perm_all
* perm_webroot
* perm_cartridges
* restart_app
* restart_perl
* set_debug_level_2
* check_perl_syntax
* check_js_syntax
* perl_critic
* organize_imports
* import_xml
* import_hook
* delete_xml
* delete_hook
* ... see [Flakes.sublime-settings](https://github.com/ePages-rnd/sublimetext-epages-flakes/blob/master/Flakes.sublime-settings)

### Useful helpers
* open file from clipboard
* open file on vm
* open error/debug/... log
* Perl snippets for debug and stacktrace logging

Development (TODO)
------------
* Add *Snippets* for javascript. (E.g. `define` module, `testcase` module,...)
* Copy to shared function?
* Open terminal with *ssh session on vm* in current file context.
