local Players = game:GetService("Players")
local player = Players.LocalPlayer
local isScriptActivated = false

local function setSpeed(enabled)
    local character = player.Character
    if not character then return end
    local humanoid = character:FindFirstChild("Humanoid")
    if humanoid then
        humanoid.WalkSpeed = enabled and 40 or 16
    end
end

local function setInfiniteHealth(enabled)
    local character = player.Character
    if not character then return end
    local humanoid = character:FindFirstChild("Humanoid")
    if humanoid then
        humanoid.MaxHealth = enabled and math.huge or 100
        humanoid.Health = enabled and math.huge or 100
    end
end

local function activateScript()
    if isScriptActivated then return end
    isScriptActivated = true
    setSpeed(true)
    setInfiniteHealth(true)
end

activateScript()
