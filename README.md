getgenv().start_tick = tick()

local load = Instance.new("ScreenGui")
local Main = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local Top = Instance.new("Frame")
local UICorner_2 = Instance.new("UICorner")
local cat = Instance.new("TextLabel")
local ori = Instance.new("TextLabel")
local word = Instance.new("TextLabel")

local loader = {}
loader.games = {}
local ts = game:GetService("TweenService")

load.Name = "load"
load.Parent = game.CoreGui
load.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
if syn then
	syn.protect_gui(load)
end

Main.Name = "Main"
Main.Parent = load
Main.AnchorPoint = Vector2.new(0.5, 0.5)
Main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Main.Position = UDim2.new(0.5, 0, 0.5, 0)
Main.Size = UDim2.new(0, 232, 0, 60)
Main.BackgroundTransparency = 1

UICorner.CornerRadius = UDim.new(0, 5)
UICorner.Parent = Main

Top.Name = "Top"
Top.Parent = Main
Top.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Top.BorderSizePixel = 0
Top.Size = UDim2.new(0, 232, 0, 23)
Top.BackgroundTransparency = 1

UICorner_2.CornerRadius = UDim.new(0, 5)
UICorner_2.Parent = Top

cat.Name = "cat"
cat.Parent = Top
cat.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
cat.BackgroundTransparency = 1.000
cat.TextTransparency = 1.000
cat.Position = UDim2.new(0.0258620698, 0, 0, 0)
cat.Size = UDim2.new(0, 160, 0, 23)
cat.Font = Enum.Font.SourceSans
cat.Text = "SkyHax"
cat.TextColor3 = Color3.fromRGB(127, 0, 191)
cat.TextSize = 16.000
cat.TextXAlignment = Enum.TextXAlignment.Left

ori.Name = "ori"
ori.Parent = Top
ori.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ori.BackgroundTransparency = 1.000
ori.TextTransparency = 1.000
ori.Size = UDim2.new(0, 78, 0, 23)
ori.Font = Enum.Font.SourceSans
ori.Text = "SkyHax"
ori.TextColor3 = Color3.fromRGB(0, 255, 127)
ori.TextSize = 16.000


word.Name = "word"
word.Parent = Main
word.BackgroundColor3 = Color3.fromRGB(85, 255, 127)
word.BackgroundTransparency = 1.000
word.Position = UDim2.new(0.0258620698, 0, 0.508333325, 0)
word.Size = UDim2.new(0, 220, 0, 23)
word.Font = Enum.Font.SourceSans
word.TextTransparency = 1.000
word.Text = "SkyHax ~"
word.TextColor3 = Color3.fromRGB(255, 255, 255)
word.TextSize = 19.000
word.TextScaled = true

function loader:addGame(id, name, url)
	loader.games[tostring(id)] = {name = name, loadstring = url}
end

function loader:detectGame()
	local detectedGame = self.games[tostring(game.PlaceId)]
	if detectedGame then
		return detectedGame
	else
		return
	end
end

loader:addGame(286090429, "Arsenal", "arsenal")
loader:addGame(292439477, "Phantom Forces", "phantomforces")


local detectedGame = loader:detectGame()

spawn(function()
	ts:Create(Main, TweenInfo.new(0.5), {BackgroundTransparency = 0}):Play()
	ts:Create(cat, TweenInfo.new(0.5), {TextTransparency = 0}):Play()
	ts:Create(ori, TweenInfo.new(0.5), {TextTransparency = 0}):Play()
	ts:Create(Top, TweenInfo.new(0.5), {BackgroundTransparency = 0}):Play()
	ts:Create(word, TweenInfo.new(0.5), {TextTransparency = 0}):Play()
    
    wait(0.5)
    
	word.Text = "loaded in " .. math.floor((tick() - getgenv().start_tick) * 10) / 10 .. " seconds."

    if getgenv().loaded then
        word.Text = "the script is already loaded!"
    else
        getgenv().loaded = true
        if detectedGame then
            word.Text = "supported game! loading ".. detectedGame.name
            if not pcall(function()
                loadstring(game:HttpGet("https://github.com/Bobby12123/d/tree/main/".. detectedGame.loadstring ..".lua"))()
            end) then 
                word.Text = "the script failed to load!"
            end
        else
            word.Text = "we are currently working on universal..."
        end
    end

	wait(1)
    
	cat.Visible = false
	ori.Visible = false
	word.Visible = false
	Top.Visible = false
	Main:TweenSize(UDim2.new(0, 0, 0, 60), Enum.EasingDirection.In, Enum.EasingStyle.Linear, 1, false)
    
	wait(1)

	load:Destroy()
end)
