Paste This In Client

```
RegisterNetEvent('consumables:client:superjump')
AddEventHandler('consumables:client:superjump', function()
    QBCore.Functions.Progressbar("use_superjump", "Using Super Jump", 1500, false, true, {
        disableMovement = false,
        disableCarMovement = false,
        disableMouse = false,
        disableCombat = true,
    }, {
        animDict = "mp_suicide",
        anim = "pill_fp",
        flags = 49,
    }, {}, {}, function() -- Done
        TriggerServerEvent("consumables:server:superjump")
        TriggerEvent('inventory:client:ItemBox', QBCore.Shared.Items['superjump'], 'remove')
        QBCore.Functions.Notify('Super Jump Power Started', 'success')
        local superJump = true
        Citizen.CreateThread(function()
            while superJump do
                SetSuperJumpThisFrame(PlayerId(), 1000)
                Wait(5)
            end
        end)

        Citizen.CreateThread(function()
            Wait(30000) -- Wait for 30 seconds (30 seconds = 30000 milliseconds)
            superJump = false
            print("Thanks Rojin Chhetri")
            QBCore.Functions.Notify('Super Jump Power Ended', 'error')
        end)
    end, function() -- Cancel
        QBCore.Functions.Notify('Canceled..', 'error')
    end)
end)
```

Paste This In Server

```
QBCore.Functions.CreateUseableItem("superjump", function(source)
    TriggerClientEvent("consumables:client:superjump", source)
end)
RegisterNetEvent('consumables:server:superjump', function()
    local Player = QBCore.Functions.GetPlayer(source)

    if not Player then return end

    Player.Functions.RemoveItem('superjump', 1)
end)
```

Make sure to add item on shared.lua on qb-core. Enjoy It may be useful for events and fun