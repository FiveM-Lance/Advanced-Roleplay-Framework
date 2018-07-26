# Advanced-Roleplay-Framework
Advanced Roleplay Framework - Coming Soon?
# ARF Boilerplate
All scripts using this framework must use the following lines in the beginning of their .lua files:
- Client:
```lua
ARF = nil

RegisterNetEvent("arf:receivePlayerData")
AddEventHandler("arf:receivePlayerData", function(data)
	ARF = {}
	ARF.PlayerData = data[1]
end)

AddEventHandler('arf:getSharedObject', function(cb)
	cb(ARF)
end)
```
- Server:
```lua
ARF = nil

Citizen.CreateThread(function()
	TriggerServerEvent("arf:getPlayerData")
	while ARF == nil do
		Citizen.Wait(0)
		TriggerEvent('arf:getSharedObject', function(data) 
			ARF = data
		end)
	end
end)
