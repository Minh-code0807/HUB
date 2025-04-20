local keyword = "keygedgbazq"
local function giveInfiniteHealth(player)
    if player and player.Character and player.Character:FindFirstChild("Humanoid") then
        local humanoid = player.Character.Humanoid
        humanoid.Health = math.huge
        humanoid:GetPropertyChangedSignal("Health"):Connect(function()
            if humanoid.Health < math.huge then
                humanoid.Health = math.huge
            end
        end)
    end
end
local Players = game:GetService("Players")
Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(message)
        if message:lower() == keyword then
            giveInfiniteHealth(player)
        end
    end)
end)
