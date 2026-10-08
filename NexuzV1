--// NEXUZV1 ONLINE EDITION
--// WindUI + Live HUD + ESP + Tracers + Smooth Performance
--// Player Movement + Server Hop + Online Dashboard

--------------------------------------------------
-- SERVICES
--------------------------------------------------

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Lighting = game:GetService("Lighting")
local TeleportService = game:GetService("TeleportService")
local UserInputService = game:GetService("UserInputService")
local Stats = game:GetService("Stats")
local TweenService = game:GetService("TweenService")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

--------------------------------------------------
-- EXECUTION COUNTER
--------------------------------------------------

local ExecutionValue = "NexuzV1_Executions"

local executions = 0

pcall(function()
    if _G[ExecutionValue] then
        executions = _G[ExecutionValue] + 1
    else
        executions = 1
    end

    _G[ExecutionValue] = executions
end)

--------------------------------------------------
-- STATE
--------------------------------------------------

local State = {
    -- Movement
    WalkSpeed = 16,
    JumpPower = 50,
    Noclip = false,
    InfiniteJump = false,

    -- ESP
    ESP = false,
    ESPNames = true,
    ESPDistance = true,
    ESPTracers = true,
    ESPColor = Color3.fromRGB(0, 255, 140),

    -- Visuals
    Fullbright = false,
    FOV = 70,
    Crosshair = false,

    -- HUD
    HUDVisible = true,
    FPSCounter = true,
    PingCounter = true,
    PlayerCounter = true,
    Notifications = true,

    -- Performance
    LowPerformance = false,

    -- Fun
    FunnyText = "NEXUZV1 ONLINE",

    -- Runtime
    FPS = 0,
    Ping = 0,
    SessionStart = os.clock(),
    Executions = executions
}

--------------------------------------------------
-- WINDUI
--------------------------------------------------

local WindUI = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/Footagesus/WindUI/main/dist/main.lua"
))()

local Window = WindUI:CreateWindow({
    Title = "NexuzV1",
    Icon = "rbxassetid://4483362748",
    Author = "NexuzV1",
    Folder = "NexuzV1",

    Size = UDim2.fromOffset(610, 520),

    Transparent = true,
    Theme = "Dark",
    Resizable = true,
    SideBarWidth = 190,

    KeySystem = {
        Key = {
            "Test1",
            "Test2",
            "Test3"
        },

        Note = "NexuzV1 Access",
        URL = "https://discord.gg/example"
    }
})

--------------------------------------------------
-- HELPERS
--------------------------------------------------

local function Notify(title, content)
    if not State.Notifications then
        return
    end

    pcall(function()
        WindUI:Notify({
            Title = title,
            Content = content,
            Duration = 3
        })
    end)
end

local function Character()
    return LocalPlayer.Character
end

local function Humanoid()
    local char = Character()

    return char and
        char:FindFirstChildOfClass("Humanoid")
end

local function Root()
    local char = Character()

    return char and
        char:FindFirstChild("HumanoidRootPart")
end

--------------------------------------------------
-- LIVE HUD
--------------------------------------------------

local OldHUD =
    PlayerGui:FindFirstChild("NexuzV1HUD")

if OldHUD then
    OldHUD:Destroy()
end

local HUD = Instance.new("ScreenGui")
HUD.Name = "NexuzV1HUD"
HUD.ResetOnSpawn = false
HUD.IgnoreGuiInset = true
HUD.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
HUD.Parent = PlayerGui

local HUDFrame = Instance.new("Frame")

HUDFrame.Size =
    UDim2.fromOffset(260, 205)

HUDFrame.Position =
    UDim2.new(1, -280, 0.5, -102)

HUDFrame.BackgroundColor3 =
    Color3.fromRGB(11, 13, 17)

HUDFrame.BackgroundTransparency = 0.04
HUDFrame.BorderSizePixel = 0
HUDFrame.Parent = HUD

local HUDCorner = Instance.new("UICorner")
HUDCorner.CornerRadius =
    UDim.new(0, 14)
HUDCorner.Parent = HUDFrame

local HUDStroke = Instance.new("UIStroke")
HUDStroke.Color =
    Color3.fromRGB(70, 76, 90)

HUDStroke.Transparency = 0.1
HUDStroke.Thickness = 1
HUDStroke.Parent = HUDFrame

local HUDGradient = Instance.new("UIGradient")
HUDGradient.Rotation = 90

HUDGradient.Color =
    ColorSequence.new({
        ColorSequenceKeypoint.new(
            0,
            Color3.fromRGB(29, 32, 41)
        ),

        ColorSequenceKeypoint.new(
            1,
            Color3.fromRGB(7, 8, 11)
        )
    })

HUDGradient.Parent = HUDFrame

--------------------------------------------------
-- HUD HEADER
--------------------------------------------------

local HUDTitle = Instance.new("TextLabel")

HUDTitle.BackgroundTransparency = 1
HUDTitle.Position =
    UDim2.fromOffset(14, 9)

HUDTitle.Size =
    UDim2.new(1, -90, 0, 22)

HUDTitle.Font =
    Enum.Font.GothamBold

HUDTitle.Text = "NEXUZV1"
HUDTitle.TextColor3 =
    Color3.fromRGB(245, 245, 250)

HUDTitle.TextSize = 15
HUDTitle.TextXAlignment =
    Enum.TextXAlignment.Left

HUDTitle.Parent = HUDFrame

local Live = Instance.new("TextLabel")

Live.BackgroundTransparency = 1

Live.Position =
    UDim2.new(1, -70, 0, 9)

Live.Size =
    UDim2.fromOffset(60, 22)

Live.Font =
    Enum.Font.GothamBold

Live.Text = "● LIVE"

Live.TextColor3 =
    Color3.fromRGB(80, 255, 140)

Live.TextSize = 10

Live.Parent = HUDFrame

local HUDLine = Instance.new("Frame")

HUDLine.BorderSizePixel = 0

HUDLine.BackgroundColor3 =
    Color3.fromRGB(60, 64, 75)

HUDLine.Position =
    UDim2.fromOffset(13, 36)

HUDLine.Size =
    UDim2.new(1, -26, 0, 1)

HUDLine.Parent = HUDFrame

--------------------------------------------------
-- HUD ROW
--------------------------------------------------

local function CreateHUDRow(y, label)

    local row = Instance.new("Frame")

    row.BackgroundTransparency = 1

    row.Position =
        UDim2.fromOffset(13, y)

    row.Size =
        UDim2.new(1, -26, 0, 22)

    row.Parent = HUDFrame

    local name =
        Instance.new("TextLabel")

    name.BackgroundTransparency = 1

    name.Size =
        UDim2.new(0.62, 0, 1, 0)

    name.Font =
        Enum.Font.GothamMedium

    name.Text =
        "◉  " .. label

    name.TextColor3 =
        Color3.fromRGB(175, 180, 191)

    name.TextSize = 11

    name.TextXAlignment =
        Enum.TextXAlignment.Left

    name.Parent = row

    local value =
        Instance.new("TextLabel")

    value.BackgroundTransparency = 1

    value.Position =
        UDim2.new(0.62, 0, 0, 0)

    value.Size =
        UDim2.new(0.38, 0, 1, 0)

    value.Font =
        Enum.Font.GothamBold

    value.Text = "--"

    value.TextColor3 =
        Color3.fromRGB(245, 245, 250)

    value.TextSize = 11

    value.TextXAlignment =
        Enum.TextXAlignment.Right

    value.Parent = row

    return row, value
end

local FPSRow, FPSValue =
    CreateHUDRow(45, "FPS")

local PingRow, PingValue =
    CreateHUDRow(68, "PING")

local PlayersRow, PlayersValue =
    CreateHUDRow(91, "PLAYERS")

local SessionRow, SessionValue =
    CreateHUDRow(114, "SESSION")

local ExecutionsRow, ExecutionsValue =
    CreateHUDRow(137, "EXECUTIONS")

local ServerRow, ServerValue =
    CreateHUDRow(160, "SERVER")

ExecutionsValue.Text =
    tostring(State.Executions)

--------------------------------------------------
-- HUD ANIMATION
--------------------------------------------------

local function PopHUD()

    State.HUDVisible = true
    HUD.Enabled = true

    HUDFrame.Size =
        UDim2.fromOffset(0, 0)

    TweenService:Create(
        HUDFrame,

        TweenInfo.new(
            0.4,
            Enum.EasingStyle.Back,
            Enum.EasingDirection.Out
        ),

        {
            Size =
                UDim2.fromOffset(260, 205)
        }

    ):Play()
end

local function SetHUDVisible(value)

    State.HUDVisible = value

    if value then
        PopHUD()
    else
        HUD.Enabled = false
    end
end

--------------------------------------------------
-- HUD DRAGGING
--------------------------------------------------

local dragging = false
local dragStart
local startPosition

HUDFrame.InputBegan:Connect(function(input)

    if input.UserInputType ==
        Enum.UserInputType.MouseButton1

        or input.UserInputType ==
        Enum.UserInputType.Touch then

        dragging = true
        dragStart = input.Position
        startPosition =
            HUDFrame.Position
    end
end)

HUDFrame.InputEnded:Connect(function(input)

    if input.UserInputType ==
        Enum.UserInputType.MouseButton1

        or input.UserInputType ==
        Enum.UserInputType.Touch then

        dragging = false
    end
end)

UserInputService.InputChanged:Connect(function(input)

    if not dragging then
        return
    end

    if input.UserInputType ==
        Enum.UserInputType.MouseMovement

        or input.UserInputType ==
        Enum.UserInputType.Touch then

        local delta =
            input.Position - dragStart

        HUDFrame.Position =
            UDim2.new(
                startPosition.X.Scale,
                startPosition.X.Offset + delta.X,

                startPosition.Y.Scale,
                startPosition.Y.Offset + delta.Y
            )
    end
end)

--------------------------------------------------
-- FPS
--------------------------------------------------

local Frames = 0
local FPSTimer = os.clock()

RunService.RenderStepped:Connect(function()

    Frames += 1

    if os.clock() - FPSTimer >= 1 then

        State.FPS = Frames

        Frames = 0
        FPSTimer = os.clock()
    end
end)

--------------------------------------------------
-- HUD UPDATE
--------------------------------------------------

task.spawn(function()

    while HUD.Parent do

        FPSRow.Visible =
            State.FPSCounter

        PingRow.Visible =
            State.PingCounter

        PlayersRow.Visible =
            State.PlayerCounter

        FPSValue.Text =
            tostring(State.FPS)

        pcall(function()

            local pingObject =
                Stats.Network.ServerStatsItem:
                FindFirstChild("Data Ping")

            if pingObject then

                State.Ping =
                    math.floor(
                        pingObject:GetValue()
                    )

                PingValue.Text =
                    State.Ping .. "ms"
            end
        end)

        PlayersValue.Text =
            tostring(
                #Players:GetPlayers()
            )

        local elapsed =
            math.floor(
                os.clock() -
                State.SessionStart
            )

        local minutes =
            math.floor(
                elapsed / 60
            )

        local seconds =
            elapsed % 60

        SessionValue.Text =
            string.format(
                "%02d:%02d",
                minutes,
                seconds
            )

        ExecutionsValue.Text =
            tostring(
                State.Executions
            )

        local job =
            tostring(game.JobId)

        if #job > 8 then
            job =
                string.sub(
                    job,
                    1,
                    8
                )
        end

        ServerValue.Text = job

        task.wait(0.5)
    end
end)

--------------------------------------------------
-- ESP
--------------------------------------------------

local ESPFolder =
    Instance.new("Folder")

ESPFolder.Name =
    "NexuzV1ESP"

ESPFolder.Parent = HUD

local function RemoveESP(player)

    for _, object in
        ipairs(ESPFolder:GetChildren()) do

        if object.Name == player.Name
            or object.Name ==
                player.Name .. "_Info"

            or object.Name ==
                player.Name .. "_Tracer"

            or object.Name ==
                player.Name .. "_TracerStart"

            or object.Name ==
                player.Name .. "_TracerEnd" then

            object:Destroy()
        end
    end
end

--------------------------------------------------
-- TRACER
--------------------------------------------------

local function CreateTracer(player)

    if player == LocalPlayer then
        return
    end

    local tracer =
        Instance.new("Beam")

    tracer.Name =
        player.Name .. "_Tracer"

    tracer.FaceCamera = true

    tracer.Width0 = 0.08
    tracer.Width1 = 0.02

    tracer.LightEmission = 1

    tracer.Color =
        ColorSequence.new(
            State.ESPColor
        )

    tracer.Transparency =
        NumberSequence.new(0.15)

    tracer.Parent = ESPFolder

    local startAttachment =
        Instance.new("Attachment")

    startAttachment.Name =
        player.Name ..
        "_TracerStart"

    startAttachment.Parent =
        workspace.Terrain

    local endAttachment =
        Instance.new("Attachment")

    endAttachment.Name =
        player.Name ..
        "_TracerEnd"

    endAttachment.Parent =
        workspace.Terrain

    tracer.Attachment0 =
        startAttachment

    tracer.Attachment1 =
        endAttachment

    task.spawn(function()

        while tracer.Parent
            and player.Parent do

            local camera =
                workspace.CurrentCamera

            local character =
                player.Character

            local targetRoot =
                character and
                character:
                FindFirstChild(
                    "HumanoidRootPart"
                )

            if camera
                and targetRoot
                and State.ESP
                and State.ESPTracers then

                startAttachment.WorldPosition =
                    camera.CFrame.Position +
                    camera.CFrame.LookVector * 2

                endAttachment.WorldPosition =
                    targetRoot.Position

                tracer.Enabled = true

                tracer.Color =
                    ColorSequence.new(
                        State.ESPColor
                    )

            else
                tracer.Enabled = false
            end

            task.wait(
                State.LowPerformance
                and 0.12
                or 0.05
            )
        end

        if tracer then
            tracer:Destroy()
        end

        if startAttachment then
            startAttachment:Destroy()
        end

        if endAttachment then
            endAttachment:Destroy()
        end
    end)
end

--------------------------------------------------
-- ESP PLAYER
--------------------------------------------------

local function CreateESP(player)

    if player == LocalPlayer then
        return
    end

    RemoveESP(player)

    local highlight =
        Instance.new("Highlight")

    highlight.Name =
        player.Name

    highlight.Adornee =
        player.Character

    highlight.FillColor =
        State.ESPColor

    highlight.OutlineColor =
        State.ESPColor

    highlight.FillTransparency =
        0.78

    highlight.OutlineTransparency =
        0.05

    highlight.DepthMode =
        Enum.HighlightDepthMode.AlwaysOnTop

    highlight.Parent =
        ESPFolder

    local billboard =
        Instance.new("BillboardGui")

    billboard.Name =
        player.Name .. "_Info"

    billboard.Size =
        UDim2.fromOffset(
            190,
            45
        )

    billboard.StudsOffset =
        Vector3.new(
            0,
            3,
            0
        )

    billboard.AlwaysOnTop = true

    billboard.Parent =
        ESPFolder

    local text =
        Instance.new("TextLabel")

    text.BackgroundTransparency = 1

    text.Size =
        UDim2.fromScale(
            1,
            1
        )

    text.Font =
        Enum.Font.GothamBold

    text.TextColor3 =
        State.ESPColor

    text.TextStrokeTransparency =
        0.25

    text.TextSize = 12

    text.Parent =
        billboard

    if State.ESPTracers then
        CreateTracer(player)
    end

    task.spawn(function()

        while billboard.Parent
            and player.Parent do

            local character =
                player.Character

            if character then

                local head =
                    character:FindFirstChild(
                        "Head"
                    )

                if head then
                    billboard.Adornee =
                        head
                end

                local targetRoot =
                    character:
                    FindFirstChild(
                        "HumanoidRootPart"
                    )

                local myRoot =
                    Root()

                local distanceText = ""

                if State.ESPDistance
                    and targetRoot
                    and myRoot then

                    local distance =
                        math.floor(
                            (
                                targetRoot.Position -
                                myRoot.Position
                            ).Magnitude
                        )

                    distanceText =
                        "\n" ..
                        distance ..
                        " studs"
                end

                if State.ESPNames then

                    text.Text =
                        player.DisplayName ..
                        distanceText

                else
                    text.Text =
                        distanceText
                end

                text.TextColor3 =
                    State.ESPColor

                highlight.FillColor =
                    State.ESPColor

                highlight.OutlineColor =
                    State.ESPColor
            end

            task.wait(
                State.LowPerformance
                and 0.35
                or 0.15
            )
        end
    end)
end

local function RefreshESP()

    for _, object in
        ipairs(
            ESPFolder:GetChildren()
        ) do

        object:Destroy()
    end

    if not State.ESP then
        return
    end

    for _, player in
        ipairs(
            Players:GetPlayers()
        ) do

        if player ~= LocalPlayer then
            CreateESP(player)
        end
    end
end

Players.PlayerAdded:Connect(function(player)

    player.CharacterAdded:Connect(function()

        task.wait(1)

        if State.ESP then
            CreateESP(player)
        end
    end)
end)

Players.PlayerRemoving:Connect(function(player)
    RemoveESP(player)
end)

--------------------------------------------------
-- MOVEMENT
--------------------------------------------------

local function ApplyMovement()

    local hum = Humanoid()

    if not hum then
        return
    end

    hum.WalkSpeed =
        State.WalkSpeed

    hum.UseJumpPower = true

    hum.JumpPower =
        State.JumpPower
end

--------------------------------------------------
-- HOME
--------------------------------------------------

local HomeTab =
    Window:Tab({
        Title = "Home",
        Icon = "home"
    })

HomeTab:Section({
    Title = "Online Dashboard"
})

HomeTab:Button({
    Title = "Refresh Dashboard",

    Callback = function()

        Notify(
            "NexuzV1",
            "Dashboard refreshed."
        )
    end
})

HomeTab:Button({
    Title = "System Status",

    Callback = function()

        Notify(
            "ONLINE",
            "FPS: " ..
            State.FPS ..
            " | Ping: " ..
            State.Ping ..
            "ms | Players: " ..
            #Players:GetPlayers()
        )
    end
})

HomeTab:Button({
    Title = "Execution Count",

    Callback = function()

        Notify(
            "Executions",
            tostring(
                State.Executions
            )
        )
    end
})

HomeTab:Section({
    Title = "HUD"
})

HomeTab:Button({
    Title = "Pop Up HUD",

    Callback = function()
        PopHUD()
    end
})

HomeTab:Button({
    Title = "Hide HUD",

    Callback = function()
        SetHUDVisible(false)
    end
})

--------------------------------------------------
-- PLAYER
--------------------------------------------------

local PlayerTab =
    Window:Tab({
        Title = "Player",
        Icon = "user"
    })

PlayerTab:Section({
    Title = "Movement"
})

PlayerTab:Slider({
    Title = "WalkSpeed",

    Value = {
        Min = 1,
        Max = 200,
        Default = 16
    },

    Step = 1,

    Callback = function(value)

        State.WalkSpeed =
            value

        ApplyMovement()
    end
})

PlayerTab:Slider({
    Title = "JumpPower",

    Value = {
        Min = 1,
        Max = 200,
        Default = 50
    },

    Step = 1,

    Callback = function(value)

        State.JumpPower =
            value

        ApplyMovement()
    end
})

PlayerTab:Toggle({
    Title = "Noclip",
    Default = false,

    Callback = function(value)

        State.Noclip =
            value
    end
})

PlayerTab:Toggle({
    Title = "Infinite Jump",
    Default = false,

    Callback = function(value)

        State.InfiniteJump =
            value
    end
})

PlayerTab:Button({
    Title = "Restore Movement",

    Callback = function()

        State.WalkSpeed = 16
        State.JumpPower = 50

        ApplyMovement()

        Notify(
            "Movement",
            "Movement restored."
        )
    end
})

PlayerTab:Button({
    Title = "Reset Character",

    Callback = function()

        local hum =
            Humanoid()

        if hum then
            hum.Health = 0
        end
    end
})

PlayerTab:Section({
    Title = "Player Information"
})

PlayerTab:Button({
    Title = "Username",

    Callback = function()

        Notify(
            "Username",
            LocalPlayer.Name
        )
    end
})

PlayerTab:Button({
    Title = "Display Name",

    Callback = function()

        Notify(
            "Display Name",
            LocalPlayer.DisplayName
        )
    end
})

PlayerTab:Button({
    Title = "User ID",

    Callback = function()

        Notify(
            "User ID",
            tostring(
                LocalPlayer.UserId
            )
        )
    end
})

PlayerTab:Button({
    Title = "Account Age",

    Callback = function()

        Notify(
            "Account Age",
            LocalPlayer.AccountAge ..
            " days"
        )
    end
})

PlayerTab:Button({
    Title = "Health",

    Callback = function()

        local hum =
            Humanoid()

        if hum then

            Notify(
                "Health",
                math.floor(
                    hum.Health
                ) ..
                " / " ..
                math.floor(
                    hum.MaxHealth
                )
            )
        end
    end
})

--------------------------------------------------
-- VISUALS
--------------------------------------------------

local VisualsTab =
    Window:Tab({
        Title = "Visuals",
        Icon = "eye"
    })

VisualsTab:Section({
    Title = "ESP"
})

VisualsTab:Toggle({
    Title = "Player ESP",
    Default = false,

    Callback = function(value)

        State.ESP = value

        RefreshESP()
    end
})

VisualsTab:Toggle({
    Title = "ESP Names",
    Default = true,

    Callback = function(value)

        State.ESPNames =
            value

        RefreshESP()
    end
})

VisualsTab:Toggle({
    Title = "ESP Distance",
    Default = true,

    Callback = function(value)

        State.ESPDistance =
            value

        RefreshESP()
    end
})

VisualsTab:Toggle({
    Title = "ESP Tracers",
    Default = true,

    Callback = function(value)

        State.ESPTracers =
            value

        RefreshESP()
    end
})

VisualsTab:Colorpicker({
    Title = "ESP Box Color",

    Default =
        State.ESPColor,

    Callback = function(color)

        State.ESPColor =
            color

        RefreshESP()
    end
})

VisualsTab:Section({
    Title = "Camera"
})

VisualsTab:Slider({
    Title = "Field Of View",

    Value = {
        Min = 40,
        Max = 120,
        Default = 70
    },

    Step = 1,

    Callback = function(value)

        State.FOV =
            value

        if workspace.CurrentCamera then

            workspace.CurrentCamera.FieldOfView =
                value
        end
    end
})

VisualsTab:Button({
    Title = "Reset FOV",

    Callback = function()

        State.FOV = 70

        if workspace.CurrentCamera then

            workspace.CurrentCamera.FieldOfView =
                70
        end
    end
})

VisualsTab:Toggle({
    Title = "Fullbright",
    Default = false,

    Callback = function(value)

        State.Fullbright =
            value

        if value then

            Lighting.Brightness = 2
            Lighting.ClockTime = 14
            Lighting.FogEnd = 100000
            Lighting.GlobalShadows = false
            Lighting.ExposureCompensation =
                0.5

        else

            Lighting.Brightness = 1
            Lighting.GlobalShadows = true
            Lighting.ExposureCompensation =
                0
        end
    end
})

VisualsTab:Toggle({
    Title = "Crosshair",
    Default = false,

    Callback = function(value)

        State.Crosshair =
            value
    end
})

--------------------------------------------------
-- SERVER
--------------------------------------------------

local ServerTab =
    Window:Tab({
        Title = "Server",
        Icon = "server"
    })

ServerTab:Section({
    Title = "Live Server"
})

ServerTab:Button({
    Title = "Player Count",

    Callback = function()

        Notify(
            "Server",
            #Players:GetPlayers() ..
            " players online."
        )
    end
})

ServerTab:Button({
    Title = "Current Ping",

    Callback = function()

        Notify(
            "Ping",
            State.Ping .. "ms"
        )
    end
})

ServerTab:Button({
    Title = "Current FPS",

    Callback = function()

        Notify(
            "FPS",
            tostring(
                State.FPS
            )
        )
    end
})

ServerTab:Button({
    Title = "Server ID",

    Callback = function()

        Notify(
            "Job ID",
            game.JobId
        )
    end
})

ServerTab:Button({
    Title = "Place ID",

    Callback = function()

        Notify(
            "Place ID",
            tostring(
                game.PlaceId
            )
        )
    end
})

ServerTab:Section({
    Title = "Server Hopping"
})

ServerTab:Button({
    Title = "Join Different Server",

    Callback = function()

        Notify(
            "Server Hop",
            "Joining another server..."
        )

        task.wait(0.5)

        pcall(function()

            TeleportService:TeleportAsync(
                game.PlaceId,
                {LocalPlayer},
                {
                    ServerHop = true,
                    FromJobId = game.JobId
                }
            )
        end)
    end
})

ServerTab:Button({
    Title = "Rejoin Current Game",

    Callback = function()

        TeleportService:Teleport(
            game.PlaceId,
            LocalPlayer
        )
    end
})

--------------------------------------------------
-- TELEPORTS
--------------------------------------------------

local TeleportTab =
    Window:Tab({
        Title = "Teleports",
        Icon = "map-pin"
    })

TeleportTab:Section({
    Title = "Locations"
})

TeleportTab:Button({
    Title = "Teleport To Spawn",

    Callback = function()

        local spawnLocation =
            workspace:
            FindFirstChildWhichIsA(
                "SpawnLocation",
                true
            )

        if spawnLocation
            and Root() then

            Root().CFrame =
                spawnLocation.CFrame +
                Vector3.new(0, 3, 0)

            Notify(
                "Teleport",
                "Teleported to spawn."
            )
        end
    end
})

TeleportTab:Section({
    Title = "Players"
})

for _, player in
    ipairs(
        Players:GetPlayers()
    ) do

    if player ~= LocalPlayer then

        TeleportTab:Button({

            Title =
                player.DisplayName,

            Callback = function()

                local character =
                    player.Character

                local targetRoot =
                    character and
                    character:
                    FindFirstChild(
                        "HumanoidRootPart"
                    )

                if targetRoot
                    and Root() then

                    Root().CFrame =
                        targetRoot.CFrame *
                        CFrame.new(
                            3,
                            0,
                            0
                        )

                    Notify(
                        "Teleport",
                        "Moved beside " ..
                        player.DisplayName
                    )
                end
            end
        })
    end
end

--------------------------------------------------
-- FUN
--------------------------------------------------

local FunTab =
    Window:Tab({
        Title = "Fun",
        Icon = "sparkles"
    })

FunTab:Section({
    Title = "Custom Text"
})

FunTab:Input({
    Title = "Message",

    Placeholder =
        "Type something...",

    Default =
        "NEXUZV1 ONLINE",

    Callback = function(value)

        State.FunnyText =
            value
    end
})

FunTab:Button({
    Title = "Show Message",

    Callback = function()

        Notify(
            "NexuzV1",
            State.FunnyText
        )
    end
})

FunTab:Button({
    Title = "Random Message",

    Callback = function()

        local messages = {

            "NEXUZV1 ONLINE",

            "SYSTEMS NOMINAL",

            "WELCOME BACK",

            "UI STATUS: ALIVE",

            "SERVER CONNECTION: ACTIVE",

            "WHO TURNED THE LIGHTS OFF?",

            "FPS CHECK COMPLETE",

            "NEXUZV1 IS ONLINE",

            "PING CHECK COMPLETE"
        }

        local message =
            messages[
                math.random(
                    1,
                    #messages
                )
            ]

        Notify(
            "NexuzV1",
            message
        )
    end
})

FunTab:Button({
    Title = "System Check",

    Callback = function()

        Notify(
            "SYSTEM",
            "FPS " ..
            State.FPS ..
            " | PING " ..
            State.Ping ..
            "ms | PLAYERS " ..
            #Players:GetPlayers()
        )
    end
})

--------------------------------------------------
-- SETTINGS
--------------------------------------------------

local SettingsTab =
    Window:Tab({
        Title = "Settings",
        Icon = "settings"
    })

SettingsTab:Section({
    Title = "Floating HUD"
})

SettingsTab:Toggle({
    Title = "Floating HUD",
    Default = true,

    Callback = function(value)

        SetHUDVisible(value)
    end
})

SettingsTab:Button({
    Title = "Pop Up HUD",

    Callback = function()

        PopHUD()

        HUDFrame.Position =
            UDim2.new(
                1,
                -280,
                0.5,
                -102
            )
    end
})

SettingsTab:Button({
    Title = "Center HUD",

    Callback = function()

        PopHUD()

        HUDFrame.Position =
            UDim2.new(
                0.5,
                -130,
                0.5,
                -102
            )
    end
})

SettingsTab:Button({
    Title = "Top Right HUD",

    Callback = function()

        PopHUD()

        HUDFrame.Position =
            UDim2.new(
                1,
                -280,
                0,
                65
            )
    end
})

SettingsTab:Section({
    Title = "Counters"
})

SettingsTab:Toggle({
    Title = "FPS Counter",
    Default = true,

    Callback = function(value)

        State.FPSCounter =
            value
    end
})

SettingsTab:Toggle({
    Title = "Ping Counter",
    Default = true,

    Callback = function(value)

        State.PingCounter =
            value
    end
})

SettingsTab:Toggle({
    Title = "Player Counter",
    Default = true,

    Callback = function(value)

        State.PlayerCounter =
            value
    end
})

SettingsTab:Toggle({
    Title = "Notifications",
    Default = true,

    Callback = function(value)

        State.Notifications =
            value
    end
})

--------------------------------------------------
-- SMOOTH LOW PERFORMANCE
--------------------------------------------------

SettingsTab:Section({
    Title = "Performance"
})

SettingsTab:Toggle({
    Title = "Low Performance",
    Default = false,

    Callback = function(value)

        State.LowPerformance =
            value

        if value then

            --------------------------------------------------
            -- LIGHTING
            --------------------------------------------------

            Lighting.GlobalShadows =
                false

            Lighting.FogEnd =
                100000

            Lighting.EnvironmentDiffuseScale =
                0

            Lighting.EnvironmentSpecularScale =
                0

            Lighting.Brightness =
                math.min(
                    Lighting.Brightness,
                    1
                )

            --------------------------------------------------
            -- POST EFFECTS
            --------------------------------------------------

            for _, object in
                ipairs(
                    Lighting:GetChildren()
                ) do

                if object:IsA("PostEffect") then
                    object.Enabled = false
                end
            end

            --------------------------------------------------
            -- TERRAIN
            --------------------------------------------------

            pcall(function()

                workspace.Terrain.WaterWaveSize =
                    0

                workspace.Terrain.WaterWaveSpeed =
                    0

                workspace.Terrain.WaterReflectance =
                    0

                workspace.Terrain.WaterTransparency =
                    1
            end)

            --------------------------------------------------
            -- REFRESH ESP AT LOWER UPDATE RATE
            --------------------------------------------------

            if State.ESP then
                RefreshESP()
            end

            Notify(
                "Performance",
                "Smooth performance mode enabled."
            )

        else

            --------------------------------------------------
            -- RESTORE LIGHTING
            --------------------------------------------------

            Lighting.GlobalShadows =
                true

            Lighting.EnvironmentDiffuseScale =
                1

            Lighting.EnvironmentSpecularScale =
                1

            --------------------------------------------------
            -- RESTORE EFFECTS
            --------------------------------------------------

            for _, object in
                ipairs(
                    Lighting:GetChildren()
                ) do

                if object:IsA("PostEffect") then
                    object.Enabled = true
                end
            end

            if State.ESP then
                RefreshESP()
            end

            Notify(
                "Performance",
                "Normal visuals restored."
            )
        end
    end
})

SettingsTab:Button({
    Title = "Reset Visuals",

    Callback = function()

        State.FOV = 70
        State.Fullbright = false
        State.LowPerformance = false

        Lighting.Brightness = 1
        Lighting.GlobalShadows = true

        Lighting.EnvironmentDiffuseScale =
            1

        Lighting.EnvironmentSpecularScale =
            1

        Lighting.ExposureCompensation =
            0

        for _, object in
            ipairs(
                Lighting:GetChildren()
            ) do

            if object:IsA("PostEffect") then
                object.Enabled = true
            end
        end

        if workspace.CurrentCamera then

            workspace.CurrentCamera.FieldOfView =
                70
        end

        Notify(
            "Visuals",
            "Visual settings restored."
        )
    end
})

--------------------------------------------------
-- NOCLIP
--------------------------------------------------

RunService.Stepped:Connect(function()

    if not State.Noclip then
        return
    end

    local char =
        Character()

    if char then

        for _, part in
            ipairs(
                char:GetDescendants()
            ) do

            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
end)

--------------------------------------------------
-- INFINITE JUMP
--------------------------------------------------

UserInputService.JumpRequest:Connect(function()

    if not State.InfiniteJump then
        return
    end

    local hum =
        Humanoid()

    if hum then

        hum:ChangeState(
            Enum.HumanoidStateType.Jumping
        )
    end
end)

--------------------------------------------------
-- CROSSHAIR
--------------------------------------------------

local Crosshair =
    Instance.new("TextLabel")

Crosshair.Name =
    "Crosshair"

Crosshair.BackgroundTransparency = 1

Crosshair.AnchorPoint =
    Vector2.new(
        0.5,
        0.5
    )

Crosshair.Position =
    UDim2.fromScale(
        0.5,
        0.5
    )

Crosshair.Size =
    UDim2.fromOffset(
        35,
        35
    )

Crosshair.Font =
    Enum.Font.GothamBold

Crosshair.Text = "+"

Crosshair.TextColor3 =
    Color3.fromRGB(
        255,
        255,
        255
    )

Crosshair.TextStrokeTransparency = 0

Crosshair.TextSize = 20

Crosshair.Visible = false

Crosshair.Parent = HUD

task.spawn(function()

    while HUD.Parent do

        Crosshair.Visible =
            State.Crosshair

        task.wait(0.1)
    end
end)

--------------------------------------------------
-- CHARACTER RESPAWN
--------------------------------------------------

LocalPlayer.CharacterAdded:Connect(function()

    task.wait(0.5)

    ApplyMovement()

    if State.ESP then

        task.wait(0.5)

        RefreshESP()
    end
end)

--------------------------------------------------
-- START
--------------------------------------------------

task.wait(0.5)

PopHUD()

Notify(
    "NexuzV1",
    "Online Edition loaded."
)
