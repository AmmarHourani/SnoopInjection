# SnoopInjection

ManagedInjectorLauncherXX-X.0.exe windowHandle "assembly.Location" "className" "methodName"

Great work from https://github.com/snoopwpf

simplified to be used for injection/detouring purposes rather than WPF

simple discription of work mechanism

1) Launch Inject()-method from the ManagedInjector***.dll targeted at proper version of run-time.

2) From that method write our strings, containing assembly path, class name, method name into target process’s memory via VirtualAllocEx + WriteProcessMemory from Windows API.

3) Install a WH_CALLWNDPROC-type hook specific to process’s main window thread.

4) Send WM_GOBABYGO with the address of our strings as a parameter.

5) Inside of the hook procedure, when WM_GOBABYGO comes, read strings from the process memory. Load the proper Snoop.exe-assembly and execute the method (via reflection).

6) Uninstall windows hook and free memory we’ve allocated for strings.
