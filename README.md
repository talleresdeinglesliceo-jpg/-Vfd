local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

if CoreGui:FindFirstChild("LuxedHUD") then
    CoreGui.LuxedHUD:Destroy()
end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "LuxedHUD"
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = CoreGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 240, 0, 150)
frame.AnchorPoint = Vector2.new(0.5, 0)
frame.Position = UDim2.new(0.5, 0, 0, 15)
frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
frame.BackgroundTransparency = 0.35
frame.BorderSizePixel = 0
frame.Parent = screenGui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 10)
uiCorner.Parent = frame

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, -30, 0, 25)
titleLabel.Position = UDim2.new(0, 10, 0, 5)
titleLabel.BackgroundTransparency = 1
titleLabel.Font = Enum.Font.GothamBold
titleLabel.Text = "⚡ LUXED HUD"
titleLabel.TextColor3 = Color3.fromRGB(0, 150, 255)
titleLabel.TextSize = 13
titleLabel.TextXAlignment = Enum.TextXAlignment.Left
titleLabel.Parent = frame

local combatLabel = Instance.new("TextLabel")
combatLabel.Size = UDim2.new(1, -20, 0, 22)
combatLabel.Position = UDim2.new(0, 10, 0, 32)
combatLabel.BackgroundTransparency = 1
combatLabel.Font = Enum.Font.GothamBold
combatLabel.Text = "⚔️ [ COMBAT & VISUALS ]"
combatLabel.TextColor3 = Color3.fromRGB(0, 150, 255)
combatLabel.TextSize = 11
combatLabel.TextXAlignment = Enum.TextXAlignment.Center
combatLabel.Parent = frame

-- Toggle Silent Aim
local silentContainer = Instance.new("Frame")
silentContainer.Size = UDim2.new(1, -20, 0, 26)
silentContainer.Position = UDim2.new(0, 10, 0, 62)
silentContainer.BackgroundTransparency = 1
silentContainer.Parent = frame

local silentText = Instance.new("TextLabel")
silentText.Size = UDim2.new(0, 120, 1, 0)
silentText.Position = UDim2.new(0, 0, 0, 0)
silentText.BackgroundTransparency = 1
silentText.Font = Enum.Font.GothamSemibold
silentText.Text = "Silent Aim"
silentText.TextColor3 = Color3.fromRGB(255, 255, 255)
silentText.TextSize = 11
silentText.TextXAlignment = Enum.TextXAlignment.Left
silentText.Parent = silentContainer

local toggleSwitch = Instance.new("TextButton")
toggleSwitch.Size = UDim2.new(0, 40, 0, 20)
toggleSwitch.Position = UDim2.new(1, -40, 0.5, -10)
toggleSwitch.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
toggleSwitch.AutoButtonColor = false
toggleSwitch.Text = ""
toggleSwitch.Parent = silentContainer

local switchCorner = Instance.new("UICorner")
switchCorner.CornerRadius = UDim.new(1, 0)
switchCorner.Parent = toggleSwitch

local switchKnob = Instance.new("Frame")
switchKnob.Size = UDim2.new(0, 16, 0, 16)
switchKnob.Position = UDim2.new(1, -18, 0.5, -8)
switchKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
switchKnob.Parent = toggleSwitch

local knobCorner = Instance.new("UICorner")
knobCorner.CornerRadius = UDim.new(1, 0)
knobCorner.Parent = switchKnob

-- Toggle ESP Box
local espContainer = Instance.new("Frame")
espContainer.Size = UDim2.new(1, -20, 0, 26)
espContainer.Position = UDim2.new(0, 10, 0, 94)
espContainer.BackgroundTransparency = 1
espContainer.Parent = frame

local espText = Instance.new("TextLabel")
espText.Size = UDim2.new(0, 120, 1, 0)
espText.Position = UDim2.new(0, 0, 0, 0)
espText.BackgroundTransparency = 1
espText.Font = Enum.Font.GothamSemibold
espText.Text = "ESP Box"
espText.TextColor3 = Color3.fromRGB(255, 255, 255)
espText.TextSize = 11
espText.TextXAlignment = Enum.TextXAlignment.Left
espText.Parent = espContainer

local toggleEspSwitch = Instance.new("TextButton")
toggleEspSwitch.Size = UDim2.new(0, 40, 0, 20)
toggleEspSwitch.Position = UDim2.new(1, -40, 0.5, -10)
toggleEspSwitch.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
toggleEspSwitch.AutoButtonColor = false
toggleEspSwitch.Text = ""
toggleEspSwitch.Parent = espContainer

local espSwitchCorner = Instance.new("UICorner")
espSwitchCorner.CornerRadius = UDim.new(1, 0)
espSwitchCorner.Parent = toggleEspSwitch

local espSwitchKnob = Instance.new("Frame")
espSwitchKnob.Size = UDim2.new(0, 16, 0, 16)
espSwitchKnob.Position = UDim2.new(1, -18, 0.5, -8)
espSwitchKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
espSwitchKnob.Parent = toggleEspSwitch

local espKnobCorner = Instance.new("UICorner")
espKnobCorner.CornerRadius = UDim.new(1, 0)
espKnobCorner.Parent = espSwitchKnob

local silentActive = true
local espActive = true

toggleSwitch.MouseButton1Click:Connect(function()
    silentActive = not silentActive
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    if silentActive then
        TweenService:Create(toggleSwitch, info, {BackgroundColor3 = Color3.fromRGB(0, 150, 255)}):Play()
        TweenService:Create(switchKnob, info, {Position = UDim2.new(1, -18, 0.5, -8)}):Play()
    else
        TweenService:Create(toggleSwitch, info, {BackgroundColor3 = Color3.fromRGB(60, 60, 60)}):Play()
        TweenService:Create(switchKnob, info, {Position = UDim2.new(0, 2, 0.5, -8)}):Play()
    end
end)

toggleEspSwitch.MouseButton1Click:Connect(function()
    espActive = not espActive
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    if espActive then
        TweenService:Create(toggleEspSwitch, info, {BackgroundColor3 = Color3.fromRGB(0, 150, 255)}):Play()
        TweenService:Create(espSwitchKnob, info, {Position = UDim2.new(1, -18, 0.5, -8)}):Play()
    else
        TweenService:Create(toggleEspSwitch, info, {BackgroundColor3 = Color3.fromRGB(60, 60, 60)}):Play()
        TweenService:Create(espSwitchKnob, info, {Position = UDim2.new(0, 2, 0.5, -8)}):Play()
    end
end)

local toggleBtn = Instance.new("TextButton")
toggleBtn.Size = UDim2.new(0, 24, 0, 24)
toggleBtn.Position = UDim2.new(1, -28, 0, 5)
toggleBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
toggleBtn.BackgroundTransparency = 0.3
toggleBtn.Font = Enum.Font.GothamBold
toggleBtn.Text = "-"
toggleBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleBtn.TextSize = 14
toggleBtn.Parent = frame

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 6)
btnCorner.Parent = toggleBtn

local isMinimized = false

-- Sistema de Arrastre (Dragging) para cuando esté minimizado
local dragging, dragInput, dragStart, startPos

toggleBtn.InputBegan:Connect(function(input)
    if isMinimized and (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position
        
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

toggleBtn.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging and isMinimized then
        local delta = input.Position - dragStart
        frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

toggleBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    
    if isMinimized then
        combatLabel.Visible = false
        silentContainer.Visible = false
        espContainer.Visible = false
        titleLabel.Visible = false
        
        TweenService:Create(frame, info, {Size = UDim2.new(0, 50, 0, 50)}):Play()
        toggleBtn.Text = "+"
        TweenService:Create(toggleBtn, info, {Size = UDim2.new(1, 0, 1, 0), Position = UDim2.new(0, 0, 0, 0), BackgroundTransparency = 0.1}):Play()
    else
        TweenService:Create(frame, info, {Size = UDim2.new(0, 240, 0, 150)}):Play()
        toggleBtn.Text = "-"
        TweenService:Create(toggleBtn, info, {Size = UDim2.new(0, 24, 0, 24), Position = UDim2.new(1, -28, 0, 5), BackgroundTransparency = 0.3}):Play()
        
        task.wait(0.15)
        titleLabel.Visible = true
        combatLabel.Visible = true
        silentContainer.Visible = true
        espContainer.Visible = true
    end
end)

local function isTeamMate(player)
    if player.Team and LocalPlayer.Team and player.Team == LocalPlayer.Team then
        return true
    end
    return false
end

local function getClosestTarget()
    local closestTarget = nil
    local shortestDistance = math.huge
    local mousePos = UserInputService:GetMouseLocation()

    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and not isTeamMate(player) and player.Character then
            local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
            local torso = player.Character:FindFirstChild("HumanoidRootPart") 
                       or player.Character:FindFirstChild("UpperTorso") 
                       or player.Character:FindFirstChild("LowerTorso")
            
            if humanoid and humanoid.Health > 0 and torso then
                local screenPos, onScreen = Camera:WorldToViewportPoint(torso.Position)
                if onScreen then
                    local distance = (Vector2.new(screenPos.X, screenPos.Y) - mousePos).Magnitude
                    if distance < shortestDistance then
                        shortestDistance = distance
                        closestTarget = torso
                    end
                end
            end
        end
    end
    
    return closestTarget
end

local espCache = {}

local function removeEsp(player)
    if espCache[player] then
        for _, drawing in pairs(espCache[player]) do
            drawing:Remove()
        end
        espCache[player] = nil
    end
end

RunService.RenderStepped:Connect(function()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            if espActive and player.Character and player.Character:FindFirstChild("HumanoidRootPart") and player.Character:FindFirstChildOfClass("Humanoid") and player.Character.Humanoid.Health > 0 and not isTeamMate(player) then
                local character = player.Character
                local rootPart = character.HumanoidRootPart
                
                if not espCache[player] then
                    local box = Drawing.new("Square")
                    box.Visible = false
                    box.Color = Color3.fromRGB(0, 150, 255)
                    box.Thickness = 1.5
                    box.Filled = false
                    espCache[player] = {Box = box}
                end
                
                local box = espCache[player].Box
                local vector, onScreen = Camera:WorldToViewportPoint(rootPart.Position)
                
                if onScreen then
                    local size = Vector2.new(2000 / vector.Z, 3000 / vector.Z)
                    box.Size = size
                    box.Position = Vector2.new(vector.X - size.X / 2, vector.Y - size.Y / 2)
                    box.Visible = true
                else
                    box.Visible = false
                end
            else
                if espCache[player] then
                    espCache[player].Box.Visible = false
                end
            end
        end
    end
end)

Players.PlayerRemoving:Connect(function(player)
    removeEsp(player)
end)

local oldNamecall
oldNamecall = hookmetamethod(game, "__namecall", function(self, ...)
    local method = getnamecallmethod()
    local args = {...}
    
    if silentActive and (method == "FireServer" or method == "InvokeServer") then
        local target = getClosestTarget()
        if target then
            pcall(function()
                for i, v in ipairs(args) do
                    local t = typeof(v)
                    if t == "Vector3" then
                        args[i] = target.Position
                    elseif t == "CFrame" then
                        args[i] = CFrame.new(v.Position, target.Position)
                    elseif t == "Instance" and v:IsA("BasePart") then
                        args[i] = target
                    end
                end
            end)
            return oldNamecall(self, unpack(args))
        end
    end
    
    return oldNamecall(self, ...)
end)
