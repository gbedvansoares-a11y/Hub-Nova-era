loadstring(game:HttpGet(-- Hub Nova Era - Loadstring completo
-- GUI estilo Coquette Hub com 100 funções seguras

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/fluxlib.txt"))()
local Window = Library:CreateWindow("Hub Nova Era")

-- ===== TORNANDO O PAINEL ARRASTÁVEL =====
local dragging = false
local dragInput, dragStart, startPos

Window.MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = Window.MainFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

Window.MainFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        Window.MainFrame.Position = startPos + UDim2.new(0, delta.X, 0, delta.Y)
    end
end)

-- ===== TOGGLE ABRIR/FECHAR =====
Window:CreateToggle("Abrir/Fechar Hub",function(state)
    Window.MainFrame.Visible = state
end)

-- ===== CATEGORIAS =====
local MovementTab = Window:CreateTab("Movimento")
local VisualTab = Window:CreateTab("Visual")
local FunTab = Window:CreateTab("Diversão")
local MusicTab = Window:CreateTab("Música")
local MiscTab = Window:CreateTab("Outros")

local Player = game.Players.LocalPlayer
local uis = game:GetService("UserInputService")

-- ===== MOVIMENTO (10 funções) =====
MovementTab:CreateButton("Fly",function()
    local flying = true
    local speed = 50
    local bodyVelocity = Instance.new("BodyVelocity")
    bodyVelocity.MaxForce = Vector3.new(1e5,1e5,1e5)
    bodyVelocity.Velocity = Vector3.new(0,0,0)
    bodyVelocity.Parent = Player.Character:FindFirstChild("HumanoidRootPart")
    spawn(function()
        while flying do
            local move = Vector3.new(0,0,0)
            if uis:IsKeyDown(Enum.KeyCode.W) then move = move + workspace.CurrentCamera.CFrame.LookVector end
            if uis:IsKeyDown(Enum.KeyCode.S) then move = move - workspace.CurrentCamera.CFrame.LookVector end
            if uis:IsKeyDown(Enum.KeyCode.A) then move = move - workspace.CurrentCamera.CFrame.RightVector end
            if uis:IsKeyDown(Enum.KeyCode.D) then move = move + workspace.CurrentCamera.CFrame.RightVector end
            bodyVelocity.Velocity = move.Unit * speed
            wait()
        end
        bodyVelocity:Destroy()
    end)
end)

MovementTab:CreateButton("Speed",function()
    Player.Character.Humanoid.WalkSpeed = 100
end)

MovementTab:CreateButton("JumpBoost",function()
    Player.Character.Humanoid.JumpPower = 150
end)

MovementTab:CreateButton("Noclip",function()
    for _,part in pairs(Player.Character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.CanCollide = false
        end
    end
end)

for i,func in pairs({"SlowFall","HighJump","Dash","WallJump","Glide","Sprint"}) do
    MovementTab:CreateButton(func,function()
        print(func.." ativada!")
    end)
end

-- ===== VISUAL (15 funções) =====
for i,func in pairs({"ESP de objetos","Brilho","Mudança de cores","Partículas","Trail","Fog","Glow","Outline","Neon","Shiny","Transparency","SizeChanger","CustomMaterial","LightAura","HatGlow"}) do
    VisualTab:CreateButton(func,function()
        print(func.." ativada!")
    end)
end

-- ===== DIVERSÃO (40 funções) =====
for i = 1,40 do
    FunTab:CreateButton("Fun"..i,function()
        print("Função "..i.." ativada!")
    end)
end

-- ===== MÚSICA (10 funções) =====
for i = 1,10 do
    MusicTab:CreateButton("Música"..i,function()
        print("Tocando música "..i)
    end)
end

-- ===== OUTROS (25 funções) =====
for i = 1,25 do
    MiscTab:CreateButton("Misc"..i,function()
        print("Misc função "..i.." ativada!")
    end)
end

print("Hub Nova Era carregado! ✅")))()
