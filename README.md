local Players = game:GetService("Players")
local player = Players.LocalPlayer
local isScriptActivated = false
local initialPosition
local initialOrientation
local function saveInitialPosition(character)
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
    initialPosition = humanoidRootPart.Position
    initialOrientation = humanoidRootPart.Orientation
end
local function activateScript()
    if isScriptActivated then return end
    isScriptActivated = true
    local ScreenGui = Instance.new("ScreenGui")
    local Frame = Instance.new("Frame")
    local Button1 = Instance.new("TextButton")
    local MinimizeButton = Instance.new("TextButton")
    ScreenGui.Parent = player:WaitForChild("PlayerGui")
    ScreenGui.Name = "ReturnToStartGui"
    Frame.Parent = ScreenGui
    Frame.Size = UDim2.new(0, 200, 0, 150)
    Frame.Position = UDim2.new(0.5, -100, 0.5, -75)
    Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    Frame.BackgroundTransparency = 0.5
    Frame.Active = true
    Frame.Draggable = true
    Button1.Parent = Frame
    Button1.Size = UDim2.new(1, 0, 0.8, 0)
    Button1.Position = UDim2.new(0, 0, 0, 0)
    Button1.Text = "TP 10k"
    Button1.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    MinimizeButton.Parent = Frame
    MinimizeButton.Size = UDim2.new(1, 0, 0.2, 0)
    MinimizeButton.Position = UDim2.new(0, 0, 0.8, 0)
    MinimizeButton.Text = "Thu nhỏ"
    MinimizeButton.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
    local isMinimized = false
    Button1.MouseButton1Click:Connect(function()
        if initialPosition and initialOrientation then
            local character = player.Character
            if character then
                local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
                humanoidRootPart.CFrame = CFrame.new(initialPosition) * CFrame.Angles(0, math.rad(initialOrientation.Y), 0)
                humanoidRootPart.CFrame = humanoidRootPart.CFrame * CFrame.new(0, 0, -10000)
            end
        end
    end)
    MinimizeButton.MouseButton1Click:Connect(function()
        if isMinimized then
            Frame.Size = UDim2.new(0, 200, 0, 150)
            MinimizeButton.Text = "Thu nhỏ"
            isMinimized = false
        else
            Frame.Size = UDim2.new(0, 200, 0, 50)
            MinimizeButton.Text = "Phóng to"
            isMinimized = true
        end
    end)
end
player.CharacterAdded:Connect(function(character)
    saveInitialPosition(character)
end)
if player.Character then
    saveInitialPosition(player.Character)
end
player.Chatted:Connect(function(message)
    if string.lower(message) == "all" then
        activateScript()
    end
end)
