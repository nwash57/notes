##### Execution Policy
- `Get-ExecutionPolicy`
- `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine`

##### String Interpolation
`"my string with a $($variable)"`
`"my string with a ${variable}"`
**`${...}`** (enclosing the variable name in `{` and `}`) is indeed **_always_ necessary if a variable name contains _special characters_**, such as **spaces, `.`, or `-`**.