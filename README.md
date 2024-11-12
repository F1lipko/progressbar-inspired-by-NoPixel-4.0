# Creator of original resoursce [Click here](https://kane-shop.tebex.io/category/2596522)
# Standalone Progressbar inspired by NoPixel 4.0.

![Screenshot 2024-01-06 175641](https://github.com/rohKane/progressbar/assets/47999933/93ffa56f-215e-4138-a667-ae3be2de6aab)
![Screenshot 2024-01-06 174953](https://github.com/rohKane/progressbar/assets/47999933/bb656b22-017a-411a-bb7a-6196fab0844a)

# Ox_lib integration tutorial DOWN HERE
### To integrate progressbar into ox_lib
 
 ## RENAME RESOURSCE TO progressbar 
- First go into ox_lib/resource/interface/client/progress.lua
- Then find **function lib.progressBar(data)**
- And then replace that whole function code with mine here

```
function lib.progressBar(data)
    while progress ~= nil do Wait(0) end

    if not interruptProgress(data) then
            playerState.invBusy = true
            exports['progressbar']:Progress({
            name = "random_task",
            duration = data.duration,
            label = data.label,
            useWhileDead = false,
            canCancel = true,
            controlDisables = {
                disableMovement = false,
                disableCarMovement = false,
                disableMouse = false,
                disableCombat = false,
            },
         }, function(cancelled)
            if not cancelled then
                -- finished
                --SendNUIMessage({
                    --action = 'progress',
                    --data = {
                        --label = data.label,
                        --duration = data.duration
                        --duration = -100
                    --}
                --})
                progress = nil
                playerState.invBusy = false
            else
                -- cancelled
                print("omg")
                -- Reset progress whether it's finished or cancelled
                progress = false
                Citizen.Wait(1000)
                progress = nil
                playerState.invBusy = false
            end
         end)

        return startProgress(data)
    end
end
```

