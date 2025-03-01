local screenGui = game.Players.LocalPlayer:FindFirstChild("PlayerGui"):FindFirstChild("ScreenGui")
if screenGui then
	screenGui:Destroy()
end

screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 220, 0, 335)
frame.Position = UDim2.new(0.357, 0, 0.207, 0)
frame.BackgroundColor3 = Color3.new(0, 0, 0)
frame.Active = true
frame.Draggable = false -- Desactivamos la propiedad Draggable para manejarlo manualmente
frame.Parent = screenGui

local uiCorner = Instance.new("UICorner")
uiCorner.Parent = frame

local scrollingFrame = Instance.new("ScrollingFrame")
scrollingFrame.Size = UDim2.new(1, 0, 1, 0)
scrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 40 * 10)
scrollingFrame.ScrollBarThickness = 5
scrollingFrame.BackgroundTransparency = 1
scrollingFrame.ZIndex = 2
scrollingFrame.Parent = frame

local animations = {
	{"Combo 3", "109845134167647"},
	{"Jason Combo 3", "101736016625776"},
	{"Failed Machete Attack", "121086746534252"},
	{"Player Death Animation", "97176944963316"},
	{"Player Death V2", "71908227364423"},
	{"Round Start Jason", "73797519945529"},
	{"Fake Stun", "75595031025056"},
	{"R", "85591573377728"}
}

local activeTrack

for i, anim in ipairs(animations) do
	local textLabel = Instance.new("TextLabel")
	textLabel.Size = UDim2.new(0, 150, 0, 30)
	textLabel.Position = UDim2.new(0, 10, 0, (i - 1) * 40)
	textLabel.Text = anim[1]
	textLabel.TextColor3 = Color3.new(1, 1, 1)
	textLabel.BackgroundTransparency = 1
	textLabel.ZIndex = 3
	textLabel.Parent = scrollingFrame

	local playButton = Instance.new("TextButton")
	playButton.Size = UDim2.new(0, 50, 0, 30)
	playButton.Position = UDim2.new(0, 170, 0, (i - 1) * 40)
	playButton.Text = "Play"
	playButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
	playButton.TextColor3 = Color3.new(1, 1, 1)
	playButton.ZIndex = 3
	playButton.Parent = scrollingFrame

	playButton.MouseButton1Click:Connect(function()
		local character = game.Players.LocalPlayer.Character
		if character then
			local humanoid = character:FindFirstChildOfClass("Humanoid")
			if humanoid then
				local animator = humanoid:FindFirstChildOfClass("Animator")
				if not animator then
					animator = Instance.new("Animator")
					animator.Parent = humanoid
				end
				local animation = Instance.new("Animation")
				animation.AnimationId = "rbxassetid://" .. anim[2]
				local track = animator:LoadAnimation(animation)
				track:Play()
				activeTrack = track
			end
		end
	end)
end

local stopButton = Instance.new("TextButton")
stopButton.Size = UDim2.new(1, 0, 0, 40)
stopButton.Position = UDim2.new(0, 0, 0, #animations * 40)
stopButton.Text = "Stop Animation"
stopButton.BackgroundColor3 = Color3.new(1, 0, 0)
stopButton.TextColor3 = Color3.new(1, 1, 1)
stopButton.ZIndex = 3
stopButton.Parent = scrollingFrame

stopButton.MouseButton1Click:Connect(function()
	if activeTrack then
		activeTrack:Stop()
		activeTrack = nil
	end
end)

-- Hacer que el frame se pueda mover al arrastrarlo
local userInputService = game:GetService("UserInputService")
local dragging, dragInput, dragStart, startPos

local function update(input)
	local delta = input.Position - dragStart
	frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

frame.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = frame.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

frame.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		dragInput = input
	end
end)

userInputService.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		update(input)
	end
end)
