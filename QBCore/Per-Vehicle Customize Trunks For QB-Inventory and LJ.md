In lj-inventory/config.lua add these lines at the bottom of the config:

```
Config.maxweight = 10000 -- Maximum Capacity of an un-configured trunk by default: 10 kg
Config.slots = 15 -- How many slots in those trunks by default: 15 slots
```

In lj-inventory/client/main.lua replace these lines:

```
                local vehicleClass = GetVehicleClass(curVeh)
                local maxweight
                local slots
                if vehicleClass == 0 then
                    maxweight = 38000
                    slots = 30
                elseif vehicleClass == 1 then
                    maxweight = 50000
                    slots = 40
                elseif vehicleClass == 2 then
                    maxweight = 75000
                    slots = 50
                elseif vehicleClass == 3 then
                    maxweight = 42000
                    slots = 35
                elseif vehicleClass == 4 then
                    maxweight = 38000
                    slots = 30
                elseif vehicleClass == 5 then
                    maxweight = 30000
                    slots = 25
                elseif vehicleClass == 6 then
                    maxweight = 30000
                    slots = 25
                elseif vehicleClass == 7 then
                    maxweight = 30000
                    slots = 25
                elseif vehicleClass == 8 then
                    maxweight = 15000
                    slots = 15
                elseif vehicleClass == 9 then
                    maxweight = 60000
                    slots = 35
                elseif vehicleClass == 12 then
                    maxweight = 120000
                    slots = 35
                elseif vehicleClass == 13 then
                    maxweight = 0
                    slots = 0
                elseif vehicleClass == 14 then
                    maxweight = 120000
                    slots = 50
                elseif vehicleClass == 15 then
                    maxweight = 120000
                    slots = 50
                elseif vehicleClass == 16 then
                    maxweight = 120000
                    slots = 50
                else
                    maxweight = 60000
                    slots = 35 
```

With these lines: 

```
local hash = GetEntityModel(curVeh)
                local maxweight = Config.maxweight
                local slots = Config.slots
                local VehicleHashes = QBCore.Shared.VehicleHashes[hash]

                if VehicleHashes and VehicleHashes.maxweight and VehicleHashes.slots then
                    maxweight = VehicleHashes.maxweight
                    slots = VehicleHashes.slots 
```

In qb-core/shared/vehicle.lua format your vehicles like this:

```
['asbo'] = {
        ['name'] = 'Asbo',
        ['brand'] = 'Maxwell',
        ['model'] = 'asbo',
        ['price'] = 4000,
        ['category'] = 'compacts',
        ['categoryLabel'] = 'Compacts',
        ['hash'] = `asbo`,
        ['maxweight'] = 38000,
        ['slots'] = 30,
        ['shop'] = 'pdm',
    },
```

Maxweight is in kg
38000 = 38.00
Default Maxweight for unconfigured vehicles is 10000 (10kg)