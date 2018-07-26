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
ARF = {}

ARF.SyncDataToClient = function(_source, data)
	TriggerClientEvent("arf:receivePlayerData", _source, data)
end

ARF.GetClientData = function(_source)
	local id = GetPlayerIdentifiers(_source)
	MySQL.Async.fetchAll("SELECT * FROM users WHERE identifier = '"..id[1].."'", {}, function(result)
		if result[1] == nil then
			MySQL.Async.execute('INSERT INTO users (identifier, license, department, rank, permission_level) VALUES ("'..id[1]..'","'..id[2] ..'","'..config.newUsers.DefaultDepartment..'", "'..config.newUsers.DefaultRank ..'",'..config.newUsers.DefaultPermissionLevel..');', {}, function(e) end)
			SetTimeout(150, function()
				ARF.GetClientData(_source)
			end)
		else
			local data = result
			ARF.SyncDataToClient(_source, data)
		end
	end)
end

RegisterNetEvent('arf:getPlayerData')
AddEventHandler('arf:getPlayerData', function()
	local _source = source
	ARF.GetClientData(_source)
end)

AddEventHandler('arf:getSharedObject', function(cb)
	cb(ARF)
end)
