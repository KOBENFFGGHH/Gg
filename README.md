-- [Date] --
Date = os.date("%A".." ".."%B".." ".."%d".." ".."%Y")

-- [GGE Z] --

local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local tween = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local LocalPlayer = game:GetService("Players").LocalPlayer
local Mouse = LocalPlayer:GetMouse()

-- [Animation Text] --

local function AnimateText(Text)
	for i = 1, #Text, 1 do
		game:GetService("Players").LocalPlayer.PlayerGui.Main.Version.Text = string.sub(Text, 1, i)
		wait(0.01)
	end
    task.spawn(function()
        while task.wait() do
            local t = 5; 
            local hue = tick() % t / t
            local color = Color3.fromHSV(hue, 1, 1)
            game:GetService("Players").LocalPlayer.PlayerGui.Main.Version.TextColor3 = color
        end
    end)
end

-- [Create Variables UI] --
do  local ui =  game:GetService("CoreGui").RobloxGui.Modules.Profile.Utils:FindFirstChild("UILibrary")  if ui then ui:Destroy() end end
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local LocalPlayer = game:GetService("Players").LocalPlayer
local Mouse = LocalPlayer:GetMouse()
getgenv().Settings = {
	Key = Enum.KeyCode.Delete
}
local function MakeDraggable(topbarobject, object)
	local Dragging = nil
	local DragInput = nil	
	local DragStart = nil
	local StartPosition = nil

	local function Update(input)
		local Delta = input.Position - DragStart
		local pos =
			UDim2.new(
				StartPosition.X.Scale,
				StartPosition.X.Offset + Delta.X,
				StartPosition.Y.Scale,
				StartPosition.Y.Offset + Delta.Y
			)
		local Tween = TweenService:Create(object, TweenInfo.new(0.2), {Position = pos})
		Tween:Play()
	end

	topbarobject.InputBegan:Connect(
		function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				Dragging = true
				DragStart = input.Position
				StartPosition = object.Position

				input.Changed:Connect(
					function()
						if input.UserInputState == Enum.UserInputState.End then
							Dragging = false
						end
					end
				)
			end
		end
	)

	topbarobject.InputChanged:Connect(
		function(input)
			if
				input.UserInputType == Enum.UserInputType.MouseMovement or
				input.UserInputType == Enum.UserInputType.Touch
			then
				DragInput = input
			end
		end
	)

	UserInputService.InputChanged:Connect(
		function(input)
			if input == DragInput and Dragging then
				Update(input)
			end
		end
	)
end
local function tablefound(ta, object)
	for i,v in pairs(ta) do
		if v == object then
			return true
		end
	end
	return false
end
local ActualTypes = {
	RoundFrame = "ImageLabel",
	Shadow = "ImageLabel",
	Circle = "ImageLabel",
	CircleButton = "ImageButton",
	Frame = "Frame",
	Label = "TextLabel",
	Button = "TextButton",
	SmoothButton = "ImageButton",
	Box = "TextBox",
	ScrollingFrame = "ScrollingFrame",
	Menu = "ImageButton",
	NavBar = "ImageButton"
}
local Properties = {
	RoundFrame = {
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=16663324629",
		ScaleType = Enum.ScaleType.Slice,
		SliceCenter = Rect.new(3,3,297,297)
	},
	SmoothButton = {
		AutoButtonColor = false,
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5554237731",
		ScaleType = Enum.ScaleType.Slice,
		SliceCenter = Rect.new(3,3,297,297)
	},
	Shadow = {
		Name = "Shadow",
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5554236805",
		ScaleType = Enum.ScaleType.Slice,
		SliceCenter = Rect.new(23,23,277,277),
		Size = UDim2.fromScale(1,1) + UDim2.fromOffset(30,30),
		Position = UDim2.fromOffset(-15,-15)
	},
	Circle = {
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5554831670"
	},
	CircleButton = {
		BackgroundTransparency = 1,
		AutoButtonColor = false,
		Image = "http://www.roblox.com/asset/?id=5554831670"
	},
	Frame = {
		BackgroundTransparency = 1,
		BorderSizePixel = 0,
		Size = UDim2.fromScale(1,1)
	},
	Label = {
		BackgroundTransparency = 1,
		Position = UDim2.fromOffset(5,0),
		Size = UDim2.fromScale(1,1) - UDim2.fromOffset(5,0),
		TextSize = 14,
		TextXAlignment = Enum.TextXAlignment.Left
	},
	Button = {
		BackgroundTransparency = 1,
		Position = UDim2.fromOffset(5,0),
		Size = UDim2.fromScale(1,1) - UDim2.fromOffset(5,0),
		TextSize = 14,
		TextXAlignment = Enum.TextXAlignment.Left
	},
	Box = {
		BackgroundTransparency = 1,
		Position = UDim2.fromOffset(5,0),
		Size = UDim2.fromScale(1,1) - UDim2.fromOffset(5,0),
		TextSize = 14,
		TextXAlignment = Enum.TextXAlignment.Left
	},
	ScrollingFrame = {
		BackgroundTransparency = 1,
		ScrollBarThickness = 0,
		CanvasSize = UDim2.fromScale(0,0),
		Size = UDim2.fromScale(1,1)
	},
	Menu = {
		Name = "More",
		AutoButtonColor = false,
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5555108481",
		Size = UDim2.fromOffset(20,20),
		Position = UDim2.fromScale(1,0.5) - UDim2.fromOffset(25,10)
	},
	NavBar = {
		Name = "SheetToggle",
		Image = "http://www.roblox.com/asset/?id=5576439039",
		BackgroundTransparency = 1,
		Size = UDim2.fromOffset(20,20),
		Position = UDim2.fromOffset(5,5),
		AutoButtonColor = false
	}
}
local Types = {
	"RoundFrame",
	"Shadow",
	"Circle",
	"CircleButton",
	"Frame",
	"Label",
	"Button",
	"SmoothButton",
	"Box",
	"ScrollingFrame",
	"Menu",
	"NavBar"
}
function FindType(String)
	for _, Type in next, Types do
		if Type:sub(1, #String):lower() == String:lower() then
			return Type
		end
	end
	return false
end
local Objects = {}
function Objects.new(Type)
	local TargetType = FindType(Type)
	if TargetType then
		local NewImage = Instance.new(ActualTypes[TargetType])
		if Properties[TargetType] then
			for Property, Value in next, Properties[TargetType] do
				NewImage[Property] = Value
			end
		end
		return NewImage
	else
		return Instance.new(Type)
	end
end
local function GetXY(GuiObject)
	local Max, May = GuiObject.AbsoluteSize.X, GuiObject.AbsoluteSize.Y
	local Px, Py = math.clamp(Mouse.X - GuiObject.AbsolutePosition.X, 0, Max), math.clamp(Mouse.Y - GuiObject.AbsolutePosition.Y, 0, May)
	return Px/Max, Py/May
end
local function CircleAnim(GuiObject, EndColour, StartColour)
	local PX, PY = GetXY(GuiObject)
	local Circle = Objects.new("Shadow")
	Circle.Size = UDim2.fromScale(0,0)
	Circle.Position = UDim2.fromScale(PX,PY)
	Circle.ImageColor3 = StartColour or GuiObject.ImageColor3
	Circle.ZIndex = 200
	Circle.Parent = GuiObject
	local Size = GuiObject.AbsoluteSize.X
	TweenService:Create(Circle, TweenInfo.new(0.5), {Position = UDim2.fromScale(PX,PY) - UDim2.fromOffset(Size/2,Size/2), ImageTransparency = 1, ImageColor3 = EndColour, Size = UDim2.fromOffset(Size,Size)}):Play()
	spawn(function()
		wait(0.5)
		Circle:Destroy()
	end)
end
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local LocalPlayer = game:GetService("Players").LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local UILibrary = Instance.new("ScreenGui")
UILibrary.Name = "UILibrary"
UILibrary.Parent = game:GetService("CoreGui").RobloxGui.Modules.Profile.Utils
UILibrary.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
local Library = {}
local function tablefound(ta, object)
	for i,v in pairs(ta) do
		if v == object then
			return true
		end
	end
	return false
end
function Library.xova()

	local FocusUI = false

	local PageOrders = -1

	local Main = Instance.new("Frame")
	local MainUICorner = Instance.new("UICorner")
	local Topbar = Instance.new("Frame")
	local Logo = Instance.new("ImageButton")
	local Title = Instance.new("TextLabel")
	local Description = Instance.new("TextLabel")
	local Scrollbar = Instance.new("Frame")
	local ScrollbarUICorner = Instance.new("UICorner")
	local Main2 = Instance.new("Frame")
	local Main2UICorner = Instance.new("UICorner")
	local ContainerPage = Instance.new("Frame")
	local FolderPage = Instance.new("Folder")
	local FolderUIPageLayout = Instance.new("UIPageLayout")

	local KeyButton = Instance.new("TextButton")

	KeyButton.Name = "KeyButton"
	KeyButton.Parent = Main
	KeyButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	KeyButton.BackgroundTransparency = 1.000
	KeyButton.Position = UDim2.new(0.816176474, 0, 0.0122137405, 0)
	KeyButton.Size = UDim2.new(0, 94, 0, 23)
	KeyButton.Font = Enum.Font.GothamMedium
	KeyButton.Text = "[L]"
	KeyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
	KeyButton.TextSize = 12.000
	KeyButton.TextTransparency = 0.500
	KeyButton.TextXAlignment = Enum.TextXAlignment.Right
	KeyButton.TextWrapped = true

	local LeftScrollbar = Instance.new("ImageButton")
	local RightScrollbar = Instance.new("ImageButton")

	LeftScrollbar.Name = "LeftScrollbar"
	LeftScrollbar.Parent = Scrollbar
	LeftScrollbar.AnchorPoint = Vector2.new(0.5, 0.5)
	LeftScrollbar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	LeftScrollbar.BackgroundTransparency = 1.000
	LeftScrollbar.Position = UDim2.new(-0.0381203443, 0, 0.5, 0)
	LeftScrollbar.Rotation = 180.000
	LeftScrollbar.Size = UDim2.new(0, 40, 0, 40)
	LeftScrollbar.Image = "http://www.roblox.com/asset/?id=6026663699"
	LeftScrollbar.ImageTransparency = 0.500

	RightScrollbar.Name = "RightScrollbar"
	RightScrollbar.Parent = Scrollbar
	RightScrollbar.AnchorPoint = Vector2.new(0.5, 0.5)
	RightScrollbar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	RightScrollbar.BackgroundTransparency = 1.000
	RightScrollbar.Position = UDim2.new(1.03579271, 0, 0.5, 0)
	RightScrollbar.Size = UDim2.new(0, 40, 0, 40)
	RightScrollbar.Image = "http://www.roblox.com/asset/?id=6026663699"
	RightScrollbar.ImageTransparency = 0.500

	Main.Name = "Main"
	Main.Parent = UILibrary
	Main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
	Main.BorderSizePixel = 0
	Main.AnchorPoint = Vector2.new(0.5,0.5)
	Main.Position = UDim2.new(0.5, 0, 0.5, 0)
	Main.Size = UDim2.new(0, 0, 0, 0)
	Main.ClipsDescendants = true

	TweenService:Create(Main,TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),{Size = UDim2.new(0, 544, 0, 245)}):Play()

	MainUICorner.CornerRadius = UDim.new(0, 9)
	MainUICorner.Name = "MainUICorner"
	MainUICorner.Parent = Main

	KeyButton.MouseButton1Click:Connect(function()
		KeyButton.Text = "[ Select Key ]"
		local inputwait = UserInputService.InputBegan:wait()
		if inputwait.KeyCode.Name ~= "Unknown" then
			getgenv().Settings.Key = inputwait.KeyCode
			KeyButton.Text = "[ " .. getgenv().Settings.Key.Name .." ] "

			Key = inputwait.KeyCode.Name
		end
	end)
	local uitoggled = false
	UserInputService.InputBegan:Connect(function(io, p)
		if io.KeyCode == getgenv().Settings.Key then
			if uitoggled == false then
				uitoggled = true
				TweenService:Create(
					Main,
					TweenInfo.new(.5, Enum.EasingStyle.Quart, Enum.EasingDirection.In),
					{Size = UDim2.new(0, 0, 0, 0)}
				):Play()
			else
				TweenService:Create(
					Main,
					TweenInfo.new(.5, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),
					{Size = UDim2.new(0, 544, 0, 655)}
				):Play()
				repeat wait() until Main.Size == UDim2.new(0, 544, 0, 655)
				uitoggled = false
			end
		end
	end)

	Topbar.Name = "Topbar"
	Topbar.Parent = Main
	Topbar.Active = true
	Topbar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Topbar.BackgroundTransparency = 1.000
	Topbar.Size = UDim2.new(0, 544, 0, 48)

	Logo.Name = "Logo"
	Logo.Parent = Topbar
	Logo.Active = true
	Logo.AnchorPoint = Vector2.new(0.5, 0.5)
	Logo.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Logo.BackgroundTransparency = 1.000
	Logo.Position = UDim2.new(0.0439999998, 0, 0.5, 0)
	Logo.Size = UDim2.new(0, 35, 0, 35)
	Logo.Image = "rbxassetid://16663324629"

	Title.Name = "Title"
	Title.Parent = Topbar
	Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Title.BackgroundTransparency = 1.000
	Title.Position = UDim2.new(0.0882352963, 0, 0, 0)
	Title.Size = UDim2.new(0, 483, 0, 31)
	Title.Font = Enum.Font.GothamMedium
	Title.Text = "Attack Hub"
	Title.TextColor3 = Color3.fromRGB(255, 255, 255)
	Title.TextSize = 14.000
	Title.TextWrapped = true
	Title.TextXAlignment = Enum.TextXAlignment.Left

	Description.Name = "Description"
	Description.Parent = Topbar
	Description.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Description.BackgroundTransparency = 1.000
	Description.Position = UDim2.new(0.0882352963, 0, 0, 0)
	Description.Size = UDim2.new(0, 483, 0, 67)
	Description.Font = Enum.Font.GothamMedium
	Description.Text = ""..Date
	Description.TextColor3 = Color3.fromRGB(255, 255, 255)
	Description.TextSize = 12.000
	Description.TextTransparency = 0.500
	Description.TextWrapped = true
	Description.TextXAlignment = Enum.TextXAlignment.Left

	function Library.Notifcation(options)

		local visualTitle = options.Title or "Notifcation"
		local visualDesc = options.Desc or "scription"
		local visualDelays = options.Delays or 10

		local Notification = Instance.new("Frame")
		local NotificationUIGradient = Instance.new("UIGradient")
		local NotificationUICorner = Instance.new("UICorner")
		local NotifcationMain = Instance.new("Frame")
		local NotifcationMainUICorner = Instance.new("UICorner")
		local Glow = Instance.new("ImageLabel")
		local Title = Instance.new("TextLabel")
		local Desc = Instance.new("TextLabel")
		local ButtonBar = Instance.new("TextButton")
		local ButtonBarUICorner = Instance.new("UICorner")
		local Line = Instance.new("Frame")
		local LineMain = Instance.new("Frame")

		Notification.Name = "Notification"
		Notification.Parent = Main
		Notification.Active = false
		Notification.AnchorPoint = Vector2.new(0.5,0.5)
		Notification.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Notification.BackgroundTransparency = 0.020
		Notification.ClipsDescendants = true
		Notification.Position = UDim2.new(0.5,0,0.5,0)
		Notification.Size = UDim2.new(0, 0, 0, 0)

		Notification:TweenSizeAndPosition(UDim2.new(0, 544, 0, 655),  UDim2.new(0.5, 0, 0.5,0), "Out", "Quart", 0.2, true)

		NotificationUIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(0, 0, 0)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(15, 15, 15))}
		NotificationUIGradient.Rotation = 90
		NotificationUIGradient.Name = "NotificationUIGradient"
		NotificationUIGradient.Parent = Notification

		NotificationUICorner.Name = "NotificationUICorner"
		NotificationUICorner.Parent = Notification

		NotifcationMain.Name = "NotifcationMain"
		NotifcationMain.Parent = Notification
		NotifcationMain.AnchorPoint = Vector2.new(0.5, 0.5)
		NotifcationMain.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
		NotifcationMain.Position = UDim2.new(0.5, 0, 0.5, 0)
		NotifcationMain.Size = UDim2.new(0, 377, 0, 294)

		NotifcationMainUICorner.Name = "NotifcationMainUICorner"
		NotifcationMainUICorner.Parent = NotifcationMain

		Glow.Name = "Glow"
		Glow.Parent = NotifcationMain
		Glow.AnchorPoint = Vector2.new(0.5, 0.5)
		Glow.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
		Glow.BackgroundTransparency = 1.000
		Glow.Position = UDim2.new(0.5, 0, 0.506802738, 0)
		Glow.Size = UDim2.new(0, 417, 0, 325)
		Glow.Image = "rbxassetid://5028857084"
		Glow.ImageColor3 = Color3.fromRGB(0, 0, 0)

		Title.Name = "Title"
		Title.Parent = NotifcationMain
		Title.Active = true
		Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Title.BackgroundTransparency = 1.000
		Title.Position = UDim2.new(0.0212201588, 0, 0.0289115645, 0)
		Title.Size = UDim2.new(0, 362, 0, 26)
		Title.Font = Enum.Font.GothamMedium
		Title.TextColor3 = Color3.fromRGB(255, 255, 255)
		Title.TextSize = 14.000
		Title.Text = visualTitle
		Title.TextWrapped = true

		Desc.Name = "Desc"
		Desc.Parent = NotifcationMain
		Desc.Active = true
		Desc.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Desc.BackgroundTransparency = 1.000
		Desc.Position = UDim2.new(0.0212201588, 0, 0.127551019, 0)
		Desc.Size = UDim2.new(0, 362, 0, 40)
		Desc.Font = Enum.Font.GothamMedium
		Desc.TextColor3 = Color3.fromRGB(255, 255, 255)
		Desc.TextSize = 12.000
		Desc.TextTransparency = 0.500
		Desc.TextWrapped = true
		Desc.Text = visualDesc
		Desc.TextYAlignment = Enum.TextYAlignment.Top

		ButtonBar.Name = "ButtonBar"
		ButtonBar.Parent = Desc
		ButtonBar.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
		ButtonBar.BackgroundTransparency = 0.500
		ButtonBar.BorderSizePixel = 0
		ButtonBar.Position = UDim2.new(0, 0, 5.39750051, 0)
		ButtonBar.Size = UDim2.new(0, 362, 0, 26)
		ButtonBar.Font = Enum.Font.GothamMedium
		ButtonBar.TextColor3 = Color3.fromRGB(255, 255, 255)
		ButtonBar.TextSize = 12.000
		ButtonBar.TextTransparency = 0.500
		ButtonBar.ClipsDescendants = true
		ButtonBar.AutoButtonColor = false

		ButtonBarUICorner.CornerRadius = UDim.new(0, 4)
		ButtonBarUICorner.Name = "ButtonBarUICorner"
		ButtonBarUICorner.Parent = ButtonBar

		Line.Name = "Line"
		Line.Parent = Desc
		Line.Active = true
		Line.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
		Line.BorderSizePixel = 0
		Line.Position = UDim2.new(0.00552486209, 0, 5.1500001, 0)
		Line.Size = UDim2.new(0, 360, 0, 5)

		LineMain.Name = "LineMain"
		LineMain.Parent = Line
		LineMain.Active = true
		LineMain.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
		LineMain.BorderSizePixel = 0
		LineMain.Size = UDim2.new(0, 360, 0, 5)

		ButtonBar.MouseEnter:Connect(function()
			TweenService:Create(
				ButtonBar,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{TextTransparency = 0}
			):Play()
			TweenService:Create(
				ButtonBar,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{BackgroundTransparency = 0}
			):Play()
		end)

		ButtonBar.MouseLeave:Connect(function()
			TweenService:Create(
				ButtonBar,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{TextTransparency = 0.5}
			):Play()
			TweenService:Create(
				ButtonBar,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{BackgroundTransparency = 0.5}
			):Play()
		end)

		ButtonBar.MouseButton1Click:Connect(function()
			CircleAnim(ButtonBar,Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,255))
			TweenService:Create(
				Notification,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{BackgroundTransparency = 1}
			):Play()
			Notification:TweenSize(UDim2.new(0, 0, 0, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, .2, true)
			TweenService:Create(
				Notification,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{BackgroundTransparency = 1}
			):Play()
			wait(.2)
			Notification:Destroy()
		end)

		TweenService:Create(
			LineMain,
			TweenInfo.new(tonumber(visualDelays), Enum.EasingStyle.Sine, Enum.EasingDirection.Out),
			{Size = UDim2.new(0, 0, 0, 5)} -- UDim2.new(0, 128, 0, 25)
		):Play()
		delay(tonumber(visualDelays),function()
			TweenService:Create(
				Notification,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{BackgroundTransparency = 1}
			):Play()
			Notification:TweenSize(UDim2.new(0, 0, 0, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, .2, true)
			TweenService:Create(
				Notification,
				TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{BackgroundTransparency = 1}
			):Play()
			wait(.2)
			Notification:Destroy()
		end)
	end

	---

	Scrollbar.Name = "Scrollbar"
	Scrollbar.Parent = Main
	Scrollbar.Active = true
	Scrollbar.AnchorPoint = Vector2.new(0.5, 0.5)
	Scrollbar.BackgroundColor3 = Color3.fromRGB(23, 23, 23)
	Scrollbar.BorderColor3 = Color3.fromRGB(27, 42, 53)
	Scrollbar.BorderSizePixel = 0
	Scrollbar.Position = UDim2.new(0.5, 0, 0.110076346, 0)
	Scrollbar.Size = UDim2.new(0, 460, 0, 35)

	ScrollbarUICorner.CornerRadius = UDim.new(0, 4)
	ScrollbarUICorner.Name = "ScrollbarUICorner"
	ScrollbarUICorner.Parent = Scrollbar

	Main2.Name = "Main2"
	Main2.Parent = Main
	Main2.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	Main2.BorderSizePixel = 0
	Main2.Position = UDim2.new(0.0202205889, 0, 0.151145041, 0)
	Main2.Size = UDim2.new(0, 520, 0, 545)

	local Main2UICorner = Instance.new("UICorner")

	Main2UICorner.CornerRadius = UDim.new(0, 4)
	Main2UICorner.Parent = Main2

	ContainerPage.Name = "ContainerPage"
	ContainerPage.Parent = Main2
	ContainerPage.Active = true
	ContainerPage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ContainerPage.BackgroundTransparency = 1.000
	ContainerPage.ClipsDescendants = true
	ContainerPage.Size = UDim2.new(0, 520, 0, 545)

	FolderPage.Name = "FolderPage"
	FolderPage.Parent = ContainerPage

	FolderUIPageLayout.Name = "FolderUIPageLayout"
	FolderUIPageLayout.Parent = FolderPage
	FolderUIPageLayout.SortOrder = Enum.SortOrder.LayoutOrder
	FolderUIPageLayout.EasingDirection = Enum.EasingDirection.InOut
	FolderUIPageLayout.EasingStyle = Enum.EasingStyle.Quad
	FolderUIPageLayout.Padding = UDim.new(0, 10)
	FolderUIPageLayout.TweenTime = 0.300

	MakeDraggable(Topbar,Main)

	local Scrollingbar = Instance.new("ScrollingFrame")
	local ScrollingbarUIListLayout = Instance.new("UIListLayout")
	local ScrollingbarUIPadding = Instance.new("UIPadding")

	Scrollingbar.Name = "Scrollingbar"
	Scrollingbar.Parent = Scrollbar
	Scrollingbar.Active = true
	Scrollingbar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Scrollingbar.BackgroundTransparency = 1.000
	Scrollingbar.BorderSizePixel = 0
	Scrollingbar.Size = UDim2.new(0, 460, 0, 37)
	Scrollingbar.BottomImage = ""
	Scrollingbar.ScrollBarThickness = 0
	Scrollingbar.TopImage = ""

	ScrollingbarUIListLayout.Name = "ScrollingbarUIListLayout"
	ScrollingbarUIListLayout.Parent = Scrollingbar
	ScrollingbarUIListLayout.FillDirection = Enum.FillDirection.Horizontal
	ScrollingbarUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	ScrollingbarUIListLayout.Padding = UDim.new(0, 5)

	ScrollingbarUIPadding.Name = "ScrollingbarUIPadding"
	ScrollingbarUIPadding.Parent = Scrollingbar
	ScrollingbarUIPadding.PaddingLeft = UDim.new(0, 5)
	ScrollingbarUIPadding.PaddingTop = UDim.new(0, 5)

	local LibraryTab = {}

	function LibraryTab.create(Title)
		PageOrders = PageOrders + 1

		local name = tostring(Title) or tostring(math.random(500,100000))

		local ButtonBar = Instance.new("TextButton")
		local ButtonBarUICorner = Instance.new("UICorner")

		ButtonBar.Name = name.."_ButtonBar"
		ButtonBar.Parent = Scrollingbar
		ButtonBar.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
		ButtonBar.BorderSizePixel = 0
		ButtonBar.BackgroundTransparency = 0.65
		ButtonBar.Font = Enum.Font.GothamMedium
		ButtonBar.TextColor3 = Color3.fromRGB(255, 255, 255)
		ButtonBar.TextSize = 12.000
		ButtonBar.Text = tostring(Title)
		ButtonBar.TextTransparency = 0.500
		ButtonBar.AutoButtonColor = false

		if ButtonBar.Name == name.."_ButtonBar" then
			ButtonBar.Size = UDim2.new(0, 70 + ButtonBar.TextBounds.X, 0, 25)
		end

		ButtonBarUICorner.CornerRadius = UDim.new(0, 4)
		ButtonBarUICorner.Name = "ButtonBarUICorner"
		ButtonBarUICorner.Parent = ButtonBar


		local MainPage = Instance.new("Frame")
		MainPage.Name = name.."_MainPage"
		MainPage.Parent = FolderPage
		MainPage.Active = true
		MainPage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		MainPage.BackgroundTransparency = 1.000
		MainPage.Size = UDim2.new(0, 520, 0, 545)

		MainPage.LayoutOrder = PageOrders

		local ScrollingMainPage = Instance.new("ScrollingFrame")
		local ScrollingMainPageUIListLayout = Instance.new("UIListLayout")
		local ScrollingMainPageUIPadding = Instance.new("UIPadding")

		ScrollingMainPage.Name = "ScrollingMainPage"
		ScrollingMainPage.Parent = MainPage
		ScrollingMainPage.Active = true
		ScrollingMainPage.AnchorPoint = Vector2.new(0.5, 0.5)
		ScrollingMainPage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		ScrollingMainPage.BackgroundTransparency = 1.000
		ScrollingMainPage.BorderSizePixel = 0
		ScrollingMainPage.Position = UDim2.new(0.5, 0, 0.5, 0)
		ScrollingMainPage.Size = UDim2.new(0, 510, 0, 535)
		ScrollingMainPage.BottomImage = ""
		ScrollingMainPage.ScrollBarThickness = 3
		ScrollingMainPage.TopImage = ""

		ScrollingMainPageUIListLayout.Name = "ScrollingMainPageUIListLayout"
		ScrollingMainPageUIListLayout.Parent = ScrollingMainPage
		ScrollingMainPageUIListLayout.FillDirection = Enum.FillDirection.Horizontal
		ScrollingMainPageUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		ScrollingMainPageUIListLayout.Padding = UDim.new(0, 5)

		ScrollingMainPageUIPadding.Name = "ScrollingMainPageUIPadding"
		ScrollingMainPageUIPadding.Parent = ScrollingMainPage
		ScrollingMainPageUIPadding.PaddingLeft = UDim.new(0, 5)
		ScrollingMainPageUIPadding.PaddingTop = UDim.new(0, 5)

		local LeftFrame = Instance.new("Frame")
		local LeftFrameUIPadding = Instance.new("UIPadding")
		local LeftFrameUIListLayout = Instance.new("UIListLayout")

		local RightFrame = Instance.new("Frame")
		local RightFrameUIPadding = Instance.new("UIPadding")
		local RightFrameUIListLayout = Instance.new("UIListLayout")

		LeftFrame.Name = "LeftFrame"
		LeftFrame.Parent = ScrollingMainPage
		LeftFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		LeftFrame.BackgroundTransparency = 1.000
		LeftFrame.Size = UDim2.new(0, 245, 0, 524)

		LeftFrameUIPadding.Name = "LeftFrameUIPadding"
		LeftFrameUIPadding.Parent = LeftFrame
		LeftFrameUIPadding.PaddingLeft = UDim.new(0, 5)
		LeftFrameUIPadding.PaddingTop = UDim.new(0, 5)

		LeftFrameUIListLayout.Name = "LeftFrameUIListLayout"
		LeftFrameUIListLayout.Parent = LeftFrame
		LeftFrameUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		LeftFrameUIListLayout.Padding = UDim.new(0, 15)

		RightFrame.Name = "RightFrame"
		RightFrame.Parent = ScrollingMainPage
		RightFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		RightFrame.BackgroundTransparency = 1.000
		RightFrame.Size = UDim2.new(0, 245, 0, 524)

		RightFrameUIPadding.Name = "RightFrameUIPadding"
		RightFrameUIPadding.Parent = RightFrame
		RightFrameUIPadding.PaddingLeft = UDim.new(0, 5)
		RightFrameUIPadding.PaddingTop = UDim.new(0, 5)

		RightFrameUIListLayout.Name = "RightFrameUIListLayout"
		RightFrameUIListLayout.Parent = RightFrame
		RightFrameUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		RightFrameUIListLayout.Padding = UDim.new(0, 15)

		LeftFrameUIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			LeftFrame.Size = UDim2.new(0, 245, 0, LeftFrameUIListLayout.AbsoluteContentSize.Y + 35)
		end)

		RightFrameUIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			RightFrame.Size = UDim2.new(0, 245, 0, RightFrameUIListLayout.AbsoluteContentSize.Y + 35)
		end)

		local function GetType(value)
			if value == 1 then
				return LeftFrame
			elseif value == 2 then
				return RightFrame
			else
				return LeftFrame
			end
		end

		LeftFrameUIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			if LeftFrameUIListLayout.AbsoluteContentSize.Y > RightFrameUIListLayout.AbsoluteContentSize.Y then
				ScrollingMainPage.CanvasSize = UDim2.new(0, 0, 0, LeftFrameUIListLayout.AbsoluteContentSize.Y +35)
			end
		end)
		RightFrameUIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			if RightFrameUIListLayout.AbsoluteContentSize.Y > LeftFrameUIListLayout.AbsoluteContentSize.Y then
				ScrollingMainPage.CanvasSize = UDim2.new(0, 0, 0, RightFrameUIListLayout.AbsoluteContentSize.Y +35)
			end
		end)

		ButtonBar.MouseButton1Click:connect(function()
			if MainPage.Name == name.."_MainPage" then
				FolderUIPageLayout:JumpToIndex(MainPage.LayoutOrder)
				for i ,v in next , Scrollingbar:GetChildren() do
					if v:IsA("TextButton") then
						TweenService:Create(
							v,
							TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
							{TextTransparency = 0.5}
						):Play()
						TweenService:Create(
							v,
							TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
							{BackgroundTransparency = 0.65}
						):Play()
					end
				end
				TweenService:Create(
					ButtonBar,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{TextTransparency = 0}
				):Play()
				TweenService:Create(
					ButtonBar,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundTransparency = 0}
				):Play()
			end
		end)

		if FocusUI == false then
			TweenService:Create(
				ButtonBar,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{TextTransparency = 0}
			):Play()
			TweenService:Create(
				ButtonBar,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{BackgroundTransparency = 0}
			):Play()
			MainPage.Visible = true
			MainPage.Name  = name.."_MainPage"
			FocusUI  = true
		end

		local LibraryPage = {}

		function LibraryPage.xovapage(Type)
			local PageFrame = Instance.new("Frame")
			local PageFrameUICorner = Instance.new("UICorner")
			local Line = Instance.new("Frame")
			local PageFrameMain = Instance.new("Frame")
			local PageFrameMainUICorner = Instance.new("UICorner")
			local PageFrameMainUIListLayout = Instance.new("UIListLayout")
			local PageFrameMainUIPadding = Instance.new("UIPadding")

			PageFrame.Name = "PageFrame"
			PageFrame.Parent = GetType(Type)
			PageFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
			PageFrame.BorderSizePixel = 0
			PageFrame.Size = UDim2.new(0, 235, 0, 100)

			PageFrameUICorner.CornerRadius = UDim.new(0, 4)
			PageFrameUICorner.Name = "PageFrameUICorner"
			PageFrameUICorner.Parent = PageFrame

			Line.Name = "Line"
			Line.Parent = PageFrame
			Line.Active = true
			Line.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
			Line.BorderSizePixel = 0
			Line.Size = UDim2.new(0, 235, 0, 2)
			Line.ZIndex = 2

			PageFrameMain.Name = "PageFrameMain"
			PageFrameMain.Parent = PageFrame
			PageFrameMain.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
			PageFrameMain.BorderSizePixel = 0
			PageFrameMain.Position = UDim2.new(0, 0, 0.02, 0)
			PageFrameMain.Size = UDim2.new(0, 235, 0, 98)

			PageFrameMainUICorner.CornerRadius = UDim.new(0, 4)
			PageFrameMainUICorner.Name = "PageFrameMainUICorner"
			PageFrameMainUICorner.Parent = PageFrameMain

			PageFrameMainUIListLayout.Name = "PageFrameMainUIListLayout"
			PageFrameMainUIListLayout.Parent = PageFrameMain
			PageFrameMainUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
			PageFrameMainUIListLayout.Padding = UDim.new(0, 5)

			PageFrameMainUIPadding.Name = "PageFrameMainUIPadding"
			PageFrameMainUIPadding.Parent = PageFrameMain
			PageFrameMainUIPadding.PaddingLeft = UDim.new(0, 5)
			PageFrameMainUIPadding.PaddingTop = UDim.new(0, 5)

			game:GetService("RunService").Stepped:Connect(function ()
				pcall(function ()
					Scrollingbar.CanvasSize = UDim2.new(0,ScrollingbarUIListLayout.AbsoluteContentSize.X + 10,0,0)
					PageFrameMain.Size =  UDim2.new(0, 235, 0,PageFrameMainUIListLayout.AbsoluteContentSize.Y + 15)
					PageFrame.Size =  UDim2.new(0, 235, 0,PageFrameMainUIListLayout.AbsoluteContentSize.Y + 15)
				end)
			end)

			LeftScrollbar.MouseEnter:Connect(function()
				TweenService:Create(
					LeftScrollbar,
					TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{ImageTransparency = 0}
				):Play()
			end)

			LeftScrollbar.MouseLeave:Connect(function()
				TweenService:Create(
					LeftScrollbar,
					TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{ImageTransparency = 0.5}
				):Play()
			end)

			RightScrollbar.MouseEnter:Connect(function()
				TweenService:Create(
					RightScrollbar,
					TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{ImageTransparency = 0}
				):Play()
			end)

			RightScrollbar.MouseLeave:Connect(function()
				TweenService:Create(
					RightScrollbar,
					TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{ImageTransparency = 0.5}
				):Play()
			end)

			local LibraryFunction = {}

			function LibraryFunction.Label(options)

				local visual = options.Title

				local LabelFrame = Instance.new("Frame")
				local Label = Instance.new("TextLabel")

				LabelFrame.Name = "LabelFrame"
				LabelFrame.Parent = PageFrameMain
				LabelFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				LabelFrame.BackgroundTransparency = 1.000
				LabelFrame.Size = UDim2.new(0, 225, 0, 25)

				Label.Name = "Label"
				Label.Parent = LabelFrame
				Label.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Label.BackgroundTransparency = 1.000
				Label.Size = UDim2.new(0, 225, 0, 25)
				Label.Font = Enum.Font.Gotham
				Label.TextColor3 = Color3.fromRGB(255, 255, 255)
				Label.TextSize = 12.000
				Label.TextWrapped = true
				Label.TextTransparency = 0.500
				Label.Text = visual or ""

				local LabelFunction = {}

				function LabelFunction.UpdateColor(value)
					TweenService:Create(
						Label,
						TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
						{TextColor3 = value}
					):Play()
				end

				function LabelFunction.Update(value)
					Label.Text = tostring(value)
				end
				return LabelFunction
			end

			function LibraryFunction.Toggle(options)

				local visualTitle = options.Title or "Toggle"
				local visualDesc = options.Desc or "Description"
				local visualMode = options.Mode or 1
				local visualdefault = options.Default or false
				local visualcallback = options.callback or function() end

				if visualMode == 1 then

					local ToggleFrame = Instance.new("Frame")
					local ToggleFrameUICorner = Instance.new("UICorner")
					local ToggleTitle = Instance.new("TextLabel")
					local Toggle = Instance.new("ImageButton")
					local ToggleUICorner = Instance.new("UICorner")
					local ToggleInner = Instance.new("ImageButton")
					local ToggleInnerUICorner = Instance.new("UICorner")
					local ToggleButton = Instance.new("TextButton")

					ToggleFrame.Name = "ToggleFrame"
					ToggleFrame.Parent = PageFrameMain
					ToggleFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
					ToggleFrame.BorderColor3 = Color3.fromRGB(27, 42, 53)
					ToggleFrame.BorderSizePixel = 0
					ToggleFrame.Size = UDim2.new(0, 225, 0, 29)

					ToggleFrameUICorner.CornerRadius = UDim.new(0, 4)
					ToggleFrameUICorner.Name = "ToggleFrameUICorner"
					ToggleFrameUICorner.Parent = ToggleFrame

					ToggleTitle.Name = "ToggleTitle"
					ToggleTitle.Parent = ToggleFrame
					ToggleTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ToggleTitle.BackgroundTransparency = 1.000
					ToggleTitle.Position = UDim2.new(0.0488888882, 0, 0, 0)
					ToggleTitle.Size = UDim2.new(0, 170, 0, 29)
					ToggleTitle.Font = Enum.Font.GothamMedium
					ToggleTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
					ToggleTitle.TextSize = 12.000
					ToggleTitle.Text = visualTitle
					ToggleTitle.TextTransparency = 0.500
					ToggleTitle.TextWrapped = true
					ToggleTitle.TextXAlignment = Enum.TextXAlignment.Left

					Toggle.Name = "Toggle"
					Toggle.Parent = ToggleTitle
					Toggle.AnchorPoint = Vector2.new(0.5, 0.5)
					Toggle.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
					Toggle.BackgroundTransparency = 1.000
					Toggle.Position = UDim2.new(1.14999998, 0, 0.5, 0)
					Toggle.Size = UDim2.new(0, 19, 0, 19)
					Toggle.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
					Toggle.ImageColor3 = Color3.fromRGB(30, 30, 30)

					ToggleUICorner.CornerRadius = UDim.new(0, 30)
					ToggleUICorner.Name = "ToggleUICorner"
					ToggleUICorner.Parent = Toggle

					ToggleInner.Name = "ToggleInner"
					ToggleInner.Parent = Toggle
					ToggleInner.AnchorPoint = Vector2.new(0.5, 0.5)
					ToggleInner.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
					ToggleInner.BackgroundTransparency = 1.000
					ToggleInner.Position = UDim2.new(0.5, 0, 0.5, 0)
					ToggleInner.Size = UDim2.new(0, 0, 0, 0)
					ToggleInner.Image = "http://www.roblox.com/asset/?id=6031625146"
					ToggleInner.ImageColor3 = Color3.fromRGB(0, 255, 255)

					ToggleInnerUICorner.CornerRadius = UDim.new(0, 30)
					ToggleInnerUICorner.Name = "ToggleInnerUICorner"
					ToggleInnerUICorner.Parent = ToggleInner

					ToggleButton.Name = "ToggleButton"
					ToggleButton.Parent = ToggleFrame
					ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ToggleButton.BackgroundTransparency = 1.000
					ToggleButton.Size = UDim2.new(0, 225, 0, 29)
					ToggleButton.AutoButtonColor = false
					ToggleButton.Font = Enum.Font.SourceSans
					ToggleButton.Text = ""
					ToggleButton.TextColor3 = Color3.fromRGB(0, 0, 0)
					ToggleButton.TextSize = 14.000
					ToggleButton.ClipsDescendants = true

					local visual = {toggle = false , lock = true , togglefunction ={

					},}

					ToggleButton.MouseEnter:Connect(function()
						if visual.toggle == false and visual.lock == true then
							TweenService:Create(
								ToggleTitle,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{TextTransparency = 0}
							):Play()
						end
					end)

					ToggleButton.MouseLeave:Connect(function()
						if visual.toggle == false and visual.lock == true then
							TweenService:Create(
								ToggleTitle,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{TextTransparency = 0.5}
							):Play()
						end
					end)

					ToggleButton.MouseButton1Down:Connect(function()
						CircleAnim(ToggleButton,Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,255))
						if visual.toggle == false and visual.lock == true then
							TweenService:Create(
								ToggleInner,
								TweenInfo.new(0.2, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
								{Size = UDim2.new(0, 15, 0, 15)}
							):Play()
						elseif visual.lock == true then
							TweenService:Create(
								ToggleInner,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{Size = UDim2.new(0, 0, 0, 0)}
							):Play()
						end
						if  visual.lock == true  then
							visual.toggle = not visual.toggle
							options.callback(visual.toggle)
						end
					end)

					if visualdefault == true then
						CircleAnim(ToggleButton,Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,255))
						TweenService:Create(
							ToggleInner,
							TweenInfo.new(0.2, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
							{Size = UDim2.new(0, 15, 0, 15)}
						):Play()
						if  visual.lock == true  then
							visual.toggle = not visual.toggle
							options.callback(visual.toggle)
						end
					end

					local LockerFrame = Instance.new("Frame")
					local LockIcon = Instance.new("ImageLabel")

					LockerFrame.Name = "LockerFrame"
					LockerFrame.Parent = ToggleFrame
					LockerFrame.Active = true
					LockerFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
					LockerFrame.BackgroundTransparency = 0.200
					LockerFrame.BorderSizePixel = 0
					LockerFrame.ClipsDescendants = true
					LockerFrame.Position = UDim2.new(-0.0222222228, 0, 0, 0)
					LockerFrame.Size = UDim2.new(0, 235, 0, 29)
					LockerFrame.BackgroundTransparency = 1

					LockIcon.Name = "LockIcon"
					LockIcon.Parent = LockerFrame
					LockIcon.AnchorPoint = Vector2.new(0.5, 0.5)
					LockIcon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					LockIcon.BackgroundTransparency = 1.000
					LockIcon.Position = UDim2.new(0.5, 0, 0.5, 0)
					LockIcon.Size = UDim2.new(0, 0, 0, 0)
					LockIcon.Image = "http://www.roblox.com/asset/?id=14742039447"

					function visual.togglefunction.lock()
						visual.lock = false
						TweenService:Create(
							LockerFrame,
							TweenInfo.new(.4, Enum.EasingStyle.Sine, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0.1}
						):Play()
						wait(0.5)
						TweenService:Create(
							LockIcon,
							TweenInfo.new(.2, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 20, 0, 20)}
						):Play()
					end
					function visual.togglefunction.unlock()
						visual.lock = true
						TweenService:Create(
							LockerFrame,
							TweenInfo.new(.4, Enum.EasingStyle.Sine, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 1}
						):Play()
						wait(0.5)
						TweenService:Create(
							LockIcon,
							TweenInfo.new(.2, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 0, 0, 0)}
						):Play()
					end

					LockerFrame.MouseEnter:Connect(function()
						for i = 1,3 do
							TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = 10}):Play()
							wait(.1)
							TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = -10}):Play()
							wait(.1)
						end
						TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = 0}):Play()
					end)
					LockerFrame.MouseLeave:Connect(function()
						TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = 0}):Play()
					end)
					return visual.togglefunction
				elseif visualMode == 2 then

					local ToggleFrame = Instance.new("Frame")
					local ToggleFrameUICorner = Instance.new("UICorner")
					local ToggleTitle = Instance.new("TextLabel")
					local Toggle = Instance.new("ImageButton")
					local ToggleUICorner = Instance.new("UICorner")
					local ToggleInner = Instance.new("ImageButton")
					local ToggleInnerUICorner = Instance.new("UICorner")
					local ToggleButton = Instance.new("TextButton")

					ToggleFrame.Name = "ToggleFrame"
					ToggleFrame.Parent = PageFrameMain
					ToggleFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
					ToggleFrame.BorderColor3 = Color3.fromRGB(27, 42, 53)
					ToggleFrame.BorderSizePixel = 0
					ToggleFrame.Size = UDim2.new(0, 225, 0, 57)

					ToggleFrameUICorner.CornerRadius = UDim.new(0, 4)
					ToggleFrameUICorner.Name = "ToggleFrameUICorner"
					ToggleFrameUICorner.Parent = ToggleFrame

					ToggleTitle.Name = "ToggleTitle"
					ToggleTitle.Parent = ToggleFrame
					ToggleTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ToggleTitle.BackgroundTransparency = 1.000
					ToggleTitle.Position = UDim2.new(0.0488888882, 0, 0, 0)
					ToggleTitle.Size = UDim2.new(0, 170, 0, 29)
					ToggleTitle.Font = Enum.Font.GothamMedium
					ToggleTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
					ToggleTitle.TextSize = 12.000
					ToggleTitle.Text = visualTitle
					ToggleTitle.TextTransparency = 0.500
					ToggleTitle.TextWrapped = true
					ToggleTitle.TextXAlignment = Enum.TextXAlignment.Left

					local ToggleDesc = Instance.new("TextLabel")

					ToggleDesc.Name = "ToggleDesc"
					ToggleDesc.Parent = ToggleFrame
					ToggleDesc.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ToggleDesc.BackgroundTransparency = 1.000
					ToggleDesc.Position = UDim2.new(0.0488888882, 0, 0.508771956, 0)
					ToggleDesc.Size = UDim2.new(0, 170, 0, 22)
					ToggleDesc.Font = Enum.Font.GothamMedium
					ToggleDesc.TextColor3 = Color3.fromRGB(255, 255, 255)
					ToggleDesc.TextSize = 12.000
					ToggleDesc.Text = visualDesc
					ToggleDesc.TextTransparency = 0.700
					ToggleDesc.TextWrapped = true
					ToggleDesc.TextXAlignment = Enum.TextXAlignment.Left

					Toggle.Name = "Toggle"
					Toggle.Parent = ToggleTitle
					Toggle.AnchorPoint = Vector2.new(0.5, 0.5)
					Toggle.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
					Toggle.BackgroundTransparency = 1.000
					Toggle.Position = UDim2.new(1.14999998, 0, 0.5, 0)
					Toggle.Size = UDim2.new(0, 19, 0, 19)
					Toggle.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
					Toggle.ImageColor3 = Color3.fromRGB(30, 30, 30)

					ToggleUICorner.CornerRadius = UDim.new(0, 30)
					ToggleUICorner.Name = "ToggleUICorner"
					ToggleUICorner.Parent = Toggle

					ToggleInner.Name = "ToggleInner"
					ToggleInner.Parent = Toggle
					ToggleInner.AnchorPoint = Vector2.new(0.5, 0.5)
					ToggleInner.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
					ToggleInner.BackgroundTransparency = 1.000
					ToggleInner.Position = UDim2.new(0.5, 0, 0.5, 0)
					ToggleInner.Size = UDim2.new(0, 0, 0, 0)
					ToggleInner.Image = "http://www.roblox.com/asset/?id=6031625146"
					ToggleInner.ImageColor3 = Color3.fromRGB(0, 255, 255)

					ToggleInnerUICorner.CornerRadius = UDim.new(0, 30)
					ToggleInnerUICorner.Name = "ToggleInnerUICorner"
					ToggleInnerUICorner.Parent = ToggleInner

					ToggleButton.Name = "ToggleButton"
					ToggleButton.Parent = ToggleFrame
					ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ToggleButton.BackgroundTransparency = 1.000
					ToggleButton.Size = UDim2.new(0, 225, 0, 57)
					ToggleButton.AutoButtonColor = false
					ToggleButton.Font = Enum.Font.SourceSans
					ToggleButton.Text = ""
					ToggleButton.TextColor3 = Color3.fromRGB(0, 0, 0)
					ToggleButton.TextSize = 14.000
					ToggleButton.ClipsDescendants = true

					local visual = {toggle = false , lock = true , togglefunction ={

					},}

					ToggleButton.MouseEnter:Connect(function()
						if visual.toggle == false and visual.lock == true then
							TweenService:Create(
								ToggleTitle,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{TextTransparency = 0}
							):Play()
						end
					end)

					ToggleButton.MouseLeave:Connect(function()
						if visual.toggle == false and visual.lock == true then
							TweenService:Create(
								ToggleTitle,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{TextTransparency = 0.5}
							):Play()
						end
					end)

					ToggleButton.MouseButton1Down:Connect(function()
						CircleAnim(ToggleButton,Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,255))
						if visual.toggle == false and visual.lock == true then
							TweenService:Create(
								ToggleInner,
								TweenInfo.new(0.2, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
								{Size = UDim2.new(0, 15, 0, 15)}
							):Play()
						elseif visual.lock == true then
							TweenService:Create(
								ToggleInner,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{Size = UDim2.new(0, 0, 0, 0)}
							):Play()
						end
						if  visual.lock == true  then
							visual.toggle = not visual.toggle
							options.callback(visual.toggle)
						end
					end)

					if visualdefault == true then
						CircleAnim(ToggleButton,Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,255))
						TweenService:Create(
							ToggleInner,
							TweenInfo.new(0.2, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
							{Size = UDim2.new(0, 15, 0, 15)}
						):Play()
						if  visual.lock == true  then
							visual.toggle = not visual.toggle
							options.callback(visual.toggle)
						end
					end

					local LockerFrame = Instance.new("Frame")
					local LockIcon = Instance.new("ImageLabel")

					LockerFrame.Name = "LockerFrame"
					LockerFrame.Parent = ToggleFrame
					LockerFrame.Active = true
					LockerFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
					LockerFrame.BackgroundTransparency = 0.200
					LockerFrame.BorderSizePixel = 0
					LockerFrame.ClipsDescendants = true
					LockerFrame.Position = UDim2.new(-0.0222222228, 0, 0, 0)
					LockerFrame.Size = UDim2.new(0, 235, 0, 57)
					LockerFrame.BackgroundTransparency = 1

					LockIcon.Name = "LockIcon"
					LockIcon.Parent = LockerFrame
					LockIcon.AnchorPoint = Vector2.new(0.5, 0.5)
					LockIcon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					LockIcon.BackgroundTransparency = 1.000
					LockIcon.Position = UDim2.new(0.5, 0, 0.5, 0)
					LockIcon.Size = UDim2.new(0, 0, 0, 0)
					LockIcon.Image = "http://www.roblox.com/asset/?id=14742039447"

					function visual.togglefunction.ChangeDesc(value)
						ToggleDesc.Text = tostring(value)
					end

					function visual.togglefunction.lock()
						visual.lock = false
						TweenService:Create(
							LockerFrame,
							TweenInfo.new(.4, Enum.EasingStyle.Sine, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0.1}
						):Play()
						wait(0.5)
						TweenService:Create(
							LockIcon,
							TweenInfo.new(.2, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 20, 0, 20)}
						):Play()
					end
					function visual.togglefunction.unlock()
						visual.lock = true
						TweenService:Create(
							LockerFrame,
							TweenInfo.new(.4, Enum.EasingStyle.Sine, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 1}
						):Play()
						wait(0.5)
						TweenService:Create(
							LockIcon,
							TweenInfo.new(.2, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 0, 0, 0)}
						):Play()
					end

					LockerFrame.MouseEnter:Connect(function()
						for i = 1,3 do
							TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = 10}):Play()
							wait(.1)
							TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = -10}):Play()
							wait(.1)
						end
						TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = 0}):Play()
					end)
					LockerFrame.MouseLeave:Connect(function()
						TweenService:Create(LockIcon, TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {Rotation = 0}):Play()
					end)
					return visual.togglefunction
				end
			end

			function LibraryFunction.Button(options)

				local visualMode = options.Mode or false
				local visualTitle = options.Title or "Button"
				local visualcallback = options.callback or function() end
				local visualdefault = options.Default or false

				if options.Mode == true then

					local ButtonFocus = false

					local ButtonFrame = Instance.new("Frame")
					local Button = Instance.new("TextButton")
					local ButtonCorner = Instance.new("UICorner")

					ButtonFrame.Name = "ButtonFrame"
					ButtonFrame.Parent = PageFrameMain
					ButtonFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ButtonFrame.BackgroundTransparency = 1.000
					ButtonFrame.Size = UDim2.new(0, 225, 0, 25)

					Button.Name = "Button"
					Button.Parent = ButtonFrame
					Button.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
					Button.BackgroundTransparency = 0.500
					Button.Size = UDim2.new(0, 225, 0, 25)
					Button.Font = Enum.Font.GothamMedium
					Button.TextColor3 = Color3.fromRGB(255, 255, 255)
					Button.TextSize = 12.000
					Button.TextTransparency = 0.500
					Button.Text = visualTitle
					Button.TextWrapped = true
					Button.ClipsDescendants = true
					Button.AutoButtonColor = false

					ButtonCorner.CornerRadius = UDim.new(0, 4)
					ButtonCorner.Name = "ButtonCorner"
					ButtonCorner.Parent = Button

					Button.MouseEnter:Connect(function()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0}
						):Play()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0}
						):Play()
					end)

					Button.MouseLeave:Connect(function()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0.5}
						):Play()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0.5}
						):Play()
					end)

					Button.MouseButton1Down:Connect(function()
						if ButtonFocus == false then
							TweenService:Create(
								Button,
								TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
								{TextTransparency = 0}
							):Play()
							TweenService:Create(
								Button,
								TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
								{BackgroundTransparency = 0}
							):Play()
							TweenService:Create(
								Button,
								TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
								{BackgroundColor3 = Color3.fromRGB(85, 170, 127)}
							):Play()
						else
							TweenService:Create(
								Button,
								TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
								{TextTransparency = 0.5}
							):Play()
							TweenService:Create(
								Button,
								TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
								{BackgroundTransparency = 0.5}
							):Play()
							TweenService:Create(
								Button,
								TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
								{BackgroundColor3 = Color3.fromRGB(0, 255, 255)}
							):Play()
						end
						ButtonFocus = not ButtonFocus
						CircleAnim(Button,Color3.fromRGB(0, 0, 0),Color3.fromRGB(0, 0, 0))
						options.callback(ButtonFocus)
					end)

					if options.Default == true then
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0}
						):Play()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0}
						):Play()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundColor3 = Color3.fromRGB(85, 170, 127)}
						):Play()
						ButtonFocus = not ButtonFocus
						CircleAnim(Button,Color3.fromRGB(0, 0, 0),Color3.fromRGB(0, 0, 0))
						options.callback(ButtonFocus)
					end

				else

					local ButtonFrame = Instance.new("Frame")
					local Button = Instance.new("TextButton")
					local ButtonCorner = Instance.new("UICorner")

					ButtonFrame.Name = "ButtonFrame"
					ButtonFrame.Parent = PageFrameMain
					ButtonFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ButtonFrame.BackgroundTransparency = 1.000
					ButtonFrame.Size = UDim2.new(0, 225, 0, 25)

					Button.Name = "Button"
					Button.Parent = ButtonFrame
					Button.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
					Button.BackgroundTransparency = 0.500
					Button.Size = UDim2.new(0, 225, 0, 25)
					Button.Font = Enum.Font.GothamMedium
					Button.TextColor3 = Color3.fromRGB(255, 255, 255)
					Button.TextSize = 12.000
					Button.TextTransparency = 0.500
					Button.Text = visualTitle
					Button.TextWrapped = true
					Button.ClipsDescendants = true
					Button.AutoButtonColor = false

					ButtonCorner.CornerRadius = UDim.new(0, 4)
					ButtonCorner.Name = "ButtonCorner"
					ButtonCorner.Parent = Button

					Button.MouseEnter:Connect(function()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0}
						):Play()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0}
						):Play()
					end)

					Button.MouseLeave:Connect(function()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0.5}
						):Play()
						TweenService:Create(
							Button,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0.5}
						):Play()
					end)

					Button.MouseButton1Down:Connect(function()
						CircleAnim(Button,Color3.fromRGB(0, 0, 0),Color3.fromRGB(0, 0, 0))
						pcall(options.callback)
					end)

				end
			end

			function LibraryFunction.Line()
				local LineFrame = Instance.new("Frame")
				local Line = Instance.new("Frame")

				LineFrame.Name = "LineFrame"
				LineFrame.Parent = PageFrameMain
				LineFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				LineFrame.BackgroundTransparency = 1.000
				LineFrame.Size = UDim2.new(0, 225, 0, 5)

				Line.Name = "Line"
				Line.Parent = LineFrame
				Line.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Line.BackgroundTransparency = 0.750
				Line.BorderSizePixel = 0
				Line.Size = UDim2.new(0, 225, 0, 1)
			end

			function LibraryFunction.Dropdown(options)

				local DropdownFunctions = false
				local visualTitle = options.Title or "Dropdown : nil"
				local visualItem = options.Item or {}
				local visualcallback = options.callback or function(Item) return end 

				local DropdownFrame = Instance.new("Frame")
				local DropdownFrameUICorner = Instance.new("UICorner")
				local DropdownTitle = Instance.new("TextLabel")
				local Arrow = Instance.new("ImageLabel")
				local DropdownButton = Instance.new("TextButton")

				DropdownFrame.Name = "DropdownFrame"
				DropdownFrame.Parent = PageFrameMain
				DropdownFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
				DropdownFrame.BorderColor3 = Color3.fromRGB(27, 42, 53)
				DropdownFrame.BorderSizePixel = 0
				DropdownFrame.Position = UDim2.new(0, 0, 0.392857134, 0)
				DropdownFrame.Size = UDim2.new(0, 225, 0, 30)

				DropdownFrameUICorner.CornerRadius = UDim.new(0, 4)
				DropdownFrameUICorner.Name = "DropdownFrameUICorner"
				DropdownFrameUICorner.Parent = DropdownFrame

				DropdownTitle.Name = "DropdownTitle"
				DropdownTitle.Parent = DropdownFrame
				DropdownTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				DropdownTitle.BackgroundTransparency = 1.000
				DropdownTitle.Position = UDim2.new(0.0488888882, 0, 0, 0)
				DropdownTitle.Size = UDim2.new(0, 170, 0, 29)
				DropdownTitle.Font = Enum.Font.GothamMedium
				DropdownTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
				DropdownTitle.TextSize = 12.000
				DropdownTitle.Text = visualTitle.." : "
				DropdownTitle.TextTransparency = 0.500
				DropdownTitle.TextWrapped = true
				DropdownTitle.TextXAlignment = Enum.TextXAlignment.Left

				Arrow.Name = "Arrow"
				Arrow.Parent = DropdownTitle
				Arrow.AnchorPoint = Vector2.new(0.5, 0.5)
				Arrow.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Arrow.BackgroundTransparency = 1.000
				Arrow.Position = UDim2.new(1.14999998, 0, 0.5, 0)
				Arrow.Size = UDim2.new(0, 20, 0, 20)
				Arrow.Image = "http://www.roblox.com/asset/?id=6031094674"
				Arrow.ImageTransparency = 0.500

				DropdownButton.Name = "DropdownButton"
				DropdownButton.Parent = DropdownFrame
				DropdownButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				DropdownButton.BackgroundTransparency = 1.000
				DropdownButton.Size = UDim2.new(0, 225, 0, 29)
				DropdownButton.AutoButtonColor = false
				DropdownButton.Font = Enum.Font.SourceSans
				DropdownButton.Text = ""
				DropdownButton.TextColor3 = Color3.fromRGB(0, 0, 0)
				DropdownButton.TextSize = 14.000

				local SelectionFrame = Instance.new("Frame")
				local SelectionFrameUICorner = Instance.new("UICorner")
				local SearchFrame = Instance.new("Frame")
				local SearchFrameUICorner = Instance.new("UICorner")
				local SearchBar = Instance.new("TextBox")
				local SelectionScrolling = Instance.new("ScrollingFrame")
				local SelectionScrollingUIListLayout = Instance.new("UIListLayout")
				local SelectionScrollingUIPadding = Instance.new("UIPadding")

				SelectionFrame.Name = "SelectionFrame"
				SelectionFrame.Parent = PageFrameMain
				SelectionFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
				SelectionFrame.BorderColor3 = Color3.fromRGB(27, 42, 53)
				SelectionFrame.BorderSizePixel = 0
				SelectionFrame.Position = UDim2.new(0, 0, 0.497023821, 0)
				SelectionFrame.Size = UDim2.new(0, 225, 0, 0)
				SelectionFrame.ClipsDescendants = true

				SelectionFrameUICorner.CornerRadius = UDim.new(0, 4)
				SelectionFrameUICorner.Name = "SelectionFrameUICorner"
				SelectionFrameUICorner.Parent = SelectionFrame

				SearchFrame.Name = "SearchFrame"
				SearchFrame.Parent = SelectionFrame
				SearchFrame.Active = true
				SearchFrame.AnchorPoint = Vector2.new(0.5, 0.5)
				SearchFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
				SearchFrame.BorderSizePixel = 0
				SearchFrame.Position = UDim2.new(0.5, 0, 0.150000006, 0)
				SearchFrame.Size = UDim2.new(0, 215, 0, 25)

				SearchFrameUICorner.CornerRadius = UDim.new(0, 4)
				SearchFrameUICorner.Name = "SearchFrameUICorner"
				SearchFrameUICorner.Parent = SearchFrame

				SearchBar.Name = "SearchBar"
				SearchBar.Parent = SearchFrame
				SearchBar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				SearchBar.BackgroundTransparency = 1.000
				SearchBar.BorderColor3 = Color3.fromRGB(27, 42, 53)
				SearchBar.Position = UDim2.new(0.0279069766, 0, 0, 0)
				SearchBar.Size = UDim2.new(0, 205, 0, 25)
				SearchBar.Font = Enum.Font.GothamMedium
				SearchBar.PlaceholderText = "Search . . ."
				SearchBar.Text = ""
				SearchBar.TextColor3 = Color3.fromRGB(255, 255, 255)
				SearchBar.TextSize = 12.000
				SearchBar.TextTransparency = 0.500
				SearchBar.TextWrapped = true
				SearchBar.TextXAlignment = Enum.TextXAlignment.Left

				SelectionScrolling.Name = "SelectionScrolling"
				SelectionScrolling.Parent = SelectionFrame
				SelectionScrolling.Active = true
				SelectionScrolling.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				SelectionScrolling.BackgroundTransparency = 1.000
				SelectionScrolling.BorderSizePixel = 0
				SelectionScrolling.Position = UDim2.new(0.0219999999, 0, 0.289999992, 0)
				SelectionScrolling.Size = UDim2.new(0, 215, 0, 75)
				SelectionScrolling.BottomImage = ""
				SelectionScrolling.ScrollBarThickness = 2
				SelectionScrolling.TopImage = ""

				SelectionScrollingUIListLayout.Name = "SelectionScrollingUIListLayout"
				SelectionScrollingUIListLayout.Parent = SelectionScrolling
				SelectionScrollingUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
				SelectionScrollingUIListLayout.Padding = UDim.new(0, 5)

				SelectionScrollingUIPadding.Name = "SelectionScrollingUIPadding"
				SelectionScrollingUIPadding.Parent = SelectionScrolling
				SelectionScrollingUIPadding.PaddingLeft = UDim.new(0, 5)
				SelectionScrollingUIPadding.PaddingTop = UDim.new(0, 5)

				for i,v in pairs(visualItem) do

					local ButtonBar = Instance.new("TextButton")
					local ButtonBarUIGradient = Instance.new("UIGradient")
					local ButtonBarUICorner = Instance.new("UICorner")

					ButtonBar.Name = "ButtonBar"
					ButtonBar.Parent = SelectionScrolling
					ButtonBar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
					ButtonBar.BorderSizePixel = 0
					ButtonBar.Size = UDim2.new(0, 204, 0, 18)
					ButtonBar.Font = Enum.Font.Gotham
					ButtonBar.TextColor3 = Color3.fromRGB(255, 255, 255)
					ButtonBar.TextSize = 12.000
					ButtonBar.Text = tostring(v)
					ButtonBar.TextTransparency = 0.500
					ButtonBar.BackgroundTransparency = 0.5
					ButtonBar.TextWrapped = true
					ButtonBar.AutoButtonColor = false
					ButtonBar.ClipsDescendants = true

					ButtonBarUIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(20, 20, 20)), ColorSequenceKeypoint.new(0.52, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(20, 20, 20))}
					ButtonBarUIGradient.Name = "ButtonBarUIGradient"
					ButtonBarUIGradient.Parent = ButtonBar

					ButtonBarUICorner.CornerRadius = UDim.new(0, 4)
					ButtonBarUICorner.Name = "ButtonBarUICorner"
					ButtonBarUICorner.Parent = ButtonBar

					ButtonBar.MouseEnter:Connect(function()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0}
						):Play()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0}
						):Play()
					end)

					ButtonBar.MouseLeave:Connect(function()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0.5}
						):Play()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0.5}
						):Play()
					end)

					ButtonBar.MouseButton1Down:Connect(function()
						ButtonBar.TextSize = 0
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextSize = 12}
						):Play()
						DropdownTitle.Text = tostring(visualTitle.." : "..v)
						CircleAnim(ButtonBar,Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,255))
						options.callback(v)
					end)
				end

				function UpdateInputOfSearchText()
					local InputText = string.upper(SearchBar.Text)
					for _,button in pairs(SelectionScrolling:GetChildren())do
						if button:IsA("TextButton") then
							if InputText == "" or string.find(string.upper(button.Text),InputText) ~= nil then
								button.Visible = true
							else
								button.Visible = false
							end
						end
					end
				end

				SearchBar.Changed:Connect(UpdateInputOfSearchText)

				DropdownButton.MouseButton1Down:Connect(function()
					if DropdownFunctions == false  then
						TweenService:Create(
							SelectionFrame,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 225, 0, 116)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Rotation = 90}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageColor3 = Color3.fromRGB(0, 255, 255)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageTransparency = 0}
						):Play()
					else
						TweenService:Create(
							SelectionFrame,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 225, 0, 0)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Rotation = 0}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageColor3 = Color3.fromRGB(255, 255, 255)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageTransparency = 0.5}
						):Play()
					end
					SelectionScrolling.CanvasSize = UDim2.new(0,0,0,SelectionScrollingUIListLayout.AbsoluteContentSize.Y + 10)
					DropdownFunctions = not DropdownFunctions
				end)

				local DropdownVisual = {}

				function DropdownVisual.Clear()
					TweenService:Create(
						SelectionFrame,
						TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
						{Size = UDim2.new(0, 225, 0, 0)}
					):Play()
					DropdownFunctions = not DropdownFunctions
					DropdownTitle.Text = tostring(visualTitle.." : ")
					for i, v in next, SelectionScrolling:GetChildren() do
						if v:IsA("TextButton") then
							v:Destroy()
						end
					end
				end

				function DropdownVisual.Add(value)

					local ButtonBar = Instance.new("TextButton")
					local ButtonBarUIGradient = Instance.new("UIGradient")
					local ButtonBarUICorner = Instance.new("UICorner")

					ButtonBar.Name = "ButtonBar"
					ButtonBar.Parent = SelectionScrolling
					ButtonBar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
					ButtonBar.BorderSizePixel = 0
					ButtonBar.Size = UDim2.new(0, 204, 0, 18)
					ButtonBar.Font = Enum.Font.Gotham
					ButtonBar.TextColor3 = Color3.fromRGB(255, 255, 255)
					ButtonBar.TextSize = 12.000
					ButtonBar.Text = tostring(value)
					ButtonBar.TextTransparency = 0.500
					ButtonBar.BackgroundTransparency = 0.5
					ButtonBar.TextWrapped = true
					ButtonBar.AutoButtonColor = false
					ButtonBar.ClipsDescendants = true

					ButtonBarUIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(20, 20, 20)), ColorSequenceKeypoint.new(0.52, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(20, 20, 20))}
					ButtonBarUIGradient.Name = "ButtonBarUIGradient"
					ButtonBarUIGradient.Parent = ButtonBar

					ButtonBarUICorner.CornerRadius = UDim.new(0, 4)
					ButtonBarUICorner.Name = "ButtonBarUICorner"
					ButtonBarUICorner.Parent = ButtonBar

					ButtonBar.MouseEnter:Connect(function()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0}
						):Play()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0}
						):Play()
					end)

					ButtonBar.MouseLeave:Connect(function()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{BackgroundTransparency = 0.5}
						):Play()
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextTransparency = 0.5}
						):Play()
					end)

					ButtonBar.MouseButton1Down:Connect(function()
						ButtonBar.TextSize = 0
						TweenService:Create(
							ButtonBar,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{TextSize = 12}
						):Play()
						DropdownTitle.Text = tostring(visualTitle.." : "..value)
						CircleAnim(ButtonBar,Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,255))
						options.callback(value)
					end)
					SelectionScrolling.CanvasSize = UDim2.new(0,0,0,SelectionScrollingUIListLayout.AbsoluteContentSize.Y + 10)
				end

				return DropdownVisual
			end

			function LibraryFunction.MultiDropdown(options)
				local DropdownFunctions = false
				local MultiDropdown = {}
				local visualTitle = options.Title or "Dropdown : nil"
				local visualItem = options.Item or {}
				local visualcallback = options.callback or function(Item) return end
				local visualdefault = options.Default or {}

				local DropdownFrame = Instance.new("Frame")
				local DropdownFrameUICorner = Instance.new("UICorner")
				local DropdownTitle = Instance.new("TextLabel")
				local Arrow = Instance.new("ImageLabel")
				local DropdownButton = Instance.new("TextButton")

				DropdownFrame.Name = "DropdownFrame"
				DropdownFrame.Parent = PageFrameMain
				DropdownFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
				DropdownFrame.BorderColor3 = Color3.fromRGB(27, 42, 53)
				DropdownFrame.BorderSizePixel = 0
				DropdownFrame.Position = UDim2.new(0, 0, 0.392857134, 0)
				DropdownFrame.Size = UDim2.new(0, 225, 0, 30)

				DropdownFrameUICorner.CornerRadius = UDim.new(0, 4)
				DropdownFrameUICorner.Name = "DropdownFrameUICorner"
				DropdownFrameUICorner.Parent = DropdownFrame

				DropdownTitle.Name = "DropdownTitle"
				DropdownTitle.Parent = DropdownFrame
				DropdownTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				DropdownTitle.BackgroundTransparency = 1.000
				DropdownTitle.Position = UDim2.new(0.0488888882, 0, 0, 0)
				DropdownTitle.Size = UDim2.new(0, 170, 0, 29)
				DropdownTitle.Font = Enum.Font.GothamMedium
				DropdownTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
				DropdownTitle.TextSize = 12.000
				DropdownTitle.Text = visualTitle.." : "
				DropdownTitle.TextTransparency = 0.500
				DropdownTitle.TextWrapped = true
				DropdownTitle.TextXAlignment = Enum.TextXAlignment.Left

				Arrow.Name = "Arrow"
				Arrow.Parent = DropdownTitle
				Arrow.AnchorPoint = Vector2.new(0.5, 0.5)
				Arrow.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Arrow.BackgroundTransparency = 1.000
				Arrow.Position = UDim2.new(1.14999998, 0, 0.5, 0)
				Arrow.Size = UDim2.new(0, 20, 0, 20)
				Arrow.Image = "http://www.roblox.com/asset/?id=6031094674"
				Arrow.ImageTransparency = 0.500

				DropdownButton.Name = "DropdownButton"
				DropdownButton.Parent = DropdownFrame
				DropdownButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				DropdownButton.BackgroundTransparency = 1.000
				DropdownButton.Size = UDim2.new(0, 225, 0, 29)
				DropdownButton.AutoButtonColor = false
				DropdownButton.Font = Enum.Font.SourceSans
				DropdownButton.Text = ""
				DropdownButton.TextColor3 = Color3.fromRGB(0, 0, 0)
				DropdownButton.TextSize = 14.000

				local SelectionMultiFrame = Instance.new("Frame")
				local SelectionFrameUICorner = Instance.new("UICorner")
				local SearchFrame = Instance.new("Frame")
				local SearchFrameUICorner = Instance.new("UICorner")
				local SearchBar = Instance.new("TextBox")
				local SelectionScrolling = Instance.new("ScrollingFrame")
				local SelectionScrollingUIListLayout = Instance.new("UIListLayout")
				local SelectionScrollingUIPadding = Instance.new("UIPadding")

				SelectionMultiFrame.Name = "SelectionMultiFrame"
				SelectionMultiFrame.Parent = PageFrameMain
				SelectionMultiFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
				SelectionMultiFrame.BorderColor3 = Color3.fromRGB(27, 42, 53)
				SelectionMultiFrame.BorderSizePixel = 0
				SelectionMultiFrame.Position = UDim2.new(0, 0, 0.497023821, 0)
				SelectionMultiFrame.Size = UDim2.new(0, 225, 0, 0)
				SelectionMultiFrame.ClipsDescendants = true

				SelectionFrameUICorner.CornerRadius = UDim.new(0, 4)
				SelectionFrameUICorner.Name = "SelectionFrameUICorner"
				SelectionFrameUICorner.Parent = SelectionMultiFrame

				SearchFrame.Name = "SearchFrame"
				SearchFrame.Parent = SelectionMultiFrame
				SearchFrame.Active = true
				SearchFrame.AnchorPoint = Vector2.new(0.5, 0.5)
				SearchFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
				SearchFrame.BorderSizePixel = 0
				SearchFrame.Position = UDim2.new(0.5, 0, 0.150000006, 0)
				SearchFrame.Size = UDim2.new(0, 215, 0, 25)

				SearchFrameUICorner.CornerRadius = UDim.new(0, 4)
				SearchFrameUICorner.Name = "SearchFrameUICorner"
				SearchFrameUICorner.Parent = SearchFrame

				SearchBar.Name = "SearchBar"
				SearchBar.Parent = SearchFrame
				SearchBar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				SearchBar.BackgroundTransparency = 1.000
				SearchBar.BorderColor3 = Color3.fromRGB(27, 42, 53)
				SearchBar.Position = UDim2.new(0.0279069766, 0, 0, 0)
				SearchBar.Size = UDim2.new(0, 205, 0, 25)
				SearchBar.Font = Enum.Font.GothamMedium
				SearchBar.PlaceholderText = "Search . . ."
				SearchBar.Text = ""
				SearchBar.TextColor3 = Color3.fromRGB(255, 255, 255)
				SearchBar.TextSize = 12.000
				SearchBar.TextTransparency = 0.500
				SearchBar.TextWrapped = true
				SearchBar.TextXAlignment = Enum.TextXAlignment.Left

				SelectionScrolling.Name = "SelectionScrolling"
				SelectionScrolling.Parent = SelectionMultiFrame
				SelectionScrolling.Active = true
				SelectionScrolling.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				SelectionScrolling.BackgroundTransparency = 1.000
				SelectionScrolling.BorderSizePixel = 0
				SelectionScrolling.Position = UDim2.new(0.0219999999, 0, 0.289999992, 0)
				SelectionScrolling.Size = UDim2.new(0, 215, 0, 75)
				SelectionScrolling.BottomImage = ""
				SelectionScrolling.ScrollBarThickness = 2
				SelectionScrolling.TopImage = ""

				SelectionScrollingUIListLayout.Name = "SelectionScrollingUIListLayout"
				SelectionScrollingUIListLayout.Parent = SelectionScrolling
				SelectionScrollingUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
				SelectionScrollingUIListLayout.Padding = UDim.new(0, 5)

				SelectionScrollingUIPadding.Name = "SelectionScrollingUIPadding"
				SelectionScrollingUIPadding.Parent = SelectionScrolling
				SelectionScrollingUIPadding.PaddingLeft = UDim.new(0, 5)
				SelectionScrollingUIPadding.PaddingTop = UDim.new(0, 5)

				function UpdateInputOfSearchText()
					local InputText = string.upper(SearchBar.Text)
					for _,button in pairs(SelectionScrolling:GetChildren())do
						if button:IsA("Frame") then
							for i,v in pairs(button:GetChildren()) do
								if v.Name == "TextButton" then
									for o,p in pairs(v:GetChildren()) do
										if p.Name == "TextLabel" then
											if InputText == "" or string.find(string.upper(p.Text),InputText) ~= nil then
												button.Visible = true
											else
												button.Visible = false
											end
										end
									end
								end
							end
						end
					end
				end

				SearchBar.Changed:Connect(UpdateInputOfSearchText)

				for i,v in pairs(visualItem) do

					local ListFrame = Instance.new("Frame")
					local TextButton = Instance.new("TextButton")
					local TextLabel = Instance.new("TextLabel")
					local Toggle = Instance.new("ImageButton")
					local ToggleUICorner = Instance.new("UICorner")
					local ToggleInner = Instance.new("ImageButton")
					local ToggleInnerUICorner = Instance.new("UICorner")

					ListFrame.Name = "ListFrame"
					ListFrame.Parent = SelectionScrolling
					ListFrame.Active = true
					ListFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ListFrame.BackgroundTransparency = 1.000
					ListFrame.Size = UDim2.new(0, 204, 0, 26)

					TextButton.Name = "TextButton"
					TextButton.Parent = ListFrame
					TextButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					TextButton.BackgroundTransparency = 1.000
					TextButton.Size = UDim2.new(0, 204, 0, 26)
					TextButton.Font = Enum.Font.SourceSans
					TextButton.Text = ""
					TextButton.TextColor3 = Color3.fromRGB(0, 0, 0)
					TextButton.TextSize = 14.000

					TextLabel.Name = "TextLabel"
					TextLabel.Parent = TextButton
					TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					TextLabel.BackgroundTransparency = 1.000
					TextLabel.Position = UDim2.new(0.156862751, 0, 0, 0)
					TextLabel.Size = UDim2.new(0, 172, 0, 26)
					TextLabel.Font = Enum.Font.GothamMedium
					TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
					TextLabel.TextSize = 12.000
					TextLabel.Text = tostring(v)
					TextLabel.TextTransparency = 0.500
					TextLabel.TextXAlignment = Enum.TextXAlignment.Left

					Toggle.Name = "Toggle"
					Toggle.Parent = TextButton
					Toggle.AnchorPoint = Vector2.new(0.5, 0.5)
					Toggle.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
					Toggle.BackgroundTransparency = 1.000
					Toggle.Position = UDim2.new(0.0500000007, 0, 0.5, 0)
					Toggle.Size = UDim2.new(0, 19, 0, 19)
					Toggle.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
					Toggle.ImageColor3 = Color3.fromRGB(30, 30, 30)

					ToggleUICorner.CornerRadius = UDim.new(0, 30)
					ToggleUICorner.Name = "ToggleUICorner"
					ToggleUICorner.Parent = Toggle

					ToggleInner.Name = "ToggleInner"
					ToggleInner.Parent = Toggle
					ToggleInner.AnchorPoint = Vector2.new(0.5, 0.5)
					ToggleInner.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
					ToggleInner.BackgroundTransparency = 1.000
					ToggleInner.Position = UDim2.new(0.5, 0, 0.5, 0)
					ToggleInner.Size = UDim2.new(0, 0, 0, 0)
					ToggleInner.Image = "http://www.roblox.com/asset/?id=6031625146"
					ToggleInner.ImageColor3 = Color3.fromRGB(0, 255, 255)

					ToggleInnerUICorner.CornerRadius = UDim.new(0, 30)
					ToggleInnerUICorner.Name = "ToggleInnerUICorner"
					ToggleInnerUICorner.Parent = ToggleInner

					for o,p in pairs(visualdefault) do
						if v == p  then
							table.insert(MultiDropdown,p)
							TweenService:Create(
								ToggleInner,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{Size = UDim2.new(0, 15, 0, 15)}
							):Play()
							DropdownTitle.Text = tostring(visualTitle.." : "..table.concat(MultiDropdown,","))
							pcall(visualcallback,MultiDropdown)
						end
					end

					TextButton.MouseButton1Down:Connect(function()
						if tablefound(MultiDropdown,v) == false then
							table.insert(MultiDropdown,v)
							TweenService:Create(
								ToggleInner,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{Size = UDim2.new(0, 15, 0, 15)}
							):Play()
						else
							for ine,va in pairs(MultiDropdown) do
								if va == v then
									table.remove(MultiDropdown,ine)
								end
							end
							TweenService:Create(
								ToggleInner,
								TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
								{Size = UDim2.new(0, 0, 0, 0)}
							):Play()
						end
						pcall(visualcallback,MultiDropdown)
						DropdownTitle.Text = tostring(visualTitle.." : "..table.concat(MultiDropdown,","))
					end)
				end

				DropdownButton.MouseButton1Down:Connect(function()
					if DropdownFunctions == false  then
						TweenService:Create(
							SelectionMultiFrame,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 225, 0, 116)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Rotation = 90}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageColor3 = Color3.fromRGB(0, 255, 255)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageTransparency = 0}
						):Play()
					else
						TweenService:Create(
							SelectionMultiFrame,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Size = UDim2.new(0, 225, 0, 0)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{Rotation = 0}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageColor3 = Color3.fromRGB(255, 255, 255)}
						):Play()
						TweenService:Create(
							Arrow,
							TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
							{ImageTransparency = 0.5}
						):Play()
					end
					SelectionScrolling.CanvasSize = UDim2.new(0,0,0,SelectionScrollingUIListLayout.AbsoluteContentSize.Y + 10)
					DropdownFunctions = not DropdownFunctions
				end)
			end

			function LibraryFunction.Slider(options)

				local sliderfunc = {}

				local visualTitle = options.Title or "Slider : nil"
				local visualMax = options.Max or 100
				local visualMin = options.Min or 0
				local visualDefault = options.Default or 50
				local visualcallback = options.callback or function() end

				local SliderFrame = Instance.new("Frame")
				local SliderFrame2 = Instance.new("Frame")
				local SliderFrame2UICorner = Instance.new("UICorner")
				local CustomValueMain = Instance.new("Frame")	
				local CustomValueMainUICorner = Instance.new("UICorner")
				local TextBox = Instance.new("TextBox")
				local UICorner = Instance.new("UICorner")
				local SliderValueFrame = Instance.new("Frame")
				local SliderValueFrame_2 = Instance.new("Frame")
				local SliderValueFrame_3 = Instance.new("Frame")
				local UICorner_2 = Instance.new("UICorner")
				local SliderFrameUICorner = Instance.new("UICorner")
				local SliderTitle = Instance.new("TextLabel")

				SliderFrame.Name = "SliderFrame"
				SliderFrame.Parent = PageFrameMain
				SliderFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
				SliderFrame.BorderSizePixel = 0
				SliderFrame.ClipsDescendants = true
				SliderFrame.Position = UDim2.new(0, 0, 0.857142866, 0)
				SliderFrame.Size = UDim2.new(0, 225, 0, 42)

				SliderFrame2.Name = "SliderFrame2"
				SliderFrame2.Parent = SliderFrame
				SliderFrame2.AnchorPoint = Vector2.new(0.5, 0.5)
				SliderFrame2.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
				SliderFrame2.BackgroundTransparency = 1.000
				SliderFrame2.BorderSizePixel = 0
				SliderFrame2.ClipsDescendants = true
				SliderFrame2.Position = UDim2.new(0.503888905, 0, 0.5, 0)
				SliderFrame2.Size = UDim2.new(0, 222, 0, 42)

				SliderFrame2UICorner.CornerRadius = UDim.new(0, 4)
				SliderFrame2UICorner.Name = "SliderFrame2UICorner"
				SliderFrame2UICorner.Parent = SliderFrame2

				CustomValueMain.Name = "CustomValueMain"
				CustomValueMain.Parent = SliderFrame2
				CustomValueMain.AnchorPoint = Vector2.new(0.5, 0.5)
				CustomValueMain.BackgroundColor3 = Color3.fromRGB(23,23,23)
				CustomValueMain.BackgroundTransparency = 0
				CustomValueMain.BorderSizePixel = 0
				CustomValueMain.ClipsDescendants = true
				CustomValueMain.Position = UDim2.new(0.8, 0, 0.35, 0)
				CustomValueMain.Size = UDim2.new(0, 80, 0, 20)

				CustomValueMainUICorner.CornerRadius = UDim.new(0, 4)
				CustomValueMainUICorner.Name = "CustomValueMainUICorner"
				CustomValueMainUICorner.Parent = CustomValueMain

				TextBox.Parent = CustomValueMain
				TextBox.AnchorPoint = Vector2.new(0.5, 0.5)
				TextBox.BackgroundColor3 = Color3.fromRGB(23, 23, 23)
				TextBox.BackgroundTransparency = 1.000
				TextBox.BorderSizePixel = 0
				TextBox.ClipsDescendants = true
				TextBox.Position = UDim2.new(0.5, 0, 0.5, 0)
				TextBox.Size = UDim2.new(0, 68, 0, 18)
				TextBox.Font = Enum.Font.GothamMedium
				TextBox.TextSize = 12
				TextBox.PlaceholderColor3 = Color3.fromRGB(222, 222, 222)
				TextBox.Text = tostring(visualDefault and math.floor( (visualDefault / visualMax) * (visualMax - visualMin) + visualMin) or 0)
				TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
				TextBox.TextTransparency = 0

				UICorner.CornerRadius = UDim.new(0, 4)
				UICorner.Name = ""
				UICorner.Parent = TextBox

				SliderValueFrame.Name = "SliderValueFrame"
				SliderValueFrame.Parent = SliderFrame2
				SliderValueFrame.AnchorPoint = Vector2.new(0.5, 0.5)
				SliderValueFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
				SliderValueFrame.BorderSizePixel = 0
				SliderValueFrame.Position = UDim2.new(0.5, 0, 0.769999981, 0)
				SliderValueFrame.Size = UDim2.new(0, 215, 0, 5)

				SliderValueFrame_2.Name = "SliderValueFrame"
				SliderValueFrame_2.Parent = SliderValueFrame
				SliderValueFrame_2.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
				SliderValueFrame_2.BorderSizePixel = 0
				SliderValueFrame_2.Size = UDim2.new((visualDefault or 0) / visualMax, 0, 0, 5)

				SliderValueFrame_3.Name = "SliderValueFrame"
				SliderValueFrame_3.Parent = SliderValueFrame
				SliderValueFrame_3.AnchorPoint = Vector2.new(0.5, 0.5)
				SliderValueFrame_3.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
				SliderValueFrame_3.BorderSizePixel = 0
				SliderValueFrame_3.ClipsDescendants = true
				SliderValueFrame_3.Position = UDim2.new((visualDefault or 0)/visualMax, 0.5, 0.5,0.5, 0)
				SliderValueFrame_3.Size = UDim2.new(0, 10, 0, 10)

				UICorner_2.CornerRadius = UDim.new(0, 300)
				UICorner_2.Name = ""
				UICorner_2.Parent = SliderValueFrame_3

				SliderFrameUICorner.CornerRadius = UDim.new(0, 4)
				SliderFrameUICorner.Name = "SliderFrameUICorner"
				SliderFrameUICorner.Parent = SliderFrame

				SliderTitle.Name = "SliderTitle"
				SliderTitle.Parent = SliderFrame
				SliderTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				SliderTitle.BackgroundTransparency = 1.000
				SliderTitle.Position = UDim2.new(0.034351144, 0, 0, 0)
				SliderTitle.Size = UDim2.new(0, 150, 0, 27)
				SliderTitle.Font = Enum.Font.GothamMedium
				SliderTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
				SliderTitle.TextSize = 12.000
				SliderTitle.Text = visualTitle
				SliderTitle.TextWrapped = true
				SliderTitle.TextTransparency = 0.500
				SliderTitle.TextXAlignment = Enum.TextXAlignment.Left

				local function move(input)
					local pos =
						UDim2.new(
							math.clamp((input.Position.X - SliderValueFrame.AbsolutePosition.X) / SliderValueFrame.AbsoluteSize.X, 0, 1),
							0,
							0.5,
							0
						)
					local pos1 =
						UDim2.new(
							math.clamp((input.Position.X - SliderValueFrame.AbsolutePosition.X) / SliderValueFrame.AbsoluteSize.X, 0, 1),
							0,
							0,
							5
						)

					SliderValueFrame_2:TweenSize(pos1, "Out", "Sine", 0.2, true)
					SliderValueFrame_3:TweenPosition(pos, "Out", "Sine", 0.2, true)
					local value = math.floor(((pos.X.Scale * visualMax) / visualMax) * (visualMax - visualMin) + visualMin)
					TextBox.Text = tostring(value)
					pcall(options.callback, TextBox.Text)
				end

				local dragging = false

				SliderFrame.InputBegan:Connect(
					function(input)
						if input.UserInputType == Enum.UserInputType.MouseButton1 then
							dragging = true

						end
					end
				)
				SliderFrame.InputEnded:Connect(
					function(input)
						if input.UserInputType == Enum.UserInputType.MouseButton1 then
							dragging = false

						end
					end
				)


				SliderValueFrame.InputBegan:Connect(
					function(input)
						if input.UserInputType == Enum.UserInputType.MouseButton1 then
							dragging = true

						end
					end
				)
				SliderValueFrame.InputEnded:Connect(
					function(input)
						if input.UserInputType == Enum.UserInputType.MouseButton1 then
							dragging = false

						end
					end
				)
				game:GetService("UserInputService").InputChanged:Connect(function(input)
					if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
						move(input)
					end
				end)

				TextBox.FocusLost:Connect(function()
					if TextBox.Text == "" then
						TextBox.Text  = visualDefault
					end
					if  tonumber(TextBox.Text) > visualMax then
						TextBox.Text  = visualMax
					end
					SliderValueFrame_2:TweenSize(UDim2.new((TextBox.Text or 0) / visualMax, 0, 0, 5), "Out", "Sine", 0.2, true)
					SliderValueFrame_3:TweenPosition(UDim2.new((TextBox.Text or 0)/visualMax, 0,0.5, 0) , "Out", "Sine", 0.2, true)
					TextBox.Text = tostring(TextBox.Text and math.floor( (TextBox.Text / visualMax) * (visualMax - visualMin) + visualMin) )
					pcall(options.callback, TextBox.Text)
				end)

				function sliderfunc.Update(value)
					SliderValueFrame_2:TweenSize(UDim2.new((value or 0) / visualMax, 0, 0, 5), "Out", "Sine", 0.2, true)
					SliderValueFrame_3:TweenPosition(UDim2.new((value or 0)/visualMax, 0,0.5, 0) , "Out", "Sine", 0.2, true)
					pcall(function()
						pcall(options.callback, TextBox.Text)
					end)
				end
				return sliderfunc
			end

			return LibraryFunction
		end
		return LibraryPage
	end
	LeftScrollbar.MouseButton1Down:Connect(function()
		FolderUIPageLayout:Previous()
		TweenService:Create(
			LeftScrollbar,
			TweenInfo.new(0.1, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out),
			{Size = UDim2.new(0, 20, 0, 20)}
		):Play()
		repeat wait() until LeftScrollbar.Size == UDim2.new(0, 20, 0, 20)
		TweenService:Create(
			LeftScrollbar,
			TweenInfo.new(0.1, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out),
			{Size = UDim2.new(0, 40, 0, 40)}
		):Play()
		for i ,v in next , Scrollingbar:GetChildren() do
			if v:IsA("TextButton") and v.Name == tostring(FolderUIPageLayout.CurrentPage):gsub("%MainPage", "ButtonBar") then
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{TextTransparency = 0}
				):Play()
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundTransparency = 0}
				):Play()
			elseif v:IsA("TextButton") then
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{TextTransparency = 0.5}
				):Play()
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundTransparency = 0.65}
				):Play()
			end
		end
	end)
	RightScrollbar.MouseButton1Down:Connect(function()
		FolderUIPageLayout:Next()
		TweenService:Create(
			RightScrollbar,
			TweenInfo.new(0.1, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out),
			{Size = UDim2.new(0, 20, 0, 20)}
		):Play()
		repeat wait() until RightScrollbar.Size == UDim2.new(0, 20, 0, 20)
		TweenService:Create(
			RightScrollbar,
			TweenInfo.new(0.1, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out),
			{Size = UDim2.new(0, 40, 0, 40)}
		):Play()
		for i ,v in next , Scrollingbar:GetChildren() do
			if v:IsA("TextButton") and v.Name == tostring(FolderUIPageLayout.CurrentPage):gsub("%MainPage", "ButtonBar") then
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{TextTransparency = 0}
				):Play()
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundTransparency = 0}
				):Play()
			elseif v:IsA("TextButton") then
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{TextTransparency = 0.5}
				):Play()
				TweenService:Create(
					v,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundTransparency = 0.65}
				):Play()
			end
		end
	end)
	return LibraryTab
end
return Library
