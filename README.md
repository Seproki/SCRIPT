--- Hello Kino :) your the new owner of VBA nice doing nothing and gaining access 
-- to a whole game & community well im pretty sure your Dumb Af and just using this 
-- game for profit without caring about the community so im sure you dont mind if 
-- everyone Cheats Right? :) Im excited for the rewrite please make it a bit more 
-- exciting then this one and if you use Any of Snakes Code then LMAO RIP. 
-- From your Friendly neighbour Hood Ape Blankais <3 ps STEPHAN DID GOOD !!!! --- 
----- keybinds are z,x,c,v,b,n,m,f,g,h,j,k,r F = activate spikehackz = Change spikehack to fastx = change spikehack to super fast --
----- v = change spike hack so u can spike from backrow b = long spike that means high spike and semi fast--------------------------------
----- n = normal fast spike ( legit fast spike ) gotta hit it fast m = slow spike next to the net ----- 
------ H = disable the auto set R = activate sprint modifier if u press shift it auto activate infsprint ----
--- and i updated it so you have No Cooldown when Executed ------------ 
---------------- Have Fun ,Blank-----------------------------------------------------------------

local plr = game.Players.LocalPlayer
local old;
old = hookmetamethod(game,"__index",function(a,b)
    if tostring(b) == "JumpPower" and getcallingscript() == plr.PlayerGui.LocalScript then
        return 32
    end
    return old(a,b)
end)

local library = loadstring(game:HttpGet(('https://raw.githubusercontent.com/AikaV3rm/UiLib/master/Lib.lua')))()
local w = library:CreateWindow("Blankais Reborn V2")
local b = w:CreateFolder("Main")
local m = w:CreateFolder("Misc")
local ws,jp,hh = 16,32,2.1663174629211

b:Button("APE MODE",function()
    cooldwon = hookfunction(wait, function(jump)
        if jump == 0.5 then return cooldwon() end
        return cooldwon(jump)
        end)
    local LocalPlayer = game.Players.LocalPlayer
    local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:wait()
    local Humanoid = Character:WaitForChild("Humanoid", 1)
    local Hrp = Character:WaitForChild("HumanoidRootPart", 1)
    local Mouse = LocalPlayer:GetMouse()
    local f = LocalPlayer.Backpack.Input
    local set = false
    local bumping = false
    local spiking = false
    local sprinting = false
    local holdingm1 = false
    local sprintmodifier = false
    local canset = true
    local setdir = false
    local setpower = 1
    _G.speed = 1.35
    _G.height = 0.160000000
    
    local LabelsTest = Instance.new("ScreenGui")
    local Labels = Instance.new("Folder")
    local Example = Instance.new("TextLabel")
    local Remove = Instance.new("TextButton")
    local Add = Instance.new("TextButton")
    
    LabelsTest.Name = "LabelsTest"
    LabelsTest.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
    LabelsTest.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    
    Labels.Name = "Labels"
    Labels.Parent = LabelsTest
    
    Example.Name = "Example"
    Example.Parent = LabelsTest
    Example.BackgroundColor3 = Color3.new(1, 1, 1)
    Example.BackgroundTransparency = 1
    Example.Position = UDim2.new(0.875999451, 0, 0.966830373, 0)
    Example.Size = UDim2.new(0.117271982, 0, 0.0324324518, 0)
    Example.Visible = false
    Example.Font = Enum.Font.SourceSansBold
    Example.Text = "BlaBla..."
    Example.TextColor3 = Color3.new(1, 1, 1)
    Example.TextScaled = true
    Example.TextSize = 14
    Example.TextStrokeTransparency = 0
    Example.TextWrapped = true
    Example.TextXAlignment = Enum.TextXAlignment.Right
    
    local function addBtn(Name)
        local label = Example:Clone()
        label.Visible = true
        label.Name = Name
        label.Text = Name
        label.TextColor3 = Color3.fromRGB(math.random(0,255),math.random(0,255),math.random(0,255))
        local sameColor = true
        repeat
            if #Labels:GetChildren() > 0 then
                for i,v in pairs(Labels:GetChildren()) do 
                    if label.TextColor3 ~= v.TextColor3 then
                        sameColor = false
                    else
                        label.TextColor3 = Color3.fromRGB(math.random(0,255),math.random(0,255),math.random(0,255))
                    end
                end
            else
                sameColor = false
            end
        until(sameColor == false)
        label.Parent = Labels
    end
    
    local function removeBtn(Name, HardName)
        for i,v in pairs(Labels:GetChildren()) do
            if HardName then
                if string.find(v.Name, HardName) then
                    v:Destroy()
                end
            else
                if v.Name == Name then
                    v:Destroy()
                end
            end
        end
    end
    
    local function changeName(Name, NewName)
        for i,v in pairs(Labels:GetChildren()) do
            if string.find(v.Name, Name) then
                v.Name = NewName
                v.Text = NewName
            end
        end
    end
    
    local function recalculate()
        local positionedLabels = 0
        for i,v in pairs(Labels:GetChildren()) do
            if positionedLabels > 0 then 
                v.Position = Example.Position - UDim2.new(0,0,Example.Size.Y.Scale*positionedLabels,0)
            else
                v.Position = Example.Position
            end
            positionedLabels = positionedLabels + 1
        end
    end
    
    Labels.ChildAdded:Connect(function()
        recalculate()
    end)
    
    Labels.ChildRemoved:Connect(function()
        recalculate()
    end)
    
    local function animcheck(a)
        local g = false
        for i,v in pairs(Humanoid:GetPlayingAnimationTracks()) do 
            if tostring(v) == a then
                g = true
            end
        end
        return g
    end
    
    addBtn("Set(Enabled/No Dir)")
    
    Mouse.Button1Down:Connect(function()
        if Humanoid.FloorMaterial == Enum.Material.Air or Character:FindFirstChild("ServeBall") or animcheck("Bump") or animcheck("Dive") or animcheck("Spike") or not canset then return end
        set = true
        while set do
            if Humanoid.FloorMaterial == Enum.Material.Air or Character:FindFirstChild("ServeBall") or animcheck("Bump") or animcheck("Dive") or animcheck("Spike") then return end
            f:FireServer("set_start")
            if setdir then
                f:FireServer("set", { ["Velocity"] = Vector3.new(Hrp.Velocity.X,Hrp.Velocity.Y,Hrp.Velocity.Z), ["power"] = setpower })
            else
                f:FireServer("set", { ["Velocity"] = Vector3.new(0,0,0), ["power"] = 1 })
            end
            wait()
        end
    end)
    
    Mouse.Button1Up:Connect(function()
        set = false
    end)
    
    Mouse.Button2Down:Connect(function()
        if Humanoid.FloorMaterial == Enum.Material.Air or Character:FindFirstChild("ServeBall") or animcheck("Set") or animcheck("Dive") or animcheck("Spike") then return end
        addBtn("Bumping")
        bumping = true
        while bumping do
            if Humanoid.FloorMaterial == Enum.Material.Air or Character:FindFirstChild("ServeBall") or animcheck("Set") or animcheck("Dive") or animcheck("Spike") then return end
            f:FireServer("bump_start")
            f:FireServer("bump", { ["power"] = 1 })
            wait()
        end
    end)
    
    Mouse.Button2Up:Connect(function()
        removeBtn("Bumping")
        bumping = false
    end)
    
    Mouse.KeyDown:Connect(function(key)
        if key == "f" then
            if not spiking then
                addBtn("SpikeHack(Fast)")
                _G.speed = 1.35
                _G.height = 0.160000000
                spiking = true
            else
                removeBtn(nil, "SpikeHack")
                spiking = false
            end
        elseif key == "z" then
            changeName("SpikeHack", "SpikeHack(Fast)")
            _G.speed = 1.35
            _G.height = 0.160000000
        elseif key == "x" then
            changeName("SpikeHack", "SpikeHack(Super Fast)")
            _G.speed = 1.5
            _G.height = 0.10
        elseif key == "c" then
            changeName("SpikeHack", "SpikeHack(Next to Net)")
            _G.speed = 1
            _G.height = 0.0463371426
        elseif key == "v" then
            changeName("SpikeHack", "SpikeHack(Fast Middle)")
            _G.speed = 1.2
            _G.height = 0.060
        elseif key == "m" then
            changeName("SpikeHack", "SpikeHack(Slow)")
            _G.speed = 0.65
            _G.height = 0.400
        elseif key == "n" then
            changeName("SpikeHack", "SpikeHack(Fast Legit)")
            _G.speed = 1
            _G.height = 0.162000000
        elseif key == "b" then
            changeName("SpikeHack", "SpikeHack(Line/High Legit)")
            _G.speed = 1
            _G.height = 0.317	
        elseif key == "y" then
            changeName("SpikeHack", "SpikeHack(Line/Super High Semi-Legit)")
            _G.height = 0.396052
            _G.speed = 1
        elseif key == "p" then
            changeName("SpikeHack", "SpikeHack(Net/Wing Spiker)")
            _G.height = -0.4
            _G.speed = 1.15
        elseif key == "l" then
            changeName("SpikeHack", "SpikeHack(Net(Close)/Wing Spiker)")
            _G.height = -0.9
            _G.speed = 1.15	
        elseif key == "q" then
            if animcheck("Dive") or Hrp:FindFirstChild("BodyVelocity") or not set then return end
            addBtn("DiveHack")
            local new = LocalPlayer.PlayerGui.LocalScript:Clone()
            new.Parent = LocalPlayer.PlayerGui
            Hrp.BodyGyro.D = 2000
            local rd = Hrp.BodyGyro.Changed:Connect(function(f)
                if f == "D" then
                    Hrp.BodyGyro.D = 2000
                end
            end)
            local rda = Humanoid:GetPropertyChangedSignal("WalkSpeed"):Connect(function()
                if Humanoid.WalkSpeed == 16 then
                    Humanoid.WalkSpeed = 8
                end
            end)
            getsenv(new).dive()
            new:Destroy()
            repeat wait() until not Hrp:FindFirstChild("BodyVelocity") rd:Disconnect() rda:Disconnect()
            removeBtn("DiveHack")
        elseif key == "0" then
            addBtn("InfSprint")
            sprinting = true
            Humanoid.WalkSpeed = 24
            local rd = Humanoid:GetPropertyChangedSignal("WalkSpeed"):Connect(function()
                if Humanoid.WalkSpeed == 16 and not sprintmodifier then
                    Humanoid.WalkSpeed = 24
                elseif Humanoid.WalkSpeed == 16 and sprintmodifier or Humanoid.WalkSpeed == 24 and sprintmodifier then
                    Humanoid.WalkSpeed = 30
                end
            end)
            repeat wait() until not sprinting rd:Disconnect()
        elseif key == "r" then
            if not sprintmodifier then
                addBtn("SprintModifier")
                sprintmodifier = true
            else
                removeBtn("SprintModifier")
                sprintmodifier = false
            end
        elseif key == "h" then
            if canset then
                changeName("Set", "Set(Disabled)")
                canset = false
            else
                if setdir then
                    changeName("Set", "Set(Enabled/Dir)" .. setpower)
                else
                    changeName("Set", "Set(Enabled/No Dir)" .. setpower)
                end
                canset = true		
            end
        elseif key == "j" then
            if not setdir then
                changeName("Set", "Set(Enabled/Dir)" .. setpower)
                setdir = true
            else
                setpower = 1
                changeName("Set", "Set(Enabled/No Dir)" .. setpower)
                setdir = false
            end
        elseif key == "k" then
            if setpower == 1 and setdir then
                setpower = 0.35
                changeName("Set", "Set(Enabled/Dir)" .. setpower)
            elseif setpower == 0.35 and setdir then
                setpower = 1
                changeName("Set", "Set(Enabled/Dir)" .. setpower)
            end
        end
    end)
    
    Mouse.KeyUp:Connect(function(key)
        if key == "0" then
            removeBtn("InfSprint")
            sprinting = false
            Humanoid.WalkSpeed = 16
        end
    end)
    
    local meta = getrawmetatable(game)
    local old
    old = hookfunction(meta.__namecall, function(self,...)
        local args = {...}
        local method = getnamecallmethod()
        
           if method == "FireServer" and args[1] == "spike" and type(args[2]) == "table" and spiking then 
            args[2]["dir"] = Vector3.new(args[2]["dir"].x, _G.height, args[2]["dir"].z)
            args[2]["power"] = _G.speed
            return old(self, unpack(args))
        end
        return old(self, unpack(args))
    end)
end)

m:Slider("WalkSpeed",{
    min = 16;
    max = 200;
    precise = false;
},function(value)
    ws = value
end)

m:Slider("JumpPower",{
    min = 32;
    max = 200;
    precise = false;
},function(value)
    jp = value
end)

m:Slider("Hip Height",{
    min = 2.1663174629211;
    max = 200;
    precise = false;
},function(value)
    hh = value
end)

m:Button("Inf Jump",function()
    function Action(Object, Function) if Object ~= nil then Function(Object); end end
    game:GetService'UserInputService'.InputBegan:connect(function(UserInput)
        if UserInput.UserInputType == Enum.UserInputType.Keyboard and UserInput.KeyCode == Enum.KeyCode.Space then
            Action(plr.Character.Humanoid, function(self)
                if self:GetState() == Enum.HumanoidStateType.Jumping or self:GetState() == Enum.HumanoidStateType.Freefall then
                    Action(self.Parent.HumanoidRootPart, function(self)
                        self.Velocity = Vector3.new(0, 50, 0);
                    end)
                end
            end)
        end
    end)
end)

m:Button("Open Shiftlock",function()
    plr.DevEnableMouseLock = true
end)

m:Button("Made By Seproki",function()
end)

m:Button("Destroy Gui",function(value)
    for i,v in pairs(game:GetService("CoreGui"):GetChildren()) do
        if v:FindFirstChild("HiI'mSexyDon'tTouchMePls") then
            v:Destroy()
        end
    end
end)

game:GetService("RunService").Stepped:Connect(function()
    pcall(function()
        plr.Character.Humanoid.WalkSpeed = ws
        plr.Character.Humanoid.JumpPower = jp
        plr.Character.Humanoid.HipHeight = hh
    end)
end)
