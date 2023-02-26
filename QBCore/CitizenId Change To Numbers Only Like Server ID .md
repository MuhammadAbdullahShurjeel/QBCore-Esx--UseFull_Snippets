
QBCORE/SERVER/PLAYER.lua

```
local CitizenId = 0 
function QBCore.Player.CreateCitizenId()
    local UniqueFound = false
    while not UniqueFound do
        CitizenId = CitizenId + 1
        local result = MySQL.prepare.await('SELECT COUNT(*) as count FROM players WHERE citizenid = ?', { CitizenId }) -- 1, 2, 3, 4
        if result == 0 then
            UniqueFound = true
        end
    end
    return CitizenId
end
```