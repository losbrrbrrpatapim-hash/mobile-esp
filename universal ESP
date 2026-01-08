-- SERVICES
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- SETTINGS
local ESP_ENABLED = true

-- APPLY ESP
local function applyESP(character)
	if character:FindFirstChild("RedBoxESP") then return end

	local root = character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local box = Instance.new("BoxHandleAdornment")
	box.Name = "RedBoxESP"
	box.Adornee = root
	box.Size = Vector3.new(4, 6, 2)
	box.Transparency = 0.8 -- very transparent
	box.Color3 = Color3.fromRGB(255, 0, 0)
	box.LineThickness = 0.05 -- thin
	box.AlwaysOnTop = true
	box.ZIndex = 10
	box.Enabled = ESP_ENABLED
	box.Parent = character
end

-- PLAYER SETUP
local function setupPlayer(player)
	if player == LocalPlayer then return end

	player.CharacterAdded:Connect(function(char)
		task.wait(1)
		applyESP(char)
	end)

	if player.Character then
		applyESP(player.Character)
	end
end

for _, p in ipairs(Players:GetPlayers()) do
	setupPlayer(p)
end
Players.PlayerAdded:Connect(setupPlayer)

-- GUI
local gui = Instance.new("ScreenGui")
gui.Name = "MobileESP"
gui.ResetOnSpawn = false
gui.Parent = PlayerGui

-- DRAGGABLE TOGGLE BUTTON
local toggle = Instance.new("TextButton")
toggle.Size = UDim2.new(0, 120, 0, 50)
toggle.Position = UDim2.new(0, 20, 0, 20)
toggle.Text = "ESP: ON"
toggle.TextScaled = true
toggle.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
toggle.Parent = gui
toggle.Active = true
toggle.Draggable = true

toggle.MouseButton1Click:Connect(function()
	ESP_ENABLED = not ESP_ENABLED
	toggle.Text = ESP_ENABLED and "ESP: ON" or "ESP: OFF"

	for _, obj in ipairs(workspace:GetDescendants()) do
		if obj:IsA("Model") and obj:FindFirstChild("RedBoxESP") then
			obj.RedBoxESP.Enabled = ESP_ENABLED
		end
	end
end)

-- CLOSE BUTTON
local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 120, 0, 40)
close.Position = UDim2.new(0, 20, 0, 80)
close.Text = "Close"
close.TextScaled = true
close.BackgroundColor3 = Color3.fromRGB(255, 80, 80)
close.Parent = gui

-- LOGO BUTTON
local logo = Instance.new("TextButton")
logo.Size = UDim2.new(0, 50, 0, 50)
logo.Position = UDim2.new(0, 20, 0, 20)
logo.Text = "ESP"
logo.TextScaled = true
logo.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
logo.Visible = false
logo.Parent = gui
logo.Active = true
logo.Draggable = true

close.MouseButton1Click:Connect(function()
	toggle.Visible = false
	close.Visible = false
	logo.Visible = true
end)

logo.MouseButton1Click:Connect(function()
	toggle.Visible = true
	close.Visible = true
	logo.Visible = false
end)
