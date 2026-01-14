--========================================
-- hog blue | PAINEL CLIENT (JOGO PRÓPRIO)
--========================================

-- SERVIÇOS
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- CONFIG
local SPEED_MULT = 10
local FLY_FORCE = 60

-- CORES
local YELLOW = Color3.fromRGB(255,215,0)
local BLACK  = Color3.fromRGB(10,10,10)
local GRAY   = Color3.fromRGB(40,40,40)
local RED    = Color3.fromRGB(255,60,60)

-- FUNÇÕES BÁSICAS
local function getChar()
	return player.Character or player.CharacterAdded:Wait()
end

local function getHumanoid()
	return getChar():WaitForChild("Humanoid")
end

--========================================
-- GUI
--========================================
local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.Name = "hog_blue_gui"
gui.ResetOnSpawn = false

-- BOTÃO ABRIR
local openBtn = Instance.new("TextButton", gui)
openBtn.Size = UDim2.fromScale(0.15,0.07)
openBtn.Position = UDim2.fromScale(0.05,0.5)
openBtn.Text = "☰ hog blue"
openBtn.BackgroundColor3 = BLACK
openBtn.TextColor3 = YELLOW
openBtn.TextScaled = true
openBtn.BorderSizePixel = 0
openBtn.Active = true
openBtn.Draggable = true

-- PAINEL
local panel = Instance.new("Frame", gui)
panel.Size = UDim2.fromScale(0.6,0.6)
panel.Position = UDim2.fromScale(0.2,0.2)
panel.BackgroundColor3 = BLACK
panel.Visible = false
panel.BorderSizePixel = 0

-- TÍTULO
local title = Instance.new("TextLabel", panel)
title.Size = UDim2.fromScale(1,0.15)
title.Text = "hog blue"
title.TextScaled = true
title.BackgroundColor3 = YELLOW
title.TextColor3 = BLACK
title.BorderSizePixel = 0

-- FECHAR
local closeBtn = Instance.new("TextButton", panel)
closeBtn.Size = UDim2.fromScale(0.12,0.1)
closeBtn.Position = UDim2.fromScale(0.86,0.02)
closeBtn.Text = "X"
closeBtn.TextScaled = true
closeBtn.BackgroundColor3 = RED
closeBtn.TextColor3 = Color3.new(1,1,1)
closeBtn.BorderSizePixel = 0

-- CONTAINER
local container = Instance.new("Frame", panel)
container.Position = UDim2.fromScale(0,0.15)
container.Size = UDim2.fromScale(1,0.85)
container.BackgroundTransparency = 1

local layout = Instance.new("UIListLayout", container)
layout.Padding = UDim.new(0,8)
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center

--========================================
-- BOTÃO PADRÃO
--========================================
local function createButton(text, callback)
	local btn = Instance.new("TextButton", container)
	btn.Size = UDim2.fromScale(0.9,0.1)
	btn.Text = text
	btn.TextScaled = true
	btn.BackgroundColor3 = GRAY
	btn.TextColor3 = YELLOW
	btn.BorderSizePixel = 0
	btn.MouseButton1Click:Connect(callback)
end

--========================================
-- FUNÇÕES
--========================================
createButton("⚡ Speed 10x", function()
	getHumanoid().WalkSpeed = 16 * SPEED_MULT
end)

createButton("🕊️ Voar (clique sobe)", function()
	local hrp = getChar():WaitForChild("HumanoidRootPart")
	local bv = Instance.new("BodyVelocity")
	bv.Velocity = Vector3.new(0, FLY_FORCE, 0)
	bv.MaxForce = Vector3.new(0, math.huge, 0)
	bv.Parent = hrp
	game.Debris:AddItem(bv, 0.25)
end)

createButton("👁️ Ver nomes", function()
	print("ver nomes ativado")
end)

createButton("🧠 Ver Brainrots", function()
	print("ver brainrots ativado")
end)

createButton("🔴 Ver nomes dos Brainrots", function()
	print("nomes dos brainrots (VERMELHO)")
end)

createButton("⏱️ Ver minutos do laser", function()
	print("tempo do laser")
end)

createButton("🧬 Brainrot Secreto", function()
	print("linha secreta ativada")
end)

--========================================
-- CONTROLES
--========================================
openBtn.MouseButton1Click:Connect(function()
	panel.Visible = true
	openBtn.Visible = false
end)

closeBtn.MouseButton1Click:Connect(function()
	panel.Visible = false
	openBtn.Visible = true
end)
