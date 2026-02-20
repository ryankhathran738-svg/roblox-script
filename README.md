local player = game.Players.LocalPlayer
local spawnCFrame = nil

-- إنشاء GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TeleportGui"
screenGui.ResetOnSpawn = false -- هذا أهم سطر عشان ما يختفي بعد الموت
screenGui.Parent = player:WaitForChild("PlayerGui")

local button = Instance.new("TextButton")
button.Parent = screenGui
button.Size = UDim2.new(0,150,0,50)
button.Position = UDim2.new(0.9, -160, 0.9, -60)
button.Text = "Go to Spawn"
button.BackgroundColor3 = Color3.fromRGB(0,170,255)
button.TextColor3 = Color3.fromRGB(255,255,255)
button.TextScaled = true

-- تسجيل مكان الرسباون الأول
local function onCharacterAdded(character)
	local hrp = character:WaitForChild("HumanoidRootPart")
	if not spawnCFrame then
		spawnCFrame = hrp.CFrame
	end
end

player.CharacterAdded:Connect(onCharacterAdded)

if player.Character then
	onCharacterAdded(player.Character)
end

-- وظيفة التليبورتيشن
button.MouseButton1Click:Connect(function()
	local character = player.Character
	if character and spawnCFrame then
		local hrp = character:FindFirstChild("HumanoidRootPart")
		if hrp then
			hrp.CFrame = spawnCFrame + Vector3.new(0,3,0)
		end
	end
end)
