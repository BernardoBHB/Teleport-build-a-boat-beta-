-- ==========================================
-- TELEPORT HUB (FORMATO CFRAME)
-- ==========================================

local player = game.Players.LocalPlayer

-- 1. Aqui você configura os nomes e cola o CFrame.new(...) exato de cada local
local locais = {
	Slot1 = {nome = "ultima area", coords = CFrame.new(-1.861766, 3295.577881, 2265.220459)},
	Slot2 = {nome = "area inicial", coords = CFrame.new(45.803066, 2.998025, 27.018297)},
	Slot3 = {nome = "Arena", coords = CFrame.new(150, 10, 150)},
	Slot4 = {nome = "Loja", coords = CFrame.new(-100, 10, 50)},
	Slot5 = {nome = "Boss", coords = CFrame.new(300, 20, -200)}
}

-- ==========================================
-- CRIAÇÃO DA INTERFACE (GUI)
-- ==========================================
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TeleportHub"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 280)
frame.Position = UDim2.new(0.02, 0, 0.4, 0) 
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true 
frame.Parent = screenGui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 8)
uiCorner.Parent = frame

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextScaled = true
title.Font = Enum.Font.GothamBold
title.Text = "Teleportes"
title.Parent = frame

-- ==========================================
-- LÓGICA DOS BOTÕES
-- ==========================================
local function criarBotao(index, info)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(0.8, 0, 0, 35)
	btn.Position = UDim2.new(0.1, 0, 0, 10 + (index * 42)) 
	btn.BackgroundColor3 = Color3.fromRGB(0, 120, 200)
	btn.TextColor3 = Color3.fromRGB(255, 255, 255)
	btn.Font = Enum.Font.GothamBold
	btn.TextScaled = true
	btn.Text = info.nome
	btn.Parent = frame

	local btnCorner = Instance.new("UICorner")
	btnCorner.CornerRadius = UDim.new(0, 6)
	btnCorner.Parent = btn

	btn.MouseButton1Click:Connect(function()
		local character = player.Character or player.CharacterAdded:Wait()
		local rootPart = character:FindFirstChild("HumanoidRootPart")
		
		if rootPart then
			-- Como você já usou CFrame.new() lá em cima, aqui aplicamos direto
			rootPart.CFrame = info.coords
		end
	end)
end

criarBotao(1, locais.Slot1)
criarBotao(2, locais.Slot2)
criarBotao(3, locais.Slot3)
criarBotao(4, locais.Slot4)
criarBotao(5, locais.Slot5)
