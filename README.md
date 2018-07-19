# Advanced-Roleplay-Framework
Advanced Roleplay Framework - Coming Soon?
# ARF Boilerplate
All scripts using this framework must use the following lines in the beginning of their .lua files:
- Client:
```
LSX = nil

Citizen.CreateThread(function()
	while true do
  	Citizen.Wait(0)
		if LSX ~= nil then
			TriggerServerEvent("action:syncToServer", GetPlayerName(PlayerId()))
			break
		else
			TriggerEvent('lsx:getSharedObject', function(data) 
				LSX = data
			end)
		end
	end
end)
