# Advanced-Roleplay-Framework
Advanced Roleplay Framework - Coming Soon?
# ARF Boilerplate

## Use the following lines of code and the documentation in order to make a resource using this framework.

### Client.lua

```lua
ARF = nil

RegisterNetEvent("arf:receivePlayerData")
AddEventHandler("arf:receivePlayerData", function(data)
	ARF = {}
	ARF.PlayerData = data
end)
```

### Server.lua

```lua
ARF = nil

Citizen.CreateThread(function()
	TriggerServerEvent("arf:getPlayerData")
end)
```
