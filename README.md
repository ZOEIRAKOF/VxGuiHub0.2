-- ============================================
--  VxGuiHub - Painel Om (v3.8) — COMPLETO
-- ============================================

-- CONFIG
local CFG = {
    Nome     = "VxGuiHub - Painel Om",
    Cor      = Color3.fromRGB(30, 100, 220),
    CorDark  = Color3.fromRGB(20, 20, 30),
    CorTxt   = Color3.fromRGB(255, 255, 255),
    Tamanho  = UDim2.new(0, 320, 0, 420),
    LogoID   = "rbxassetid://131377687077341",
    AimID    = "rbxassetid://84459412139159",
    AvisoFile = "VxGuiHub_Accepted.txt",
    YT_Link   = "https://youtube.com/@zoeirakof?si=tgKzQMS56xgadJRb",
}

-- SERVIÇOS
local Players = game:GetService("Players")
local UIS     = game:GetService("UserInputService")
local Tween   = game:GetService("TweenService")
local LP      = Players.LocalPlayer

-- HELPERS
local function novo(cls, props, parent)
    local obj = Instance.new(cls)
    for k, v in pairs(props or {}) do obj[k] = v end
    if parent then obj.Parent = parent end
    return obj
end

local function canto(obj, raio)
    return novo("UICorner", {CornerRadius = UDim.new(0, raio or 6)}, obj)
end

-- VERIFICA AVISO
local jaAceitou = false
pcall(function()
    if isfile and isfile(CFG.AvisoFile) then
        jaAceitou = true
    end
end)

-- ============================================
--  AVISO DE SEGURANÇA
-- ============================================
if not jaAceitou then
    local AvisoGui = novo("ScreenGui", {
        Name = "VxAviso",
        ResetOnSpawn = false,
        IgnoreGuiInset = true,
        DisplayOrder = 999,
    }, LP:WaitForChild("PlayerGui"))

    local Fundo = novo("Frame", {
        Size = UDim2.new(1, 0, 1, 0),
        BackgroundColor3 = Color3.new(0, 0, 0),
        BackgroundTransparency = 0.5,
        BorderSizePixel = 0,
    }, AvisoGui)

    local Box = novo("Frame", {
        Size = UDim2.new(0, 340, 0, 340),
        Position = UDim2.new(0.5, -170, 0.5, -170),
        BackgroundColor3 = CFG.CorDark,
        BorderSizePixel = 0,
    }, Fundo)
    canto(Box, 14)

    novo("UIStroke", {
        Color = Color3.fromRGB(220, 60, 60),
        Thickness = 2,
    }, Box)

    local Topo = novo("Frame", {
        Size = UDim2.new(1, 0, 0, 45),
        BackgroundColor3 = Color3.fromRGB(180, 40, 40),
        BorderSizePixel = 0,
    }, Box)
    canto(Topo, 14)

    novo("TextLabel", {
        Size = UDim2.new(1, -20, 1, 0),
        Position = UDim2.new(0, 10, 0, 0),
        BackgroundTransparency = 1,
        Text = "⚠️  AVISO IMPORTANTE",
        TextColor3 = Color3.new(1, 1, 1),
        TextSize = 16,
        Font = Enum.Font.GothamBold,
        TextXAlignment = Enum.TextXAlignment.Center,
    }, Topo)

    novo("TextLabel", {
        Size = UDim2.new(1, -30, 0, 220),
        Position = UDim2.new(0, 15, 0, 60),
        BackgroundTransparency = 1,
        Text = "VxGuiHub - Painel Om\n\n" ..
               "• Alguns scripts ficam PERMANENTES\n  depois de executados\n\n" ..
               "• Alguns podem TRAVAR o jogo\n\n" ..
               "• Alguns podem pegar no MOBILE\n\n" ..
               "Use com cautela e por sua conta\n" ..
               "e risco.",
        TextColor3 = Color3.fromRGB(220, 220, 220),
        TextSize = 12,
        Font = Enum.Font.Gotham,
        TextWrapped = true,
        TextXAlignment = Enum.TextXAlignment.Left,
        TextYAlignment = Enum.TextYAlignment.Top,
    }, Box)

    local BtnOK = novo("TextButton", {
        Size = UDim2.new(0, 280, 0, 42),
        Position = UDim2.new(0.5, -140, 1, -55),
        BackgroundColor3 = Color3.fromRGB(40, 160, 80),
        Text = "ENTENDI E ACEITO",
        TextColor3 = Color3.new(1, 1, 1),
        TextSize = 14,
        Font = Enum.Font.GothamBold,
        BorderSizePixel = 0,
        AutoButtonColor = false,
    }, Box)
    canto(BtnOK, 8)

    novo("UIStroke", {
        Color = Color3.fromRGB(80, 220, 130),
        Thickness = 2,
    }, BtnOK)

    BtnOK.MouseButton1Click:Connect(function()
        pcall(function()
            if writefile then
                writefile(CFG.AvisoFile, "aceito")
            end
        end)
        AvisoGui:Destroy()
    end)

    repeat task.wait(0.1) until not AvisoGui.Parent
end

-- ============================================
--  HUB PRINCIPAL
-- ============================================

local Gui = novo("ScreenGui", {
    Name = "VxGuiHub",
    ResetOnSpawn = false,
    IgnoreGuiInset = true,
    Parent = LP:WaitForChild("PlayerGui")
})

local Janela = novo("Frame", {
    Size = CFG.Tamanho,
    Position = UDim2.new(0.5, -CFG.Tamanho.X.Offset/2, 0.5, -CFG.Tamanho.Y.Offset/2),
    BackgroundColor3 = CFG.CorDark,
    BorderSizePixel = 0,
}, Gui)
canto(Janela, 10)

local Titulo = novo("Frame", {
    Size = UDim2.new(1, 0, 0, 40),
    BackgroundColor3 = CFG.Cor,
    BorderSizePixel = 0,
    Active = true,
}, Janela)
canto(Titulo, 10)

novo("ImageLabel", {
    Size = UDim2.new(0, 26, 0, 26),
    Position = UDim2.new(0, 10, 0, 7),
    BackgroundTransparency = 1,
    Image = CFG.LogoID,
    ScaleType = Enum.ScaleType.Fit,
}, Titulo)

novo("TextLabel", {
    Size = UDim2.new(1, -50, 1, 0),
    Position = UDim2.new(0, 42, 0, 0),
    BackgroundTransparency = 1,
    Text = CFG.Nome,
    TextColor3 = CFG.CorTxt,
    TextSize = 15,
    Font = Enum.Font.GothamBold,
    TextXAlignment = Enum.TextXAlignment.Left,
}, Titulo)

local function botaoTitulo(txt, cor, posX, callback)
    local b = novo("TextButton", {
        Size = UDim2.new(0, 30, 0, 30),
        Position = UDim2.new(1, posX, 0, 5),
        BackgroundColor3 = cor,
        Text = txt,
        TextColor3 = Color3.new(1,1,1),
        Font = Enum.Font.GothamBold,
        TextSize = 16,
        BorderSizePixel = 0,
    }, Titulo)
    canto(b, 6)
    b.MouseButton1Click:Connect(callback)
    return b
end

local BtnMin    = botaoTitulo("—", Color3.fromRGB(220,160,30), -70)
local BtnFechar = botaoTitulo("X", Color3.fromRGB(200,50,50),   -35)

local Flutuante = novo("TextButton", {
    Size = UDim2.new(0, 55, 0, 55),
    Position = UDim2.new(0, 15, 0.5, -27),
    BackgroundColor3 = CFG.Cor,
    Text = "",
    BorderSizePixel = 0,
    Active = true,
    Draggable = true,
    Visible = false,
}, Gui)
canto(Flutuante, 999)

local LogoFlutuante = novo("ImageLabel", {
    Size = UDim2.new(1, -6, 1, -6),
    Position = UDim2.new(0, 3, 0, 3),
    BackgroundTransparency = 1,
    Image = CFG.LogoID,
    ScaleType = Enum.ScaleType.Fit,
}, Flutuante)
canto(LogoFlutuante, 999)

local function mostrar()  Janela.Visible = true  Flutuante.Visible = false end
local function esconder() Janela.Visible = false Flutuante.Visible = true  end

Flutuante.MouseButton1Click:Connect(mostrar)
BtnMin.MouseButton1Click:Connect(esconder)
BtnFechar.MouseButton1Click:Connect(esconder)

-- ABAS
local AbasFrame = novo("Frame", {
    Size = UDim2.new(1, -20, 0, 30),
    Position = UDim2.new(0, 10, 0, 45),
    BackgroundTransparency = 1,
}, Janela)

novo("UIListLayout", {
    FillDirection = Enum.FillDirection.Horizontal,
    HorizontalAlignment = Enum.HorizontalAlignment.Center,
    Padding = UDim.new(0, 4),
    SortOrder = Enum.SortOrder.LayoutOrder,
}, AbasFrame)

local abas = {}

local function criarAba(nome)
    local id = #abas + 1
    local btn = novo("TextButton", {
        Size = UDim2.new(0.24, 0, 1, 0),
        BackgroundColor3 = CFG.Cor,
        BackgroundTransparency = 0.35,
        Text = nome,
        TextColor3 = CFG.CorTxt,
        TextSize = 11,
        Font = Enum.Font.GothamBold,
        BorderSizePixel = 0,
        LayoutOrder = id,
    }, AbasFrame)
    canto(btn)

    local cont = novo("ScrollingFrame", {
        Size = UDim2.new(1, -20, 1, -95),
        Position = UDim2.new(0, 10, 0, 85),
        BackgroundTransparency = 1,
        BorderSizePixel = 0,
        ScrollBarThickness = 5,
        ScrollBarImageColor3 = CFG.Cor,
        AutomaticCanvasSize = Enum.AutomaticSize.Y,
        CanvasSize = UDim2.new(0,0,0,0),
        Visible = false,
    }, Janela)

    novo("UIListLayout", {
        Padding = UDim.new(0, 6),
        SortOrder = Enum.SortOrder.LayoutOrder,
    }, cont)

    novo("UIPadding", {PaddingTop = UDim.new(0, 4)}, cont)

    abas[id] = {btn = btn, cont = cont}

    btn.MouseButton1Click:Connect(function()
        for i, aba in pairs(abas) do
            local ativa = (i == id)
            aba.cont.Visible = ativa
            aba.btn.BackgroundTransparency = ativa and 0 or 0.35
        end
    end)

    return cont
end

local AbaESP       = criarAba("ESP")
local AbaChars     = criarAba("PERS")
local AbaAssassino = criarAba("ASSAS")
local AbaCriador   = criarAba("CRIADOR")

for i, aba in pairs(abas) do
    local ativa = (i == 1)
    aba.cont.Visible = ativa
    aba.btn.BackgroundTransparency = ativa and 0 or 0.35
end

-- ARRASTAR
do
    local drag, ini, startPos
    Titulo.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1
        or i.UserInputType == Enum.UserInputType.Touch then
            drag = true
            ini = i.Position
            startPos = Janela.Position
        end
    end)
    Titulo.InputEnded:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1
        or i.UserInputType == Enum.UserInputType.Touch then
            drag = false
        end
    end)
    UIS.InputChanged:Connect(function(i)
        if drag and (i.UserInputType == Enum.UserInputType.MouseMovement
        or i.UserInputType == Enum.UserInputType.Touch) then
            local d = i.Position - ini
            Janela.Position = UDim2.new(
                startPos.X.Scale, startPos.X.Offset + d.X,
                startPos.Y.Scale, startPos.Y.Offset + d.Y
            )
        end
    end)
end

-- FUNÇÕES DE BOTÃO
local function addBotao(nome, cor, url, container)
    local ativo = false
    local tweenAtual = nil

    local btn = novo("TextButton", {
        Size = UDim2.new(1, 0, 0, 36),
        BackgroundColor3 = cor,
        BackgroundTransparency = 0.35,
        Text = nome,
        TextColor3 = CFG.CorTxt,
        TextSize = 15,
        Font = Enum.Font.GothamBold,
        BorderSizePixel = 0,
    }, container)
    canto(btn)

    local stroke = novo("UIStroke", {
        Color = Color3.new(1,1,1),
        Thickness = 0,
        Transparency = 1,
    }, btn)

    btn.MouseEnter:Connect(function()
        if not ativo then btn.BackgroundTransparency = 0.15 end
    end)
    btn.MouseLeave:Connect(function()
        if not ativo then btn.BackgroundTransparency = 0.35 end
    end)

    btn.MouseButton1Click:Connect(function()
        if ativo then
            ativo = false
            btn.BackgroundTransparency = 0.35
            if tweenAtual then tweenAtual:Cancel() end
            stroke.Thickness = 0
            stroke.Transparency = 1
        else
            ativo = true
            btn.BackgroundTransparency = 0
            local info = TweenInfo.new(0.8, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut, -1, true)
            tweenAtual = Tween:Create(stroke, info, {Thickness = 4, Transparency = 0})
            tweenAtual:Play()
            pcall(function()
                loadstring(game:HttpGet(url))()
            end)
        end
    end)
end

local function addScript(nome, cor, codigo, container)
    local ativo = false
    local tweenAtual = nil

    local btn = novo("TextButton", {
        Size = UDim2.new(1, 0, 0, 36),
        BackgroundColor3 = cor,
        BackgroundTransparency = 0.35,
        Text = nome,
        TextColor3 = CFG.CorTxt,
        TextSize = 15,
        Font = Enum.Font.GothamBold,
        BorderSizePixel = 0,
    }, container)
    canto(btn)

    local stroke = novo("UIStroke", {
        Color = Color3.new(1,1,1),
        Thickness = 0,
        Transparency = 1,
    }, btn)

    btn.MouseEnter:Connect(function()
        if not ativo then btn.BackgroundTransparency = 0.15 end
    end)
    btn.MouseLeave:Connect(function()
        if not ativo then btn.BackgroundTransparency = 0.35 end
    end)

    btn.MouseButton1Click:Connect(function()
        if ativo then
            ativo = false
            btn.BackgroundTransparency = 0.35
            if tweenAtual then tweenAtual:Cancel() end
            stroke.Thickness = 0
            stroke.Transparency = 1
        else
            ativo = true
            btn.BackgroundTransparency = 0
            local info = TweenInfo.new(0.8, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut, -1, true)
            tweenAtual = Tween:Create(stroke, info, {Thickness = 4, Transparency = 0})
            tweenAtual:Play()
            pcall(codigo)
        end
    end)
end

local function addScriptRainbow(nome, codigo, container)
    local ativo = false
    local tweenAtual = nil
    local rainbowAtivo = true
    local tempo = 0

    local btn = novo("TextButton", {
        Size = UDim2.new(1, 0, 0, 36),
        BackgroundColor3 = Color3.fromRGB(180, 60, 220),
        BackgroundTransparency = 0.35,
        Text = nome,
        TextColor3 = CFG.CorTxt,
        TextSize = 15,
        Font = Enum.Font.GothamBold,
        BorderSizePixel = 0,
    }, container)
    canto(btn)

    local stroke = novo("UIStroke", {
        Color = Color3.new(1,1,1),
        Thickness = 0,
        Transparency = 1,
    }, btn)

    task.spawn(function()
        while rainbowAtivo and btn.Parent do
            tempo = (tempo + 0.008) % 1
            local cor = Color3.fromHSV(tempo, 0.9, 1)
            btn.BackgroundColor3 = cor
            task.wait(0.03)
        end
    end)

    btn.MouseEnter:Connect(function()
        if not ativo then btn.BackgroundTransparency = 0.15 end
    end)
    btn.MouseLeave:Connect(function()
        if not ativo then btn.BackgroundTransparency = 0.35 end
    end)

    btn.MouseButton1Click:Connect(function()
        if ativo then
            ativo = false
            btn.BackgroundTransparency = 0.35
            if tweenAtual then tweenAtual:Cancel() end
            stroke.Thickness = 0
            stroke.Transparency = 1
        else
            ativo = true
            btn.BackgroundTransparency = 0
            local info = TweenInfo.new(0.8, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut, -1, true)
            tweenAtual = Tween:Create(stroke, info, {Thickness = 4, Transparency = 0})
            tweenAtual:Play()
            pcall(codigo)
        end
    end)
end

-- ============================================
--  ABA ESP / UTIL
-- ============================================

addBotao("Infinite Yield", Color3.fromRGB(30,100,220),
    "https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source", AbaESP)

addBotao("ESP GERAL", Color3.fromRGB(130,60,200),
    "https://pastebin.com/raw/E90bbcdw", AbaESP)

addBotao("Insta Revive", Color3.fromRGB(30,160,60),
    "https://rawscripts.net/raw/Universal-Script-insta-revive-228036", AbaESP)

addBotao("Anti-Void", Color3.fromRGB(40,200,220),
    "https://rawscripts.net/raw/Outcome-Memories-v0.2-NOT-PERFECT-anti-void-239371", AbaESP)

addScript("No Trap (Tails Doll)", Color3.fromRGB(200,60,160), function()
    task.spawn(function()
        while true do
            local projectile = workspace:FindFirstChild("Projectile")
            if projectile then
                local traps = projectile:FindFirstChild("Traps")
                if traps and traps:IsA("Folder") then
                    traps:Destroy()
                end
            end
            task.wait(0.2)
        end
    end)
    workspace.DescendantAdded:Connect(function(obj)
        if obj:IsA("Folder") and obj.Name == "Traps"
        and obj.Parent and obj.Parent.Name == "Projectile" then
            obj:Destroy()
        end
    end)
end, AbaESP)

addScript("T Pose", Color3.fromRGB(240, 240, 240), function()
    local RunService = game:GetService("RunService")
    local character = LP.Character
    if not character then return end

    if _G.TPoseLoop then _G.TPoseLoop:Disconnect() end

    local function clearAnims(model)
        for _, obj in ipairs(model:GetDescendants()) do
            if obj:IsA("Animator") or obj:IsA("AnimationTrack") or obj:IsA("Animation") then
                obj:Destroy()
            end
        end
    end
    clearAnims(character)

    local oldNamecall
    oldNamecall = hookmetamethod(game, "__namecall", function(self, ...)
        local method = getnamecallmethod()
        local args = {...}
        if method == "FindFirstChild" or method == "FindFirstChildOfClass" or method == "WaitForChild" then
            if args[1] == "Animator" or args[1] == "AnimationController" then
                return nil
            end
        end
        if method == "LoadAnimation" or method == "loadAnimation" then
            return nil
        end
        return oldNamecall(self, ...)
    end)

    local motors, bones = {}, {}
    for _, item in ipairs(character:GetDescendants()) do
        if item:IsA("Motor6D") or item:IsA("Motor") then
            table.insert(motors, item)
        elseif item:IsA("Bone") then
            table.insert(bones, item)
        end
    end

    _G.TPoseLoop = RunService.PreRender:Connect(function()
        if not character or not character.Parent then
            if _G.TPoseLoop then _G.TPoseLoop:Disconnect() end
            return
        end
        local hum = character:FindFirstChildOfClass("Humanoid") or character:FindFirstChildOfClass("AnimationController")
        if hum then
            local anim = hum:FindFirstChildOfClass("Animator")
            if anim then anim:Destroy() end
        end
        for _, motor in ipairs(motors) do
            if motor and motor.Parent then motor.Transform = CFrame.new() end
        end
        for _, bone in ipairs(bones) do
            if bone and bone.Parent then bone.CFrame = CFrame.new(bone.CFrame.Position) end
        end
    end)
end, AbaESP)

-- ============================================
--  ABA PERSONAGENS
-- ============================================

addBotao("Tails Fly", Color3.fromRGB(230,190,40),
    "https://rawscripts.net/raw/Universal-Script-Tails-fly-inf-227277", AbaChars)

addBotao("Eggman Fake Double Jump", Color3.fromRGB(230,130,30),
    "https://rawscripts.net/raw/Universal-Script-Eggman-fake-double-jump-230167", AbaChars)

addBotao("Knuckle Ova", Color3.fromRGB(180,40,40),
    "https://pastebin.com/raw/LWQ8uguL", AbaChars)

addBotao("Sonic Ova", Color3.fromRGB(30, 100, 220),
    "https://rawscripts.net/raw/Outcome-Memories-v0.2-Ova-sonic-216795", AbaChars)

addBotao("Metal Sonic Ova", Color3.fromRGB(40, 200, 220),
    "https://rawscripts.net/raw/Outcome-Memories-v0.2-Metal-Sonic-Rework-Reupload-202009", AbaChars)

addBotao("Eggman buff (Goat)", Color3.fromRGB(230, 130, 30),
    "https://rawscripts.net/raw/Outcome-Memories-v0.2-Eggman-custom-moveset-125899", AbaChars)

addScriptRainbow("Homing attack VARIANT", function()
    local RunService = game:GetService("RunService")
    local UIS = game:GetService("UserInputService")
    local TweenService = game:GetService("TweenService")
    local Players = game:GetService("Players")
    local player = LP
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    local root = character:WaitForChild("HumanoidRootPart")

    local HOVER_HEIGHT = 20
    local HOVER_DURATION = 4
    local ASCEND_TIME = 0.6
    local DASH_SPEED = 275
    local DASH_STOP_DISTANCE = 3
    local MOUSE_HITBOX_RADIUS = 30
    local HIGHLIGHT_RADIUS = 200
    local MULTI_HOMING_COUNT = 3
    local MULTI_HOMING_INTERVAL = 0.7

    local isHovering = false
    local hoverStart = 0
    local highlights = {}

    local function highlightPlayers()
        for _, p in ipairs(Players:GetPlayers()) do
            if p ~= player and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                local distance = (p.Character.HumanoidRootPart.Position - root.Position).Magnitude
                if distance <= HIGHLIGHT_RADIUS and not highlights[p] then
                    local highlight = Instance.new("Highlight")
                    highlight.Adornee = p.Character
                    highlight.FillTransparency = 1
                    highlight.OutlineColor = Color3.new(1,1,1)
                    highlight.OutlineTransparency = 0
                    highlight.Parent = p.Character
                    highlights[p] = highlight
                end
            end
        end
    end

    local function removeHighlights()
        for _, hl in pairs(highlights) do
            if hl then hl:Destroy() end
        end
        highlights = {}
    end

    local function startHover()
        if isHovering then return end
        isHovering = true
        hoverStart = tick()
        humanoid.AutoRotate = false
        humanoid:ChangeState(Enum.HumanoidStateType.Physics)
        highlightPlayers()
        local targetCFrame = root.CFrame + Vector3.new(0, HOVER_HEIGHT, 0)
        TweenService:Create(root, TweenInfo.new(ASCEND_TIME, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {CFrame = targetCFrame}):Play()
    end

    local function stopHover()
        isHovering = false
        humanoid.AutoRotate = true
        humanoid:ChangeState(Enum.HumanoidStateType.Freefall)
        removeHighlights()
    end

    local function dashToPlayer(p)
        if not p or not p.Character or not p.Character:FindFirstChild("HumanoidRootPart") then return end
        game:GetService("VirtualUser"):CaptureController()
        game:GetService("VirtualUser"):Button1Down(Vector2.new())
        stopHover()
        local connection
        connection = RunService.Heartbeat:Connect(function()
            if not root or not p.Character or not p.Character:FindFirstChild("HumanoidRootPart") then
                connection:Disconnect()
                return
            end
            local direction = p.Character.HumanoidRootPart.Position - root.Position
            if direction.Magnitude < DASH_STOP_DISTANCE then
                connection:Disconnect()
                root.Velocity = Vector3.new(0,0,0)
                return
            end
            local moveVector = direction.Unit * DASH_SPEED
            root.Velocity = Vector3.new(moveVector.X, moveVector.Y, moveVector.Z)
        end)
    end

    local function multiHome(p)
        for i = 1, MULTI_HOMING_COUNT do
            task.delay(MULTI_HOMING_INTERVAL * i, function()
                if p and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                    dashToPlayer(p)
                end
            end)
        end
    end

    UIS.InputBegan:Connect(function(input, gp)
        if gp then return end
        if input.KeyCode == Enum.KeyCode.R then startHover() end
    end)

    local mouse = player:GetMouse()
    mouse.Button1Down:Connect(function()
        if not isHovering then return end
        local closestPlayer, closestDistance = nil, math.huge
        for _, p in ipairs(Players:GetPlayers()) do
            if p ~= player and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                local distance = (p.Character.HumanoidRootPart.Position - mouse.Hit.Position).Magnitude
                if distance <= MOUSE_HITBOX_RADIUS and distance < closestDistance then
                    closestDistance = distance
                    closestPlayer = p
                end
            end
        end
        if closestPlayer then
            dashToPlayer(closestPlayer)
            multiHome(closestPlayer)
        end
    end)

    RunService.Heartbeat:Connect(function()
        if not isHovering then return end
        if tick() - hoverStart >= HOVER_DURATION then
            stopHover()
        else
            root.Velocity = Vector3.new(0,0,0)
        end
    end)
end, AbaChars)

addScript("Sonic Spindash Inst", Color3.fromRGB(30, 100, 220), function()
    local Players = game:GetService("Players")
    local UIS = game:GetService("UserInputService")
    local player = LP

    local function IsEXE(model)
        if not model then return false end
        local targetName = model:GetAttribute("Character") or model.Name
        local killers = {"TailsDoll", "Kolossos", "2011x", "Fleetway", "Tripwire", "Furnace", "Lord X", "EXE"}
        for _, k in pairs(killers) do
            if string.find(string.lower(tostring(targetName)), string.lower(k)) then return true end
        end
        return false
    end

    local FIRST_RADIUS, OTHER_RADIUS = 5, 40
    local FIRST_CD, OTHER_CD = 0.6, 0.5
    local TOTAL_HITS = 4
    local LAUNCH_SPEED = 160

    local function getRoot()
        local character = player.Character or player.CharacterAdded:Wait()
        return character:WaitForChild("HumanoidRootPart")
    end

    local function getNearestEXE(radius, root)
        local nearest, shortest = nil, radius
        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") and IsEXE(plr.Character) then
                local dist = (plr.Character.HumanoidRootPart.Position - root.Position).Magnitude
                if dist <= shortest then shortest = dist nearest = plr end
            end
        end
        return nearest
    end

    local function launchTo(target, root)
        if not target or not target.Character then return end
        local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
        if not targetRoot then return end
        local direction = (targetRoot.Position - root.Position).Unit
        root.AssemblyLinearVelocity = direction * LAUNCH_SPEED
    end

    local function doHits()
        local root = getRoot()
        for hit = 1, TOTAL_HITS do
            if not root.Parent then return end
            if hit == 1 then
                getNearestEXE(FIRST_RADIUS, root)
                task.wait(FIRST_CD)
            else
                local target = getNearestEXE(OTHER_RADIUS, root)
                if target then launchTo(target, root) end
                task.wait(OTHER_CD)
            end
        end
    end

    local function triggerAbility()
        task.spawn(function()
            pcall(function()
                player.PlayerGui.Round.Game.RemoteFunction:InvokeServer(1)
            end)
        end)
        task.spawn(doHits)
    end

    UIS.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        if input.KeyCode == Enum.KeyCode.R then triggerAbility() end
    end)
end, AbaChars)

-- Silent Aim Amy
addScriptRainbow("Silent Aim Amy (Blazer, Silver)", function()
    local Players = game:GetService("Players")
    local Workspace = game:GetService("Workspace")
    local RunService = game:GetService("RunService")
    local Camera = Workspace.CurrentCamera
    local player = LP

    local unpack = table.unpack or unpack
    local newcclosure = newcclosure or function(f) return f end

    local Config = {
        active = true,
        projSpeed = 300,
        leadMul = 1.0,
        smooth = true,
        predict = true,
        targetPart = "UpperTorso",
        stickyEnabled = true,
        stickyTime = 8,
        priority = "nearest",
        maxDist = 500,
        minDist = 0,
        hitChance = 100,
        adaptiveLead = true,
        dirChangeDetect = true,
        airPredict = true,
    }

    local State = {
        posRock = nil, dirRock = nil,
        name = nil, amIChar = false,
        targetPart = nil, targetChar = nil,
        origin = Vector3.zero,
        interceptTime = 0,
        hookMouse2 = false, hookNC = false,
        lastTargetKey = nil,
        stickyLockKey = nil,
        stickySince = 0,
        targetState = "Grounded",
    }

    local function isKiller(model)
        if not model or not model.Parent then return false end
        if not model:IsA("Model") then return false end
        return model:GetAttribute("Team") == "EXE"
    end

    local function isAlive(model)
        if not model then return false end
        local h = model:FindFirstChildOfClass("Humanoid")
        return h and h.Health > 0
    end

    local function getHP(model)
        if not model then return 0 end
        local h = model:FindFirstChildOfClass("Humanoid")
        return h and h.Health or 0
    end

    local function findPart(char)
        if not char or not char.Parent then return nil end        return char:FindFirstChild(Config.targetPart)
            or char:FindFirstChild("UpperTorso")
            or char:FindFirstChild("Torso")
            or char:FindFirstChild("HumanoidRootPart")
            or char:FindFirstChild("Head")
    end

    local function getOrigin(char)
        if not char or not char.Parent then return Vector3.zero end
        local head = char:FindFirstChild("Head")
        if head then return head.Position end
        local hrp = char:FindFirstChild("HumanoidRootPart")
        if hrp then return hrp.Position + Vector3.new(0, 1.5, 0) end
        return Vector3.zero
    end

    local function getHumanoidState(char)
        if not char then return "Grounded" end
        local hum = char:FindFirstChildOfClass("Humanoid")
        if not hum then return "Grounded" end
        local ok, state = pcall(function() return hum:GetState() end)
        if not ok or not state then return "Grounded" end
        if state == Enum.HumanoidStateType.Jumping then return "Jumping" end
        if state == Enum.HumanoidStateType.Freefall then return "Falling" end
        return "Grounded"
    end

    local velHistory = {}
    local HISTORY_SIZE = 12

    local function pushSample(pos, key)
        if key ~= State.lastTargetKey then
            velHistory = {}
            State.lastTargetKey = key
        end
        table.insert(velHistory, {pos = pos, t = tick()})
        while #velHistory > HISTORY_SIZE do
            table.remove(velHistory, 1)
        end
        local now = tick()
        for i = #velHistory, 1, -1 do
            if now - velHistory[i].t > 0.4 then
                table.remove(velHistory, i)
            end
        end
    end

    local function getSmoothedVelocity(part)
        if #velHistory < 2 then
            return part.AssemblyLinearVelocity or Vector3.zero
        end
        local totalVel, totalWeight = Vector3.zero, 0
        local now = tick()
        for i = 2, #velHistory do
            local p1, p2 = velHistory[i-1], velHistory[i]
            local dt = p2.t - p1.t
            if dt > 0.001 then
                local v = (p2.pos - p1.pos) / dt
                local w = 1 / (now - p2.t + 0.05)
                totalVel = totalVel + v * w
                totalWeight = totalWeight + w
            end
        end
        if totalWeight <= 0 then
            return part.AssemblyLinearVelocity or Vector3.zero
        end
        return totalVel / totalWeight
    end

    local function getDirectionChangeFactor()
        if not Config.dirChangeDetect then return 0 end
        if #velHistory < 4 then return 0 end
        local first = velHistory[1]
        local midIdx = math.max(2, math.floor(#velHistory / 2))
        local mid = velHistory[midIdx]
        local last = velHistory[#velHistory]
        local v1 = mid.pos - first.pos
        local v2 = last.pos - mid.pos
        if v1.Magnitude < 0.1 or v2.Magnitude < 0.1 then return 0 end
        local dot = v1.Unit:Dot(v2.Unit)
        return math.clamp((1 - dot) * 0.5, 0, 1)
    end

    local function solveIntercept(origin, targetPos, targetVel, speed)
        if type(speed) ~= "number" or speed <= 0 then return nil end
        local D = targetPos - origin
        local V = targetVel
        local S = speed
        local a = V:Dot(V) - S*S
        local b = 2 * D:Dot(V)
        local c = D:Dot(D)

        if math.abs(a) < 1e-6 then
            if math.abs(b) < 1e-6 then return nil end
            local t = -c / b
            return (t > 0 and t < 3) and t or nil
        end

        local disc = b*b - 4*a*c
        if disc < 0 then return nil end

        local sq = math.sqrt(disc)
        local t1 = (-b + sq) / (2*a)
        local t2 = (-b - sq) / (2*a)

        local best = nil
        if t1 > 0 and t2 > 0 then best = math.min(t1, t2)
        elseif t1 > 0 then best = t1
        elseif t2 > 0 then best = t2 end

        if best and best > 0 and best < 3 then return best end
        return nil
    end

    local function computePos(targetPart, origin, speed)
        if not targetPart or not targetPart.Parent then return nil end
        local curPos = targetPart.Position
        if not Config.predict then return curPos end

        local vel
        if Config.smooth then vel = getSmoothedVelocity(targetPart)
        else vel = targetPart.AssemblyLinearVelocity or Vector3.zero end
        if vel.Magnitude > 400 then vel = vel.Unit * 400 end

        local t = solveIntercept(origin, curPos, vel, speed)
        if not t then return curPos end

        local dist = (curPos - origin).Magnitude
        local leadToUse = Config.leadMul
        if Config.adaptiveLead then
            if dist > 60 then leadToUse = leadToUse * 1.15
            elseif dist > 40 then leadToUse = leadToUse * 1.08
            elseif dist < 15 then leadToUse = leadToUse * 0.95 end
            if leadToUse > 1.8 then leadToUse = 1.8 end
        end

        if Config.dirChangeDetect then
            local dc = getDirectionChangeFactor()
            if dc > 0.3 then t = t * (1 - dc * 0.5) end
        end

        t = t * leadToUse
        if t > 3 then t = 3 end
        State.interceptTime = t

        local predicted = curPos + vel * t

        local state = getHumanoidState(targetPart.Parent)
        State.targetState = state
        if Config.airPredict and (state == "Jumping" or state == "Falling") then
            local vFull = targetPart.AssemblyLinearVelocity or Vector3.zero
            local yPred = curPos.Y + vFull.Y * t - 0.5 * 196.2 * t * t
            predicted = Vector3.new(predicted.X, yPred, predicted.Z)
        end

        local offset = predicted - curPos
        if offset.Magnitude > 150 then
            predicted = curPos + offset.Unit * 150
        end

        return predicted
    end

    local lastUpdate = 0

    local function update()
        local now = tick()
        if now - lastUpdate < 0.014 then return end
        lastUpdate = now

        if not Config.active then
            State.posRock = nil
            State.dirRock = nil
            State.name = nil
            State.amIChar = false
            State.targetPart = nil
            State.targetChar = nil
            velHistory = {}
            return
        end

        local myChar = player.Character
        if not myChar or not myChar.Parent then
            State.amIChar = false
            State.posRock = nil
            return
        end

        State.amIChar = true

        local myPart = myChar:FindFirstChild("HumanoidRootPart")
        if not myPart then
            State.posRock = nil
            return
        end

        local myPos = myPart.Position
        local origin = getOrigin(myChar)
        State.origin = origin

        local candidates = {}

        local pf = Workspace:FindFirstChild("Players")
        if pf then
            for _, m in ipairs(pf:GetChildren()) do
                if m:IsA("Model") and m ~= myChar and isKiller(m) and isAlive(m) then
                    local r = findPart(m)
                    if r then
                        local d = (r.Position - myPos).Magnitude
                        if d <= Config.maxDist and d >= Config.minDist then
                            table.insert(candidates, {part=r, model=m, name=m.Name, dist=d, key=m})
                        end
                    end
                end
            end
        end

        if #candidates == 0 then
            for _, m in ipairs(Workspace:GetChildren()) do
                if m:IsA("Model") and m ~= myChar and m.Name ~= "Players" and isKiller(m) and isAlive(m) then
                    local r = findPart(m)
                    if r then
                        local d = (r.Position - myPos).Magnitude
                        if d <= Config.maxDist and d >= Config.minDist then
                            table.insert(candidates, {part=r, model=m, name=m.Name, dist=d, key=m})
                        end
                    end
                end
            end
        end

        if Config.stickyEnabled and State.stickyLockKey then
            local found = false
            for _, c in ipairs(candidates) do
                if c.key == State.stickyLockKey then found = true; break end
            end
            if not found or (now - State.stickySince) > Config.stickyTime then
                State.stickyLockKey = nil
            end
        end

        local chosen = nil
        if Config.stickyEnabled and State.stickyLockKey then
            for _, c in ipairs(candidates) do
                if c.key == State.stickyLockKey then chosen = c; break end
            end
        end
        if not chosen and #candidates > 0 then
            table.sort(candidates, function(a, b)
                if Config.priority == "nearest" then return a.dist < b.dist end
                if Config.priority == "farthest" then return a.dist > b.dist end
                if Config.priority == "lowestHP" then return getHP(a.model) < getHP(b.model) end
                return a.dist < b.dist
            end)
            chosen = candidates[1]
            if Config.stickyEnabled then
                State.stickyLockKey = chosen.key
                State.stickySince = now
            end
        end

        if chosen and chosen.part then
            pushSample(chosen.part.Position, chosen.key)
            State.targetPart = chosen.part
            State.targetChar = chosen.model
            State.name = chosen.name

            State.posRock = computePos(chosen.part, origin, Config.projSpeed)

            if State.posRock then
                local d = State.posRock - origin
                State.dirRock = d.Magnitude > 0.01 and d.Unit or Vector3.new(0,0,-1)
            end
        else
            State.posRock = nil
            State.dirRock = nil
            State.name = nil
            State.targetPart = nil
            State.targetChar = nil
            velHistory = {}
        end
    end

    pcall(function() RunService.Heartbeat:Connect(update) end)
    pcall(function() RunService.RenderStepped:Connect(update) end)

    local hookedRemotes = {}

    local function tryHookMouse2()
        local char = player.Character
        if not char then return end
        local cam = char:FindFirstChild("cam")
        if not cam then return end
        local mouse2 = cam:FindFirstChild("Mouse2")
        if not mouse2 then return end
        if hookedRemotes[mouse2] then return end
        hookedRemotes[mouse2] = true

        pcall(function()
            mouse2.OnClientInvoke = function(param)
                if not Config.active then return nil end
                if not State.posRock or typeof(State.posRock) ~= "Vector3" then return nil end
                if Config.hitChance < 100 then
                    if math.random(1, 100) > Config.hitChance then return nil end
                end
                if param == "gethitpos" then return State.posRock end
                if typeof(param) == "string" then return State.posRock end
                if typeof(param) == "table" then
                    local dir = State.posRock - State.origin
                    if dir.Magnitude < 0.01 then dir = Vector3.new(0,0,-1) end
                    return { Origin = State.origin, Direction = dir.Unit, etc = State.posRock }
                end
                return State.posRock
            end
            State.hookMouse2 = true
        end)
    end

    task.spawn(function()
        while task.wait(0.3) do pcall(tryHookMouse2) end
    end)
    pcall(tryHookMouse2)

    player.CharacterAdded:Connect(function()
        task.wait(2)
        hookedRemotes = {}
        State.hookMouse2 = false
        pcall(tryHookMouse2)
    end)

    pcall(function()
        local mt = getrawmetatable(game)
        if not mt or not mt.__namecall then return end
        local oldNC = mt.__namecall
        setreadonly(mt, false)

        local GET_POS = {
            gethitpos=true, gethitposition=true, gettargetposition=true,
            getmousehit=true, gethitpoint=true, gettarget=true,
            gettargetpos=true, getaimpos=true,
        }
        local GET_DIR = {
            getaimdirection=true, getfiredirection=true, gettargetdirection=true,
            getshotdirection=true, getlaunchdirection=true,
        }
        local PREFIX = {"fire","shoot","attack","cast","launch","throw","swing"}

        mt.__namecall = newcclosure(function(self, ...)
            if not Config.active or not State.amIChar then return oldNC(self, ...) end
            local method = getnamecallmethod()
            if not method then return oldNC(self, ...) end
            local m = string.lower(method)
            local pos = State.posRock
            local dir = State.dirRock
            if not pos or typeof(pos) ~= "Vector3" then return oldNC(self, ...) end
            if GET_POS[m] then return pos end
            if GET_DIR[m] and dir then return dir end
            if method == "Raycast" and self == Workspace then
                local args = {...}
                if typeof(args[1]) == "Vector3" and typeof(args[2]) == "Vector3" then
                    if not Camera or (args[1] - Camera.CFrame.Position).Magnitude >= 1 then
                        local nd = pos - args[1]
                        if nd.Magnitude > 0.01 then
                            args[2] = nd.Unit * args[2].Magnitude
                            return oldNC(self, unpack(args))
                        end
                    end
                end
            end
            for _, prefix in ipairs(PREFIX) do
                if m:find(prefix, 1, true) then
                    local args = {...}
                    local replaced = false
                    for i, v in ipairs(args) do
                        if typeof(v) == "Vector3" then args[i] = pos; replaced = true end
                    end
                    if replaced then return oldNC(self, unpack(args)) end
                    break
                end
            end
            return oldNC(self, ...)
        end)
        setreadonly(mt, true)
        State.hookNC = true
    end)

    local gui = Instance.new("ScreenGui")
    gui.Name = "VxAimDot"
    gui.ResetOnSpawn = false
    gui.IgnoreGuiInset = true
    gui.DisplayOrder = 100
    gui.Parent = player:WaitForChild("PlayerGui")

    local dot = Instance.new("ImageLabel")
    dot.Size = UDim2.new(0, 30, 0, 30)
    dot.BackgroundTransparency = 1
    dot.Image = "rbxassetid://84459412139159"
    dot.ScaleType = Enum.ScaleType.Fit
    dot.Visible = false
    dot.ZIndex = 5
    dot.Parent = gui

    task.spawn(function()
        while task.wait(0.03) do
            pcall(function()
                if Config.active and State.posRock and Camera then
                    local sp, onScreen = Camera:WorldToViewportPoint(State.posRock)
                    if onScreen then
                        dot.Visible = true
                        dot.Position = UDim2.new(0, sp.X - 15, 0, sp.Y - 15)
                    else
                        dot.Visible = false
                    end
                else
                    dot.Visible = false
                end
            end)
        end
    end)
end, AbaChars)

-- ============================================
--  ABA ASSASSINO
-- ============================================

addBotao("Fleety Ova", Color3.fromRGB(230, 200, 40),
    "https://pastebin.com/raw/GxB9GET8", AbaAssassino)

addBotao("2011x pular no invisível", Color3.fromRGB(180, 40, 40),
    "https://raw.githubusercontent.com/nkojimioji-bit/scripts/main/2011x%20invis%20jump.lua", AbaAssassino)

addBotao("Kolossos cancelar o charge", Color3.fromRGB(120, 20, 20),
    "https://raw.githubusercontent.com/nkojimioji-bit/scripts/main/kolossos%20anti%20wall%20stop.lua", AbaAssassino)

addBotao("Fleety (Sukuna)", Color3.fromRGB(140, 0, 0),
    "https://rawscripts.net/raw/Outcome-Memories-v0.2-Sukuna-reskin-for-Fleetway-225231", AbaAssassino)

addBotao("2011x (Crimson X)", Color3.fromRGB(20, 30, 120),
    "https://rawscripts.net/raw/Universal-Script-(PC-ONLY-FOR-NOW)-MY5T-CRIMSON-X-MOVESET-FE-R15-226374", AbaAssassino)

-- ============================================
--  ABA CRIADOR
-- ============================================

novo("TextLabel", {
    Size = UDim2.new(1, -20, 0, 60),
    Position = UDim2.new(0, 10, 0, 20),
    BackgroundTransparency = 1,
    Text = "🎬 ZOEIRAKOF",
    TextColor3 = Color3.fromRGB(255, 40, 40),
    TextSize = 26,
    Font = Enum.Font.GothamBold,
    TextXAlignment = Enum.TextXAlignment.Center,
}, AbaCriador)

novo("TextLabel", {
    Size = UDim2.new(1, -20, 0, 30),
    Position = UDim2.new(0, 10, 0, 85),
    BackgroundTransparency = 1,
    Text = "Criador do VxGuilhermeOriginal",
    TextColor3 = Color3.fromRGB(220, 220, 220),
    TextSize = 14,
    Font = Enum.Font.Gotham,
    TextXAlignment = Enum.TextXAlignment.Center,
}, AbaCriador)

novo("TextLabel", {
    Size = UDim2.new(1, -20, 0, 30),
    Position = UDim2.new(0, 10, 0, 120),
    BackgroundTransparency = 1,
    Text = "youtube.com/@zoeirakof",
    TextColor3 = Color3.fromRGB(150, 150, 150),
    TextSize = 11,
    Font = Enum.Font.Gotham,
    TextXAlignment = Enum.TextXAlignment.Center,
}, AbaCriador)

local BtnYT = novo("TextButton", {
    Size = UDim2.new(1, -20, 0, 50),
    Position = UDim2.new(0, 10, 0, 170),
    BackgroundColor3 = Color3.fromRGB(200, 30, 30),
    Text = "📺 ABRIR YOUTUBE",
    TextColor3 = Color3.new(1, 1, 1),
    TextSize = 15,
    Font = Enum.Font.GothamBold,
    BorderSizePixel = 0,
    AutoButtonColor = false,
}, AbaCriador)
canto(BtnYT, 10)

novo("UIStroke", {
    Color = Color3.fromRGB(255, 80, 80),
    Thickness = 2,
}, BtnYT)

BtnYT.MouseEnter:Connect(function()
    BtnYT.BackgroundColor3 = Color3.fromRGB(230, 50, 50)
end)
BtnYT.MouseLeave:Connect(function()
    BtnYT.BackgroundColor3 = Color3.fromRGB(200, 30, 30)
end)

BtnYT.MouseButton1Click:Connect(function()
    local link = CFG.YT_Link

    pcall(function()
        if gui and gui.OpenWeb then
            gui:OpenWeb(link)
            return
        end
    end)

    pcall(function()
        if setclipboard then
            setclipboard(link)
        end
    end)

    pcall(function()
        game:GetService("GuiService"):OpenBrowserWindow(link)
    end)

    pcall(function()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "ZOEIRAKOF",
            Text = "Abrindo canal... se não abrir, link copiado!",
            Duration = 5
        })
    end)
end)

-- ============================================