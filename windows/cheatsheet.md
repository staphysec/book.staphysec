# CheatSheet



```
# Run Commands on remote host
Invoke-Command -Computer <name> -ScriptBlock {whoami} -Credential $cred

# Create session for another user
new-pssession -computername . -credential $cred
enter-pssession <ID>
```
