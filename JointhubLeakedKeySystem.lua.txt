-- Leaked By Jointhub.gg: https://discord.gg/nN6qyeKyV
-- Leaked By LeakHub: https://discord.gg/Ut46D4cwx
-- All this shit is leak, Bby

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")
local StarterGui = game:GetService("StarterGui")
local RunService = game:GetService("RunService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer

local ExecutorSupport = {
    Mobile = false,
    Executor = "Unknown"
}
pcall(function()
    if identifyexecutor then
        ExecutorSupport.Executor = identifyexecutor()
    elseif KRNL_LOADED then
        ExecutorSupport.Executor = "KRNL"
    elseif syn then
        ExecutorSupport.Executor = "Synapse X"
    elseif SENTINEL_LOADED then
        ExecutorSupport.Executor = "Sentinel"
    elseif getexecutorname then
        ExecutorSupport.Executor = getexecutorname()
    end
end)
pcall(function()
    ExecutorSupport.Mobile = UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled
end)
getgenv().SwimMethod = false
getgenv().TeleportSettings = { Speed = 0.25 }
getgenv().auraenabled = false
getgenv().killaurahigh = false
getgenv().rainbowbeam = false
getgenv().hitpart = "Head"
getgenv().damage = 100
getgenv().cooldown = 0
getgenv().beamcolor = Color3.fromRGB(0, 200, 80)
Config = Config or {}
Config.TheBronx = { carfly = false, carflyspeed = 120 }
_G.respawn = false
local staminaEnabled = false
local hungerEnabled = false
local sleepEnabled = false
local AntiLoseEnabled = false
local Noclipping = nil
local flyEnabled = false
local guiEnabled = true
local enhancedWalk = false
local speed = 16
local hitboxextender = false
local Size = 4
local Transparency = 0.85
local HitboxColor = Color3.fromRGB(255, 0, 0)
local SelectedPlayer = nil
local rainbowHitbox = false
local nametagEnabled = true
local animation = Instance.new("Animation")
animation.AnimationId = "rbxassetid://78828590676720"
local bodyGyro, movementConnection, freezeConnection, animationTrack
local hum, seat, car, root, bv, bg, lastCar
local target1 = nil
task.spawn(function()
    while task.wait() do
        if getgenv().SwimMethod then
            local p = Players.LocalPlayer
            if p and p.Character and p.Character:FindFirstChild("Humanoid") then
                p.Character.Humanoid:ChangeState(Enum.HumanoidStateType.FallingDown)
            end
        end
    end
end)
local locations = {
    ["🏦 Bank"] = Vector3.new(-1216.5316162109375, 253.8797607421875, -3636.446044921875),
    ["💵 Money Wash"] = Vector3.new(-977.1771, 253.6838, -692.5855),
    ["💰 Pawn Shop"] = Vector3.new(-1049.6431, 253.5367, -814.2697),
    ["🔐 Bank Vault"] = Vector3.new(-217.568359375, 373.7984924316406, -1216.20947265625),
    ["🔫 GunShop 1"] = Vector3.new(92994.6640625, 122098.5078125, 17225.943359375),
    ["🔫 GunShop 2"] = Vector3.new(66195.4453125, 123615.7109375, 5750.28271484375),
    ["🔫 GunShop Lobby"] = Vector3.new(-224.3818359375, 283.8034362792969, -794.7174072265625),
    ["🔫 GunShop 3"] = Vector3.new(60820.3086, 87609.1484, -351.4746),
    ["🏢 Pent House"] = Vector3.new(-1482.804443359375, 463.39385986328125, -3690.70751953125),
    ["🏠 Mini Mansion"] = Vector3.new(-791.5180053710938, 256.7944641113281, 1414.4248046875),
    ["🎒 Backpack Shop"] = Vector3.new(-692.4142456054688, 253.78091430664062, -681.0672607421875),
    ["💎 Frozen Shop"] = Vector3.new(-216.31436157226562, 284.031494140625, -1169.032470703125),
    ["👕 Drip Store"] = Vector3.new(67462, 10489.21484375, 546.1941528320312),
    ["🍗 Chicken Wings"] = Vector3.new(-957.9142, 253.5367, -815.9442),
    ["🚗 Car Dealer"] = Vector3.new(-401.99371337890625, 253.4141082763672, -1248.8380126953125),
    ["🐍 Exotic Dealer"] = Vector3.new(-1523.5654296875, 273.9729919433594, -990.6575317382812),
    ["🚧 Construction"] = Vector3.new(-1731.8307, 370.8123, -1176.8387),
    ["🚔 Prison"] = Vector3.new(-1135.0464, 254.7160, -3330.9954),
    ["🏥 Hospital"] = Vector3.new(-1589.504150390625, 254.27223205566406, 17.6555233001709),
    ["🏧 ATM 1"] = Vector3.new(-1011.9066162109375, 253.7509002685547, -1153.7340087890734),
    ["🏧 ATM 2"] = Vector3.new(-739.9456176757812, 287.12518310546875, -793.5716552734375),
    ["🏕️ TrailerPark"] = Vector3.new(-1522.76904296875, 253.16094970703125, 2344.95947265625),
    ["🍳 Cook Spot"] = Vector3.new(-741.1889038085938, 262.9556579589844, -955.7835083007812),
    ["🎨 Tattoo Shop"] = Vector3.new(-659.76806640625, 254.13262939453125, -461.2218322753906),
    ["⛽ Gas Station"] = Vector3.new(-1412.353759765625, 254.7757110595703, 2892.250048828125),
    ["💵 Dollar General"] = Vector3.new(-388.8291931152344, 253.8165283203125, -1036.4705810546875),
    ["🛒 Bronx Market"] = Vector3.new(-428.1142578125, 334.32501220703125, -581.2235107421875),
    ["🍟 McDonalds"] = Vector3.new(-1011.2984619140625, 253.9326629638672, -1147.4130859375),
    ["⚔️ Striker Man"] = Vector3.new(-1427.686767578125, 254.2161865234375, 2777.208740234375),
    ["🌸 Sell Seeds"] = Vector3.new(-1419.4013671875, 253.28067016601562, 2034.50341796875),
    ["🌿 Grow Seeds"] = Vector3.new(-935.8598022460938, 267.469482421875, -1132.88818359375),
    ["🌱 Buy Seeds"] = Vector3.new(51371.56640625, 21680.416015625, 21681.03759765625),
    ["🏚️ Basement"] = Vector3.new(-194.34603881835938, 239.5054168701172, 1238.91845703125),
    ["🏀 Court"] = Vector3.new(-1722.821533203125, 236.94708251953125, -589.066650390625),
}
local outfits = {
    ["Blue Spider"] = {
        Hats = {"MRHoodieBRR"},
        Shirts = {"Blue Sp5der Hoodie"},
        Pants = {"Blue Sp5der Sweats"},
        Shiestys = {"Shiesty"},
        Masks = {}
    },
    ["Spider Man"] = {
        Hats = {},
        Shirts = {"Spiderman"},
        Pants = {"Spiderman"},
        Shiestys = {"RedShiesty"},
        Masks = {}
    },
    ["Blood Clown"] = {
        Hats = {},
        Shirts = {"Red B Jacket"},
        Pants = {"Red B Shorts"},
        Shiestys = {},
        Masks = {"MRCLOWN MAN"}
    },
    ["Crip Clown"] = {
        Hats = {},
        Shirts = {"Blu C Amiri Hoodie"},
        Pants = {"Blu B Shorts"},
        Shiestys = {},
        Masks = {"MRCLOWN MAN"}
    },
    ["Red Spider"] = {
        Hats = {"MRHoodieBRR"},
        Shirts = {"Red Sp5der Sweats"},
        Pants = {"Red Sp5der Sweats"},
        Shiestys = {"Shiesty"},
        Masks = {}
    },
}
local ExemptItems = {"Phone", "Fist", "Shiesty", "Bandage", "Lemonade", "Car keys"}
local function Notify(title, text, duration)
    pcall(function()
        StarterGui:SetCore("SendNotification", {
            Title = title,
            Text = text,
            Duration = duration or 3
        })
    end)
end
local function enableSwimMethod()
    getgenv().SwimMethod = true
end
local function disableSwimMethod()
    getgenv().SwimMethod = false
end
local function findProximityPromptRecursive(obj)
    if not obj then return nil end
    if obj:IsA("ProximityPrompt") then return obj end
    for _, child in ipairs(obj:GetChildren()) do
        local p = findProximityPromptRecursive(child)
        if p then return p end
    end
    return nil
end
local function BypassTp(destinationCFrame)
    local character = LocalPlayer.Character
    if not character or not character:FindFirstChild("HumanoidRootPart") then return end
    local hrp = character.HumanoidRootPart
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    enableSwimMethod()
    if humanoid then pcall(function() humanoid:ChangeState(Enum.HumanoidStateType.FallingDown) end) end
    task.wait(0.7)
    local n = 0
    repeat task.wait(0.05); n = n + 1 until not LocalPlayer:GetAttribute("LastACPos") or n > 10
    pcall(function()
        hrp.Velocity = Vector3.zero
        hrp.AssemblyLinearVelocity = Vector3.zero
        hrp.AssemblyAngularVelocity = Vector3.zero
    end)
    local off = Vector3.new(math.random(-1,1), 0, math.random(-1,1))
    if typeof(destinationCFrame) == "CFrame" then hrp.CFrame = destinationCFrame + off
    elseif typeof(destinationCFrame) == "Vector3" then hrp.CFrame = CFrame.new(destinationCFrame) + off end
    task.delay(0.3, disableSwimMethod)
end

getgenv().antiFling = false
getgenv()._antiFlingLastSafePos = nil
task.spawn(function()
    while true do task.wait(0.06)
        if getgenv().antiFling then
            local c = LocalPlayer.Character; if not c then continue end
            local hrp = c:FindFirstChild("HumanoidRootPart")
            local hum = c:FindFirstChildOfClass("Humanoid")
            if not hrp or not hum then continue end
            if hum.FloorMaterial ~= Enum.Material.Air then
                getgenv()._antiFlingLastSafePos = hrp.CFrame
            end
            local vel = hrp.AssemblyLinearVelocity
            if vel.Magnitude > 120 then
                hrp.AssemblyLinearVelocity = Vector3.zero
                for _,v in pairs(c:GetDescendants()) do
                    if v:IsA("BodyVelocity") or v:IsA("LinearVelocity") or v:IsA("VectorForce") or v:IsA("BodyForce") then
                        pcall(function() v:Destroy() end)
                    end
                end
                task.wait(0.1)
                local dest = getgenv()._antiFlingLastSafePos
                if dest then
                    task.spawn(function() pcall(function() BypassTp(dest) end) end)
                else
                    hrp.AssemblyLinearVelocity = Vector3.zero
                end
            end
        end
    end
end)

local function applyEffects()
    local char = LocalPlayer.Character
    if not char then return end
    if staminaEnabled then
        pcall(function()
            local staminaScript = LocalPlayer.PlayerGui:FindFirstChild("Run", true)
            if staminaScript then
                local scriptObj = staminaScript:FindFirstChild("StaminaBarScript", true)
                if scriptObj then scriptObj:Destroy() end
            end
        end)
    end
    if hungerEnabled then
        pcall(function()
            local hungerScript = LocalPlayer.PlayerGui:FindFirstChild("Hunger", true)
            if hungerScript then
                local scriptObj = hungerScript:FindFirstChild("HungerBarScript", true)
                if scriptObj then scriptObj:Destroy() end
            end
        end)
    end
    if sleepEnabled then
        pcall(function()
            local s = LocalPlayer.PlayerGui.SleepGui.Frame.sleep.SleepBar.sleepScript
            s.Disabled = true
            s.Disabled = false
            s.Disabled = true
        end)
    end
end
local function setCollide(state)
    local char = LocalPlayer.Character
    if char then
        for _, p in pairs(char:GetDescendants()) do
            if p:IsA("BasePart") then p.CanCollide = state end
        end
    end
end
local function equipOutfitItem(category, itemName)
    pcall(function() ReplicatedStorage.ClothShopRemote:FireServer("Buy", category, itemName) end)
    task.wait(0.3)
    pcall(function() ReplicatedStorage.ClothShopRemote:FireServer("Wear", category, itemName) end)
    task.wait(0.2)
end
local function equipOutfit(outfitName)
    local outfit = outfits[outfitName]
    if not outfit then Notify("Outfit","Outfit not found!",3) return end
    pcall(function() ReplicatedStorage.ClothShopRemote:FireServer("Reset Data") end)
    task.wait(0.3)
    Notify("Outfit","Changing to "..outfitName.."...",2)
    for _, hatName in ipairs(outfit.Hats or {}) do equipOutfitItem("Hats", hatName) end
    for _, shirtName in ipairs(outfit.Shirts or {}) do equipOutfitItem("Shirts", shirtName) end
    for _, pantsName in ipairs(outfit.Pants or {}) do equipOutfitItem("Pants", pantsName) end
    for _, shiesty in ipairs(outfit.Shiestys or {}) do equipOutfitItem("Shiestys", shiesty) end
    for _, mask in ipairs(outfit.Masks or {}) do equipOutfitItem("Masks", mask) end
    Notify("Outfit","Equipped: "..outfitName,3)
end
function dmg(target, hpart, damage)
    pcall(function()
        local tool = LocalPlayer.Character:FindFirstChildWhichIsA("Tool")
        if not tool then return end
        local targetPart = target.Character[hpart]
        local hitpos = targetPart.Position
        ReplicatedStorage.InflictTarget:FireServer(
            tool,
            LocalPlayer,
            target.Character.Humanoid,
            targetPart,
            damage,
            {0, 0, false, false,
                tool.GunScript_Server.IgniteScript,
                tool.GunScript_Server.IcifyScript,
                100, 100},
            {false, 5, 3},
            targetPart,
            {false, {1930359546}, 1, 1.5, 1},
            hitpos,
            Vector3.new(0.07, -0.1, -0.99),
            true
        )
    end)
end

function KillGunMod(target,hpart,damage)
    local tool=checkgun(); if not tool then return end
    local tc=target and target.Character; if not tc then return end
    local hum=tc:FindFirstChildWhichIsA("Humanoid"); if not hum then return end
    local head=tc:FindFirstChild(hpart or "Head") or tc:FindFirstChild("HumanoidRootPart"); if not head then return end
    if not damage or damage==math.huge then
        local sd; pcall(function() local st=tool:FindFirstChild("Setting"); if st then local s=require(st); if s then sd=tonumber(s.Damage) or tonumber(s.BaseDamage) end end end)
        damage = sd or 200
    end
    local handle=tool:FindFirstChild("Handle"); if not handle then return end
    local gsl=tool:FindFirstChild("GunScript_Local")
    local gss=tool:FindFirstChild("GunScript_Server")
    local fp=handle:FindFirstChild("GunFirePoint") or handle
    local origin=fp.Position
    local dir=(head.Position-origin); dir=dir.Magnitude>0 and dir.Unit or Vector3.new(0,0,-1)
    local infOrigin=head.Position - dir*3
    local ig=gss and gss:FindFirstChild("IgniteScript")
    local ic=gss and gss:FindFirstChild("IcifyScript")
    pcall(function()
        local setting=tool:FindFirstChild("Setting")
        if setting then local s=require(setting); if s then s.LimitedAmmoEnabled=false; s.Ammo=10000; s.AmmoPerMag=10000; s.MagCount=10000; s.StoredAmmo=10000; s.MaxAmmo=10000 end end
    end)
    pcall(function() ReplicatedStorage.VisualizeMuzzle:FireServer(handle,true,{false,7,Color3.new(1,1.1098,0),15,true,0.02}, gsl and gsl:FindFirstChild("MuzzleEffect")) end)
    pcall(function() ReplicatedStorage.VisualizeBullet:FireServer(
        tool, handle, dir, fp,
        {true,{112139677907598,92977228204408,112139677907598,92977228204408},1,1,3.5, gsl and gsl:FindFirstChild("HitEffect"), true},
        {true,{0,0,0,0,0,0},1,1,1, gsl and gsl:FindFirstChild("BloodEffect")},
        {true,0.2,{3696144972},true,7,1},
        {false,8,true,{163064102},1,1.5,1,false, gsl and gsl:FindFirstChild("ExplosionEffect")},
        {false,Vector3.new(0.1,0,0),Vector3.new(-0.1,0,0), gsl and gsl:FindFirstChild("TracerEffect"), nil, gsl and gsl:FindFirstChild("ParticleEffect"),300,500,0,Vector3.zero,Vector3.new(0.4,0.4,0.4),Color3.new(0.639,0.635,0.611),1,Enum.Material.Neon,Enum.PartType.Cylinder,false,6696543809,0,Vector3.new(0.007,0.007,0.007)},
        {true,{269514869,269514887,269514807,269514817},0.5,1,1.5,100},
        {false,3,Color3.new(1,0.647,0.6),6,true}
    ) end)
    pcall(function() ReplicatedStorage.InflictTarget:FireServer(
        tool, LocalPlayer, hum, head, damage,
        {0,0,false,false,ig,ic,100,100},
        {false,5,3}, head,
        {false,{1930359546},1,1.5,1},
        infOrigin, dir
    ) end)
end

function wsSlimeKill(p)
    if not p or not p.Character then return end
    local th = p.Character:FindFirstChild("HumanoidRootPart")
    local myChar = LocalPlayer.Character
    local hrp = myChar and myChar:FindFirstChild("HumanoidRootPart")
    if not th or not hrp then return end
    checkgun()
    local original = hrp.CFrame
    pcall(function() hrp.CFrame = th.CFrame end)
    pcall(function() hrp.Anchored = true end)
    task.wait(0.07)
    pcall(function() KillGunMod(p, "Head", math.huge) end)
    task.wait(0.07)
    pcall(function() KillGunMod(p, "Head", math.huge) end)
    task.wait(0.18)
    pcall(function() KillGunMod(p, "Head", math.huge) end)
    task.wait(0.1)
    pcall(function() hrp.Anchored = false end)
    local h2 = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if h2 and original then pcall(function() h2.CFrame = original end) end
end

function hasGunInHand()
    local char=LocalPlayer.Character; if not char then return false end
    for _,v in pairs(char:GetChildren()) do
        if v:IsA("Tool") and (v:FindFirstChild("GunScript_Local") or v:FindFirstChild("GunScript_Server")) then return true end
    end
    return false
end

function BigGunNotify(mode)
    pcall(function()
        local blocked  = (mode ~= "ammo")
        local WAL_BLUE = Color3.fromRGB(0,113,220)
        local SPARK    = Color3.fromRGB(255,194,32)
        local headCol  = blocked and Color3.fromRGB(255,99,99) or Color3.fromRGB(244,246,255)
        local headTxt, bodyTxt
        if mode == "ammo" then
            headTxt = "No ammo? Just shoot the gun"
            bodyTxt = "If it says no ammo left, just shoot the gun once and it'll work again."
        elseif mode == "noknife" then
            headTxt = "Needs a knife -- go grab one!"
            bodyTxt = "Equip a knife first (Kitchen Knife, Cleaver, Axe, Machete...)."
        else
            headTxt = "Needs a gun -- go get ur pipe dumbass"
            bodyTxt = "This won't do anything until you've got a gun in your hand."
        end
        local parent = (gethui and gethui()) or game:GetService("CoreGui")
        local old = parent:FindFirstChild("_GunWarnGui"); if old then old:Destroy() end
        local TS = game:GetService("TweenService")
        local gui = Instance.new("ScreenGui")
        gui.Name = "_GunWarnGui"; gui.ResetOnSpawn = false; gui.IgnoreGuiInset = true; gui.DisplayOrder = 99999
        gui.Parent = parent
        local card = Instance.new("Frame")
        card.AnchorPoint = Vector2.new(0.5,0)
        card.Position = UDim2.new(0.5,0,0,-150)
        card.Size = UDim2.new(0,470,0,104)
        card.BackgroundColor3 = Color3.fromRGB(16,20,30); card.BackgroundTransparency = 0.03
        card.BorderSizePixel = 0; card.Parent = gui
        Instance.new("UICorner",card).CornerRadius = UDim.new(0,18)
        local grad = Instance.new("UIGradient")
        grad.Color = ColorSequence.new({ColorSequenceKeypoint.new(0,Color3.fromRGB(22,28,42)),ColorSequenceKeypoint.new(1,Color3.fromRGB(13,16,24))}); grad.Rotation = 90; grad.Parent = card
        local stroke = Instance.new("UIStroke"); stroke.Color = WAL_BLUE; stroke.Thickness = 1; stroke.Transparency = 0.45; stroke.Parent = card
        local accent = Instance.new("Frame")
        accent.Size = UDim2.new(0,4,1,-26); accent.Position = UDim2.fromOffset(0,13)
        accent.BackgroundColor3 = blocked and Color3.fromRGB(232,66,66) or WAL_BLUE; accent.BorderSizePixel = 0; accent.Parent = card
        Instance.new("UICorner",accent).CornerRadius = UDim.new(1,0)
        local badge = Instance.new("Frame")
        badge.Position = UDim2.fromOffset(16,16); badge.Size = UDim2.fromOffset(40,40)
        badge.BackgroundColor3 = WAL_BLUE; badge.BorderSizePixel = 0; badge.Parent = card
        Instance.new("UICorner",badge).CornerRadius = UDim.new(0,11)
        local bgrad = Instance.new("UIGradient")
        bgrad.Color = ColorSequence.new({ColorSequenceKeypoint.new(0,Color3.fromRGB(0,200,80)),ColorSequenceKeypoint.new(1,WAL_BLUE)}); bgrad.Rotation = 130; bgrad.Parent = badge
        local bl = Instance.new("TextLabel"); bl.Size = UDim2.fromScale(1,1); bl.BackgroundTransparency = 1
        bl.Font = Enum.Font.GothamBlack; bl.TextSize = 19; bl.TextColor3 = SPARK; bl.Text = "J"; bl.Parent = badge
        local title = Instance.new("TextLabel")
        title.Position = UDim2.fromOffset(66,16); title.Size = UDim2.new(1,-130,0,15)
        title.BackgroundTransparency = 1; title.Font = Enum.Font.GothamBold; title.TextSize = 13
        title.TextColor3 = Color3.fromRGB(228,234,246); title.TextXAlignment = Enum.TextXAlignment.Left
        title.Text = "Jointhub.gg"; title.Parent = card
        local tm = Instance.new("TextLabel")
        tm.Position = UDim2.new(1,-58,0,16); tm.Size = UDim2.fromOffset(46,15)
        tm.BackgroundTransparency = 1; tm.Font = Enum.Font.Gotham; tm.TextSize = 10.5
        tm.TextColor3 = Color3.fromRGB(120,134,160); tm.TextXAlignment = Enum.TextXAlignment.Right
        tm.Text = "now"; tm.Parent = card
        local l1 = Instance.new("TextLabel")
        l1.Position = UDim2.fromOffset(66,35); l1.Size = UDim2.new(1,-82,0,20)
        l1.BackgroundTransparency = 1; l1.Font = Enum.Font.GothamBold; l1.TextSize = 14.5
        l1.TextColor3 = headCol; l1.TextXAlignment = Enum.TextXAlignment.Left
        l1.TextTruncate = Enum.TextTruncate.AtEnd; l1.Text = headTxt; l1.Parent = card
        local l2 = Instance.new("TextLabel")
        l2.Position = UDim2.fromOffset(66,56); l2.Size = UDim2.new(1,-82,0,40)
        l2.BackgroundTransparency = 1; l2.Font = Enum.Font.Gotham; l2.TextSize = 12.5
        l2.TextColor3 = Color3.fromRGB(140,152,176); l2.TextXAlignment = Enum.TextXAlignment.Left
        l2.TextYAlignment = Enum.TextYAlignment.Top; l2.TextWrapped = true; l2.Text = bodyTxt; l2.Parent = card
        local TI_IN = TweenInfo.new(0.42, Enum.EasingStyle.Back, Enum.EasingDirection.Out)
        local TI_OUT = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
        TS:Create(card, TI_IN, {Position = UDim2.new(0.5,0,0,18)}):Play()
        task.delay(5, function()
            pcall(function() TS:Create(card, TI_OUT, {Position = UDim2.new(0.5,0,0,-150)}):Play() end)
            task.delay(0.4, function() pcall(function() gui:Destroy() end) end)
        end)
    end)
end
function checkgun()
    local player = game.Players.LocalPlayer
    local gunTool = nil
    for _, v in pairs(player.Backpack:GetDescendants()) do
        if v:IsA("LocalScript") and v.Name == "GunScript_Local" then
            gunTool = v.Parent
            break
        end
    end
    if not gunTool and player.Character then
        for _, v in pairs(player.Character:GetDescendants()) do
            if v:IsA("LocalScript") and v.Name == "GunScript_Local" then
                gunTool = v.Parent
                break
            end
        end
    end
    if gunTool and gunTool:IsA("Tool") then
        player.Character:WaitForChild("Humanoid"):EquipTool(gunTool)
    end
    return gunTool
end
function GetGunSettings()
    local char = LocalPlayer.Character
    local tool = char and char:FindFirstChildOfClass("Tool")
    if not tool or not tool:FindFirstChild("Setting") then return nil, nil end
    return require(tool.Setting), tool
end
local _nativeFPP = fireproximityprompt
local function fireproximityprompt(prompt)
    if not (prompt and prompt:IsA("ProximityPrompt")) then return end

    if _nativeFPP then
        if pcall(_nativeFPP, prompt, 1) then return end
        if pcall(_nativeFPP, prompt) then return end
    end

    pcall(function()
        local oldHold, oldDist, oldLoS = prompt.HoldDuration, prompt.MaxActivationDistance, prompt.RequiresLineOfSight
        prompt.HoldDuration = 0
        prompt.MaxActivationDistance = math.max(oldDist, 1000)
        prompt.RequiresLineOfSight = false
        prompt:InputHoldBegin()
        task.wait()
        prompt:InputHoldEnd()
        prompt.MaxActivationDistance = oldDist
        prompt.HoldDuration = oldHold
        prompt.RequiresLineOfSight = oldLoS
    end)
end
local allowedKnifeTools = {
    ["Kitchen Knife"] = true,
    ["ButterflyKnife"] = true,
    ["Melee"] = true,
    Cleaver = true,
    Axe = true,
    Blade = true,
    Machete = true
}
local function GetAttackEvent(tool)
    if tool and tool:FindFirstChild("MeleeSystem") then
        return tool.MeleeSystem:FindFirstChild("AttackEvent")
    end
    return nil
end
local function getcp()
    local mouse = LocalPlayer:GetMouse()
    local closest, dist = nil, math.huge
    for _, v in pairs(Players:GetPlayers()) do
        if v ~= LocalPlayer and v.Character and v.Character:FindFirstChild("Head") then
            local pos, onScreen = workspace.CurrentCamera:WorldToScreenPoint(v.Character.Head.Position)
            if onScreen then
                local d = (Vector2.new(pos.X, pos.Y) - Vector2.new(mouse.X, mouse.Y)).Magnitude
                if d < dist then dist = d; closest = v end
            end
        end
    end
    return closest
end
RunService.RenderStepped:Connect(function()
    target1 = getcp()
end)
local function MarketHasItem(toolName)
    local market = ReplicatedStorage:FindFirstChild("MarketItems")
    if not market then return false end
    for _, item in ipairs(market:GetChildren()) do
        if item.Name == toolName and item:FindFirstChild("owner") and item.owner.Value == LocalPlayer.Name then
            return true
        end
    end
    return false
end
local function BackpackHasItem(toolName)
    for _, tool in ipairs(LocalPlayer.Backpack:GetChildren()) do
        if tool:IsA("Tool") and tool.Name == toolName then return true end
    end
    return false
end
local function ForcePutToMarket(toolName)
    local endTime = os.clock() + 12
    while os.clock() < endTime do
        if MarketHasItem(toolName) then return true end
        pcall(function() ReplicatedStorage.ListWeaponRemote:FireServer(toolName, 999999) end)
        task.wait(0.15)
    end
    return false
end
local function ForceRetrieveFromMarket(toolName)
    local market = ReplicatedStorage:WaitForChild("MarketItems", 10)
    if not market then return false end
    local endTime = os.clock() + 12
    while os.clock() < endTime do
        for _, item in ipairs(market:GetChildren()) do
            if item.Name == toolName and item:FindFirstChild("owner") and item.owner.Value == LocalPlayer.Name and item:GetAttribute("SpecialId") then
                local special = item:GetAttribute("SpecialId")
                pcall(function() ReplicatedStorage.BuyItemRemote:FireServer(toolName, "Remove", special) end)
                task.wait(0.2)
                pcall(function() ReplicatedStorage.BackpackRemote:InvokeServer("Grab", toolName) end)
                task.wait(0.2)
                if BackpackHasItem(toolName) then return true end
            end
        end
        task.wait(0.3)
    end
    return false
end
local function CreateNametag(char)
    if not char then return end
    local head = char:WaitForChild("Head", 5)
    if not head then return end
    local old = head:FindFirstChild("JointhubTag")
    if old then old:Destroy() end
    local billboard = Instance.new("BillboardGui")
    billboard.Name = "JointhubTag"
    billboard.Adornee = head
    billboard.Size = UDim2.new(0, 200, 0, 50)
    billboard.StudsOffset = Vector3.new(0, 2.5, 0)
    billboard.AlwaysOnTop = true
    billboard.Parent = head
    local tag = Instance.new("TextLabel")
    tag.Size = UDim2.new(1, 0, 1, 0)
    tag.BackgroundTransparency = 1
    tag.Text = "Leaked By Jointhub.gg"
    tag.TextColor3 = Color3.fromRGB(255, 255, 0)
    tag.TextStrokeTransparency = 0.5
    tag.TextStrokeColor3 = Color3.new(0, 0, 0)
    tag.Font = Enum.Font.GothamBold
    tag.TextSize = 14
    tag.Parent = billboard
    task.spawn(function()
        while billboard and billboard.Parent do
            TweenService:Create(tag, TweenInfo.new(1), {TextColor3 = Color3.fromRGB(0, 200, 80)}):Play()
            task.wait(1)
            TweenService:Create(tag, TweenInfo.new(1), {TextColor3 = Color3.fromRGB(255, 255, 0)}):Play()
            task.wait(1)
        end
    end)
end
local LoadingScreen = Instance.new("ScreenGui")
LoadingScreen.Name = "JointhubLoading"
LoadingScreen.IgnoreGuiInset = true
LoadingScreen.DisplayOrder = 9999
LoadingScreen.Parent = CoreGui
local LoadingFrame = Instance.new("Frame")
LoadingFrame.Size = UDim2.new(1, 0, 1, 0)
LoadingFrame.BackgroundColor3 = Color3.fromRGB(8, 8, 12)
LoadingFrame.BackgroundTransparency = 1
LoadingFrame.BorderSizePixel = 0
LoadingFrame.Parent = LoadingScreen
TweenService:Create(LoadingFrame, TweenInfo.new(0.8, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {BackgroundTransparency = 0}):Play()
task.wait(0.8)
for i = 0, 30 do
    local stripe = Instance.new("Frame", LoadingFrame)
    stripe.Size = UDim2.new(1, 0, 0, 1)
    stripe.Position = UDim2.new(0, 0, 0, i * 25)
    stripe.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    stripe.BackgroundTransparency = 0.96
    stripe.BorderSizePixel = 0
end
local CenterBox = Instance.new("Frame", LoadingFrame)
CenterBox.Size = UDim2.new(0, 0, 0, 0)
CenterBox.AnchorPoint = Vector2.new(0.5, 0.5)
CenterBox.Position = UDim2.new(0.5, 0, 0.5, 0)
CenterBox.BackgroundColor3 = Color3.fromRGB(14, 14, 20)
CenterBox.BorderSizePixel = 0
CenterBox.ClipsDescendants = true
Instance.new("UICorner", CenterBox).CornerRadius = UDim.new(0, 10)
local cStroke = Instance.new("UIStroke", CenterBox)
cStroke.Color = Color3.fromRGB(0, 200, 80)
cStroke.Thickness = 1.5
cStroke.Transparency = 1
task.delay(0.1, function()
    TweenService:Create(CenterBox, TweenInfo.new(0.7, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {Size = UDim2.new(0, 280, 0, 140)}):Play()
    TweenService:Create(cStroke, TweenInfo.new(1, Enum.EasingStyle.Sine), {Transparency = 0.3}):Play()
end)
task.spawn(function()
    task.wait(1)
    while CenterBox and CenterBox.Parent do
        TweenService:Create(cStroke, TweenInfo.new(1.2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Transparency = 0.1}):Play()
        task.wait(1.2)
        TweenService:Create(cStroke, TweenInfo.new(1.2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Transparency = 0.6}):Play()
        task.wait(1.2)
    end
end)
local Title = Instance.new("TextLabel", CenterBox)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Position = UDim2.new(0, 0, 0, 15)
Title.BackgroundTransparency = 1
Title.Text = "LEAKED BY JOINTHUB.GG"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextTransparency = 1
Title.TextSize = 28
Title.Font = Enum.Font.GothamBlack
Title.TextXAlignment = Enum.TextXAlignment.Center
local TitleStroke = Instance.new("UIStroke", Title)
TitleStroke.Color = Color3.fromRGB(0, 140, 56)
TitleStroke.Thickness = 1
TitleStroke.Transparency = 1
task.delay(0.6, function()
    TweenService:Create(Title, TweenInfo.new(0.5, Enum.EasingStyle.Quint), {TextTransparency = 0}):Play()
    TweenService:Create(TitleStroke, TweenInfo.new(0.5, Enum.EasingStyle.Quint), {Transparency = 0}):Play()
end)
local DotHolder = Instance.new("Frame", CenterBox)
DotHolder.Size = UDim2.new(0, 60, 0, 12)
DotHolder.AnchorPoint = Vector2.new(0.5, 0)
DotHolder.Position = UDim2.new(0.5, 0, 0, 68)
DotHolder.BackgroundTransparency = 1
local ldots = {}
for i = 1, 3 do
    local dot = Instance.new("Frame", DotHolder)
    dot.Size = UDim2.new(0, 8, 0, 8)
    dot.Position = UDim2.new(0, (i - 1) * 22 + 4, 0, 2)
    dot.BackgroundColor3 = Color3.fromRGB(0, 200, 80)
    dot.BackgroundTransparency = 1
    dot.BorderSizePixel = 0
    Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)
    ldots[i] = dot
end
task.delay(0.8, function()
    for _, d in ipairs(ldots) do TweenService:Create(d, TweenInfo.new(0.3), {BackgroundTransparency = 0}):Play() end
end)
task.spawn(function()
    task.wait(0.9)
    while CenterBox and CenterBox.Parent do
        for i, dot in ipairs(ldots) do
            TweenService:Create(dot, TweenInfo.new(0.25, Enum.EasingStyle.Quint, Enum.EasingDirection.Out), {
                Position = UDim2.new(0, (i - 1) * 22 + 4, 0, -5),
                BackgroundColor3 = Color3.fromRGB(120, 255, 170)
            }):Play()
            task.wait(0.12)
            TweenService:Create(dot, TweenInfo.new(0.25, Enum.EasingStyle.Quint, Enum.EasingDirection.In), {
                Position = UDim2.new(0, (i - 1) * 22 + 4, 0, 2),
                BackgroundColor3 = Color3.fromRGB(0, 200, 80)
            }):Play()
        end
        task.wait(0.4)
    end
end)
local StatusText = Instance.new("TextLabel", CenterBox)
StatusText.Size = UDim2.new(1, 0, 0, 20)
StatusText.Position = UDim2.new(0, 0, 0, 90)
StatusText.BackgroundTransparency = 1
StatusText.Text = "Starting up..."
StatusText.TextColor3 = Color3.fromRGB(120, 120, 140)
StatusText.TextTransparency = 1
StatusText.TextSize = 11
StatusText.Font = Enum.Font.Gotham
task.delay(0.7, function()
    TweenService:Create(StatusText, TweenInfo.new(0.4), {TextTransparency = 0}):Play()
end)
local VerTag = Instance.new("TextLabel", CenterBox)
VerTag.Size = UDim2.new(1, 0, 0, 14)
VerTag.Position = UDim2.new(0, 0, 1, -16)
VerTag.BackgroundTransparency = 1
VerTag.Text = "v3.0"
VerTag.TextColor3 = Color3.fromRGB(60, 60, 80)
VerTag.TextTransparency = 1
VerTag.TextSize = 9
VerTag.Font = Enum.Font.Gotham
task.delay(0.8, function() TweenService:Create(VerTag, TweenInfo.new(0.4), {TextTransparency = 0}):Play() end)
local loadingSteps = {
    {text = "Starting up...", wait = 0.5},
    {text = "Hooking remotes...", wait = 0.5},
    {text = "Building UI...", wait = 0.5},
    {text = "Ready", wait = 0.4},
}
task.spawn(function()
    task.wait(0.8)
    for _, step in ipairs(loadingSteps) do
        TweenService:Create(StatusText, TweenInfo.new(0.15), {TextTransparency = 0.6}):Play()
        task.wait(0.15)
        StatusText.Text = step.text
        TweenService:Create(StatusText, TweenInfo.new(0.15), {TextTransparency = 0}):Play()
        task.wait(step.wait)
    end
    task.wait(0.3)
    TweenService:Create(Title, TweenInfo.new(0.5, Enum.EasingStyle.Sine), {TextTransparency = 1}):Play()
    TweenService:Create(TitleStroke, TweenInfo.new(0.5, Enum.EasingStyle.Sine), {Transparency = 1}):Play()
    TweenService:Create(StatusText, TweenInfo.new(0.5, Enum.EasingStyle.Sine), {TextTransparency = 1}):Play()
    TweenService:Create(VerTag, TweenInfo.new(0.5, Enum.EasingStyle.Sine), {TextTransparency = 1}):Play()
    for _, d in ipairs(ldots) do TweenService:Create(d, TweenInfo.new(0.4, Enum.EasingStyle.Sine), {BackgroundTransparency = 1}):Play() end
    task.wait(0.5)
    TweenService:Create(CenterBox, TweenInfo.new(0.5, Enum.EasingStyle.Sine, Enum.EasingDirection.In), {
        Size = UDim2.new(0, 0, 0, 0)
    }):Play()
    TweenService:Create(cStroke, TweenInfo.new(0.5, Enum.EasingStyle.Sine), {Transparency = 1}):Play()
    task.wait(0.5)
    TweenService:Create(LoadingFrame, TweenInfo.new(0.8, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
        BackgroundTransparency = 1
    }):Play()
    task.wait(0.9)
    LoadingScreen:Destroy()
end)
local Colors = {
    Accent = Color3.fromRGB(0, 200, 80),
    AccentDark = Color3.fromRGB(0, 140, 56),
    Background = Color3.fromRGB(15, 15, 20),
    Surface = Color3.fromRGB(25, 25, 35),
    Text = Color3.fromRGB(255, 255, 255),
    TextDim = Color3.fromRGB(150, 150, 160),
    Success = Color3.fromRGB(0, 200, 100),
    Error = Color3.fromRGB(255, 80, 80),
}

local ScreenGui, MainFrame, MainStroke, UI
local currentWidth, currentHeight
do
    local Logos = { 123096869233289, 86424706707673, 111702201685111 }
    local T = {
        Accent = Color3.fromRGB(0,190,80), AccentDim = Color3.fromRGB(0,130,55), Spark = Color3.fromRGB(120,255,170),
        Bg = Color3.fromRGB(11,14,21), Panel = Color3.fromRGB(16,20,30), Element = Color3.fromRGB(24,30,44),
        Hi = Color3.fromRGB(237,241,247), Stroke = Color3.fromRGB(34,44,64), Text = Color3.fromRGB(234,239,246),
        Sub = Color3.fromRGB(142,154,172), Dark = Color3.fromRGB(12,16,24), Off = Color3.fromRGB(235,72,72), On = Color3.fromRGB(70,215,120),
        Font = Enum.Font.Gotham, FontMed = Enum.Font.GothamMedium, FontBold = Enum.Font.GothamBold, FontTitle = Enum.Font.Bangers,
    }
    local function toHex(c) return string.format("%02X%02X%02X", math.floor(c.R*255+0.5), math.floor(c.G*255+0.5), math.floor(c.B*255+0.5)) end

    local function create(c, p, kids)
        local i = Instance.new(c)
        for k, v in pairs(p or {}) do i[k] = v end
        for _, ch in ipairs(kids or {}) do ch.Parent = i end
        return i
    end
    local function corner() return nil end
    local function stroke(o, col, t) return create("UIStroke", { Color = col or T.Stroke, Thickness = t or 1, Parent = o }) end
    local function tween(o, t, g) local tw = TweenService:Create(o, TweenInfo.new(t or 0.16, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), g) tw:Play() return tw end
    local function getParent()
        local ok, hui = pcall(function() return gethui and gethui() end)
        if ok and hui then return hui end
        local ok2, cg = pcall(function() return game:GetService("CoreGui") end)
        return ok2 and cg or LocalPlayer:WaitForChild("PlayerGui")
    end
    local function makeDraggable(frame, handle)
        local dragging, ds, sp
        handle.InputBegan:Connect(function(i)
            if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then
                dragging, ds, sp = true, i.Position, frame.Position
                i.Changed:Connect(function() if i.UserInputState == Enum.UserInputState.End then dragging = false end end)
            end
        end)
        UserInputService.InputChanged:Connect(function(i)
            if dragging and (i.UserInputType == Enum.UserInputType.MouseMovement or i.UserInputType == Enum.UserInputType.Touch) then
                local d = i.Position - ds
                frame.Position = UDim2.new(sp.X.Scale, sp.X.Offset + d.X, sp.Y.Scale, sp.Y.Offset + d.Y)
            end
        end)
    end
    local function safe(fn, ...) if typeof(fn) == "function" then local ok, e = pcall(fn, ...) if not ok then warn("[Jointhub]", e) end end end

    local ROWH, MENU_W, LIST_ROWS = 32, 340, 11
    local LIST_H = ROWH * LIST_ROWS
    local TOTAL_H = 78 + 28 + LIST_H + 28
    currentWidth, currentHeight = MENU_W, TOTAL_H

    local old = getParent():FindFirstChild("JointhubGui"); if old then old:Destroy() end
    ScreenGui = create("ScreenGui", { Name = "JointhubGui", ResetOnSpawn = false, ZIndexBehavior = Enum.ZIndexBehavior.Sibling, IgnoreGuiInset = true, DisplayOrder = 200, Parent = getParent() })

    local win = create("Frame", { Name = "Menu", Size = UDim2.fromOffset(MENU_W, TOTAL_H), Position = UDim2.fromOffset(70, 70),
        BackgroundColor3 = T.Bg, BackgroundTransparency = 0.28, BorderSizePixel = 0, ClipsDescendants = true, Parent = ScreenGui })
    MainFrame = win
    MainStroke = stroke(win, T.Stroke, 1)
    local sc = create("UIScale", { Scale = 0.93, Parent = win }) tween(sc, 0.24, { Scale = 1 })

    create("ImageLabel", { Name = "Bg", BackgroundTransparency = 1, Image = "rbxassetid://" .. Logos[1], ScaleType = Enum.ScaleType.Fit,
        ImageTransparency = 0.86, Size = UDim2.new(0.84, 0, 0.84, 0), Position = UDim2.new(0.08, 0, 0.08, 0), ZIndex = 0, Parent = win })

    local header = create("Frame", { Size = UDim2.new(1, 0, 0, 78), BackgroundColor3 = T.Panel, BackgroundTransparency = 0.22, BorderSizePixel = 0, Parent = win })
    local title = create("TextLabel", { BackgroundTransparency = 1, Text = "LEAKED BY JOINTHUB.GG", Font = T.FontTitle, TextSize = 32, TextColor3 = T.Text,
        TextXAlignment = Enum.TextXAlignment.Center, TextYAlignment = Enum.TextYAlignment.Bottom, Position = UDim2.new(0, 0, 0, 14), Size = UDim2.new(1, 0, 0, 34), Parent = header })
    create("UIGradient", { Color = ColorSequence.new{ ColorSequenceKeypoint.new(0, T.Accent), ColorSequenceKeypoint.new(0.55, T.Text), ColorSequenceKeypoint.new(1, T.Spark) }, Rotation = 6, Parent = title })
    create("TextLabel", { BackgroundTransparency = 1, Text = "M O D   M E N U", Font = T.FontBold, TextSize = 10, TextColor3 = T.Sub,
        TextXAlignment = Enum.TextXAlignment.Center, Position = UDim2.new(0, 0, 0, 52), Size = UDim2.new(1, 0, 0, 12), Parent = header })
    local hLine = create("Frame", { Size = UDim2.new(1, 0, 0, 2), Position = UDim2.new(0, 0, 1, -2), BackgroundColor3 = T.Accent, BorderSizePixel = 0, Parent = header })
    create("UIGradient", { Color = ColorSequence.new{ ColorSequenceKeypoint.new(0, T.Accent), ColorSequenceKeypoint.new(0.5, T.Spark), ColorSequenceKeypoint.new(1, T.Accent) }, Parent = hLine })

    local secBar = create("Frame", { Name = "Section", Size = UDim2.new(1, 0, 0, 28), Position = UDim2.new(0, 0, 0, 78), BackgroundColor3 = T.Accent, BackgroundTransparency = 0.12, BorderSizePixel = 0, Parent = win })
    local secLabel = create("TextLabel", { BackgroundTransparency = 1, Text = "MAIN", Font = T.FontTitle, TextSize = 17, TextColor3 = Color3.fromRGB(255,255,255),
        TextXAlignment = Enum.TextXAlignment.Left, Position = UDim2.new(0, 14, 0, 0), Size = UDim2.new(1, -60, 1, 0), Parent = secBar })
    local crumb = create("TextLabel", { BackgroundTransparency = 1, Text = "", Font = T.FontBold, TextSize = 12, TextColor3 = Color3.fromRGB(255,255,255),
        TextXAlignment = Enum.TextXAlignment.Right, Position = UDim2.new(1, -52, 0, 0), Size = UDim2.new(0, 40, 1, 0), Parent = secBar })

    local list = create("ScrollingFrame", { Name = "List", Active = true, BackgroundTransparency = 1, BorderSizePixel = 0,
        Size = UDim2.new(1, 0, 0, LIST_H), Position = UDim2.new(0, 0, 0, 106), CanvasSize = UDim2.new(0,0,0,0),
        ScrollBarThickness = 0, ScrollBarImageColor3 = T.Accent, ScrollBarImageTransparency = 0.4, Parent = win })

    local footer = create("Frame", { BackgroundColor3 = T.Panel, BackgroundTransparency = 0.22, Position = UDim2.new(0, 0, 1, -28), Size = UDim2.new(1, 0, 0, 28), BorderSizePixel = 0, Parent = win })
    local stat = create("TextLabel", { BackgroundTransparency = 1, Text = "fps", RichText = true, Font = T.Font, TextSize = 12, TextColor3 = T.Sub,
        TextXAlignment = Enum.TextXAlignment.Left, Position = UDim2.new(0, 12, 0, 0), Size = UDim2.new(0.6, 0, 1, 0), Parent = footer })
    local idxLbl = create("TextLabel", { BackgroundTransparency = 1, Text = "0 / 0", Font = T.FontBold, TextSize = 12, TextColor3 = T.Text,
        TextXAlignment = Enum.TextXAlignment.Right, Position = UDim2.new(0.4, 0, 0, 0), Size = UDim2.new(0.6, -12, 1, 0), Parent = footer })

    makeDraggable(win, header) makeDraggable(win, secBar) makeDraggable(win, win)

    do
        local frames, acc = 0, 0
        RunService.RenderStepped:Connect(function(dt)
            frames += 1 acc += dt
            if acc >= 1 then
                local fps = frames frames, acc = 0, 0
                local ping = 0 pcall(function() ping = math.floor(LocalPlayer:GetNetworkPing()*1000) end)
                local fc = (fps < 25 and T.Off) or (fps < 45 and T.Spark) or T.Accent
                local pc = (ping >= 150 and T.Off) or (ping >= 80 and T.Spark) or T.Accent
                stat.Text = string.format('<font color="#%s">%d fps</font>   <font color="#%s">%d ms</font>', toHex(fc), fps, toHex(pc), ping)
            end
        end)
    end

    local wm = create("Frame", { Name = "Toggle", Size = UDim2.new(0, 152, 0, 30), Position = UDim2.new(0.5, -76, 0, 14), BackgroundColor3 = T.Panel, BackgroundTransparency = 0.1, BorderSizePixel = 0, Parent = ScreenGui })
    stroke(wm, T.Stroke, 1)
    create("ImageLabel", { BackgroundTransparency = 1, Image = "rbxassetid://" .. Logos[2], Size = UDim2.new(0, 18, 0, 18), Position = UDim2.new(0, 9, 0.5, -9), Parent = wm })
    create("TextLabel", { BackgroundTransparency = 1, Text = "Jointhub.gg", Font = T.FontBold, TextSize = 13, TextColor3 = T.Text, TextXAlignment = Enum.TextXAlignment.Left, Position = UDim2.new(0, 34, 0, 0), Size = UDim2.new(1, -64, 1, 0), Parent = wm })
    local dotBtn = create("TextButton", { Text = "", AutoButtonColor = false, BackgroundColor3 = T.Element, Size = UDim2.new(0, 18, 0, 18), Position = UDim2.new(1, -26, 0.5, -9), Parent = wm })
    local dot = create("Frame", { BackgroundColor3 = T.Accent, Size = UDim2.new(0, 8, 0, 8), Position = UDim2.new(0.5, -4, 0.5, -4), BorderSizePixel = 0, Parent = dotBtn })
    dotBtn.MouseButton1Click:Connect(function() win.Visible = not win.Visible end)
    win:GetPropertyChangedSignal("Visible"):Connect(function() tween(dot, 0.15, { BackgroundColor3 = win.Visible and T.Accent or T.Sub }) end)
    do
        local wDrag, wStart, wPos, wMoved = false, nil, nil, false
        wm.InputBegan:Connect(function(i)
            if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then
                wDrag, wMoved, wStart, wPos = true, false, i.Position, wm.Position
            end
        end)
        UserInputService.InputChanged:Connect(function(i)
            if wDrag and (i.UserInputType == Enum.UserInputType.MouseMovement or i.UserInputType == Enum.UserInputType.Touch) then
                local d = i.Position - wStart
                if d.Magnitude > 4 then wMoved = true end
                wm.Position = UDim2.new(wPos.X.Scale, wPos.X.Offset + d.X, wPos.Y.Scale, wPos.Y.Offset + d.Y)
            end
        end)
        UserInputService.InputEnded:Connect(function(i)
            if (i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch) and wDrag then
                if not wMoved then win.Visible = not win.Visible end
                wDrag = false
            end
        end)
    end

    local ctrl = { index = 1, rows = {}, rowObjs = {} }
    local root = { Name = "JOINTHUB.GG", Items = {}, Parent = nil }
    ctrl.current = root
    local function sel(it) return it.type ~= "section" and it.type ~= "label" end

    local function buildRow(i, it)
        local y = (i - 1) * ROWH
        local btn = create("TextButton", { Text = "", AutoButtonColor = false, BackgroundTransparency = 1, Position = UDim2.new(0, 0, 0, y), Size = UDim2.new(1, 0, 0, ROWH), Parent = list })
        local hl = create("Frame", { BackgroundColor3 = T.Hi, BackgroundTransparency = 1, Position = UDim2.new(0,0,0,0), Size = UDim2.new(1,0,1,0), BorderSizePixel = 0, Parent = btn })
        local accent = create("Frame", { Size = UDim2.new(0,3,1,0), Position = UDim2.new(0,0,0,0), BackgroundColor3 = T.Accent, BorderSizePixel = 0, BackgroundTransparency = 1, Parent = btn })

        if it.type == "section" then
            create("TextLabel", { BackgroundTransparency = 1, Text = it.text, Font = T.FontBold, TextSize = 12, TextColor3 = T.Spark,
                TextXAlignment = Enum.TextXAlignment.Left, Position = UDim2.new(0, 12, 0, 0), Size = UDim2.new(1, -16, 1, 0), Parent = btn })
            return { setSel = function() end }
        end

        local lx, iconObj = 14, nil
        if it.icon then
            iconObj = create("ImageLabel", { BackgroundTransparency = 1, Image = "rbxassetid://" .. it.icon, ImageColor3 = T.Sub, Size = UDim2.new(0, 16, 0, 16), Position = UDim2.new(0, 12, 0.5, -8), Parent = btn })
            lx = 38
        end
        local label = create("TextLabel", { BackgroundTransparency = 1, Text = (it.type == "back" and "‹  Back") or it.text,
            Font = T.FontMed, TextSize = 13, TextColor3 = T.Text, TextXAlignment = Enum.TextXAlignment.Left, TextTruncate = Enum.TextTruncate.AtEnd,
            Position = UDim2.new(0, lx, 0, 0), Size = UDim2.new(1, -lx - 150, 1, 0), Parent = btn })

        local glyphs = {}
        local function addGlyph(text, xr, w, col, align, keep)
            local t = create("TextLabel", { BackgroundTransparency = 1, Text = text, Font = T.FontBold, TextSize = 13, TextColor3 = col,
                TextTruncate = Enum.TextTruncate.AtEnd,
                TextXAlignment = align or Enum.TextXAlignment.Center, Position = UDim2.new(1, xr, 0, 0), Size = UDim2.new(0, w, 1, 0), Parent = btn })
            glyphs[#glyphs+1] = { obj = t, normal = col, keep = keep } return t
        end

        if it.type == "submenu" or it.type == "dropopt" then addGlyph(">", -22, 14, T.Sub)
        elseif it.type == "toggle" then addGlyph(it.state and "ON" or "OFF", -52, 44, it.state and T.On or T.Off, Enum.TextXAlignment.Right, true)
        elseif it.type == "dropdown" then
            addGlyph(tostring(it.options[it.idx] or "-"), -150, 130, T.Spark, Enum.TextXAlignment.Right, true)
            addGlyph(">", -16, 12, T.Sub)
        elseif it.type == "slider" then
            create("TextButton", { Text = "‹", AutoButtonColor = false, BackgroundTransparency = 1, Font = T.FontBold, TextSize = 16, TextColor3 = T.Sub,
                Position = UDim2.new(1, -86, 0, 0), Size = UDim2.new(0, 18, 1, 0), Parent = btn }).MouseButton1Click:Connect(function() ctrl.index = i ctrl:updateHL() ctrl:adjust(-1) end)
            it._vlab = addGlyph(tostring(it.value), -68, 50, T.Spark)
            create("TextButton", { Text = "›", AutoButtonColor = false, BackgroundTransparency = 1, Font = T.FontBold, TextSize = 16, TextColor3 = T.Sub,
                Position = UDim2.new(1, -20, 0, 0), Size = UDim2.new(0, 18, 1, 0), Parent = btn }).MouseButton1Click:Connect(function() ctrl.index = i ctrl:updateHL() ctrl:adjust(1) end)
        elseif it.type == "textbox" then
            local boxf = create("Frame", { BackgroundColor3 = T.Element, BackgroundTransparency = 0.2, Size = UDim2.new(0, 90, 0, 22), Position = UDim2.new(1, -98, 0.5, -11), BorderSizePixel = 0, Parent = btn })
            local tb = create("TextBox", { BackgroundTransparency = 1, Text = it.value or "", PlaceholderText = it.placeholder or "...", PlaceholderColor3 = T.Sub,
                Font = T.Font, TextSize = 12, TextColor3 = T.Text, Size = UDim2.new(1, -10, 1, 0), Position = UDim2.new(0, 6, 0, 0), ClearTextOnFocus = false, Parent = boxf })
            tb.FocusLost:Connect(function(enter) it.value = tb.Text safe(it.cb, tb.Text, enter) end)
        elseif it.type == "keybind" then
            addGlyph((ctrl.listening == it) and "..." or (it.key and it.key.Name or "None"), -14, 72, T.Spark, Enum.TextXAlignment.Right, true)
        end

        local function setSel(s)
            hl.BackgroundTransparency = s and 0 or 1
            accent.BackgroundTransparency = s and 0 or 1
            label.TextColor3 = s and T.Dark or T.Text
            if iconObj then iconObj.ImageColor3 = s and T.Dark or T.Sub end
            for _, g in ipairs(glyphs) do if not g.keep then g.obj.TextColor3 = s and T.Dark or g.normal end end
        end
        setSel(false)
        if sel(it) then
            btn.MouseEnter:Connect(function() ctrl.index = i ctrl:updateHL() ctrl:updateFooter() end)
            btn.MouseButton1Click:Connect(function() ctrl.index = i ctrl:updateHL() ctrl:activate() end)
        end
        return { setSel = setSel }
    end

    function ctrl:render()
        for _, c in ipairs(list:GetChildren()) do if c:IsA("GuiButton") then c:Destroy() end end
        secLabel.Text = self.current.Name
        crumb.Text = self.current.Parent and "‹ esc" or ""
        local rows = {}
        if self.current.Parent then rows[#rows+1] = { type = "back" } end
        for _, it in ipairs(self.current.Items) do rows[#rows+1] = it end
        self.rows = rows
        if self.index > #rows then self.index = #rows end
        if self.index < 1 then self.index = 1 end
        if rows[self.index] and not sel(rows[self.index]) then for j = 1, #rows do if sel(rows[j]) then self.index = j break end end end
        self.rowObjs = {}
        for i, it in ipairs(rows) do self.rowObjs[i] = buildRow(i, it) end
        list.CanvasSize = UDim2.new(0, 0, 0, #rows * ROWH)
        list.ScrollBarThickness = (#rows > LIST_ROWS) and 4 or 0
        self:updateHL() self:updateFooter() self:scrollIntoView()
    end
    function ctrl:updateHL() for i, o in ipairs(self.rowObjs) do o.setSel(i == self.index) end end
    function ctrl:updateFooter() idxLbl.Text = string.format("%d / %d", self.index, #self.rows) end
    function ctrl:scrollIntoView()
        local top = (self.index - 1) * ROWH
        local cp = list.CanvasPosition.Y
        if top < cp then cp = top elseif top + ROWH > cp + LIST_H then cp = top + ROWH - LIST_H end
        list.CanvasPosition = Vector2.new(0, math.max(cp, 0))
    end
    function ctrl:move(d)
        local n = #self.rows if n == 0 then return end
        local i = self.index
        for _ = 1, n do i = ((i - 1 + d) % n) + 1 if sel(self.rows[i]) then break end end
        self.index = i self:updateHL() self:updateFooter() self:scrollIntoView()
    end
    function ctrl:open(p) p.Parent = p.Parent or self.current self.current = p self.index = 1 self:render() end
    function ctrl:back() if self.current.Parent then self.current = self.current.Parent self.index = 1 self:render() end end
    function ctrl:activate()
        local it = self.rows[self.index] if not it then return end
        if it.type == "back" then self:back()
        elseif it.type == "submenu" then self:open(it.target)
        elseif it.type == "button" then safe(it.cb)
        elseif it.type == "toggle" then it.state = not it.state safe(it.cb, it.state) self:render()
        elseif it.type == "slider" then self:adjust(1)
        elseif it.type == "dropdown" then
            local pg = { Name = it.text:upper(), Parent = self.current, Items = {} }
            for vi, opt in ipairs(it.options) do pg.Items[#pg.Items+1] = { type = "dropopt", text = tostring(opt), _drop = it, _vi = vi } end
            self:open(pg)
        elseif it.type == "dropopt" then it._drop.idx = it._vi safe(it._drop.cb, it._drop.options[it._vi]) self:back()
        elseif it.type == "keybind" then if self.listening == it then self.listening = nil else self.listening = it end self:render()
        end
    end
    function ctrl:adjust(d)
        local it = self.rows[self.index] if not it then return end
        if it.type == "slider" then
            it.value = math.clamp(it.value + d * it.step, it.min, it.max)
            if it._vlab then it._vlab.Text = tostring(it.value) end
            safe(it.cb, it.value)
        elseif it.type == "submenu" and d > 0 then self:open(it.target) end
    end

    UserInputService.InputBegan:Connect(function(input, gpe)
        if gpe or not win.Visible then return end
        if ctrl.listening then
            if input.UserInputType == Enum.UserInputType.Keyboard then
                local kb = ctrl.listening ; ctrl.listening = nil
                kb.key = input.KeyCode ; safe(kb.cb, input.KeyCode) ; ctrl:render()
            end
            return
        end
        local k = input.KeyCode
        if k == Enum.KeyCode.Up then ctrl:move(-1)
        elseif k == Enum.KeyCode.Down then ctrl:move(1)
        elseif k == Enum.KeyCode.Return or k == Enum.KeyCode.KeypadEnter then ctrl:activate()
        elseif k == Enum.KeyCode.Right then ctrl:adjust(1)
        elseif k == Enum.KeyCode.Left then ctrl:adjust(-1)
        elseif k == Enum.KeyCode.Backspace then ctrl:back() end
    end)

    local allItems = {}
    local function add(page, item) table.insert(page.Items, item) table.insert(allItems, item) if ctrl.current == page then ctrl:render() end return item end

    local function dummy() return setmetatable({}, { __index = function() return "" end, __newindex = function() end }) end
    UI = {}

    function UI:Fire(label)
        for _, it in ipairs(allItems) do
            if it.text == label then
                if it.type == "toggle" then it.state = not it.state safe(it.cb, it.state) ctrl:render() return it.state
                elseif it.type == "button" then safe(it.cb) return true end
            end
        end
    end
    function UI:AddTab(name, icon, order)
        local page = { Name = tostring(name):upper(), Items = {}, Parent = root }
        table.insert(root.Items, { type = "submenu", text = tostring(name), target = page, icon = Logos[2], order = order or 999 })
        table.sort(root.Items, function(a, b) return (a.order or 999) < (b.order or 999) end)
        if ctrl.current == root then ctrl:render() end
        return page
    end
    function UI:AddSection(parent, text) add(parent, { type = "section", text = tostring(text) }) return dummy() end
    function UI:AddButton(parent, text, cb) add(parent, { type = "button", text = tostring(text), cb = cb }) return dummy() end
    function UI:AddToggle(parent, text, default, cb) add(parent, { type = "toggle", text = tostring(text), state = default and true or false, cb = cb }) return dummy() end
    function UI:AddSlider(parent, text, min, max, default, cb)
        local step = math.max(1, math.floor((max - min) / 20 + 0.5))
        add(parent, { type = "slider", text = tostring(text), min = min, max = max, value = math.clamp(default or min, min, max), step = step, cb = cb })
        return dummy()
    end
    function UI:AddDropdown(parent, text, options, default, cb)
        local idx = 1
        for i, o in ipairs(options) do if o == default then idx = i end end
        local item = add(parent, { type = "dropdown", text = tostring(text), options = options, idx = idx, cb = cb })
        local function update(newOpts) item.options = newOpts or {} if item.idx > #item.options then item.idx = math.max(1, #item.options) end if ctrl.current == parent then ctrl:render() end end
        return dummy(), update
    end
    function UI:AddTextBox(parent, text, placeholder, cb)
        local item = add(parent, { type = "textbox", text = tostring(text), placeholder = placeholder, value = "", cb = cb })
        return dummy(), function() return item.value end
    end
    function UI:AddKeybind(parent, text, default, cb)
        add(parent, { type = "keybind", text = tostring(text), key = default, cb = cb })
        return dummy()
    end

    ctrl:render()
end

;(function()
local MainTab = UI:AddTab("Main", "🏠", 1)
local MoneyTab = UI:AddTab("Money/Bank", "💰", 2)
local ExploitsTab = UI:AddTab("Exploits", "💀", 3)
local FarmTab = UI:AddTab("Farm", "🌾", 4)
local CombatTab = UI:AddTab("Combat", "⚔️", 5)
local TrollingTab = UI:AddTab("Trolling", "😈", 6)
local QuickBuysTab = UI:AddTab("Quick Buys", "🛒", 7)
local SettingsTab = UI:AddTab("Settings", "⚙️", 9)
local CreditsTab = UI:AddTab("Credits", "ℹ️", 10)
local playerNames = {}
local function refreshPlayerList()
    playerNames = {}
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= LocalPlayer then table.insert(playerNames, p.Name) end
    end
    table.sort(playerNames)
    return playerNames
end
refreshPlayerList()
SelectedPlayer = playerNames[1]
local playerDropdown, updatePlayerDropdown = UI:AddDropdown(MainTab, "Select Player", playerNames, playerNames[1], function(opt)
    SelectedPlayer = opt
end)
UI:AddButton(MainTab, "🔄 Refresh Players", function()
    local newList = refreshPlayerList()
    updatePlayerDropdown(newList)
    SelectedPlayer = newList[1] or nil
    Notify("Players", "Refreshed! " .. #newList .. " players", 2)
end)
UI:AddButton(MainTab, "TP to Player", function()
    if not SelectedPlayer then return end
    local p = Players:FindFirstChild(SelectedPlayer)
    if not p or not p.Character then Notify("TP","Player not found!",2) return end
    local tgtHRP = p.Character:FindFirstChild("HumanoidRootPart"); if not tgtHRP then return end
    local myHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart"); if not myHRP then return end
    enableSwimMethod()
    task.wait(1)
    myHRP.CFrame = tgtHRP.CFrame * CFrame.new(3, 0, 0)
    task.delay(0.2, disableSwimMethod)
    Notify("TP", SelectedPlayer, 2)
end)
UI:AddButton(MainTab, "View Inventory", function()
    if SelectedPlayer then
        local p = Players:FindFirstChild(SelectedPlayer)
        if p then
            local items = {}
            for _, tool in pairs(p.Backpack:GetChildren()) do
                if tool:IsA("Tool") then table.insert(items, tool.Name) end
            end
            if p.Character then
                for _, tool in pairs(p.Character:GetChildren()) do
                    if tool:IsA("Tool") then table.insert(items, tool.Name .. " [E]") end
                end
            end
            Notify("Inv", #items > 0 and table.concat(items, ", ") or "Empty", 5)
        end
    end
end)
UI:AddButton(MainTab, "Clone Player", function()
    if SelectedPlayer then
        local p = Players:FindFirstChild(SelectedPlayer)
        if p and p.Character then
            local char = LocalPlayer.Character
            if char then
                pcall(function()
                    for _, item in pairs(p.Character:GetChildren()) do
                        if item:IsA("Shirt") or item:IsA("Pants") or item:IsA("ShirtGraphic") then
                            local existing = char:FindFirstChildOfClass(item.ClassName)
                            if existing then existing:Destroy() end
                            item:Clone().Parent = char
                        end
                    end
                end)
                Notify("Clone", "Cloned " .. SelectedPlayer, 3)
            end
        end
    end
end)
local spectateEnabled = false
UI:AddToggle(MainTab, "Spectate Player", false, function(state)
    spectateEnabled = state
    if state then
        if SelectedPlayer then
            local p = Players:FindFirstChild(SelectedPlayer)
            if p and p.Character and p.Character:FindFirstChild("Humanoid") then
                workspace.CurrentCamera.CameraSubject = p.Character.Humanoid
                Notify("Spectate", "Watching " .. SelectedPlayer, 2)
            end
        end
    else
        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
            workspace.CurrentCamera.CameraSubject = LocalPlayer.Character.Humanoid
        end
        Notify("Spectate", "Off", 2)
    end
end)
local bringPlayerEnabled = false
UI:AddToggle(MainTab, "Bring Player", false, function(state)
    bringPlayerEnabled = state
    if state and SelectedPlayer then
        local targetPlayer = Players:FindFirstChild(SelectedPlayer)
        task.spawn(function()
            while bringPlayerEnabled do
                local tCharacter = targetPlayer and targetPlayer.Character
                local tRoot = tCharacter and tCharacter:FindFirstChild("HumanoidRootPart")
                local myHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if not tRoot or not myHRP then break end
                local tHumanoid = tCharacter:FindFirstChildOfClass("Humanoid")
                if tHumanoid then tHumanoid.Sit = false end
                tRoot.CFrame = myHRP.CFrame + Vector3.new(3, 1, 0)
                task.wait(0.1)
            end
        end)
        Notify("Bring", "Bringing " .. SelectedPlayer, 2)
    end
end)
UI:AddButton(MainTab, "Kill Player", function()
    if not SelectedPlayer then Notify("Kill","Select a player first!",2) return end
    local p = Players:FindFirstChild(SelectedPlayer)
    if not p or not p.Character then Notify("Kill","Player not found!",2) return end
    if not hasGunInHand() then BigGunNotify("nogun"); return end
    BigGunNotify("ammo")
    task.spawn(function() wsSlimeKill(p) end)
    Notify("Kill","Killed "..SelectedPlayer,2)
end)
local killLoopEnabled = false
UI:AddToggle(MainTab, "Kill Loop (FAST)", false, function(state)
    killLoopEnabled = state
    getgenv().killSelectedRunning = state
    if state then
        if not SelectedPlayer then Notify("Kill Loop","Select player first!",2); killLoopEnabled=false; getgenv().killSelectedRunning=false; return end
        if not hasGunInHand() then BigGunNotify("nogun"); killLoopEnabled=false; getgenv().killSelectedRunning=false; return end
        BigGunNotify("ammo")
        Notify("Kill Loop","Started on "..SelectedPlayer,2)
        task.spawn(function()
            local hrp0 = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            local origin = hrp0 and hrp0.CFrame
            while getgenv().killSelectedRunning do
                local p = Players:FindFirstChild(SelectedPlayer)
                local th = p and p.Character and p.Character:FindFirstChild("HumanoidRootPart")
                local hum = p and p.Character and p.Character:FindFirstChildOfClass("Humanoid")
                local h = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if p and p ~= LocalPlayer and th and hum and hum.Health > 0 and h then
                    checkgun()
                    pcall(function() local s = GetGunSettings(); if s then s.LimitedAmmoEnabled=false; s.Ammo=80000; s.AmmoPerMag=80000; s.MagCount=80000; s.StoredAmmo=80000; s.MaxAmmo=80000 end end)
                    pcall(function() h.CFrame = th.CFrame end)
                    pcall(function() h.Anchored = true end)
                    task.wait(0.1)
                    pcall(function() KillGunMod(p, "Head", math.huge) end)
                    task.wait(0.1)
                    pcall(function() KillGunMod(p, "Head", math.huge) end)
                    pcall(function() h.Anchored = false end)
                    local h2 = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                    if h2 and origin then pcall(function() h2.CFrame = origin end) end
                else

                    if h and origin then pcall(function() h.CFrame = origin end) end
                    while getgenv().killSelectedRunning do
                        local tt = Players:FindFirstChild(SelectedPlayer); if not tt then break end
                        local hh = tt.Character and tt.Character:FindFirstChildOfClass("Humanoid")
                        if hh and hh.Health > 0 then break end
                        task.wait(0.3)
                    end
                    if getgenv().killSelectedRunning then task.wait(10) end
                end
            end
            local hf = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            if hf and origin then pcall(function() hf.CFrame = origin end) end
        end)
    else
        Notify("Kill Loop","Stopped",2)
    end
end)
local knifeKillEnabled = false
UI:AddToggle(MainTab, "🔪 Knife Kill Selected", false, function(state)
    knifeKillEnabled = state
    getgenv()._wsKnifeRunning = state
    if not state then getgenv()._wsKnifeRunning=false; Notify("Knife","Stopped",2); return end
    if not SelectedPlayer then Notify("Knife","Select a player first!",2); knifeKillEnabled=false; getgenv()._wsKnifeRunning=false; return end
    Notify("Knife","Knife killing "..SelectedPlayer,2)
    task.spawn(function()

        local function equipKnife()
            local char=LocalPlayer.Character; local hum=char and char:FindFirstChildOfClass("Humanoid")
            if not hum then return false end
            local cur=char:FindFirstChildWhichIsA("Tool"); if cur and allowedKnifeTools[cur.Name] then return true end
            local bp=LocalPlayer:FindFirstChild("Backpack")
            for _,t in pairs((bp and bp:GetChildren()) or {}) do if t:IsA("Tool") and allowedKnifeTools[t.Name] then pcall(function() hum:EquipTool(t) end); return true end end
            for _,t in pairs(char:GetChildren()) do if t:IsA("Tool") and allowedKnifeTools[t.Name] then pcall(function() hum:EquipTool(t) end); return true end end
            return false
        end
        if not equipKnife() then

            pcall(function() ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("Blade") end)
            local t0=tick(); repeat task.wait(0.2) until equipKnife() or (tick()-t0>6) or not getgenv()._wsKnifeRunning
            if not equipKnife() then BigGunNotify("noknife"); getgenv()._wsKnifeRunning=false; knifeKillEnabled=false; return end
        end
        getgenv().SwimMethod = true
        local hrp0 = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        local origin = hrp0 and hrp0.CFrame
        while getgenv()._wsKnifeRunning do
            local me = LocalPlayer.Character
            local myhrp = me and me:FindFirstChild("HumanoidRootPart")
            local tool = me and me:FindFirstChildWhichIsA("Tool")
            local atk = GetAttackEvent(tool)
            local t = Players:FindFirstChild(SelectedPlayer)
            local tHRP = t and t.Character and t.Character:FindFirstChild("HumanoidRootPart")
            local tHum = t and t.Character and t.Character:FindFirstChildOfClass("Humanoid")
            if myhrp and atk and tHRP and tHum and tHum.Health > 0 then
                pcall(function() myhrp.CFrame = tHRP.CFrame * CFrame.new(0,0,1.2) end)
                pcall(function() atk:FireServer() end)
            end
            task.wait(0.05)
        end
        task.delay(0.3, function() getgenv().SwimMethod=false end)
        local hf = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hf and origin then pcall(function() hf.CFrame = origin end) end
    end)
end)
UI:AddSection(MainTab, "🎮 Player Cheats")
local flyConnections = {}
local flyVelocity = nil
local flyGyro = nil
local flySeat = nil
local flySpeed = 80
local flyMobile = {fwd=false,back=false,left=false,right=false}
local flyMobileGui = nil
local function destroyFlyMobileGui()
    if flyMobileGui then pcall(function() flyMobileGui:Destroy() end); flyMobileGui=nil end
    for k in pairs(flyMobile) do flyMobile[k]=false end
end
local function buildFlyMobileGui()
    destroyFlyMobileGui()
    if not UserInputService.TouchEnabled then return end
    flyMobileGui=Instance.new("ScreenGui"); flyMobileGui.Name="WalFlyMobile"; flyMobileGui.ResetOnSpawn=false
    flyMobileGui.DisplayOrder=9997; flyMobileGui.IgnoreGuiInset=true; flyMobileGui.Parent=CoreGui
    local function Btn(label,xScale,yOffset,color)
        local b=Instance.new("TextButton",flyMobileGui); b.AnchorPoint=Vector2.new(0.5,1)
        b.Size=UDim2.new(0,65,0,65); b.Position=UDim2.new(xScale,0,1,yOffset)
        b.BackgroundColor3=color or Color3.fromRGB(0,100,200); b.BackgroundTransparency=0.2
        b.Text=label; b.TextColor3=Color3.fromRGB(255,255,255); b.TextSize=28
        b.Font=Enum.Font.GothamBold; b.BorderSizePixel=0; b.ZIndex=10; b.AutoButtonColor=false
        Instance.new("UICorner",b).CornerRadius=UDim.new(0.3,0); return b
    end
    local fwdBtn=Btn("▲",0.15,-240); local backBtn=Btn("▼",0.15,-100)
    local leftBtn=Btn("◄",0.08,-170); local rightBtn=Btn("►",0.22,-170)
    local upBtn=Btn("🔼",0.88,-175,Color3.fromRGB(0,160,80)); local downBtn=Btn("🔽",0.88,-95,Color3.fromRGB(180,40,40))
    local function wire(btn,key)
        btn.InputBegan:Connect(function(i) if i.UserInputType==Enum.UserInputType.Touch then flyMobile[key]=true; btn.BackgroundTransparency=0.05 end end)
        btn.InputEnded:Connect(function(i) if i.UserInputType==Enum.UserInputType.Touch then flyMobile[key]=false; btn.BackgroundTransparency=0.2 end end)
    end
    wire(fwdBtn,"fwd"); wire(backBtn,"back"); wire(leftBtn,"left"); wire(rightBtn,"right")
end
local function cleanupFly()
    destroyFlyMobileGui()
    for _, conn in ipairs(flyConnections) do
        if conn and conn.Disconnect then
            pcall(function() conn:Disconnect() end)
        end
    end
    flyConnections = {}
    if flyVelocity and flyVelocity.Parent then flyVelocity:Destroy(); flyVelocity = nil end
    if flyGyro and flyGyro.Parent then flyGyro:Destroy(); flyGyro = nil end
    if flySeat and flySeat.Parent then flySeat:Destroy(); flySeat = nil end
    getgenv().SwimMethod = false
    local char = LocalPlayer.Character
    if char then
        local humanoid = char:FindFirstChildWhichIsA("Humanoid")
        local hrp = char:FindFirstChild("HumanoidRootPart")
        if humanoid and hrp then
            pcall(function()
                humanoid:ChangeState(0); task.wait(0.1); humanoid:ChangeState(2)
                humanoid.PlatformStand = false; humanoid.Jump = false
                hrp.AssemblyLinearVelocity = Vector3.zero
                hrp.AssemblyAngularVelocity = Vector3.zero
            end)
        end
    end
end
local function setupFly()
    cleanupFly()
    local char = LocalPlayer.Character
    if not char then return end
    local humanoid = char:FindFirstChildWhichIsA("Humanoid")
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not humanoid or not hrp then return end
    getgenv().SwimMethod = true
    local seat = Instance.new("VehicleSeat")
    seat.Name = "FlySeat"; seat.Anchored = false; seat.CanCollide = false
    seat.Transparency = 1; seat.TopSurface = Enum.SurfaceType.Smooth
    seat.BottomSurface = Enum.SurfaceType.Smooth; seat.Parent = workspace
    seat.CFrame = hrp.CFrame * CFrame.new(0, -3, 0)
    local weld = Instance.new("Weld")
    weld.Part0 = seat; weld.Part1 = hrp; weld.C0 = CFrame.new(0, 3, 0); weld.Parent = seat
    seat:Sit(humanoid)
    flyVelocity = Instance.new("BodyVelocity")
    flyVelocity.MaxForce = Vector3.new(1e9, 1e9, 1e9); flyVelocity.Velocity = Vector3.zero; flyVelocity.Parent = hrp
    flyGyro = Instance.new("BodyGyro")
    flyGyro.MaxTorque = Vector3.new(1e9, 1e9, 1e9); flyGyro.P = 50000; flyGyro.D = 1000
    flyGyro.CFrame = hrp.CFrame; flyGyro.Parent = hrp
    flySeat = seat
    buildFlyMobileGui()
    local move = {W=false,A=false,S=false,D=false,Space=false,Shift=false}
    local inputBegan = UserInputService.InputBegan:Connect(function(i,g)
        if g then return end
        if i.KeyCode == Enum.KeyCode.W then move.W = true end
        if i.KeyCode == Enum.KeyCode.A then move.A = true end
        if i.KeyCode == Enum.KeyCode.S then move.S = true end
        if i.KeyCode == Enum.KeyCode.D then move.D = true end
        if i.KeyCode == Enum.KeyCode.Space then move.Space = true end
        if i.KeyCode == Enum.KeyCode.LeftShift then move.Shift = true end
        if i.KeyCode == Enum.KeyCode.E then flySpeed = math.clamp(flySpeed + 10, 20, 300) end
        if i.KeyCode == Enum.KeyCode.Q then flySpeed = math.clamp(flySpeed - 10, 20, 300) end
    end)
    table.insert(flyConnections, inputBegan)
    local inputEnded = UserInputService.InputEnded:Connect(function(i)
        if i.KeyCode == Enum.KeyCode.W then move.W = false end
        if i.KeyCode == Enum.KeyCode.A then move.A = false end
        if i.KeyCode == Enum.KeyCode.S then move.S = false end
        if i.KeyCode == Enum.KeyCode.D then move.D = false end
        if i.KeyCode == Enum.KeyCode.Space then move.Space = false end
        if i.KeyCode == Enum.KeyCode.LeftShift then move.Shift = false end
    end)
    table.insert(flyConnections, inputEnded)
    local renderStepped = RunService.RenderStepped:Connect(function()
        if not flyEnabled or not flyVelocity or not flyGyro then return end
        if not getgenv().SwimMethod then getgenv().SwimMethod = true end
        local cam = workspace.CurrentCamera
        flyGyro.CFrame = cam.CFrame
        local dir = Vector3.zero
        if not UserInputService.TouchEnabled then
            if move.W then dir = dir + cam.CFrame.LookVector end
            if move.S then dir = dir - cam.CFrame.LookVector end
            if move.A then dir = dir - cam.CFrame.RightVector end
            if move.D then dir = dir + cam.CFrame.RightVector end
            if move.Space then dir = dir + Vector3.new(0,1,0) end
            if move.Shift then dir = dir - Vector3.new(0,1,0) end
        else
            if flyMobile.fwd   then dir = dir + cam.CFrame.LookVector end
            if flyMobile.back  then dir = dir - cam.CFrame.LookVector end
            if flyMobile.left  then dir = dir - cam.CFrame.RightVector end
            if flyMobile.right then dir = dir + cam.CFrame.RightVector end
            if dir.Magnitude < 0.01 then
                local h = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid")
                if h then
                    local md = h.MoveDirection
                    if md.Magnitude > 0.1 then
                        dir = (cam.CFrame.RightVector * md.X) + (cam.CFrame.LookVector * -md.Z)
                    end
                end
            end
        end
        flyVelocity.Velocity = dir.Magnitude > 0 and dir.Unit * flySpeed or Vector3.zero
    end)
    table.insert(flyConnections, renderStepped)
    Notify("Fly", "Active! WASD to move, E/Q for speed", 3)
end
UI:AddToggle(MainTab, "Player Fly", false, function(state)
    flyEnabled = state
    if state then task.spawn(setupFly) else cleanupFly(); Notify("Fly", "Disabled", 2) end
end)
UI:AddSlider(MainTab, "Fly Speed", 20, 300, 80, function(val) flySpeed = val end)
UI:AddButton(MainTab, "Bring Nearest Car", function()
    task.spawn(function()
        local char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
        local hrp = char:WaitForChild("HumanoidRootPart", 3)
        local hum = char:FindFirstChildWhichIsA("Humanoid")
        if not hrp or not hum then return end
        local nearestCar, nearestDist = nil, math.huge
        local CivCars = workspace:FindFirstChild("CivCars")
        if CivCars then
            for _, car in ipairs(CivCars:GetChildren()) do
                if car:IsA("Model") then
                    local seat = car:FindFirstChild("DriveSeat")
                    if seat and not seat.Occupant then
                        if not car.PrimaryPart then
                            local body = car:FindFirstChild("Body")
                            car.PrimaryPart = (body and body:FindFirstChild("#Weight")) or seat
                        end
                        if car.PrimaryPart then
                            local dist = (car.PrimaryPart.Position - hrp.Position).Magnitude
                            if dist < nearestDist then nearestDist = dist; nearestCar = car end
                        end
                    end
                end
            end
        end
        if not nearestCar then
            for _, v in ipairs(workspace:GetDescendants()) do
                if v:IsA("VehicleSeat") and not v.Occupant then
                    local model = v:FindFirstAncestorOfClass("Model")
                    if model then
                        local dist = (v.Position - hrp.Position).Magnitude
                        if dist < nearestDist then nearestDist = dist; nearestCar = model end
                    end
                end
            end
        end
        if not nearestCar then Notify("Car","No free car found!",2) return end
        local seat = nearestCar:FindFirstChild("DriveSeat") or nearestCar:FindFirstChildWhichIsA("VehicleSeat")
        if not seat then Notify("Car","No seat!",2) return end
        if not nearestCar.PrimaryPart then nearestCar.PrimaryPart = nearestCar:FindFirstChildWhichIsA("BasePart") or seat end
        nearestCar:SetPrimaryPartCFrame(hrp.CFrame * CFrame.new(0,0,-6) * CFrame.Angles(0,math.rad(180),0))
        seat:Sit(hum)
        Notify("Car","Car brought!",2)
    end)
end)
do
local cfHum, cfSeat, cfCar, cfRoot
local cfBV, cfBG, cfLastCar
local function cfCleanup()
    if cfBV then cfBV:Destroy(); cfBV=nil end
    if cfBG then cfBG:Destroy(); cfBG=nil end
end
local function cfSetup()
    cfCleanup()
    if not Config.TheBronx.carfly then return end
    local char=LocalPlayer.Character; if not char then return end
    cfHum=char:FindFirstChildWhichIsA("Humanoid"); if not cfHum then return end
    cfSeat=cfHum.SeatPart; if not cfSeat or not cfSeat:IsA("VehicleSeat") then return end
    cfCar=cfSeat.Parent; if not cfCar then return end
    cfRoot=cfCar.PrimaryPart; if not cfRoot then return end
    cfLastCar=cfCar
    for _,v in ipairs(cfCar:GetChildren()) do
        if v:IsA("BasePart") and not v.Name:lower():find("wheel") then v.CanCollide=false end
    end
    cfBV=Instance.new("BodyVelocity"); cfBV.MaxForce=Vector3.new(1e9,1e9,1e9); cfBV.Velocity=Vector3.zero; cfBV.Parent=cfRoot
    cfBG=Instance.new("BodyGyro"); cfBG.MaxTorque=Vector3.new(1e9,1e9,1e9); cfBG.P=25000; cfBG.D=1500; cfBG.CFrame=cfRoot.CFrame; cfBG.Parent=cfRoot
end
task.spawn(function()
    while true do task.wait(0.2)
        local char=LocalPlayer.Character
        if char then
            local h=char:FindFirstChildWhichIsA("Humanoid")
            if h then
                local seat=h.SeatPart
                if seat and seat:IsA("VehicleSeat") then
                    if seat.Parent~=cfLastCar then cfSetup() end
                else if cfLastCar then cfCleanup(); cfLastCar=nil end end
            end
        end
    end
end)
local cfMGui=nil
local cfMUp,cfMDown,cfMFwd,cfMBack,cfMLeft,cfMRight=false,false,false,false,false,false
local function destroyCFMobile()
    if cfMGui then pcall(function() cfMGui:Destroy() end); cfMGui=nil end
    cfMUp=false;cfMDown=false;cfMFwd=false;cfMBack=false;cfMLeft=false;cfMRight=false
end
local function buildCFMobile()
    destroyCFMobile(); if not UserInputService.TouchEnabled then return end
    cfMGui=Instance.new("ScreenGui"); cfMGui.Name="WalCFMobile"; cfMGui.ResetOnSpawn=false
    cfMGui.DisplayOrder=9998; cfMGui.IgnoreGuiInset=true
    pcall(function() cfMGui.Parent=LocalPlayer:WaitForChild("PlayerGui") end)
    local function Btn(lbl,xs,yo)
        local b=Instance.new("TextButton",cfMGui); b.AnchorPoint=Vector2.new(0.5,1); b.Size=UDim2.new(0,65,0,65)
        b.Position=UDim2.new(xs,0,1,yo); b.BackgroundColor3=Color3.fromRGB(0,100,200); b.BackgroundTransparency=0.2
        b.Text=lbl; b.TextColor3=Color3.fromRGB(255,255,255); b.TextSize=28; b.Font=Enum.Font.GothamBold
        b.BorderSizePixel=0; b.ZIndex=10; b.AutoButtonColor=false; Instance.new("UICorner",b).CornerRadius=UDim.new(0.3,0); return b
    end
    local T=Enum.UserInputType.Touch
    local fB=Btn("▲",0.15,-240); local bB=Btn("▼",0.15,-100); local lB=Btn("◀",0.08,-170)
    local rB=Btn("▶",0.22,-170); local uB=Btn("🔼",0.88,-175); local dB=Btn("🔽",0.88,-95)
    fB.InputBegan:Connect(function(i) if i.UserInputType==T then cfMFwd=true end end); fB.InputEnded:Connect(function(i) if i.UserInputType==T then cfMFwd=false end end)
    bB.InputBegan:Connect(function(i) if i.UserInputType==T then cfMBack=true end end); bB.InputEnded:Connect(function(i) if i.UserInputType==T then cfMBack=false end end)
    lB.InputBegan:Connect(function(i) if i.UserInputType==T then cfMLeft=true end end); lB.InputEnded:Connect(function(i) if i.UserInputType==T then cfMLeft=false end end)
    rB.InputBegan:Connect(function(i) if i.UserInputType==T then cfMRight=true end end); rB.InputEnded:Connect(function(i) if i.UserInputType==T then cfMRight=false end end)
    uB.InputBegan:Connect(function(i) if i.UserInputType==T then cfMUp=true end end); uB.InputEnded:Connect(function(i) if i.UserInputType==T then cfMUp=false end end)
    dB.InputBegan:Connect(function(i) if i.UserInputType==T then cfMDown=true end end); dB.InputEnded:Connect(function(i) if i.UserInputType==T then cfMDown=false end end)
end
RunService.RenderStepped:Connect(function()
    if not Config.TheBronx.carfly then cfCleanup(); return end
    if not cfHum or cfHum.SeatPart~=cfSeat then return end
    if not cfRoot or not cfBV or not cfBG then cfSetup(); return end
    local speed=Config.TheBronx.carflyspeed or 120
    local cam=workspace.CurrentCamera; local camCF=cam.CFrame; local camLook=camCF.LookVector; local camRight=camCF.RightVector
    if not UserInputService.TouchEnabled then
        if UserInputService:IsMouseButtonPressed(Enum.UserInputType.MouseButton2) then cfBG.CFrame=CFrame.lookAt(cfRoot.Position,cfRoot.Position+camLook) end
        local move=Vector3.zero
        if UserInputService:IsKeyDown(Enum.KeyCode.W) then move=move+camLook end
        if UserInputService:IsKeyDown(Enum.KeyCode.S) then move=move-camLook end
        if UserInputService:IsKeyDown(Enum.KeyCode.A) then move=move-camRight end
        if UserInputService:IsKeyDown(Enum.KeyCode.D) then move=move+camRight end
        cfBV.Velocity=move.Magnitude>0 and move.Unit*speed or Vector3.zero
    else
        cfBG.CFrame=CFrame.lookAt(cfRoot.Position,cfRoot.Position+camLook)
        local flatFwd=Vector3.new(camLook.X,0,camLook.Z); if flatFwd.Magnitude>0.001 then flatFwd=flatFwd.Unit end
        local move=Vector3.zero
        local usingDpad = cfMFwd or cfMBack or cfMLeft or cfMRight or cfMUp or cfMDown
        if usingDpad then
            if cfMFwd then move=move+flatFwd end
            if cfMBack then move=move-flatFwd end
            if cfMLeft then move=move-camRight end
            if cfMRight then move=move+camRight end
            if cfMUp then move=move+Vector3.new(0,1,0) end
            if cfMDown then move=move-Vector3.new(0,1,0) end
        else
            local h2=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid")
            if h2 then
                local md=h2.MoveDirection
                if md.Magnitude>0 then local cl=Vector3.new(camLook.X,0,camLook.Z).Unit; move=(camRight*md.X)+(cl*-md.Z) end
                if h2:GetState()==Enum.HumanoidStateType.Jumping then move=move+Vector3.new(0,0.8,0) end
            end
        end
        cfBV.Velocity=move.Magnitude>0 and move.Unit*speed or Vector3.zero
    end
end)
task.spawn(function()
    while true do task.wait(0.5)
        if Config.TheBronx.carfly and cfSeat then buildCFMobile() else destroyCFMobile() end
    end
end)
LocalPlayer.CharacterAdded:Connect(cfCleanup)
UI:AddToggle(MainTab, "Car Fly", false, function(state)
    Config.TheBronx.carfly = state
    if state then
        local char = LocalPlayer.Character
        if char then
            local hum = char:FindFirstChildWhichIsA("Humanoid")
            if hum and hum.SeatPart and hum.SeatPart:IsA("VehicleSeat") then
                cfSetup()
                Notify("Car Fly","Active! WASD to fly",3)
            else
                Notify("Car Fly","Get in a car then enable!",3)
            end
        end
    else
        cfCleanup(); Notify("Car Fly","Disabled",2)
    end
end)
UI:AddSlider(MainTab, "Car Fly Speed", 20, 300, 120, function(val)
    Config.TheBronx.carflyspeed = val
end)
UI:AddToggle(MainTab, "WalkSpeed (3s delay)", false, function(state)
    enhancedWalk = state
    if state then
        local character = LocalPlayer.Character; if not character then return end
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        local hrp = character:FindFirstChild("HumanoidRootPart")
        if not humanoid or not hrp then return end
        hrp.AssemblyLinearVelocity = Vector3.zero; getgenv().SwimMethod = true
        Notify("WalkSpeed", "Bypassing anti-cheat (3s)...", 3)
        local freezeConn
        freezeConn = RunService.RenderStepped:Connect(function()
            if enhancedWalk and hrp then hrp.AssemblyLinearVelocity = Vector3.zero end
        end)
        task.delay(3, function()
            if freezeConn then freezeConn:Disconnect() end
            if not enhancedWalk then return end
            local bodyGyro2 = Instance.new("BodyGyro")
            bodyGyro2.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
            bodyGyro2.P = 50000; bodyGyro2.D = 1000; bodyGyro2.CFrame = hrp.CFrame; bodyGyro2.Parent = hrp
            local moveConn
            moveConn = RunService.RenderStepped:Connect(function()
                if not enhancedWalk then
                    if bodyGyro2 then bodyGyro2:Destroy() end
                    if moveConn then moveConn:Disconnect() end
                    return
                end
                local camera = workspace.CurrentCamera; local dir = Vector3.zero
                if UserInputService:IsKeyDown(Enum.KeyCode.W) then dir = dir + Vector3.new(camera.CFrame.LookVector.X, 0, camera.CFrame.LookVector.Z) end
                if UserInputService:IsKeyDown(Enum.KeyCode.S) then dir = dir - Vector3.new(camera.CFrame.LookVector.X, 0, camera.CFrame.LookVector.Z) end
                if UserInputService:IsKeyDown(Enum.KeyCode.A) then dir = dir - camera.CFrame.RightVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.D) then dir = dir + camera.CFrame.RightVector end
                if dir.Magnitude == 0 and humanoid then local md = humanoid.MoveDirection; dir = Vector3.new(md.X, 0, md.Z) end
                if dir.Magnitude > 0 then dir = dir.Unit * speed end
                local currentY = hrp.AssemblyLinearVelocity.Y
                hrp.AssemblyLinearVelocity = Vector3.new(dir.X, math.clamp(currentY, -100, -2), dir.Z)
                if dir.Magnitude > 0 then local look = dir.Unit; bodyGyro2.CFrame = CFrame.new(hrp.Position, hrp.Position + Vector3.new(look.X, 0, look.Z)) end
                hrp.RotVelocity = Vector3.zero; hrp.AssemblyAngularVelocity = Vector3.zero
            end)
            Notify("WalkSpeed", "Enabled! Move now", 2)
        end)
    else getgenv().SwimMethod = false; Notify("WalkSpeed", "Disabled", 2) end
end)
UI:AddSlider(MainTab, "Walk Speed", 16, 500, 16, function(val) speed = val end)
UI:AddSection(MainTab, "🔫 Gun Mods (Toggles)")
UI:AddButton(MainTab, "Infinite Ammo", function()
    local char = LocalPlayer.Character
    if not char then Notify("Ammo","No character!",2) return end
    local tool = char:FindFirstChildOfClass("Tool")
    if not tool then Notify("Ammo","Equip a gun first!",2) return end
    local settings, _ = GetGunSettings()
    if settings then
        settings.LimitedAmmoEnabled = false
        settings.MaxAmmo = 80000
        settings.AmmoPerMag = 80000
        settings.Ammo = 80000
        settings.StoredAmmo = 80000
        settings.MagCount = 80000
    end
    local gunScript = tool:FindFirstChild("GunScript_Local")
    if gunScript then
        pcall(function() debug.setupvalue(getsenv(gunScript).Reload, 3, 80000) end)
        pcall(function() debug.setupvalue(getsenv(gunScript).Reload, 5, 80000) end)
        Notify("Ammo","✅ Infinite Ammo (80000) — press R to reload for max",2)
    else
        Notify("Ammo","✅ Ammo values set to 80000",2)
    end
end)
local noRecoilEnabled = false
UI:AddToggle(MainTab, "No Recoil", false, function(state)
    noRecoilEnabled = state
    if state then task.spawn(function() while noRecoilEnabled do local s=GetGunSettings(); if s then s.Recoil=0 end; task.wait(0.5) end end) end
end)
local autoGunEnabled = false
UI:AddToggle(MainTab, "Auto Gun", false, function(state)
    autoGunEnabled = state
    if state then task.spawn(function() while autoGunEnabled do local s=GetGunSettings(); if s then s.Auto=true end; task.wait(0.5) end end) end
end)
local noFireRateEnabled = false
UI:AddToggle(MainTab, "No Fire Rate", false, function(state)
    noFireRateEnabled = state
    if state then task.spawn(function() while noFireRateEnabled do local s=GetGunSettings(); if s then s.FireRate=0.1 end; task.wait(0.5) end end) end
end)
local infDamageEnabled = false
UI:AddToggle(MainTab, "Inf Damage", false, function(state)
    infDamageEnabled = state
    if state then task.spawn(function() while infDamageEnabled do local s=GetGunSettings(); if s then s.BaseDamage=9e9 end; task.wait(0.5) end end) end
end)
local noSpreadEnabled = false
UI:AddToggle(MainTab, "No Spread", false, function(state)
    noSpreadEnabled = state
    if state then task.spawn(function() while noSpreadEnabled do local s=GetGunSettings(); if s then pcall(function() s.SpreadXY=0; s.SpreadYX=0; s.Spread=0; s.SpreadX=0; s.SpreadY=0 end) end; task.wait(0.5) end end) end
end)
local noJamEnabled = false
UI:AddToggle(MainTab, "No Jam", false, function(state)
    noJamEnabled = state
    if state then task.spawn(function() while noJamEnabled do local s=GetGunSettings(); if s then pcall(function() s.JamChance=0 end) end; task.wait(0.5) end end) end
end)
local gunColors = {"💖 Neon Pink", "💙 Neon Blue", "❤️ Neon Red", "💚 Neon Green", "💜 Neon Purple", "🤍 Neon White"}
UI:AddDropdown(MainTab, "Gun Color (NEON)", gunColors, gunColors[1], function(opt)
    local colorMap = {["💖 Neon Pink"]=Color3.fromRGB(255,105,180),["💙 Neon Blue"]=Color3.fromRGB(0,170,255),["❤️ Neon Red"]=Color3.fromRGB(255,0,0),["💚 Neon Green"]=Color3.fromRGB(0,255,0),["💜 Neon Purple"]=Color3.fromRGB(170,0,255),["🤍 Neon White"]=Color3.fromRGB(255,255,255)}
    local char = LocalPlayer.Character; local tool = char and char:FindFirstChildOfClass("Tool")
    if tool and colorMap[opt] then
        for _, part in pairs(tool:GetDescendants()) do if part:IsA("BasePart") and part.Name ~= "Handle" then part.Color = colorMap[opt]; part.Material = Enum.Material.Neon end end
        Notify("Gun Color", opt .. " applied!", 2)
    end
end)
local rainbowGunEnabled = false
UI:AddToggle(MainTab, "Rainbow Gun (NEON)", false, function(state)
    rainbowGunEnabled = state
    if state then task.spawn(function() while rainbowGunEnabled do local char=LocalPlayer.Character; local tool=char and char:FindFirstChildOfClass("Tool"); if tool then local color=Color3.fromHSV(tick()%1,1,1); for _,part in pairs(tool:GetDescendants()) do if part:IsA("BasePart") and part.Name~="Handle" then part.Color=color; part.Material=Enum.Material.Neon end end end; task.wait(0.05) end end) end
end)
GunSkins = {
    "rbxassetid://83922435917330",
    "rbxassetid://75965794858060",
    "rbxassetid://104925026556009",
    "rbxassetid://113000073171004",
    "rbxassetid://139546409781319"
}
function ApplySkin(tool, imageId)
    if not tool then return end
    for _, obj in ipairs(tool:GetDescendants()) do
        if obj:IsA("MeshPart") then
            -- mesh gun bodies are skinned via TextureID (decals don't show on meshes)
            pcall(function() obj.TextureID = imageId end)
            pcall(function() obj.Color = Color3.fromRGB(255,255,255) end)
        elseif obj:IsA("BasePart") then
            for _, child in ipairs(obj:GetChildren()) do
                if child.Name == "ScorpioSkin" then child:Destroy() end
            end
            for _, face in ipairs(Enum.NormalId:GetEnumItems()) do
                local decal = Instance.new("Decal")
                decal.Name = "ScorpioSkin"
                decal.Texture = imageId
                decal.Face = face
                decal.Parent = obj
            end
        end
        if obj:IsA("SpecialMesh") then
            -- legacy meshes inside Parts
            pcall(function() obj.TextureId = imageId end)
        end
    end
end
UI:AddToggle(MainTab, "Galaxy Skins", false, function(Value)
    getgenv()._galaxySkins = Value
    if Value then
        task.spawn(function()
            local index = 1
            while getgenv()._galaxySkins do
                local char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
                local tool = char:FindFirstChildOfClass("Tool")
                if tool then ApplySkin(tool, GunSkins[index]) end
                index = index + 1
                if index > #GunSkins then index = 1 end
                task.wait(2)
            end
        end)
    end
end)
UI:AddSection(MoneyTab, "💰 Dirty Money")
local function GetGoodCleaner()
    local CounterInstance = nil
    local mapFolder = workspace:FindFirstChild("1# Map")
    if mapFolder then
        for _,v in mapFolder:GetChildren() do
            if v:FindFirstChild("CounterM") then CounterInstance = v break end
        end
    end
    local searchTables = {workspace:FindFirstChild("CounterBag") and workspace.CounterBag:GetChildren() or {}}
    if CounterInstance then table.insert(searchTables, CounterInstance:GetChildren()) end
    for _,tbl in pairs(searchTables) do
        for _,v in pairs(tbl) do
            local cp = v:FindFirstChild("CashPrompt", true)
            local gp = v:FindFirstChild("GrabPrompt", true)
            if cp and cp.Enabled and cp.ObjectText == "Count Bread" and gp and not gp.Enabled then return v end
        end
    end
    return nil
end
UI:AddButton(MoneyTab, "Count Dirty Money", function() task.spawn(function() pcall(function()
    local fs = 0; pcall(function() fs = LocalPlayer.stored.FilthyStack.Value end)
    if fs == 0 then Notify("Auto Clean","You have no dirty money!",3) return end
    local character = LocalPlayer.Character
    if not character or not character:FindFirstChild("HumanoidRootPart") then return end
    local humanoid = character:FindFirstChild("Humanoid")
    if not humanoid or humanoid.Health == 0 then return end
    local Cleaner = GetGoodCleaner()
    if not Cleaner then Notify("Auto Clean","Could not find a valid cleaner!",3) return end
    local OldCF = character.HumanoidRootPart.CFrame
    Notify("Auto Clean","Cleaning money...",3)
    BypassTp(Cleaner.WorldPivot)
    task.wait(0.4)
    pcall(function() fireproximityprompt(Cleaner:FindFirstChild("CashPrompt", true)) end)
    local onLight = Cleaner:FindFirstChild("On", true)
    if onLight then repeat task.wait() until onLight.Color == Color3.fromRGB(74,156,69) end
    task.wait(0.5)
    pcall(function() fireproximityprompt(Cleaner:FindFirstChild("CashPrompt", true)) end)
    task.wait(0.25)
    BypassTp(Cleaner.WorldPivot)
    task.wait(0.4)
    repeat task.wait() until LocalPlayer.Backpack:FindFirstChild("MoneyReady")
    humanoid:EquipTool(LocalPlayer.Backpack["MoneyReady"])
    repeat
        pcall(function() fireproximityprompt(Cleaner:FindFirstChild("GrabPrompt", true)) end)
        task.wait(3)
    until not character:FindFirstChild("MoneyReady")
    repeat task.wait(1) until LocalPlayer.Backpack:FindFirstChild("BagOfMoney")
    BypassTp(CFrame.new(-1216.5113525390625, 253.8797607421875, -3635.7958984375))
    task.wait(0.3)
    pcall(function() ReplicatedStorage:WaitForChild("SetLookAngles"):FireServer(0.4, -0.1, false) end)
    humanoid:EquipTool(LocalPlayer.Backpack["BagOfMoney"])
    task.wait(2)
    local atmP = workspace:FindFirstChild("ATMMoney") and workspace.ATMMoney:FindFirstChildOfClass("ProximityPrompt")
    if atmP then pcall(function() fireproximityprompt(atmP) end) end
    BypassTp(OldCF)
    Notify("Auto Clean","Done! Money cleaned and deposited",3)
end) end) end)
UI:AddSection(MoneyTab, "🛒 Buy Items")
local buyItemsOptions = {"🍉 FijiWater", "💧 FreshWater", "🍎 Ice-Fruit Bag", "🥤 Ice-Fruit Cupz"}
UI:AddDropdown(MoneyTab, "Buy Items", buyItemsOptions, buyItemsOptions[1], function(opt)
    pcall(function()
        if opt == "🍉 FijiWater" then ReplicatedStorage.ExoticShopRemote:InvokeServer("FijiWater")
        elseif opt == "💧 FreshWater" then ReplicatedStorage.ExoticShopRemote:InvokeServer("FreshWater")
        elseif opt == "🍎 Ice-Fruit Bag" then ReplicatedStorage.ExoticShopRemote:InvokeServer("Ice-Fruit Bag")
        elseif opt == "🥤 Ice-Fruit Cupz" then ReplicatedStorage.ExoticShopRemote:InvokeServer("Ice-Fruit Cupz") end
    end)
    Notify("Bought", opt, 2)
end)
UI:AddButton(MoneyTab, "Buy All Cooking Items", function()
    pcall(function()
        ReplicatedStorage.ExoticShopRemote:InvokeServer("FijiWater"); task.wait(0.1)
        ReplicatedStorage.ExoticShopRemote:InvokeServer("FreshWater"); task.wait(0.1)
        ReplicatedStorage.ExoticShopRemote:InvokeServer("Ice-Fruit Bag"); task.wait(0.1)
        ReplicatedStorage.ExoticShopRemote:InvokeServer("Ice-Fruit Cupz")
    end)
    Notify("Buy", "All cooking items bought!", 3)
end)
UI:AddSection(MoneyTab, "🍳 Cooking & Selling")
UI:AddButton(MoneyTab, "🍳 Go to Cook Spot", function()
    BypassTp(CFrame.new(-741.19, 262.96, -955.78)); Notify("TP", "Cook Spot", 2)
end)
UI:AddButton(MoneyTab, "💸 Generate Dirty Money", function()
    local player = LocalPlayer
    local char = player.Character; if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart"); if not hrp then return end
    local humanoid = char:FindFirstChildOfClass("Humanoid"); if not humanoid then return end
    local camera = workspace.CurrentCamera
    local originalCameraType = camera.CameraType
    local originalFOV = camera.FieldOfView
    local tool = player.Backpack:FindFirstChild("Ice-Fruit Cupz")
    if tool then
        humanoid:EquipTool(tool)
        task.wait(1.0)
    else
        if not char:FindFirstChild("Ice-Fruit Cupz") then
            Notify("Error","Need Ice-Fruit Cupz in backpack!",3) return
        end
    end
    local blackScreen = Instance.new("ScreenGui")
    blackScreen.IgnoreGuiInset = true; blackScreen.Parent = CoreGui
    local frame = Instance.new("Frame", blackScreen)
    frame.BackgroundColor3 = Color3.new(0,0,0); frame.Size = UDim2.new(1,0,1,0); frame.BorderSizePixel = 0
    local msg = Instance.new("TextLabel", frame)
    msg.Text = "JOINTHUB.GG | GENERATING MONEY..."; msg.TextColor3 = Color3.fromRGB(0,200,80)
    msg.BackgroundTransparency = 1; msg.Size = UDim2.new(1,0,1,0); msg.Font = Enum.Font.GothamBold; msg.TextScaled = true
    local originalCFrame = hrp.CFrame
    local targetCFrame = CFrame.new(-69.82200622558594, 287.0635986328125, -319.79437255859375)
    enableSwimMethod()
    task.wait(1)
    hrp.CFrame = targetCFrame + Vector3.new(2, 0, 0)
    task.delay(0.25, disableSwimMethod)
    task.wait(0.5)
    camera.CameraType = Enum.CameraType.Scriptable
    local cameraOffset = Vector3.new(0, 5, 5)
    local camConn = RunService.Heartbeat:Connect(function()
        if hrp then camera.CFrame = CFrame.new(hrp.Position+cameraOffset, hrp.Position+Vector3.new(0,3,0)) end
    end)
    getgenv().instantPrompts = true
    local iceFruitSellPrompt = workspace:WaitForChild("IceFruit Sell"):FindFirstChildOfClass("ProximityPrompt")
    if iceFruitSellPrompt then
        iceFruitSellPrompt.HoldDuration = 0; iceFruitSellPrompt.MaxActivationDistance = 6
        local fireConn = RunService.Heartbeat:Connect(function()
            if getgenv().instantPrompts and iceFruitSellPrompt.Enabled then
                for _ = 1, 100 do
                    iceFruitSellPrompt:InputHoldBegin()
                    iceFruitSellPrompt:InputHoldEnd()
                end
            end
        end)
        task.spawn(function()
            task.wait(1)
            getgenv().instantPrompts = false
            fireConn:Disconnect()
            iceFruitSellPrompt.HoldDuration = 1; iceFruitSellPrompt.MaxActivationDistance = 4
            if camConn then camConn:Disconnect() end
            camera.CameraType = originalCameraType; camera.FieldOfView = originalFOV
            enableSwimMethod(); task.wait(0.5)
            hrp.CFrame = originalCFrame + Vector3.new(2,0,0)
            task.wait(0.5); disableSwimMethod()
            pcall(function() blackScreen:Destroy() end)
            Notify("Money","Done generating money!",3)
        end)
    else
        getgenv().instantPrompts = false
        if camConn then camConn:Disconnect() end
        camera.CameraType = originalCameraType
        hrp.CFrame = originalCFrame
        pcall(function() blackScreen:Destroy() end)
        Notify("Error","IceFruit Sell prompt not found!",3)
    end
end)
UI:AddToggle(MoneyTab, "Auto Deposit $30k", false, function(state)
    autoDeposit30k = state
    if state then task.spawn(function() while autoDeposit30k do pcall(function() ReplicatedStorage.BankAction:FireServer("depo", 30000) end); task.wait(0.5) end end) end
end)
local autoWithdraw90k = false
UI:AddToggle(MoneyTab, "Auto Withdraw $90k", false, function(state)
    autoWithdraw90k = state
    if state then task.spawn(function() while autoWithdraw90k do pcall(function() ReplicatedStorage.BankAction:FireServer("with", 90000) end); task.wait(0.5) end end) end
end)
UI:AddSection(MoneyTab, "💵 Money Tools")
local drop10kEnabled = false
UI:AddToggle(MoneyTab, "Drop $10k (Loop)", false, function(state)
    drop10kEnabled = state
    if state then task.spawn(function() while drop10kEnabled do pcall(function() ReplicatedStorage.BankProcessRemote:InvokeServer("Drop", 10000) end); task.wait(0.5) end end) end
end)
local drop5kEnabled = false
UI:AddToggle(MoneyTab, "Drop $5k (Loop)", false, function(state)
    drop5kEnabled = state
    if state then task.spawn(function() while drop5kEnabled do pcall(function() ReplicatedStorage.BankProcessRemote:InvokeServer("Drop", 5000) end); task.wait(0.5) end end) end
end)
UI:AddButton(MoneyTab, "Show Bank Balance", function()
    local amt = "N/A"; pcall(function() amt = tostring(LocalPlayer.stored.Bank.Value) end); Notify("Bank", "$" .. amt, 5)
end)
UI:AddSection(ExploitsTab, "🗺️ Teleport")
local locationNames = {}
for name, _ in pairs(locations) do table.insert(locationNames, name) end
table.sort(locationNames)
local selectedLocation = locationNames[1]
UI:AddDropdown(ExploitsTab, "📍 Select & Teleport", locationNames, locationNames[1], function(opt)
    if locations[opt] then BypassTp(CFrame.new(locations[opt])); Notify("TP", opt, 2) end
end)
UI:AddSection(ExploitsTab, "🎒 Drop Items")
local dropAllEnabled = false
UI:AddToggle(ExploitsTab, "Drop All Items (Loop)", false, function(state)
    dropAllEnabled = state
    getgenv().dropAllRunning = state
    if not state then Notify("Drop","Stopped dropping",2) return end
    Notify("Drop","Dropping all items...",2)
    task.spawn(function()
        local exempt = {["Fist"]=true, ["Fists"]=true, ["Phone"]=true}
        while getgenv().dropAllRunning do
            local char = LocalPlayer.Character
            local bp = LocalPlayer:FindFirstChild("Backpack")
            local tools = {}
            if char then
                for _, tool in pairs(char:GetChildren()) do
                    if tool:IsA("Tool") and not exempt[tool.Name] then
                        table.insert(tools, tool)
                    end
                end
            end
            if bp then
                for _, tool in pairs(bp:GetChildren()) do
                    if tool:IsA("Tool") and not exempt[tool.Name] then
                        table.insert(tools, tool)
                    end
                end
            end
            if #tools == 0 then task.wait(0.5) end
            for _, tool in ipairs(tools) do
                if not getgenv().dropAllRunning then break end
                if char then
                    local hum = char:FindFirstChildWhichIsA("Humanoid")
                    if hum then hum:EquipTool(tool) end
                end
                task.wait(0.1)
                pcall(function()
                    ReplicatedStorage:WaitForChild("DropItemRemote"):FireServer(tool)
                end)
                task.wait(0.15)
            end
        end
    end)
end)
local passItemsLoopEnabled = false
UI:AddToggle(ExploitsTab, "Pass Items Loop", false, function(state)
    passItemsLoopEnabled = state
    if state then
        task.spawn(function()
            while passItemsLoopEnabled do
                pcall(function() ReplicatedStorage.DropRemote:FireServer("Drop") end)
                task.wait(0.5)
            end
        end)
        Notify("Items","Pass loop ON",2)
    else
        Notify("Items","Pass loop OFF",2)
    end
end)
UI:AddButton(ExploitsTab, "Pass to Nearest", function()
    pcall(function() ReplicatedStorage.DropRemote:FireServer("Drop") end)
    Notify("Items","Passed!",2)
end)
UI:AddSection(ExploitsTab, "🏷️ Nametag")
UI:AddToggle(ExploitsTab, "Show Nametag", true, function(state)
    nametagEnabled = state
    local char = LocalPlayer.Character
    if char and char:FindFirstChild("Head") then local tag = char.Head:FindFirstChild("JointhubTag"); if tag then tag.Enabled = state end end
    if state and char then CreateNametag(char) end
end)
UI:AddSection(ExploitsTab, "💰 Dupes & Exploits")
function GetSafe()
    local safe=nil
    pcall(function() safe=workspace:WaitForChild("HomeDoorSS",3):WaitForChild("HomeDoor",3):WaitForChild("Safe",3) end)
    if not safe then
        pcall(function()
            local safes=workspace:FindFirstChild("1# Map") and workspace["1# Map"]:FindFirstChild("2 Crosswalks") and workspace["1# Map"]["2 Crosswalks"]:FindFirstChild("Safes")
            if safes then
                for _,v in ipairs(safes:GetChildren()) do
                    local u=v:FindFirstChild("Union") or v:FindFirstChildWhichIsA("BasePart")
                    if u then safe=v; break end
                end
            end
        end)
    end
    return safe
end
getgenv().plugzStoreDuped = true
function SafeDupeOnce(toolName)
    local Character=LocalPlayer.Character; if not Character or not toolName then return end
    local InventoryRemote=ReplicatedStorage:WaitForChild("Inventory")
    local BackpackRemote=ReplicatedStorage:WaitForChild("BackpackRemote")
    local Safe=GetSafe()
    if not Safe then Notify("Dupe","Safe not found!",2) return end
    pcall(function() Character.Humanoid:UnequipTools() end)
    task.spawn(function() pcall(function() BackpackRemote:InvokeServer("Store",toolName) end) end)
    task.spawn(function() pcall(function() InventoryRemote:FireServer("Change",toolName,"Backpack",Safe) end) end)
    task.wait(0.5)
    task.wait(1.5)
    pcall(function() BackpackRemote:InvokeServer("Grab",toolName) end)
    if not getgenv().plugzStoreDuped then
        pcall(function() InventoryRemote:FireServer("Change",toolName,"Inv",Safe) end)
    end
    task.wait(0.5)
end
UI:AddButton(ExploitsTab, "Safe Dupe Once", function()
    task.spawn(function()
        local char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
        local tool = char:FindFirstChildOfClass("Tool")
        if not tool then Notify("Dupe","Equip a tool first!",3) return end
        Notify("Dupe","Duping "..tool.Name.."...",3)
        SafeDupeOnce(tool.Name)
        Notify("Dupe","Done!",3)
    end)
end)
UI:AddButton(ExploitsTab, "TP to Safe", function()
    pcall(function()
        local char = LocalPlayer.Character
        if not char then return end
        local hrp = char:FindFirstChild("HumanoidRootPart")
        if not hrp then return end
        getgenv()._preDupeSavePos = hrp.CFrame
        local safe = GetSafe()
        if not safe then Notify("TP Safe","Safe not found! Going to market...",2); task.spawn(function() BypassTp(CFrame.new(-450.44, 334.31, -545.12)) end) return end
        local tpTarget = nil
        if safe:IsA("BasePart") then tpTarget = safe.CFrame
        else local part = safe:FindFirstChild("Union") or safe:FindFirstChildWhichIsA("BasePart"); if part then tpTarget = part.CFrame end end
        if tpTarget then task.spawn(function() BypassTp(tpTarget + Vector3.new(2, 0, 0)) end); Notify("TP Safe","Teleported to safe! Position saved.",2)
        else task.spawn(function() BypassTp(CFrame.new(-450.44, 334.31, -545.12)) end); Notify("TP Safe","Teleported to market area.",2) end
    end)
end)
UI:AddSection(ExploitsTab, "🛡️ Bypasses & Anti-Cheat")
UI:AddToggle(ExploitsTab, "Anti Fling", false, function(state)
    getgenv().antiFling = state
    Notify("Bypass", state and "Anti Fling ON" or "Anti Fling OFF", 2)
end)
UI:AddToggle(ExploitsTab, "Anti Fall Damage", false, function(state) if state then pcall(function() local char=LocalPlayer.Character; local fd=char:FindFirstChild("FallDamageRagdoll"); if fd then fd:Destroy() end end); Notify("Bypass","Anti Fall ON",2) end end)
UI:AddToggle(ExploitsTab, "Anti-Knockback", false, function(state) if state then pcall(function() local char=LocalPlayer.Character; for _,v in ipairs(char:GetDescendants()) do if v:IsA("BodyVelocity") or v:IsA("LinearVelocity") or v:IsA("VectorForce") then v:Destroy() end end; char.HumanoidRootPart.ChildAdded:Connect(function(v) if v:IsA("BodyVelocity") or v:IsA("LinearVelocity") or v:IsA("VectorForce") then v:Destroy() end end) end); Notify("Bypass","Anti-KB ON",2) end end)
UI:AddToggle(ExploitsTab, "Noclip", false, function(state) if state then Noclipping=RunService.Stepped:Connect(function() setCollide(false) end); Notify("Bypass","Noclip ON",2) else if Noclipping then Noclipping:Disconnect(); Noclipping=nil end; setCollide(true) end end)
UI:AddToggle(ExploitsTab, "🚗 Anti Car Knockback", false, function(state)
    getgenv()._antiCarKB = state
    if state then
        if not getgenv()._antiCarKBConn then
            getgenv()._antiCarKBConn = RunService.Heartbeat:Connect(function()
                if not getgenv()._antiCarKB then return end
                pcall(function()
                    local c = LocalPlayer.Character; if not c then return end
                    local hrp = c:FindFirstChild("HumanoidRootPart"); local hum = c:FindFirstChildOfClass("Humanoid")
                    if not hrp or not hum then return end
                    hum.PlatformStand = false
                    local st = hum:GetState()
                    if st == Enum.HumanoidStateType.Physics or st == Enum.HumanoidStateType.FallingDown or st == Enum.HumanoidStateType.Ragdoll then
                        hum:ChangeState(Enum.HumanoidStateType.GettingUp)
                    end
                    local v = hrp.AssemblyLinearVelocity
                    if math.sqrt(v.X*v.X + v.Z*v.Z) > 90 then
                        hrp.AssemblyLinearVelocity = Vector3.new(0, math.max(v.Y, -10), 0)
                        hrp.AssemblyAngularVelocity = Vector3.zero
                    end
                end)
            end)
        end
        Notify("Bypass","Anti Car Knockback ON",2)
    else
        if getgenv()._antiCarKBConn then getgenv()._antiCarKBConn:Disconnect(); getgenv()._antiCarKBConn=nil end
        Notify("Bypass","Anti Car Knockback OFF",2)
    end
end)
UI:AddToggle(ExploitsTab, "Instant Prompts", false, function(state) if state then for _,v in ipairs(workspace:GetDescendants()) do if v:IsA("ProximityPrompt") then v.HoldDuration=0; v.MaxActivationDistance=6 end end; Notify("Bypass","Instant Prompts ON",2) end end)
UI:AddToggle(ExploitsTab, "Anti Lose Items", false, function(state) AntiLoseEnabled = state; if state then Notify("Bypass", "Anti Lose ON", 2) end end)
UI:AddSection(ExploitsTab, "👤 Player Mods")
UI:AddToggle(ExploitsTab, "Infinite Stamina", false, function(state) staminaEnabled = state; if state then applyEffects() end end)
UI:AddToggle(ExploitsTab, "Infinite Hunger", false, function(state) hungerEnabled = state; if state then applyEffects() end end)
UI:AddToggle(ExploitsTab, "Infinite Sleep", false, function(state) sleepEnabled = state; if state then applyEffects() end end)
UI:AddToggle(ExploitsTab, "Infinite Jump", false, function(state)
    getgenv().InfiniteJumpEnabled = state
    if state and not getgenv().InfiniteJumpConnection then
        getgenv().InfiniteJumpConnection = UserInputService.JumpRequest:Connect(function()
            if getgenv().InfiniteJumpEnabled then local character=LocalPlayer.Character; if character and character:FindFirstChild("Humanoid") then character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping) end end
        end)
        Notify("Infinite Jump", "Enabled!", 2)
    elseif not state and getgenv().InfiniteJumpConnection then
        getgenv().InfiniteJumpConnection:Disconnect(); getgenv().InfiniteJumpConnection = nil; Notify("Infinite Jump", "Disabled", 2)
    end
end)
UI:AddToggle(ExploitsTab, "No Jump Cooldown", false, function(state)
    getgenv().NoJumpCooldownEnabled = state
    if state then
        if getgenv().NoJumpCooldownConnection then pcall(function() getgenv().NoJumpCooldownConnection:Disconnect() end) end
        getgenv().NoJumpCooldownConnection = UserInputService.JumpRequest:Connect(function()
            if not getgenv().NoJumpCooldownEnabled then return end
            local character = LocalPlayer.Character; if not character then return end
            local humanoid = character:FindFirstChildWhichIsA("Humanoid"); if not humanoid then return end
            if humanoid.FloorMaterial == Enum.Material.Air then return end
            if humanoid.Jump or humanoid:GetState() == Enum.HumanoidStateType.Jumping then return end
            humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end)
        Notify("No Jump Cooldown", "Instant jumps!", 2)
    else if getgenv().NoJumpCooldownConnection then pcall(function() getgenv().NoJumpCooldownConnection:Disconnect() end); getgenv().NoJumpCooldownConnection = nil end end
end)
UI:AddToggle(ExploitsTab, "No Rent Pay", false, function(state)
    getgenv().noRent = state
    if state then task.spawn(function() while getgenv().noRent do pcall(function() for _,v in pairs(workspace:GetDescendants()) do if v:IsA("ProximityPrompt") and (v.ActionText:lower():find("rent") or v.ObjectText:lower():find("rent")) then v.Enabled=false end end end); task.wait(5) end end); Notify("No Rent","Rent prompts disabled!",2) end
end)
UI:AddToggle(ExploitsTab, "Anti Ragdoll", false, function(state)
    getgenv().AntiRagdoll = state
    if state then pcall(function() local char=LocalPlayer.Character; if char then for _,v in pairs(char:GetDescendants()) do if v:IsA("BallSocketConstraint") or v:IsA("NoCollisionConstraint") then v:Destroy() end end end end); Notify("Anti Ragdoll","No more ragdoll!",2) end
end)
UI:AddToggle(ExploitsTab, "Spinbot", false, function(state)
    getgenv().SpinbotEnabled = state
    if state then task.spawn(function() while getgenv().SpinbotEnabled do local character=LocalPlayer.Character; if character and character:FindFirstChild("HumanoidRootPart") then character.HumanoidRootPart.CFrame=character.HumanoidRootPart.CFrame*CFrame.Angles(0,math.rad(45),0) end; RunService.RenderStepped:Wait() end end); Notify("Spinbot","Spinning!",2)
    else Notify("Spinbot","Disabled",2) end
end)
UI:AddToggle(ExploitsTab, "Anti Camera Shake", false, function(state)
    getgenv().antiCameraShake = state
    if state then
        task.spawn(function()
            while getgenv().antiCameraShake do
                pcall(function()
                    local camera=workspace.CurrentCamera; if camera then for _,child in pairs(camera:GetChildren()) do if child:IsA("ShakeEffect") or child.Name:lower():find("shake") then child:Destroy() end end end
                    local playerScripts=LocalPlayer:FindFirstChild("PlayerScripts"); if playerScripts then for _,script in pairs(playerScripts:GetDescendants()) do if script.Name:lower():find("shake") and script:IsA("LocalScript") then script.Enabled=false end end end
                end)
                task.wait(0.5)
            end
        end)
        Notify("Anti Shake", "Camera shake disabled!", 2)
    end
end)
getgenv().deathPosition = nil; getgenv().respawnWhereDied = false
local fastRespawnConnection = nil
UI:AddToggle(ExploitsTab, "Faster Respawn", false, function(state)
    _G.respawn = state
    if state then
        if fastRespawnConnection then pcall(function() fastRespawnConnection:Disconnect() end) end
        fastRespawnConnection = RunService.PreRender:Connect(function()
            if not _G.respawn then return end; if not LocalPlayer.Character then return end
            local h = LocalPlayer.Character:FindFirstChild("Humanoid")
            if h and h.Health <= 0 then pcall(function() ReplicatedStorage.LoadCharacter:FireServer() end); StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Backpack, true) end
        end)
        Notify("Respawn", "Fast respawn ON!", 2)
    else if fastRespawnConnection then pcall(function() fastRespawnConnection:Disconnect() end); fastRespawnConnection = nil end; Notify("Respawn","Disabled",2) end
end)
UI:AddToggle(ExploitsTab, "Respawn Where Died", false, function(state) getgenv().respawnWhereDied = state; if state then Notify("Respawn","Will respawn at death spot!",2) end end)
LocalPlayer.CharacterAdded:Connect(function(char)
    local humanoid = char:WaitForChild("Humanoid")
    humanoid.Died:Connect(function() local hrp=char:FindFirstChild("HumanoidRootPart"); if hrp then getgenv().deathPosition=hrp.Position end end)
    if getgenv().respawnWhereDied and getgenv().deathPosition then
        task.wait(1); getgenv().SwimMethod = true; task.wait(0.5)
        local newHRP = char:WaitForChild("HumanoidRootPart", 5)
        if newHRP then newHRP.CFrame = CFrame.new(getgenv().deathPosition) end
        getgenv().SwimMethod = false
    end
end)
UI:AddSection(FarmTab, "🎬 Studio")
UI:AddButton(FarmTab, "Studio Rob", function()
    local char = LocalPlayer.Character; if not char then return end
    local rootPart = char:FindFirstChild("HumanoidRootPart"); if not rootPart then return end
    pcall(function() for _,v in pairs(workspace.StudioPay.Money:GetDescendants()) do if v:IsA("ProximityPrompt") and v.Name=="Prompt" then v.HoldDuration=0; v.RequiresLineOfSight=false end end end)
    local prompts = {}
    pcall(function() for _,v in pairs(workspace.StudioPay.Money:GetDescendants()) do if v:IsA("ProximityPrompt") and v.Name=="Prompt" and v.Enabled then table.insert(prompts,v) end end end)
    if #prompts == 0 then Notify("Studio","Already robbed!",3) return end
    local oldCFrame = rootPart.CFrame; local camera = workspace.CurrentCamera
    for _, v in ipairs(prompts) do
        getgenv().SwimMethod = true
        local offset = Vector3.new(math.cos(math.rad(math.random(0,359))),2,math.sin(math.rad(math.random(0,359))))
        rootPart.CFrame = CFrame.new(v.Parent.Position + offset)
        local oldCameraType = camera.CameraType; camera.CameraType = Enum.CameraType.Scriptable
        local promptPos = v.Parent.Position; local conn
        conn = RunService.RenderStepped:Connect(function() camera.CFrame = CFrame.lookAt(camera.CFrame.Position, promptPos) end)
        task.wait(0.3)
        repeat fireproximityprompt(v); task.wait(0.1) until not v.Enabled
        conn:Disconnect(); camera.CameraType = oldCameraType; getgenv().SwimMethod = false
    end
    rootPart.CFrame = oldCFrame; Notify("Studio","Rob complete!",3)
end)
UI:AddButton(FarmTab, "Reset Camera to Player", function()
    pcall(function()
        local camera=workspace.CurrentCamera; local char=LocalPlayer.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            camera.CameraType=Enum.CameraType.Custom; camera.CameraSubject=char:FindFirstChild("Humanoid")
            camera.CFrame=CFrame.new(char.HumanoidRootPart.Position+Vector3.new(0,5,10),char.HumanoidRootPart.Position)
            Notify("Camera","Reset to player!",2)
        end
    end)
end)
UI:AddButton(FarmTab, "TP to Studio", function() BypassTp(CFrame.new(93427.51,14484.90,566.67)); Notify("TP","Studio",2) end)
UI:AddSection(FarmTab, "🏗️ Construction")
UI:AddButton(FarmTab, "TP to Construction", function() BypassTp(CFrame.new(-1731.83,370.81,-1176.83)); Notify("TP","Construction Site",2) end)
local constructionRunning = false
UI:AddToggle(FarmTab, "Auto Construction Farm", false, function(Value)
    local speaker = LocalPlayer
    local function getCharacter() return speaker.Character or speaker.CharacterAdded:Wait() end
    local function getBackpack() return speaker:FindFirstChild("Backpack") end
    local function hasPlyWood()
        local bp=getBackpack(); local ch=getCharacter()
        return (bp and bp:FindFirstChild("PlyWood")) or (ch and ch:FindFirstChild("PlyWood"))
    end
    local function equipPlyWood()
        local bp=getBackpack(); if bp then local pw=bp:FindFirstChild("PlyWood"); if pw then pw.Parent=getCharacter() end end
    end
    local function fireInstantPrompt(prompt)
        if prompt and prompt:IsA("ProximityPrompt") and prompt.Enabled then
            prompt.HoldDuration=0; fireproximityprompt(prompt)
        end
    end
    local function grabWood()
        local char=getCharacter()
        char:SetPrimaryPartCFrame(CFrame.new(-1727,371,-1178))
        task.wait(0)
        while constructionRunning and not hasPlyWood() do
            local prompt=workspace.ConstructionStuff["Grab Wood"]:FindFirstChildOfClass("ProximityPrompt")
            fireInstantPrompt(prompt); task.wait(0); equipPlyWood()
        end
    end
    local function buildWall(name, position)
        local ok, prompt = pcall(function()
            return workspace.ConstructionStuff[name]:FindFirstChildOfClass("ProximityPrompt")
        end)
        if not ok or not prompt then return end
        while constructionRunning and prompt and prompt.Enabled do
            getCharacter():SetPrimaryPartCFrame(position)
            task.wait(0)
            fireInstantPrompt(prompt)
            task.wait(0)
            if not hasPlyWood() then grabWood() end
        end
    end
    local function quitJob()
        pcall(function()
            local qp=workspace.ConstructionStuff:FindFirstChild("Quit Job")
            if qp then
                local prompt=qp:FindFirstChildOfClass("ProximityPrompt")
                if prompt then
                    getCharacter():SetPrimaryPartCFrame(qp.CFrame+Vector3.new(0,2,0))
                    task.wait(0.1); fireInstantPrompt(prompt)
                end
            end
        end)
    end
    if Value then
        constructionRunning=true
        enableSwimMethod()
        task.wait(1)
        local char=getCharacter()
        char:SetPrimaryPartCFrame(CFrame.new(-1728,371,-1172))
        task.wait(0.2)
        pcall(function() fireInstantPrompt(workspace.ConstructionStuff["Start Job"]:FindFirstChildOfClass("ProximityPrompt")) end)
        task.wait(0.2)
        task.spawn(function()
            while constructionRunning do
                if not hasPlyWood() then grabWood() end
                buildWall("Wall2 Prompt",CFrame.new(-1705,368,-1151))
                buildWall("Wall3 Prompt",CFrame.new(-1732,368,-1152))
                buildWall("Wall4 Prompt2",CFrame.new(-1772,368,-1152))
                buildWall("Wall1 Prompt3",CFrame.new(-1674,368,-1166))
                task.wait(0)
            end
        end)
    else
        constructionRunning=false; disableSwimMethod(); quitJob()
        pcall(function()
            local sjp=workspace.ConstructionStuff["Start Job"]:FindFirstChildOfClass("ProximityPrompt")
            if sjp and sjp.Parent then
                local ch=getCharacter()
                if ch and ch.PrimaryPart then
                    ch:SetPrimaryPartCFrame(sjp.Parent.CFrame+Vector3.new(0,2,0))
                    task.wait(0.1); fireInstantPrompt(sjp)
                end
            end
        end)
    end
    Notify("Construction", Value and "Farming..." or "Stopped", 2)
end)
UI:AddSection(FarmTab, "🗑️ Trashbags")
UI:AddButton(FarmTab, "Search Trashbags", function()
    task.spawn(function()
        local char=LocalPlayer.Character; if not char then return end
        local hrp=char:FindFirstChild("HumanoidRootPart"); if not hrp then return end
        local originalCFrame=hrp.CFrame; Notify("Farm","Searching trashbags...",2); getgenv().SwimMethod=true; task.wait(0.5)
        local foundCount=0
        pcall(function()
            for _,v in pairs(workspace:GetDescendants()) do
                if v:IsA("ProximityPrompt") and v.Name=="ProximityPrompt" and v.Parent and v.Parent.Name=="DumpsterPromt" then
                    v.HoldDuration=0; v.RequiresLineOfSight=false
                    hrp.CFrame=v.Parent.CFrame+Vector3.new(0,0.2,3); task.wait(0.3)
                    for _=1,10 do fireproximityprompt(v); task.wait(0.05) end
                    foundCount=foundCount+1; task.wait(0.1)
                end
            end
        end)
        hrp.CFrame=originalCFrame; task.wait(0.3); getgenv().SwimMethod=false; Notify("Farm","Searched "..foundCount.." trashbags!",2)
    end)
end)
UI:AddButton(FarmTab, "Sell Trashbag Items", function()
    pcall(function() for _,tool in pairs(LocalPlayer.Backpack:GetChildren()) do if tool:IsA("Tool") then pcall(function() ReplicatedStorage.PawnRemote:FireServer(tool.Name) end); task.wait(0.1) end end end)
    Notify("Sell","Items sold!",2)
end)
UI:AddSection(FarmTab, "💵 Cash")
UI:AddButton(FarmTab, "Collect Dropped Cash", function()
    local char=LocalPlayer.Character; local hrp=char and char:FindFirstChild("HumanoidRootPart"); if not hrp then return end
    local originalCFrame=hrp.CFrame
    pcall(function() for _,v in pairs(workspace.Dollas:GetDescendants()) do if v:IsA("ProximityPrompt") then v.HoldDuration=0; v.RequiresLineOfSight=false end end end)
    pcall(function() for _,v in pairs(workspace.Dollas:GetDescendants()) do if v:IsA("ProximityPrompt") then hrp.CFrame=v.Parent.CFrame; task.wait(0.25); fireproximityprompt(v); task.wait(0.25) end end end)
    hrp.CFrame=originalCFrame; Notify("Cash","Collected!",2)
end)
UI:AddSection(CombatTab, "💀 Kill Aura")
UI:AddToggle(CombatTab, "Kill Aura", false, function(state)
    if state and not hasGunInHand() then BigGunNotify("nogun"); getgenv().auraenabled=false; return end
    getgenv().auraenabled = state
    if state then
        BigGunNotify("ammo")
        task.spawn(function()
            while getgenv().auraenabled and task.wait(getgenv().cooldown) do
                task.wait()
                pcall(function()
                    local plr=game.Players.LocalPlayer
                    if plr.Character:FindFirstChildWhichIsA("Tool") and plr.Character:FindFirstChildOfClass("Tool"):FindFirstChild("GunScript_Local") then
                        if target1 and target1.Character and target1.Character:FindFirstChild("Head") then
                            local part=Instance.new("Part",workspace); part.Size=Vector3.new(0.2,0.2,(plr.Character.HumanoidRootPart.Position-target1.Character.Head.Position).Magnitude); part.Anchored=true; part.CanCollide=false
                            local color=getgenv().rainbowbeam and Color3.fromHSV(tick()%5/5,1,1) or getgenv().beamcolor
                            part.Color=color; part.Material=Enum.Material.Neon
                            local toolHandle=plr.Character:FindFirstChildWhichIsA("Tool"):FindFirstChild("Handle")
                            if toolHandle then local midpoint=(toolHandle.Position+target1.Character[getgenv().hitpart].Position)/2; part.Position=midpoint; part.CFrame=CFrame.new(midpoint,target1.Character[getgenv().hitpart].Position) end
                            task.wait(0.1); part:Destroy()
                            local tool=plr.Character:FindFirstChildWhichIsA("Tool"); local handle=tool:FindFirstChild("Handle"); local muzzleEffect=tool:FindFirstChild("GunScript_Local") and tool.GunScript_Local:FindFirstChild("MuzzleEffect")
                            if handle and muzzleEffect and game.ReplicatedStorage:FindFirstChild("VisualizeMuzzle") then game.ReplicatedStorage.VisualizeMuzzle:FireServer(handle,true,{false,7,color,15,true,0.02},muzzleEffect) end

                            local _myH=plr.Character:FindFirstChild("HumanoidRootPart"); local _tH=target1.Character:FindFirstChild("HumanoidRootPart")
                            if _myH and _tH then local _o=_myH.CFrame; pcall(function() _myH.CFrame=_tH.CFrame end); pcall(function() _myH.Anchored=true end); task.wait(0.08); KillGunMod(target1,"Head",math.huge); pcall(function() _myH.Anchored=false end); local _h2=plr.Character and plr.Character:FindFirstChild("HumanoidRootPart"); if _h2 then pcall(function() _h2.CFrame=_o end) end else KillGunMod(target1,"Head",math.huge) end
                        end
                    end
                end)
            end
        end)
        Notify("Kill Aura","ON - Attacking nearest",2)
    end
end)
UI:AddToggle(CombatTab, "Highlight Target", false, function(state) getgenv().killaurahigh = state end)
UI:AddToggle(CombatTab, "Rainbow Beam", false, function(state) getgenv().rainbowbeam = state end)
UI:AddButton(CombatTab, "Kill All (5 sec)", function()
    if not hasGunInHand() then BigGunNotify("nogun"); return end
    BigGunNotify("ammo")
    task.spawn(function()
        local gun=checkgun(); if not gun then Notify("Kill","Gun not found",3) return end
        pcall(function() local s=GetGunSettings(); if s then s.LimitedAmmoEnabled=false; s.Ammo=80000; s.AmmoPerMag=80000; s.MagCount=80000; s.StoredAmmo=80000; s.MaxAmmo=80000 end end)
        local hrp0=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        local origin=hrp0 and hrp0.CFrame
        for _,v in pairs(Players:GetPlayers()) do
            if v~=LocalPlayer and v.Character then
                local th=v.Character:FindFirstChild("HumanoidRootPart")
                local hum=v.Character:FindFirstChildOfClass("Humanoid")
                local h=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if th and hum and hum.Health>0 and h then
                    pcall(function() h.CFrame=th.CFrame end)
                    pcall(function() h.Anchored = true end)
                    task.wait(0.07)
                    pcall(function() KillGunMod(v,"Head",math.huge) end)
                    task.wait(0.07)
                    pcall(function() KillGunMod(v,"Head",math.huge) end)
                    task.wait(0.18)
                    pcall(function() KillGunMod(v,"Head",math.huge) end)
                    task.wait(0.1)
                    pcall(function() h.Anchored = false end)
                end
            end
        end
        local hf=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hf and origin then pcall(function() hf.CFrame=origin end) end
        Notify("Kill All","Done",3)
    end)
end)
UI:AddSection(CombatTab, "🌀 Server Chaos")
local bringAllRotation=0; local bringAllEnabled=false
UI:AddToggle(CombatTab, "Bring All Players (Rotate)", false, function(state)
    bringAllEnabled = state
    if state then
        task.spawn(function()
            while bringAllEnabled do
                local myHRP=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if myHRP then
                    local players={}; for _,p in pairs(Players:GetPlayers()) do if p~=LocalPlayer and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then table.insert(players,p) end end
                    local count=#players
                    if count>0 then
                        bringAllRotation=bringAllRotation+2
                        for i,p in ipairs(players) do local angle=math.rad((360/count)*i+bringAllRotation); local radius=20; pcall(function() p.Character.HumanoidRootPart.CFrame=myHRP.CFrame*CFrame.new(math.cos(angle)*radius,0,math.sin(angle)*radius) end) end
                    end
                end
                task.wait(0.05)
            end
        end)
        Notify("Bring All","Rotating circle ON (bigger)",2)
    end
end)
UI:AddSection(CombatTab, "🎯 Hitbox")
UI:AddToggle(CombatTab, "Hitbox Extender", false, function(state)
    hitboxextender = state
    if state then RunService:BindToRenderStep("Hitbox",0,function() for _,v in pairs(Players:GetPlayers()) do if v~=LocalPlayer and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then pcall(function() local hrp=v.Character.HumanoidRootPart; hrp.Size=Vector3.new(Size,Size,Size); hrp.Transparency=Transparency; hrp.Color=HitboxColor end) end end end)
    else RunService:UnbindFromRenderStep("Hitbox") end
end)
UI:AddSlider(CombatTab, "Hitbox Size", 1, 15, 4, function(val) Size = val end)
UI:AddSlider(CombatTab, "Hitbox Transparency", 0, 100, 85, function(val) Transparency = val / 100 end)
UI:AddToggle(CombatTab, "Rainbow Hitbox", false, function(state)
    rainbowHitbox = state
    if state then task.spawn(function() while rainbowHitbox do HitboxColor=Color3.fromHSV(tick()%1,1,1); task.wait(0.1) end end) end
end)
UI:AddSection(TrollingTab, "📞 Spam")
local spamPoliceEnabled = false
UI:AddToggle(TrollingTab, "Spam Call Police", false, function(state)
    spamPoliceEnabled = state
    if state then task.spawn(function() while spamPoliceEnabled do pcall(function() ReplicatedStorage.CallPolice:FireServer() end); task.wait(0.5) end end); Notify("Troll","Spamming police!",2) end
end)
UI:AddButton(TrollingTab, "Break All Glass", function()
    for _,v in ipairs(workspace:GetDescendants()) do if v.Name=="Glass" and (v:IsA("BasePart") or v:IsA("MeshPart")) then pcall(function() ReplicatedStorage.BreakGlass:InvokeServer(v) end) end end
    Notify("Troll","Glass broken!",2)
end)
local spamTweetEnabled = false
UI:AddToggle(TrollingTab, "Spam Tweet (Every 4s)", false, function(state)
    spamTweetEnabled = state
    if state then task.spawn(function() while spamTweetEnabled do pcall(function() ReplicatedStorage.Resources["#Phone"].Main:FireServer("Tweet",{"CreateTweet","Jointhub.gg on top"}) end); task.wait(4) end end); Notify("Tweet","Spamming tweets!",2) end
end)
UI:AddSection(TrollingTab, "📢 Megaphone")
UI:AddButton(TrollingTab, "🚔 PULL OVER NOW!", function() pcall(function() ReplicatedStorage.MegaphoneRemote:FireServer("PULL OVER NOW!") end); Notify("Megaphone","Sent!",2) end)
UI:AddButton(TrollingTab, "🚨 Move it FOLKS!", function() pcall(function() ReplicatedStorage.MegaphoneRemote:FireServer("Move it FOLKS!") end); Notify("Megaphone","Sent!",2) end)
UI:AddButton(TrollingTab, "👮 Driver Pull Over!", function() pcall(function() ReplicatedStorage.MegaphoneRemote:FireServer("Driver Pull Over!") end); Notify("Megaphone","Sent!",2) end)
UI:AddButton(TrollingTab, "✋ Hands UP!", function() pcall(function() ReplicatedStorage.MegaphoneRemote:FireServer("Hands UP!") end); Notify("Megaphone","Sent!",2) end)
UI:AddSection(TrollingTab, "🎭 Animations")
local trollTrack, trollTrack2, trollTrack4
UI:AddToggle(TrollingTab, "🚶 Carrying Animation", false, function(state)
    pcall(function() if state then local anim=ReplicatedStorage:FindFirstChild("BeingCarried"); if anim and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then trollTrack=LocalPlayer.Character.Humanoid:LoadAnimation(anim); trollTrack:Play() end elseif trollTrack then trollTrack:Stop() end end)
end)
UI:AddToggle(TrollingTab, "🤕 Low HP Animation", false, function(state)
    pcall(function() if state then local anim=ReplicatedStorage:FindFirstChild("LowHealthAnim"); if anim and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then trollTrack2=LocalPlayer.Character.Humanoid:LoadAnimation(anim); trollTrack2:Play() end elseif trollTrack2 then trollTrack2:Stop() end end)
end)
UI:AddToggle(TrollingTab, "🔗 Cuffing Animation", false, function(state)
    pcall(function() if state then local anim=ReplicatedStorage:FindFirstChild("cuffed"); if anim and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then trollTrack4=LocalPlayer.Character.Humanoid:LoadAnimation(anim); trollTrack4:Play() end elseif trollTrack4 then trollTrack4:Stop() end end)
end)
do
    local twerkAnim = nil
    local twerkRunning = false
    UI:AddToggle(TrollingTab, "Twerk", false, function(state)
        twerkRunning = state
        if state then
            task.spawn(function()
                local Animation = Instance.new("Animation")
                Animation.AnimationId = "rbxassetid://15693621070"
                local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
                local Humanoid = Character:WaitForChild("Humanoid")
                local LoadAnimation = Humanoid:WaitForChild("Animator"):LoadAnimation(Animation)
                twerkAnim = LoadAnimation
                LoadAnimation:Play()
                local Speed = 1; local Min = 1.6; local Max = 1.75
                LoadAnimation:AdjustSpeed(Speed); LoadAnimation.TimePosition = Min
                local Type = 1
                while task.wait() do
                    if not twerkRunning or not LoadAnimation.IsPlaying then break end
                    if Type == 1 then
                        if LoadAnimation.TimePosition >= Max then Type = 2; LoadAnimation.TimePosition = Max; LoadAnimation:AdjustSpeed(-Speed) end
                    elseif Type == 2 then
                        if LoadAnimation.TimePosition <= Min then Type = 1; LoadAnimation.TimePosition = Min; LoadAnimation:AdjustSpeed(Speed) end
                    end
                end
                twerkRunning = false
            end)
        else
            if twerkAnim then pcall(function() twerkAnim:Stop() end); twerkAnim = nil end
        end
    end)
end
UI:AddSection(TrollingTab, "👔 Outfits")
local outfitNames = {}
for name, _ in pairs(outfits) do table.insert(outfitNames, name) end
local selectedOutfit = outfitNames[1]
UI:AddDropdown(TrollingTab, "Outfit", outfitNames, outfitNames[1], function(opt) selectedOutfit = opt end)
UI:AddButton(TrollingTab, "Equip Outfit", function() equipOutfit(selectedOutfit); Notify("Outfit", selectedOutfit, 3) end)
UI:AddSection(SettingsTab, "⚙️ GUI Settings")
UI:AddButton(SettingsTab, "Copy Discord Link", function() pcall(function() setclipboard("https://discord.gg/cD42ETQ9jd") end); Notify("Discord","Copied!",2) end)
UI:AddButton(SettingsTab, "Reset GUI Position", function() MainFrame.Position=UDim2.new(0.5,-currentWidth/2,0.5,-currentHeight/2); Notify("GUI","Position reset!",2) end)
UI:AddButton(SettingsTab, "Rejoin Server", function() pcall(function() game:GetService("TeleportService"):Teleport(game.PlaceId,LocalPlayer) end) end)
UI:AddButton(SettingsTab, "Leave Game", function() pcall(function() LocalPlayer:Kick("Left via Jointhub.gg") end) end)
UI:AddButton(SettingsTab, "🔀 Server Hop", function() pcall(function() loadstring(game:HttpGet("https://[Log in to view URL]"))() end); Notify("Server","Hopping...",2) end)
UI:AddSection(SettingsTab, "🎨 Theme")
do
    local themeColors = {
        {name="🟢 Green",  a=Color3.fromRGB(0,200,80),   b=Color3.fromRGB(60,255,140)},
        {name="🟣 Purple", a=Color3.fromRGB(180,0,255),  b=Color3.fromRGB(220,80,255)},
        {name="🔵 Blue",   a=Color3.fromRGB(0,180,255),  b=Color3.fromRGB(80,220,255)},
        {name="🟡 Yellow", a=Color3.fromRGB(255,220,0),  b=Color3.fromRGB(255,240,80)},
        {name="🔴 Red",    a=Color3.fromRGB(255,50,80),  b=Color3.fromRGB(255,120,120)},
    }
    local themeIdx = 1
    local themeBtn = UI:AddButton(SettingsTab, "Color Theme", function()
        themeIdx = (themeIdx % #themeColors) + 1
        local t = themeColors[themeIdx]
        Colors.Accent = t.a
        pcall(function()
            MainStroke.Color = t.a
            for _,s in pairs(MainFrame:GetDescendants()) do
                if s:IsA("UIStroke") then pcall(function() s.Color = t.a end) end
            end
        end)
        if themeBtn then themeBtn.BackgroundColor3 = t.a; themeBtn.Text = "Color Theme" end
        Notify("Theme", t.name.." applied!", 2)
    end)
    if themeBtn then themeBtn.BackgroundColor3 = themeColors[1].a end
end
UI:AddSection(SettingsTab, "⌨️ Keybinds")
do
    local keyNames = {"None","Y","U","I","O","P","G","H","J","K","L","Z","X","C","V","B","N","M","F","T","R","E","Q"}
    local keyMap = {}
    for _,k in ipairs(keyNames) do
        if k ~= "None" then keyMap[k] = Enum.KeyCode[k] end
    end
    getgenv().wsFlyKeybind    = Enum.KeyCode.U
    getgenv().wsWalkKeybind   = Enum.KeyCode.B
    getgenv().wsCarFlyKeybind = Enum.KeyCode.O
    UI:AddDropdown(SettingsTab, "Fly Key", keyNames, "U", function(v)
        getgenv().wsFlyKeybind = keyMap[v] or nil
        Notify("Keybind", "Fly: "..(v == "None" and "cleared" or v), 2)
    end)
    UI:AddDropdown(SettingsTab, "Walk Speed Key", keyNames, "B", function(v)
        getgenv().wsWalkKeybind = keyMap[v] or nil
        Notify("Keybind", "Walk: "..(v == "None" and "cleared" or v), 2)
    end)
    UI:AddDropdown(SettingsTab, "Car Fly Key", keyNames, "O", function(v)
        getgenv().wsCarFlyKeybind = keyMap[v] or nil
        Notify("Keybind", "Car Fly: "..(v == "None" and "cleared" or v), 2)
    end)
    UserInputService.InputBegan:Connect(function(inp, gpe)
        if gpe then return end
        if getgenv().wsFlyKeybind and inp.KeyCode == getgenv().wsFlyKeybind then UI:Fire("Player Fly") end
        if getgenv().wsWalkKeybind and inp.KeyCode == getgenv().wsWalkKeybind then UI:Fire("WalkSpeed (3s delay)") end
        if getgenv().wsCarFlyKeybind and inp.KeyCode == getgenv().wsCarFlyKeybind then UI:Fire("Car Fly") end
    end)
end
UI:AddSection(SettingsTab, "🛡️ Extra Features")
UI:AddToggle(SettingsTab, "🛡️ Anti AFK", false, function(enabled)
    getgenv().AntiAFK = enabled
    if enabled then local vu=game:GetService("VirtualUser"); LocalPlayer.Idled:Connect(function() if getgenv().AntiAFK then vu:CaptureController(); vu:ClickButton2(Vector2.new()); Notify("Anti-AFK","Triggered!",2) end end); Notify("Anti-AFK","Enabled",2) end
end)
UI:AddToggle(SettingsTab, "⚡ FPS Booster", false, function(enabled)
    if enabled then settings().Rendering.QualityLevel=Enum.QualityLevel.Level01; for _,v in pairs(workspace:GetDescendants()) do if v:IsA("Part") or v:IsA("MeshPart") then v.Material=Enum.Material.SmoothPlastic; v.Reflectance=0 elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then v.Enabled=false end end; Notify("FPS","Boost Applied!",2) end
end)
UI:AddToggle(SettingsTab, "☀️ Lock to Day", false, function(enabled) if enabled then game:GetService("Lighting").ClockTime=12; Notify("Time","Locked to day!",2) end end)
UI:AddToggle(SettingsTab, "🌙 Lock to Night", false, function(enabled) if enabled then game:GetService("Lighting").ClockTime=0; Notify("Time","Locked to night!",2) end end)
UI:AddButton(SettingsTab, "⚡ Load Admin Commands", function() pcall(function() loadstring(game:HttpGet('https://[Log in to view URL]'))() end); Notify("Loaded","Admin Commands!",2) end)
UI:AddButton(SettingsTab, "🔍 Load Dex Explorer", function() pcall(function() loadstring(game:HttpGet("https://[Log in to view URL]"))() end); Notify("Loaded","Dex Explorer!",2) end)
UI:AddSection(QuickBuysTab, "🔫 Guns & Ammo")
local quickBuyGuns = {"🔫 Draco + 7.62","🔫 Clear Mag Drac + 7.62","🔫 AR Pistol + 5.56","🔫 223 Tan + 5.56","🔫 HP Browning Ext","🔫 Glock 17 Ext","🔫 Glock 22 Ext","🔫 Springfield XD Ext"}
UI:AddDropdown(QuickBuysTab, "Buy Guns", quickBuyGuns, quickBuyGuns[1], function(val)
    pcall(function()
        if val=="🔫 Draco + 7.62" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("Draco"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer("7.62")
        elseif val=="🔫 Clear Mag Drac + 7.62" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("ClearMagDrac"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer("7.62")
        elseif val=="🔫 AR Pistol + 5.56" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("ARPistol"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer("5.56")
        elseif val=="🔫 223 Tan + 5.56" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("223Tan"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer("5.56")
        elseif val=="🔫 HP Browning Ext" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("HPBrowning Ext"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer(".Extended")
        elseif val=="🔫 Glock 17 Ext" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("Glock17"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer(".Extended")
        elseif val=="🔫 Glock 22 Ext" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("Glock22"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer(".Extended")
        elseif val=="🔫 Springfield XD Ext" then ReplicatedStorage:WaitForChild("ShopRemote5"):InvokeServer("SpringField XD"); task.wait(0.1); ReplicatedStorage.ExoticShopRemote:InvokeServer(".Extended")
        end
    end)
    Notify("Bought", val, 2)
end)
local exoticItems = {"FakeCard","Ice-Fruit Bag","Ice-Fruit Cupz","FijiWater","FreshWater","G26","Lemonade","Sledge Hammer","Screw","Bandage"}
UI:AddDropdown(QuickBuysTab, "🐍 Exotic Items", exoticItems, exoticItems[1], function(val) pcall(function() ReplicatedStorage.ExoticShopRemote:InvokeServer(val) end); Notify("Bought",val,2) end)
UI:AddSection(QuickBuysTab, "🛍️ Main Shop")
local quickBuyShop = {"Shiesty","BluGloves","WhiteGloves","BlackGloves","Water","YelloCamoGloves","RedCamoGloves","PurpleCamoGloves","RawChicken","RawSteak","WhiteShiesty"}
UI:AddDropdown(QuickBuysTab, "Shop Items", quickBuyShop, quickBuyShop[1], function(val) pcall(function() ReplicatedStorage:WaitForChild("ShopRemote"):InvokeServer(val) end); Notify("Bought",val,2) end)
UI:AddSection(QuickBuysTab, "📦 Ammo & Mags")
local ammoItems = {"Extended Mag","Drum Mag","10mm Ammo","FN Mag","9mm Ammo","7.62 Ammo","5.56 Ammo"}
UI:AddDropdown(QuickBuysTab, "Ammo/Mags", ammoItems, ammoItems[1], function(val)
    pcall(function()
        if val=="Extended Mag" then ReplicatedStorage.ExoticShopRemote:InvokeServer(".Extended")
        elseif val=="Drum Mag" then ReplicatedStorage.ExoticShopRemote:InvokeServer(".Drum")
        elseif val=="10mm Ammo" then ReplicatedStorage.ExoticShopRemote:InvokeServer(".10mm")
        elseif val=="FN Mag" then ReplicatedStorage.ExoticShopRemote:InvokeServer(".FNMag")
        elseif val=="9mm Ammo" then ReplicatedStorage.ExoticShopRemote:InvokeServer("9mm")
        elseif val=="7.62 Ammo" then ReplicatedStorage.ExoticShopRemote:InvokeServer("7.62")
        elseif val=="5.56 Ammo" then ReplicatedStorage.ExoticShopRemote:InvokeServer("5.56") end
    end)
    Notify("Bought", val, 2)
end)
UI:AddSection(QuickBuysTab, "🎒 Bags")
local bagItems = {}
pcall(function() if ReplicatedStorage:FindFirstChild("BACKPACK_HATS") and ReplicatedStorage.BACKPACK_HATS:FindFirstChild("Accessories") then for _,item in ipairs(ReplicatedStorage.BACKPACK_HATS.Accessories:GetChildren()) do table.insert(bagItems,item.Name) end end end)
if #bagItems == 0 then bagItems = {"SmallBag","MediumBag","LargeBag"} end
UI:AddDropdown(QuickBuysTab, "🎒 Buy Bags", bagItems, bagItems[1], function(val)
    task.spawn(function()
        local char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
        local hrp = char:WaitForChild("HumanoidRootPart", 5)
        if not hrp then Notify("Error","No character",2) return end
        local item = workspace:FindFirstChild(val) or workspace:FindFirstChild(val, true)
        if not item then Notify("Error", val.." not found!", 2) return end
        local prompt = findProximityPromptRecursive(item)
        if not prompt then Notify("Error","No prompt on "..val, 2) return end
        local tCF
        if prompt.Parent and prompt.Parent:IsA("BasePart") then tCF = prompt.Parent.CFrame
        elseif item:IsA("Model") and item.PrimaryPart then tCF = item.PrimaryPart.CFrame
        elseif item:IsA("BasePart") then tCF = item.CFrame
        else local p = item:FindFirstChildWhichIsA("BasePart"); tCF = p and p.CFrame or CFrame.new(hrp.Position) end
        local orig = hrp.CFrame
        Notify("Buying", val.."...", 2)
        getgenv().SwimMethod = true
        task.wait(1)
        hrp.CFrame = tCF
        task.wait(0.5)
        prompt.HoldDuration = 0; prompt.MaxActivationDistance = 30
        for _ = 1, 10 do pcall(function() prompt:InputHoldBegin(); prompt:InputHoldEnd() end); task.wait(0.1) end
        prompt.MaxActivationDistance = 6
        task.wait(0.3)
        hrp.CFrame = orig
        getgenv().SwimMethod = false
        Notify("✅ Bought", val, 2)
    end)
end)
UI:AddSection(QuickBuysTab, "🔫 Other Items")
local otherItems = {}
pcall(function()
    local seen={}; local gunsFolder=workspace:FindFirstChild("GUNS"); local source=gunsFolder and gunsFolder:GetChildren() or workspace:GetChildren()
    for _,gun in ipairs(source) do if (gun:IsA("Model") or gun:IsA("Tool")) and gun.Name~="Basketball" and gun.Name~="Loader" and not seen[gun.Name] then seen[gun.Name]=true; table.insert(otherItems,gun.Name) end end
    table.sort(otherItems)
end)
if #otherItems == 0 then otherItems = {"Draco","Glock17","ARPistol"} end
UI:AddDropdown(QuickBuysTab, "🔫 Other Items", otherItems, otherItems[1], function(val)
    task.spawn(function()
        local char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
        local hrp = char:WaitForChild("HumanoidRootPart", 5)
        if not hrp then return end
        local item = (workspace:FindFirstChild("GUNS") and workspace.GUNS:FindFirstChild(val))
            or workspace:FindFirstChild(val) or workspace:FindFirstChild(val, true)
        if not item then Notify("Error", val.." not found!", 2) return end
        local prompt = findProximityPromptRecursive(item)
        if not prompt then Notify("Error","No prompt on "..val, 2) return end
        local tCF
        if prompt.Parent and prompt.Parent:IsA("BasePart") then tCF = prompt.Parent.CFrame
        elseif item:IsA("Model") and item.PrimaryPart then tCF = item.PrimaryPart.CFrame
        elseif item:IsA("BasePart") then tCF = item.CFrame
        else local p = item:FindFirstChildWhichIsA("BasePart"); tCF = p and p.CFrame or CFrame.new(hrp.Position) end
        local orig = hrp.CFrame
        Notify("Buying", val.."...", 2)
        getgenv().SwimMethod = true
        task.wait(1)
        hrp.CFrame = tCF
        task.wait(0.5)
        prompt.HoldDuration = 0; prompt.MaxActivationDistance = 30
        for _ = 1, 5 do pcall(function() prompt:InputHoldBegin(); prompt:InputHoldEnd() end); task.wait(0.1) end
        prompt.MaxActivationDistance = 6
        task.wait(0.3)
        hrp.CFrame = orig
        getgenv().SwimMethod = false
        Notify("✅ Bought", val, 2)
    end)
end)
UI:AddSection(CreditsTab, "⚙️ UI Settings & Info")
local deviceInfo = ExecutorSupport.Mobile and "Mobile (Touch)" or "Desktop"
UI:AddButton(CreditsTab, "📱 Device: " .. deviceInfo, function() end)
UI:AddButton(CreditsTab, "⚡ Executor: " .. ExecutorSupport.Executor, function() end)
UI:AddButton(CreditsTab, "Press RightShift to toggle GUI", function() end)
UI:AddButton(CreditsTab, "📋 Copy Discord Link", function() pcall(function() setclipboard("https://discord.gg/cD42ETQ9jd") end); Notify("Discord","Link copied!",2) end)
UI:AddButton(CreditsTab, "🏷️ Remove Name Tag", function()
    pcall(function() local head=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Head"); if head then local tag=head:FindFirstChild("JointhubTag"); if tag then tag:Destroy() end end end)
    Notify("Tag","Removed!",2)
end)
UI:AddSection(CreditsTab, "🔄 Server")
UI:AddButton(CreditsTab, "🔄 Rejoin Server", function() game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId,game.JobId) end)
UI:AddButton(CreditsTab, "🔀 Server Hop", function() pcall(function() loadstring(game:HttpGet("https://[Log in to view URL]"))() end); Notify("Server","Hopping...",2) end)
UI:AddButton(CreditsTab, "❌ Leave Game", function() pcall(function() LocalPlayer:Kick("Left via Jointhub.gg") end) end)
UI:AddSection(CreditsTab, "📝 Credits")
UI:AddButton(CreditsTab, "Leaked By Jointhub.gg", function() pcall(function() setclipboard("https://discord.gg/cD42ETQ9jd") end); Notify("Jointhub","Link copied!",2) end)
UI:AddButton(CreditsTab, "Join the Discord for the key", function() pcall(function() setclipboard("https://discord.gg/cD42ETQ9jd") end); Notify("Jointhub","Link copied!",2) end)
UI:AddButton(CreditsTab, "discord.gg/cD42ETQ9jd", function() pcall(function() setclipboard("https://discord.gg/cD42ETQ9jd") end); Notify("Discord","Link copied!",2) end)
UserInputService.InputBegan:Connect(function(input, processed)
    if processed then return end
    if input.KeyCode == Enum.KeyCode.RightShift then MainFrame.Visible = not MainFrame.Visible end
end)
LocalPlayer.CharacterAdded:Connect(function(char)
    task.wait(1)
    if nametagEnabled then CreateNametag(char) end
    applyEffects()
    if AntiLoseEnabled then
        local humanoid = char:WaitForChild("Humanoid")
        humanoid.Died:Connect(function()
            task.wait(0.25)
            for _, tool in ipairs(LocalPlayer.Backpack:GetChildren()) do
                if tool:IsA("Tool") and not table.find(ExemptItems, tool.Name) then ForcePutToMarket(tool.Name) end
            end
        end)
    end
end)
LocalPlayer.CharacterAdded:Connect(function()
    task.delay(2.5, function()
        if AntiLoseEnabled then
            local market = ReplicatedStorage:FindFirstChild("MarketItems")
            if market then for _, item in ipairs(market:GetChildren()) do if item:FindFirstChild("owner") and item.owner.Value == LocalPlayer.Name then ForceRetrieveFromMarket(item.Name) end end end
        end
    end)
end)
if LocalPlayer.Character and nametagEnabled then CreateNametag(LocalPlayer.Character) end
task.spawn(function()
    while true do
        task.wait(0.1)
        if _G.respawn then
            local char = LocalPlayer.Character
            if char and char:FindFirstChild("Humanoid") and char.Humanoid.Health <= 0 then
                pcall(function() ReplicatedStorage.RespawnRE:FireServer() end)
            end
        end
    end
end)
task.spawn(function()
    if not ExecutorSupport.Mobile then
        local MouseDotGui = Instance.new("ScreenGui"); MouseDotGui.Name="JointhubMouseDot"; MouseDotGui.DisplayOrder=999999
        MouseDotGui.IgnoreGuiInset=true; MouseDotGui.ResetOnSpawn=false; MouseDotGui.Parent=CoreGui
        local MouseDot = Instance.new("Frame"); MouseDot.Name="Dot"; MouseDot.Size=UDim2.new(0,8,0,8)
        MouseDot.BackgroundColor3=Color3.fromRGB(255,255,255); MouseDot.BorderSizePixel=0; MouseDot.AnchorPoint=Vector2.new(0.5,0.5); MouseDot.Parent=MouseDotGui
        Instance.new("UICorner",MouseDot).CornerRadius=UDim.new(1,0)
        RunService.RenderStepped:Connect(function() local mousePos=UserInputService:GetMouseLocation(); MouseDot.Position=UDim2.new(0,mousePos.X,0,mousePos.Y) end)
    end
end)
local function CleanupCarFly()
    if bv then bv:Destroy(); bv = nil end
    if bg then bg:Destroy(); bg = nil end
end
local function SetupCarFly()
    CleanupCarFly()
    if not Config.TheBronx.carfly then return end
    local char = LocalPlayer.Character; if not char then return end
    hum = char:FindFirstChildWhichIsA("Humanoid"); if not hum then return end
    seat = hum.SeatPart; if not seat or not seat:IsA("VehicleSeat") then return end
    car = seat.Parent; if not car then return end
    root = car.PrimaryPart; if not root then return end
    lastCar = car
    for _, v in ipairs(car:GetChildren()) do if v:IsA("BasePart") and not v.Name:lower():find("wheel") then v.CanCollide = false end end
    bv = Instance.new("BodyVelocity"); bv.MaxForce=Vector3.new(1e9,1e9,1e9); bv.Velocity=Vector3.zero; bv.Parent=root
    bg = Instance.new("BodyGyro"); bg.MaxTorque=Vector3.new(1e9,1e9,1e9); bg.P=25000; bg.D=1500; bg.CFrame=root.CFrame; bg.Parent=root
end
task.spawn(function()
    while true do
        task.wait(0.2)
        local char = LocalPlayer.Character
        if char then
        local h = char:FindFirstChildWhichIsA("Humanoid")
        if h then
        local currentSeat = h.SeatPart
        if currentSeat and currentSeat:IsA("VehicleSeat") then
            if currentSeat.Parent ~= lastCar then SetupCarFly() end
        else
            if lastCar then CleanupCarFly(); lastCar = nil end
        end
        end
        end
    end
end)
RunService.RenderStepped:Connect(function()
    if not Config.TheBronx.carfly then CleanupCarFly(); return end
    if not hum or hum.SeatPart ~= seat then return end
    if not root or not bv or not bg then SetupCarFly(); return end
    local carSpeed = Config.TheBronx.carflyspeed or 120
    local cam = workspace.CurrentCamera; local camCF = cam.CFrame
    local camLook = camCF.LookVector; local camRight = camCF.RightVector
    if not UserInputService.TouchEnabled then
        if UserInputService:IsMouseButtonPressed(Enum.UserInputType.MouseButton2) then bg.CFrame = CFrame.lookAt(root.Position, root.Position + camLook) end
        local move = Vector3.zero
        if UserInputService:IsKeyDown(Enum.KeyCode.W) then move = move + camLook end
        if UserInputService:IsKeyDown(Enum.KeyCode.S) then move = move - camLook end
        if UserInputService:IsKeyDown(Enum.KeyCode.A) then move = move - camRight end
        if UserInputService:IsKeyDown(Enum.KeyCode.D) then move = move + camRight end
        bv.Velocity = move.Magnitude > 0 and move.Unit * carSpeed or Vector3.zero
    else
        bg.CFrame = CFrame.lookAt(root.Position, root.Position + camLook)
        local move = hum.MoveDirection; local velocity = Vector3.zero
        if move.Magnitude > 0 then
            local camRight2 = camCF.RightVector; local camLook2 = Vector3.new(camCF.LookVector.X,0,camCF.LookVector.Z).Unit
            velocity = (camRight2 * move.X) + (camLook2 * -move.Z); velocity = velocity * carSpeed
        end
        local humanoid = LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid")
        if humanoid and humanoid:GetState() == Enum.HumanoidStateType.Jumping then velocity = velocity + Vector3.new(0, carSpeed * 0.8, 0) end
        bv.Velocity = velocity
    end
end)
do
local espColorMap={Red=Color3.fromRGB(255,0,0),Purple=Color3.fromRGB(138,43,226),Green=Color3.fromRGB(0,255,0),Blue=Color3.fromRGB(0,170,255),White=Color3.fromRGB(255,255,255),Yellow=Color3.fromRGB(255,255,0),Cyan=Color3.fromRGB(0,255,255),Orange=Color3.fromRGB(255,165,0),Pink=Color3.fromRGB(255,105,180)}
local chamsFillColor=Color3.fromRGB(138,43,226); local chamsOutlineColor=Color3.fromRGB(255,0,255)
local ESPSettings={Enabled=false,BoxESP=false,BoxFill=false,BoxCorners=false,NameESP=false,HealthESP=false,TracerESP=false,DistanceESP=false,Box3DESP=false,BoxColor=Color3.fromRGB(255,0,0),TracerColor=Color3.fromRGB(0,255,0),TextColor=Color3.fromRGB(255,255,255),MaxDistance=800}
local ESPObjects={}; local ChamsHighlights={}
local function CreateESPForPlayer(plr)
    if plr==LocalPlayer or ESPObjects[plr] then return end
    local corners={}; for i=1,8 do local ln=Drawing.new("Line"); ln.Thickness=2; ln.Color=ESPSettings.BoxColor; ln.Visible=false; corners[i]=ln end
    local b3d={}; for i=1,12 do local ln=Drawing.new("Line"); ln.Thickness=1; ln.Color=ESPSettings.BoxColor; ln.Visible=false; b3d[i]=ln end
    ESPObjects[plr]={Box=Drawing.new("Square"),Corners=corners,Name=Drawing.new("Text"),Health=Drawing.new("Text"),Distance=Drawing.new("Text"),Tracer=Drawing.new("Line"),TracerOutline=Drawing.new("Line"),Box3D=b3d}
    local e=ESPObjects[plr]; e.Box.Thickness=1; e.Box.Filled=false; e.Box.Color=ESPSettings.BoxColor; e.Box.Visible=false
    e.Name.Size=14; e.Name.Center=true; e.Name.Outline=true; e.Name.Color=ESPSettings.TextColor; e.Name.Visible=false
    e.Health.Size=12; e.Health.Center=true; e.Health.Outline=true; e.Health.Color=Color3.fromRGB(0,255,0); e.Health.Visible=false
    e.Distance.Size=12; e.Distance.Center=true; e.Distance.Outline=true; e.Distance.Color=Color3.fromRGB(255,255,0); e.Distance.Visible=false
    e.Tracer.Thickness=1; e.Tracer.Color=ESPSettings.TracerColor; e.Tracer.Visible=false
    e.TracerOutline.Thickness=3; e.TracerOutline.Color=Color3.new(0,0,0); e.TracerOutline.Visible=false
end
local function RemoveESPForPlayer(plr)
    if not ESPObjects[plr] then return end; local e=ESPObjects[plr]
    for _,ln in ipairs(e.Box3D or {}) do pcall(function() ln:Remove() end) end
    for _,ln in ipairs(e.Corners or {}) do pcall(function() ln:Remove() end) end
    for k,d in pairs(e) do if k~="Box3D" and k~="Corners" then pcall(function() d:Remove() end) end end
    ESPObjects[plr]=nil
end
local EDGES={{1,2},{2,3},{3,4},{4,1},{5,6},{6,7},{7,8},{8,5},{1,5},{2,6},{3,7},{4,8}}
local function UpdateESP()
    if not ESPSettings.Enabled then for _,e in pairs(ESPObjects) do pcall(function() e.Box.Visible=false; e.Name.Visible=false; e.Health.Visible=false; e.Distance.Visible=false; e.Tracer.Visible=false; e.TracerOutline.Visible=false; for _,ln in ipairs(e.Corners or {}) do ln.Visible=false end; for _,ln in ipairs(e.Box3D or {}) do ln.Visible=false end end) end; return end
    local cam=workspace.CurrentCamera; local vp=cam.ViewportSize
    for plr,e in pairs(ESPObjects) do pcall(function()
        local char=plr.Character; local hum=char and char:FindFirstChildOfClass("Humanoid"); local hrp=char and char:FindFirstChild("HumanoidRootPart"); local head=char and char:FindFirstChild("Head")
        local function hide() e.Box.Visible=false; e.Name.Visible=false; e.Health.Visible=false; e.Distance.Visible=false; e.Tracer.Visible=false; e.TracerOutline.Visible=false; for _,ln in ipairs(e.Corners or {}) do ln.Visible=false end; for _,ln in ipairs(e.Box3D or {}) do ln.Visible=false end end
        if not(char and hum and hrp and head and hum.Health>0) then hide(); return end
        local rp,on=cam:WorldToViewportPoint(hrp.Position); local hp2=cam:WorldToViewportPoint(head.Position+Vector3.new(0,0.5,0)); local lp2=cam:WorldToViewportPoint(hrp.Position-Vector3.new(0,3,0))
        local dist=(hrp.Position-cam.CFrame.Position).Magnitude
        if not(on and rp.Z>0 and dist<=ESPSettings.MaxDistance) then hide(); return end
        local bH=math.abs(hp2.Y-lp2.Y); local bW=math.max(bH/2,10)
        if ESPSettings.BoxESP then e.Box.Filled=ESPSettings.BoxFill; e.Box.Size=Vector2.new(bW,bH); e.Box.Position=Vector2.new(rp.X-bW/2,hp2.Y); e.Box.Color=ESPSettings.BoxColor; e.Box.Visible=true else e.Box.Visible=false end
        if ESPSettings.BoxCorners and e.Corners then
            local bx=rp.X-bW/2; local by=hp2.Y; local cw=math.max(bW*.25,5); local ch=math.max(bH*.25,5); local col=ESPSettings.BoxColor; local co=e.Corners
            co[1].From=Vector2.new(bx,by); co[1].To=Vector2.new(bx+cw,by); co[2].From=Vector2.new(bx,by); co[2].To=Vector2.new(bx,by+ch)
            co[3].From=Vector2.new(bx+bW,by); co[3].To=Vector2.new(bx+bW-cw,by); co[4].From=Vector2.new(bx+bW,by); co[4].To=Vector2.new(bx+bW,by+ch)
            co[5].From=Vector2.new(bx,by+bH); co[5].To=Vector2.new(bx+cw,by+bH); co[6].From=Vector2.new(bx,by+bH); co[6].To=Vector2.new(bx,by+bH-ch)
            co[7].From=Vector2.new(bx+bW,by+bH); co[7].To=Vector2.new(bx+bW-cw,by+bH); co[8].From=Vector2.new(bx+bW,by+bH); co[8].To=Vector2.new(bx+bW,by+bH-ch)
            for _,ln in ipairs(co) do ln.Color=col; ln.Visible=true end
        elseif e.Corners then for _,ln in ipairs(e.Corners) do ln.Visible=false end end
        if ESPSettings.NameESP then e.Name.Text=plr.Name; e.Name.Position=Vector2.new(rp.X,hp2.Y-18); e.Name.Color=ESPSettings.TextColor; e.Name.Visible=true else e.Name.Visible=false end
        if ESPSettings.HealthESP then local hp=math.clamp(hum.Health/hum.MaxHealth,0,1); e.Health.Text=math.floor(hp*100).."%"; e.Health.Position=Vector2.new(rp.X,lp2.Y+5); e.Health.Color=Color3.fromRGB(math.floor((1-hp)*255),math.floor(hp*255),0); e.Health.Visible=true else e.Health.Visible=false end
        if ESPSettings.DistanceESP then e.Distance.Text="["..math.floor(dist).."m]"; e.Distance.Position=Vector2.new(rp.X,lp2.Y+18); e.Distance.Visible=true else e.Distance.Visible=false end
        if ESPSettings.TracerESP then local fr=Vector2.new(vp.X/2,vp.Y); local to=Vector2.new(rp.X,lp2.Y); e.TracerOutline.From=fr; e.TracerOutline.To=to; e.TracerOutline.Visible=true; e.Tracer.From=fr; e.Tracer.To=to; e.Tracer.Color=ESPSettings.TracerColor; e.Tracer.Visible=true else e.Tracer.Visible=false; e.TracerOutline.Visible=false end
    end) end
end
for _,plr in pairs(Players:GetPlayers()) do CreateESPForPlayer(plr) end
Players.PlayerAdded:Connect(CreateESPForPlayer)
Players.PlayerRemoving:Connect(RemoveESPForPlayer)
RunService.RenderStepped:Connect(UpdateESP)
local function ApplyChams(plr)
    if plr==LocalPlayer or not plr.Character then return end
    pcall(function()
        local old=plr.Character:FindFirstChild("WalChams"); if old then old:Destroy() end
        local hi=Instance.new("Highlight"); hi.Name="WalChams"; hi.FillColor=chamsFillColor; hi.OutlineColor=chamsOutlineColor
        hi.FillTransparency=0.4; hi.OutlineTransparency=0; hi.Adornee=plr.Character; hi.Parent=plr.Character; ChamsHighlights[plr]=hi
    end)
end
local function RefreshChams()
    if not getgenv().ChamsEnabled then return end
    for _,plr in pairs(Players:GetPlayers()) do ApplyChams(plr) end
end
local VisualsTab = UI:AddTab("Visuals","👁️",3.5)

do

    local _tracerModes = {beam=false,blind=false,bigbox=false,plane=false,bigball=false,pole=false,cross=false}
    pcall(function() getgenv()._tracerModes = _tracerModes end)
    local function _VB(tool,dir,color,size,shape,mat)
        if not tool then return end
        local h=tool:FindFirstChild("Handle"); if not h then return end
        local gsl=tool:FindFirstChild("GunScript_Local"); if not gsl then return end
        local fp=h:FindFirstChild("GunFirePoint") or h
        pcall(function() ReplicatedStorage.VisualizeBullet:FireServer(tool,h,dir,fp,{true,{112139677907600,92977228204408},1,1,10,gsl:FindFirstChild("HitEffect"),true},{false,{},1,1,1,nil},{false,0,{},false,0,0},{false,0,false,{},0,0,0,false,nil},{true,Vector3.new(0.1,0,0),Vector3.new(-0.1,0,0),gsl:FindFirstChild("TracerEffect"),nil,gsl:FindFirstChild("ParticleEffect"),300,526,0,Vector3.zero,size,color,0,mat,shape,false,6696543809,0,Vector3.new(0.007,0.007,0.007)},{false,{},0.5,1,1,100},{false,0,Color3.new(1,0.647,0.6),0,false}) end)
    end
    local function _Beam(from,to,color,thick,dur)
        local d=(to-from).Magnitude; if d<0.1 then return end
        local p=Instance.new("Part"); p.Size=Vector3.new(thick,thick,d); p.CFrame=CFrame.new((from+to)/2,to); p.Anchored=true; p.CanCollide=false; p.Material=Enum.Material.Neon; p.Color=color; p.Parent=workspace
        TweenService:Create(p,TweenInfo.new(dur),{Transparency=1}):Play(); task.delay(dur+0.1,function() pcall(function() p:Destroy() end) end)
    end
    local _MFNS={
        beam=function(f,t,tool,dir) _Beam(f,t,Color3.fromRGB(0,200,255),0.28,0.5); _VB(tool,dir,Color3.fromRGB(0,200,255),Vector3.new(0.25,0.25,0.25),Enum.PartType.Cylinder,Enum.Material.Neon) end,
        blind=function(f,t,tool,dir) _Beam(f,t,Color3.new(1,1,1),0.5,0.4); task.spawn(function() for i=1,15 do _VB(tool,dir,Color3.new(1,1,1),Vector3.new(3,3,3),Enum.PartType.Ball,Enum.Material.Neon); task.wait(0.06) end end) end,
        bigbox=function(f,t,tool,dir) local c2=Color3.fromRGB(255,40,40); _Beam(f,t,c2,0.35,0.5); task.spawn(function() for i=1,10 do _VB(tool,dir,c2,Vector3.new(4,4,4),Enum.PartType.Block,Enum.Material.Neon); task.wait(0.05) end end) end,
        bigball=function(f,t,tool,dir) local c2=Color3.fromRGB(0,255,150); _Beam(f,t,c2,0.35,0.5); task.spawn(function() for i=1,10 do _VB(tool,dir,c2,Vector3.new(4,4,4),Enum.PartType.Ball,Enum.Material.Neon); task.wait(0.05) end end) end,
        pole=function(f,t,tool,dir) local c2=Color3.fromRGB(255,80,255); _Beam(f,t,c2,0.3,0.5); task.spawn(function() for i=1,10 do _VB(tool,dir,c2,Vector3.new(1,1,1),Enum.PartType.Cylinder,Enum.Material.Neon); task.wait(0.05) end end) end,
        cross=function(f,t,tool,dir) local c2=Color3.fromRGB(255,220,0); _Beam(f,t,c2,0.3,0.5); task.spawn(function() for i=1,8 do _VB(tool,dir,c2,Vector3.new(0.5,0.5,0.5),Enum.PartType.Cylinder,Enum.Material.Neon); task.wait(0.05) end end) end,
        plane=function(f,t,tool,dir) local c2=Color3.fromRGB(150,200,255); _Beam(f,t,c2,0.3,0.5); task.spawn(function() for i=1,8 do _VB(tool,dir,c2,Vector3.new(2,2,2),Enum.PartType.Block,Enum.Material.Neon); task.wait(0.06) end end) end,
    }
    local function _shootTracers(tool)
        local char=LocalPlayer.Character; if not char then return end
        local handle=tool:FindFirstChild("Handle"); if not handle then return end
        local cam=workspace.CurrentCamera; local dir=cam.CFrame.LookVector; local from=handle.Position
        local params=RaycastParams.new(); params.FilterType=Enum.RaycastFilterType.Exclude; params.FilterDescendantsInstances={char}
        local result=workspace:Raycast(from,dir*800,params); local to=result and result.Position or (from+dir*800)
        for k,v in pairs(_tracerModes) do if v and _MFNS[k] then task.spawn(_MFNS[k],from,to,tool,dir) end end
    end
    local function _hookGun(t) t.Activated:Connect(function() _shootTracers(t) end) end
    local function _hookChar(ch) ch.ChildAdded:Connect(function(c2) if c2:IsA("Tool") then _hookGun(c2) end end); for _,c2 in ipairs(ch:GetChildren()) do if c2:IsA("Tool") then _hookGun(c2) end end end
    if LocalPlayer.Character then _hookChar(LocalPlayer.Character) end
    LocalPlayer.CharacterAdded:Connect(_hookChar)

    UI:AddSection(VisualsTab, "🔫 Bullet Tracers")
    UI:AddToggle(VisualsTab, "Blue Balls Tracer", false, function(v) _tracerModes.beam=v end)
    UI:AddToggle(VisualsTab, "White Ball Tracer", false, function(v) _tracerModes.blind=v end)
    UI:AddToggle(VisualsTab, "Red Box Tracer", false, function(v) _tracerModes.bigbox=v end)
    UI:AddToggle(VisualsTab, "Neon Blue Tracer", false, function(v) _tracerModes.plane=v end)
    UI:AddToggle(VisualsTab, "Cyan Ball Tracer", false, function(v) _tracerModes.bigball=v end)
    UI:AddToggle(VisualsTab, "Pink Tracers", false, function(v) _tracerModes.pole=v end)
    UI:AddToggle(VisualsTab, "Yellow Tracer", false, function(v) _tracerModes.cross=v end)

    local CarModsTab = UI:AddTab("Car Mods", "🚗", 3.7)

    UI:AddSection(CarModsTab, "⛽ Fuel")
    local _infFuelConn
    UI:AddToggle(CarModsTab, "Inf Fuel", false, function(state)
        if _infFuelConn then _infFuelConn:Disconnect(); _infFuelConn=nil end
        if not state then return end
        local pumps, lastScan = {}, 0
        _infFuelConn = RunService.Heartbeat:Connect(function()
            local char=LocalPlayer.Character; if not char then return end
            local hum=char:FindFirstChild("Humanoid"); if not hum or not hum.SeatPart then return end
            local hrp=char:FindFirstChild("HumanoidRootPart"); if not hrp then return end
            if tick()-lastScan > 4 then
                lastScan=tick(); pumps={}
                local map=workspace:FindFirstChild("1# Map")
                if map then for _,v in ipairs(map:GetDescendants()) do if v.Name=="#Pump" and v:IsA("MeshPart") then pumps[#pumps+1]=v end end end
            end
            for _,v in ipairs(pumps) do
                if v.Parent and (v.Position-hrp.Position).Magnitude <= 18.5 then
                    if not LocalPlayer:GetAttribute("PaidGas") then pcall(function() ReplicatedStorage.RequestRefill:FireServer("Purchase") end) end
                    if LocalPlayer:GetAttribute("PaidGas") then pcall(function() ReplicatedStorage.RequestRefill:FireServer(true) end) end
                end
            end
        end)
    end)

    local VM = { SpeedEnabled=false, SpeedValue=0.005, BreakEnabled=false, BreakValue=0.05, InstantStop=false, InstantStopBind=Enum.KeyCode.V }
    local function _vmSeat()
        local char=LocalPlayer.Character; if not char then return end
        local hum=char:FindFirstChildWhichIsA("Humanoid")
        if hum and hum.SeatPart and hum.SeatPart:IsA("VehicleSeat") then return hum.SeatPart end
    end
    RunService.Heartbeat:Connect(function()
        if VM.SpeedEnabled and UserInputService:IsKeyDown(Enum.KeyCode.W) then
            local s=_vmSeat(); if s then s.AssemblyLinearVelocity = s.AssemblyLinearVelocity * Vector3.new(1+VM.SpeedValue,1,1+VM.SpeedValue) end
        end
        if VM.BreakEnabled and UserInputService:IsKeyDown(Enum.KeyCode.S) then
            local s=_vmSeat(); if s then s.AssemblyLinearVelocity = s.AssemblyLinearVelocity * Vector3.new(1-VM.BreakValue,1,1-VM.BreakValue) end
        end
        if VM.InstantStop and VM.InstantStopBind and UserInputService:IsKeyDown(VM.InstantStopBind) then
            local s=_vmSeat(); if s then s.AssemblyLinearVelocity=Vector3.new(0,0,0); s.AssemblyAngularVelocity=Vector3.new(0,0,0) end
        end
    end)
    UI:AddSection(CarModsTab, "🚗 Vehicle Modifications")
    UI:AddToggle(CarModsTab, "Velocity Speed Enabled", false, function(s) VM.SpeedEnabled=s end)
    UI:AddSlider(CarModsTab, "Speed Value", 1, 25, 5, function(v) VM.SpeedValue=v/1000 end)
    UI:AddToggle(CarModsTab, "Break Velocity Enabled", false, function(s) VM.BreakEnabled=s end)
    UI:AddSlider(CarModsTab, "Break Value", 10, 300, 50, function(v) VM.BreakValue=v/1000 end)
    UI:AddToggle(CarModsTab, "Instant Break Enabled", false, function(s) VM.InstantStop=s end)
    UI:AddKeybind(CarModsTab, "Instant Break Key", Enum.KeyCode.V, function(k) VM.InstantStopBind=k end)
end

do
    UI:AddSection(ExploitsTab, "🛡️ Admin Detection")
    UI:AddToggle(ExploitsTab, "Admin Detection (Auto Leave)", false, function(v)
        getgenv()._adminDetect = v
        if v then
            local adminIds = {7574356202,9840202816,2361804144,504603254,2059859959,1673101632,3744075531,5170526005,329097649,8879510201,1591729028,4006717220,1965457341,100696125,157944161,571073274,1913839150,1043344298,691991358,3127042754,9802505,1187817721,1188540444,3997447018,5518581701,2300787931,4246623001,336408538,7309042402,39901822,5068993693,2632508759,1196871048,97728999,8472043145,2495032,7262444842,26105082,4301940303,40871536,3602117253,2248489384}
            local adminSet = {}; for _,id in ipairs(adminIds) do adminSet[id]=true end
            for _,p in pairs(Players:GetPlayers()) do if adminSet[p.UserId] then game:GetService("TeleportService"):Teleport(game.PlaceId); return end end
            if not getgenv()._adminConn then
                getgenv()._adminConn = Players.PlayerAdded:Connect(function(p)
                    if getgenv()._adminDetect and adminSet[p.UserId] then
                        task.wait(0.5)
                        game:GetService("TeleportService"):Teleport(game.PlaceId)
                    end
                end)
            end
            Notify("Admin", "Detection ON - monitoring for admins", 3)
        else
            if getgenv()._adminConn then getgenv()._adminConn:Disconnect(); getgenv()._adminConn = nil end
            Notify("Admin", "Detection OFF", 2)
        end
    end)
end

do
    local Lighting = game:GetService("Lighting")
    local TweenSrv = game:GetService("TweenService")
    local blur = Instance.new("BlurEffect"); blur.Size = 0; blur.Enabled = false; blur.Parent = Lighting
    local cc = Instance.new("ColorCorrectionEffect"); cc.Saturation = 0; cc.Enabled = false; cc.Parent = Lighting
    local gui = Instance.new("ScreenGui"); gui.Name = "JointhubWasted"; gui.ResetOnSpawn = false; gui.IgnoreGuiInset = true; gui.DisplayOrder = 999998
    pcall(function() gui.Parent = (gethui and gethui()) or game:GetService("CoreGui") end)
    if not gui.Parent then pcall(function() gui.Parent = LocalPlayer:WaitForChild("PlayerGui") end) end
    local function edge(size, pos, anchor, rot, t0, t1)
        local f = Instance.new("Frame")
        f.Size = size; f.Position = pos; f.AnchorPoint = anchor
        f.BackgroundColor3 = Color3.fromRGB(0, 0, 0); f.BackgroundTransparency = 1; f.BorderSizePixel = 0; f.ZIndex = 2; f.Parent = gui
        local g = Instance.new("UIGradient")
        g.Rotation = rot
        g.Transparency = NumberSequence.new({ NumberSequenceKeypoint.new(0, t0), NumberSequenceKeypoint.new(1, t1) })
        g.Parent = f
        return f
    end
    local edges = {
        edge(UDim2.new(1, 0, 0.5, 0), UDim2.new(0, 0, 0, 0), Vector2.new(0, 0), 90, 0, 1),
        edge(UDim2.new(1, 0, 0.5, 0), UDim2.new(0, 0, 1, 0), Vector2.new(0, 1), 90, 1, 0),
        edge(UDim2.new(0.4, 0, 1, 0), UDim2.new(0, 0, 0, 0), Vector2.new(0, 0), 0, 0, 1),
        edge(UDim2.new(0.4, 0, 1, 0), UDim2.new(1, 0, 0, 0), Vector2.new(1, 0), 0, 1, 0),
    }
    local wasted = Instance.new("TextLabel"); wasted.Size = UDim2.new(1, 0, 0, 120); wasted.Position = UDim2.new(0, 0, 0.5, -60); wasted.BackgroundTransparency = 1; wasted.ZIndex = 5
    wasted.Font = Enum.Font.Bangers; wasted.Text = "WASTED"; wasted.TextSize = 110; wasted.TextColor3 = Color3.fromRGB(200, 0, 0)
    wasted.TextStrokeColor3 = Color3.fromRGB(0, 0, 0); wasted.TextStrokeTransparency = 0; wasted.TextTransparency = 1; wasted.Parent = gui
    local active = false
    local function show()
        active = true
        blur.Enabled = true; cc.Enabled = true
        TweenSrv:Create(blur, TweenInfo.new(0.6), { Size = 18 }):Play()
        TweenSrv:Create(cc, TweenInfo.new(0.6), { Saturation = -0.85 }):Play()
        TweenSrv:Create(wasted, TweenInfo.new(0.8), { TextTransparency = 0 }):Play()
        task.spawn(function()
            while active do
                for _, f in ipairs(edges) do TweenSrv:Create(f, TweenInfo.new(0.75, Enum.EasingStyle.Sine), { BackgroundTransparency = 0.45 }):Play() end
                TweenSrv:Create(wasted, TweenInfo.new(0.75, Enum.EasingStyle.Sine), { TextSize = 124 }):Play()
                task.wait(0.78)
                if not active then break end
                for _, f in ipairs(edges) do TweenSrv:Create(f, TweenInfo.new(0.75, Enum.EasingStyle.Sine), { BackgroundTransparency = 0.02 }):Play() end
                TweenSrv:Create(wasted, TweenInfo.new(0.75, Enum.EasingStyle.Sine), { TextSize = 108 }):Play()
                task.wait(0.78)
            end
        end)
    end
    local function hide()
        active = false
        for _, f in ipairs(edges) do TweenSrv:Create(f, TweenInfo.new(0.4), { BackgroundTransparency = 1 }):Play() end
        TweenSrv:Create(blur, TweenInfo.new(0.4), { Size = 0 }):Play()
        TweenSrv:Create(cc, TweenInfo.new(0.4), { Saturation = 0 }):Play()
        TweenSrv:Create(wasted, TweenInfo.new(0.3), { TextTransparency = 1 }):Play()
        task.delay(0.45, function() blur.Enabled = false; cc.Enabled = false end)
    end
    local function hook(char)
        local hum = char:FindFirstChildOfClass("Humanoid") or char:WaitForChild("Humanoid", 5)
        if hum then hum.Died:Connect(show) end
    end
    if LocalPlayer.Character then hook(LocalPlayer.Character) end
    LocalPlayer.CharacterAdded:Connect(function(char) hide() hook(char) end)
end
UI:AddSection(VisualsTab,"👁️ ESP")
UI:AddToggle(VisualsTab,"Enable ESP",false,function(v) ESPSettings.Enabled=v end)
UI:AddToggle(VisualsTab,"Box ESP",false,function(v) ESPSettings.BoxESP=v; if v then ESPSettings.Enabled=true end end)
UI:AddToggle(VisualsTab,"Box Fill",false,function(v) ESPSettings.BoxFill=v end)
UI:AddToggle(VisualsTab,"Box Corners",false,function(v) ESPSettings.BoxCorners=v; if v then ESPSettings.Enabled=true end end)
UI:AddToggle(VisualsTab,"3D Box ESP",false,function(v) ESPSettings.Box3DESP=v; if v then ESPSettings.Enabled=true end end)
UI:AddToggle(VisualsTab,"Name ESP",false,function(v) ESPSettings.NameESP=v; if v then ESPSettings.Enabled=true end end)
UI:AddToggle(VisualsTab,"Health ESP",false,function(v) ESPSettings.HealthESP=v; if v then ESPSettings.Enabled=true end end)
UI:AddToggle(VisualsTab,"Tracer ESP",false,function(v) ESPSettings.TracerESP=v; if v then ESPSettings.Enabled=true end end)
UI:AddToggle(VisualsTab,"Distance ESP",false,function(v) ESPSettings.DistanceESP=v; if v then ESPSettings.Enabled=true end end)
UI:AddSlider(VisualsTab,"Max Distance",100,2000,800,function(v) ESPSettings.MaxDistance=v end)
UI:AddDropdown(VisualsTab,"Box Color",{"Red","Purple","Green","Blue","White","Yellow","Cyan","Orange","Pink"},"Red",function(v)
    if espColorMap[v] then ESPSettings.BoxColor=espColorMap[v]; ESPSettings.TracerColor=espColorMap[v]
        for _,e in pairs(ESPObjects) do pcall(function() e.Box.Color=espColorMap[v]; e.Tracer.Color=espColorMap[v]; for _,ln in ipairs(e.Corners or {}) do ln.Color=espColorMap[v] end; for _,ln in ipairs(e.Box3D or {}) do ln.Color=espColorMap[v] end end) end end
end)
UI:AddSection(VisualsTab,"✨ Chams")
UI:AddToggle(VisualsTab,"Chams",false,function(v)
    getgenv().ChamsEnabled=v
    if v then
        RefreshChams()
        if getgenv().ChamsConn then getgenv().ChamsConn:Disconnect() end
        getgenv().ChamsConn=Players.PlayerAdded:Connect(function(plr) plr.CharacterAdded:Connect(function() task.wait(0.5); if getgenv().ChamsEnabled then ApplyChams(plr) end end) end)
        for _,plr in pairs(Players:GetPlayers()) do if plr~=LocalPlayer then plr.CharacterAdded:Connect(function() task.wait(0.5); if getgenv().ChamsEnabled then ApplyChams(plr) end end) end end
        spawn(function() while getgenv().ChamsEnabled do task.wait(5); RefreshChams() end end)
        Notify("Chams","Enabled",2)
    else
        for plr,hi in pairs(ChamsHighlights) do pcall(function() if hi and hi.Parent then hi:Destroy() end end) end; ChamsHighlights={}
        for _,plr in pairs(Players:GetPlayers()) do if plr.Character then local hi=plr.Character:FindFirstChild("WalChams"); if hi then hi:Destroy() end end end
        if getgenv().ChamsConn then getgenv().ChamsConn:Disconnect(); getgenv().ChamsConn=nil end; Notify("Chams","Disabled",2)
    end
end)
UI:AddDropdown(VisualsTab,"Chams Fill Color",{"Purple","Red","Green","Blue","White","Yellow","Cyan","Orange","Pink"},"Purple",function(v)
    if espColorMap[v] then chamsFillColor=espColorMap[v]; for _,hi in pairs(ChamsHighlights) do pcall(function() if hi and hi.Parent then hi.FillColor=chamsFillColor end end) end; if getgenv().ChamsEnabled then RefreshChams() end end
end)
UI:AddDropdown(VisualsTab,"Chams Outline Color",{"Pink","Red","Green","Blue","White","Yellow","Cyan","Orange","Purple"},"Pink",function(v)
    if espColorMap[v] then chamsOutlineColor=espColorMap[v]; for _,hi in pairs(ChamsHighlights) do pcall(function() if hi and hi.Parent then hi.OutlineColor=chamsOutlineColor end end) end; if getgenv().ChamsEnabled then RefreshChams() end end
end)
UI:AddSection(VisualsTab,"🌅 Sky Presets")
UI:AddButton(VisualsTab,"Day Time Sky",function()
    local L=game:GetService("Lighting"); L.ClockTime=9
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    local S=Instance.new("Sky"); S.SkyboxBk="rbxassetid://74258544564321"; S.SkyboxDn="rbxassetid://75418092548143"; S.SkyboxFt="rbxassetid://114547356324218"; S.SkyboxLf="rbxassetid://91138773974890"; S.SkyboxRt="rbxassetid://111749399946832"; S.SkyboxUp="rbxassetid://96933043812138"; S.Parent=L
end)
UI:AddButton(VisualsTab,"Night Time Sky",function()
    local L=game:GetService("Lighting")
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    local S=Instance.new("Sky"); S.SkyboxBk="rbxassetid://155624722"; S.SkyboxDn="rbxassetid://155624727"; S.SkyboxFt="rbxassetid://155624730"; S.SkyboxLf="rbxassetid://155624736"; S.SkyboxRt="rbxassetid://155624742"; S.SkyboxUp="rbxassetid://155624749"; S.Parent=L
end)
UI:AddButton(VisualsTab,"Pink Clouds",function()
    local L=game:GetService("Lighting")
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    local S=Instance.new("Sky"); S.SkyboxBk="rbxassetid://11555017034"; S.SkyboxDn="rbxassetid://11555013415"; S.SkyboxFt="rbxassetid://11555010145"; S.SkyboxLf="rbxassetid://11555006545"; S.SkyboxRt="rbxassetid://11555000712"; S.SkyboxUp="rbxassetid://11554996247"; S.Parent=L
end)
UI:AddButton(VisualsTab,"Purple Galaxy",function()
    local L=game:GetService("Lighting")
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    local S=Instance.new("Sky"); S.SkyboxBk="rbxassetid://159454299"; S.SkyboxDn="rbxassetid://159454296"; S.SkyboxFt="rbxassetid://159454293"; S.SkyboxLf="rbxassetid://159454286"; S.SkyboxRt="rbxassetid://159454300"; S.SkyboxUp="rbxassetid://159454288"; S.Parent=L
end)
UI:AddButton(VisualsTab,"Sunset",function()
    local L=game:GetService("Lighting")
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    local S=Instance.new("Sky"); S.SkyboxBk="rbxassetid://15502525195"; S.SkyboxDn="rbxassetid://15502522797"; S.SkyboxFt="rbxassetid://15502524520"; S.SkyboxLf="rbxassetid://15502522129"; S.SkyboxRt="rbxassetid://15502523711"; S.SkyboxUp="rbxassetid://15502526102"; S.Parent=L
end)
UI:AddButton(VisualsTab,"Cloudy Summer",function()
    local L=game:GetService("Lighting")
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    local S=Instance.new("Sky"); S.SkyboxBk="rbxassetid://17838127289"; S.SkyboxDn="rbxassetid://17838129609"; S.SkyboxFt="rbxassetid://17838144422"; S.SkyboxLf="rbxassetid://17838131484"; S.SkyboxRt="rbxassetid://17838148822"; S.SkyboxUp="rbxassetid://17838140709"; S.Parent=L
end)
UI:AddButton(VisualsTab,"Custom Sky",function()
    local L=game:GetService("Lighting")
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    local S=Instance.new("Sky")
    local id="rbxassetid://117345242676633"
    S.SkyboxBk=id; S.SkyboxDn=id; S.SkyboxFt=id; S.SkyboxLf=id; S.SkyboxRt=id; S.SkyboxUp=id
    S.Parent=L
end)
do
    local skies = {
        {"pat",     "72781607771925"},
        {"thinker", "109804031157929"},
        {"son",     "129967531694220"},
        {"dex",     "84585770971279"},
        {"GOD",     "82397705080892"},
        {"huh",     "99333367082849"},
    }
    for _, sky in ipairs(skies) do
        local name, id = sky[1], "rbxassetid://"..sky[2]
        UI:AddButton(VisualsTab, name, function()
            local L = game:GetService("Lighting")
            local old = L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
            local S = Instance.new("Sky")
            S.SkyboxBk=id; S.SkyboxDn=id; S.SkyboxFt=id; S.SkyboxLf=id; S.SkyboxRt=id; S.SkyboxUp=id
            S.Parent = L
        end)
    end
end
UI:AddButton(VisualsTab,"Reset Sky",function()
    local L=game:GetService("Lighting")
    local old=L:FindFirstChildOfClass("Sky"); if old then old:Destroy() end
    L.ClockTime=14
end)
end
end
end)()
Notify("JOINTHUB.GG", "Leaked By Jointhub.gg | RightShift to toggle", 5)

task.spawn(function()
    if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then return end
    local parent = (gethui and gethui()) or game:GetService("CoreGui")
    local existing = parent:FindFirstChild("_CursorDot"); if existing then existing:Destroy() end
    local dotGui = Instance.new("ScreenGui")
    dotGui.Name = "_CursorDot"; dotGui.ResetOnSpawn = false; dotGui.IgnoreGuiInset = true; dotGui.DisplayOrder = 999999
    dotGui.Parent = parent
    local dot = Instance.new("Frame")
    dot.AnchorPoint = Vector2.new(0.5,0.5); dot.Size = UDim2.fromOffset(6,6)
    dot.BackgroundColor3 = Color3.fromRGB(255,255,255); dot.BorderSizePixel = 0
    dot.ZIndex = 999999; dot.Parent = dotGui
    Instance.new("UICorner", dot).CornerRadius = UDim.new(1,0)
    local st = Instance.new("UIStroke"); st.Color = Color3.fromRGB(0,0,0); st.Thickness = 1; st.Transparency = 0.4; st.Parent = dot
    RunService.RenderStepped:Connect(function()
        local m = UserInputService:GetMouseLocation()
        dot.Position = UDim2.fromOffset(m.X, m.Y)
    end)
end)
