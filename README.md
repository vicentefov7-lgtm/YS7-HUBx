-- Bounty HUD | Blox Fruits

local Players = game:GetService("Players")
local player = Players.LocalPlayer

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "BountyHUD"
ScreenGui.ResetOnSpawn = false

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 220, 0, 55)
Frame.Position = UDim2.new(1, -235, 0, 20)
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
Frame.BorderSizePixel = 0
Frame.Parent = ScreenGui

local Corner = Instance.new("UICorner")
Corner.CornerRadius = UDim.new(0, 12)
Corner.Parent = Frame

local Label = Instance.new("TextLabel")
Label.Size = UDim2.new(1, 0, 1, 0)
Label.BackgroundTransparency = 1
Label.TextColor3 = Color3.fromRGB(255, 215, 70)
Label.TextScaled = true
Label.Font = Enum.Font.GothamBold
Label.Parent = Frame

local function updateBounty()
    local leaderstats = player:FindFirstChild("leaderstats")

    if leaderstats then
        local bounty = leaderstats:FindFirstChild("Bounty")

        if bounty then
            Label.Text = "💰 Bounty: " .. tostring(bounty.Value)
            return
        end
    end

    Label.Text = "💰 Bounty: Carregando..."
end

local leaderstats = player:WaitForChild("leaderstats", 10)

if leaderstats then
    local bounty = leaderstats:WaitForChild("Bounty", 10)

    if bounty then
        updateBounty()
        bounty:GetPropertyChangedSignal("Value"):Connect(updateBounty)
    end
end

ScreenGui.Parent = player:WaitForChild("PlayerGui")
