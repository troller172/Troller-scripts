-- Serviços
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local plr = Players.LocalPlayer
local char = plr.Character or plr.CharacterAdded:Wait()
local hrp = char:WaitForChild("HumanoidRootPart")

-- Variáveis
local savedBasePosition = nil
local flying = false
local flyConnection = nil

local espEnabled = false
local espHighlights = {}

local antiAfkEnabled = false
local antiAfkConnection = nil
local angle = 0

-- GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "TrollerScripts"
ScreenGui.Parent = plr:WaitForChild("PlayerGui")
ScreenGui.ResetOnSpawn = false

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 330, 0, 260)
frame.Position = UDim2.new(0.05, 0, 0.1, 0)
frame.BackgroundColor3 = Color3.fromRGB(15, 15, 30)
frame.Active = true
frame.Draggable = true
frame.Parent = ScreenGui

local uicorner = Instance.new("UICorner", frame)
local uistroke = Instance.new("UIStroke", frame)
uistroke.Color = Color3.fromRGB(0, 120, 255)
uistroke.Thickness = 2

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.BackgroundTransparency = 1
title.Text = "💀 Troller Scripts"
title.Font = Enum.Font.GothamBlack
title.TextColor3 = Color3.fromRGB(0, 170, 255)
title.TextSize = 24
title.Parent = frame

-- Criar botão padrão
local function createCheckbox(text, yPos)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(0, 260, 0, 40)
	btn.Position = UDim2.new(0, 35, 0, yPos)
	btn.BackgroundColor3 = Color3.fromRGB(25, 25, 60)
	btn.Font = Enum.Font.Gotham
	btn.TextColor3 = Color3.new(1, 1, 1)
	btn.TextSize = 16
	btn.AutoButtonColor = false
	btn.Text = text .. " [OFF]"
	btn.Parent = frame
	return btn
end

-- Botões
local espBtn = createCheckbox("ESP", 60)
local saveBaseBtn = createCheckbox("Salvar Base", 120)
local afkBtn = createCheckbox("Anti-AFK", 180)

-- ESP com nome branco acima da cabeça e luz vermelha em volta do corpo
local function toggleESP(state)
	-- Remove ESP anterior
	for _, h in pairs(espHighlights) do
		h:Destroy()
	end
	espHighlights = {}
	
	if state then
		for _, p in pairs(Players:GetPlayers()) do
			if p ~= plr and p.Character and p.Character:FindFirstChild("Head") and p.Character:FindFirstChild("HumanoidRootPart") then
				-- Luz vermelha em volta do corpo usando Highlight
				local highlight = Instance.new("Highlight")
				highlight.FillColor = Color3.fromRGB(255, 0, 0) -- vermelho forte
				highlight.FillTransparency = 0.5
				highlight.OutlineColor = Color3.fromRGB(255, 0, 0)
				highlight.OutlineTransparency = 0
				highlight.Adornee = p.Character
				highlight.Parent = game.CoreGui
				
				-- Nome branco flutuando
				local billboard = Instance.new("BillboardGui")
				billboard.Name = "ESPTag"
				billboard.Adornee = p.Character.Head
				billboard.Size = UDim2.new(0, 80, 0, 20)
				billboard.StudsOffset = Vector3.new(0, 2, 0)
				billboard.AlwaysOnTop = true
				billboard.Parent = game.CoreGui

				local label = Instance.new("TextLabel")
				label.Size = UDim2.new(1, 0, 1, 0)
				label.BackgroundTransparency = 1
				label.Text = p.Name
				label.TextColor3 = Color3.new(1, 1, 1) -- branco
				label.TextStrokeTransparency = 0.75
				label.Font = Enum.Font.Gotham
				label.TextScaled = true
				label.Parent = billboard

				table.insert(espHighlights, highlight)
				table.insert(espHighlights, billboard)
			end
		end
	end
end

-- Steal (voo até base)
local function flyToBase()
	if not savedBasePosition then
		warn("Nenhuma base salva para voar!")
		return
	end
	
	if flying then return end
	
	flying = true
	
	flyConnection = RunService.Heartbeat:Connect(function(dt)
		if not flying then
			flyConnection:Disconnect()
			flyConnection = nil
			return
		end
		
		local pos = hrp.Position
		local direction = (savedBasePosition - pos)
		local dist = direction.Magnitude
		
		if dist < 3 then
			flying = false
			flyConnection:Disconnect()
			flyConnection = nil
			return
		end
		
		local step = direction.Unit * 50 * dt  -- velocidade ajustada para 50
		hrp.CFrame = CFrame.new(pos + step)
	end)
end

local function stopFly()
	flying = false
	if flyConnection then
		flyConnection:Disconnect()
		flyConnection = nil
	end
end

-- Anti-AFK com círculo maior (raio 9)
local function startAntiAFK()
	if antiAfkConnection then return end

	local radius = 9
	local angleStep = math.rad(15)
	local currentAngle = 0
	local jumpCooldown = 1.5
	local lastJump = 0

	local humanoid = char:FindFirstChildOfClass("Humanoid")
	if not humanoid then return end

	antiAfkConnection = RunService.Heartbeat:Connect(function()
		if not antiAfkEnabled or not plr.Character or humanoid.Health <= 0 then
			if antiAfkConnection then
				antiAfkConnection:Disconnect()
				antiAfkConnection = nil
			end
			return
		end

		currentAngle = currentAngle + angleStep
		if currentAngle > (2 * math.pi) then currentAngle = 0 end

		local basePos = hrp.Position
		local targetX = basePos.X + math.cos(currentAngle) * radius
		local targetZ = basePos.Z + math.sin(currentAngle) * radius
		local target = Vector3.new(targetX, basePos.Y, targetZ)

		humanoid:MoveTo(target)

		if tick() - lastJump > jumpCooldown then
			if humanoid:GetState() ~= Enum.HumanoidStateType.Jumping then
				humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
			end
			lastJump = tick()
		end
	end)
end

-- Botão ESP
espBtn.MouseButton1Click:Connect(function()
	espEnabled = not espEnabled
	espBtn.Text = "ESP [" .. (espEnabled and "ON" or "OFF") .. "]"
	toggleESP(espEnabled)
end)

-- Botão Salvar Base
saveBaseBtn.MouseButton1Click:Connect(function()
	if plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
		savedBasePosition = plr.Character.HumanoidRootPart.Position
		saveBaseBtn.Text = "Base salva!"
		wait(2)
		saveBaseBtn.Text = "Salvar Base [OFF]"
	else
		saveBaseBtn.Text = "Erro ao salvar!"
		wait(2)
		saveBaseBtn.Text = "Salvar Base [OFF]"
	end
end)

-- Botão Anti-AFK
afkBtn.MouseButton1Click:Connect(function()
	antiAfkEnabled = not antiAfkEnabled
	afkBtn.Text = "Anti-AFK [" .. (antiAfkEnabled and "ON" or "OFF") .. "]"
	if antiAfkEnabled then
		startAntiAFK()
	elseif antiAfkConnection then
		antiAfkConnection:Disconnect()
		antiAfkConnection = nil
	end
end)

-- Steal com tecla "L"
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	if input.UserInputType == Enum.UserInputType.Keyboard then
		if input.KeyCode == Enum.KeyCode.L then
			if flying then
				stopFly()
			else
				flyToBase()
			end
		elseif input.KeyCode == Enum.KeyCode.LeftControl then
			frame.Visible = not frame.Visible
		end
	end
end)

-- Atualizar referência ao HRP
plr.CharacterAdded:Connect(function(character)
	char = character
	hrp = char:WaitForChild("HumanoidRootPart")
end)
