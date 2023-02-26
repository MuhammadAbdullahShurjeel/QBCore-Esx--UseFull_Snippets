This snippet makes your ped force into 1st person cam when aiming a weapon in a car and automatically switches back to 3rd person when they stop aiming. This should work for all seats in the car as well not just the driver. I saw a few other old snippets but those all had small issues like not switching back the camera after aiming or allowing people to exploit 3rd person aiming

All you need to do is copy this code into any client sided file that you want and restart that resource.

```
local isInVehicle = false

Citizen.CreateThread(function()
    while true do
        Citizen.Wait(0)

        local ped = PlayerPedId()
        local vehicle = GetVehiclePedIsIn(ped, false)

        if IsEntityDead(ped) or IsPlayerSwitchInProgress() then
            isInVehicle = false
        elseif IsPedInAnyVehicle(ped, false) and GetPedInVehicleSeat(vehicle, -1) == ped then
            isInVehicle = true
            if IsControlPressed(0, 25) then
                SetFollowPedCamViewMode(4)
                SetFollowVehicleCamViewMode(4)
            elseif not IsControlPressed(0, 25) and GetFollowPedCamViewMode() == 4 and GetFollowVehicleCamViewMode() == 4 then
                SetFollowPedCamViewMode(1)
                SetFollowVehicleCamViewMode(1)
            end
        else
            isInVehicle = false
        end
    end
end)
```