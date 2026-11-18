-- ==============================================================================
-- SHADOW X GOATJO V3 HUB | Dark Tactical UI
-- Chat: SHADOW X GOATJO | Whitelist: 5 accounts | Buffed KA | Riptide Heal
-- ==============================================================================

local Players           = game:GetService("Players")
local UserInputService  = game:GetService("UserInputService")
local RunService        = game:GetService("RunService")
local TweenService      = game:GetService("TweenService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TextChatService   = game:GetService("TextChatService")
local StarterGui        = game:GetService("StarterGui")
local LocalPlayer       = Players.LocalPlayer
local Camera            = workspace.CurrentCamera

local function tw(obj,t,props) TweenService:Create(obj,TweenInfo.new(t,Enum.EasingStyle.Quart,Enum.EasingDirection.Out),props):Play() end

local C = {
    BG=Color3.fromRGB(8,8,8), BG2=Color3.fromRGB(14,14,14), BG3=Color3.fromRGB(20,20,20),
    SIDEBAR=Color3.fromRGB(10,10,10), SIDE_SEL=Color3.fromRGB(22,22,22),
    BORDER=Color3.fromRGB(50,50,50), BRTBORDER=Color3.fromRGB(160,160,160),
    ACCENT=Color3.fromRGB(220,220,220), WHITE=Color3.fromRGB(255,255,255),
    DIM=Color3.fromRGB(160,160,160), DARK=Color3.fromRGB(90,90,90),
    TOG_ON=Color3.fromRGB(190,190,190), TOG_OFF=Color3.fromRGB(35,35,35),
    BTN=Color3.fromRGB(25,25,25),
    RED=Color3.fromRGB(180,45,45), GREEN=Color3.fromRGB(45,160,80),
    GOLD=Color3.fromRGB(210,170,80),
}

-- ==============================================================================
-- WHITELIST
-- ==============================================================================
local WHITELIST = {
    ["ITZ_SHADOW7862"] = true,
    ["SASUKE"] = true,
    ["PRINCE1286099"] = true,
    ["KINGXGAMER999"] = true,
    ["KINGXGAMER99999"] = true,
}
local function isWhitelisted(player)
    if not player then return false end
    local name = player.Name
    for wl in pairs(WHITELIST) do
        if name:lower() == wl:lower() then return true end
    end
    return false
end

-- ==============================================================================
-- CHAT NOTIFICATION SYSTEM
-- ==============================================================================
local function sendChatNotification(msg)
    pcall(function()
        if TextChatService and TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
            local textChannel = TextChatService.TextChannels.RBXGeneral
            if textChannel then textChannel:SendAsync(msg) end
        else
            StarterGui:SetCore("ChatMakeSystemMessage", {
                Text = msg, Color = Color3.fromRGB(180, 45, 45),
                Font = Enum.Font.SourceSansBold, FontSize = Enum.FontSize.Size18
            })
        end
    end)
end

local function notifyToggle(featureName, state)
    local stateText = state and "ACTIVATED" or "DEACTIVATED"
    sendChatNotification("SHADOW X GOATJO: " .. featureName .. " is " .. stateText)
end

-- ==============================================================================
-- NOTIFICATION UI
-- ==============================================================================
local notifHolder=nil
local function Notify(cfg)
    local title=cfg.Title or "SHADOW X GOATJO"; local content=cfg.Content or ""; local duration=cfg.Duration or 3
    if not notifHolder then
        local sg2=Instance.new("ScreenGui"); sg2.Name="SXG_Notifs"; sg2.ResetOnSpawn=false; sg2.IgnoreGuiInset=true
        local cok=pcall(function() sg2.Parent=game:GetService("CoreGui") end)
        if not cok then sg2.Parent=LocalPlayer.PlayerGui end
        local f=Instance.new("Frame",sg2); f.Size=UDim2.new(0,290,1,-20); f.Position=UDim2.new(1,-300,0,10); f.BackgroundTransparency=1
        local l=Instance.new("UIListLayout",f); l.Padding=UDim.new(0,6); l.VerticalAlignment=Enum.VerticalAlignment.Bottom; l.HorizontalAlignment=Enum.HorizontalAlignment.Right
        notifHolder=f
    end
    local card=Instance.new("Frame",notifHolder); card.Size=UDim2.new(1,0,0,62); card.BackgroundColor3=C.BG2; card.BorderSizePixel=0
    Instance.new("UICorner",card).CornerRadius=UDim.new(0,5)
    local sk=Instance.new("UIStroke",card); sk.Thickness=1; sk.Color=C.BRTBORDER
    local bar=Instance.new("Frame",card); bar.Size=UDim2.new(0,3,1,0); bar.BackgroundColor3=C.ACCENT; bar.BorderSizePixel=0; Instance.new("UICorner",bar).CornerRadius=UDim.new(0,3)
    local tl=Instance.new("TextLabel",card); tl.Size=UDim2.new(1,-14,0,18); tl.Position=UDim2.new(0,10,0,7); tl.Text=title; tl.TextColor3=C.WHITE; tl.TextSize=13; tl.Font=Enum.Font.GothamBold; tl.TextXAlignment=Enum.TextXAlignment.Left; tl.BackgroundTransparency=1
    local cl=Instance.new("TextLabel",card); cl.Size=UDim2.new(1,-14,0,26); cl.Position=UDim2.new(0,10,0,27); cl.Text=content; cl.TextColor3=C.DIM; cl.TextSize=11; cl.Font=Enum.Font.Gotham; cl.TextWrapped=true; cl.TextXAlignment=Enum.TextXAlignment.Left; cl.BackgroundTransparency=1
    card.Position=UDim2.new(1,60,0,0); tw(card,0.25,{Position=UDim2.new(0,0,0,0)})
    task.spawn(function()
        task.wait(duration)
        tw(card,0.3,{BackgroundTransparency=1}); tw(tl,0.3,{TextTransparency=1}); tw(cl,0.3,{TextTransparency=1}); tw(sk,0.3,{Transparency=1})
        task.wait(0.35); card:Destroy()
    end)
end

-- ==============================================================================
-- UI HELPERS & FRAMEWORK
-- ==============================================================================
local function makeDraggable(handle, frame)
    local dragging, dragInput, dragStart, startPos = false, nil, nil, nil
    handle.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true; dragStart = input.Position; startPos = frame.Position
            input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging = false end end)
        end
    end)
    handle.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput = input end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

local function brackets(parent,sz,col)
    sz=sz or 14; col=col or C.BORDER
    for _,p in ipairs({{0,-1,0,-1},{1,-sz,0,-1},{0,-1,1,-sz},{1,-sz,1,-sz}}) do
        local h=Instance.new("Frame",parent); h.Size=UDim2.new(0,sz,0,sz); h.Position=UDim2.new(p[1],p[2],p[3],p[4]); h.BackgroundTransparency=1; h.ZIndex=parent.ZIndex+2
        local hb=Instance.new("Frame",h); hb.Size=UDim2.new(1,0,0,1); hb.BackgroundColor3=col; hb.BorderSizePixel=0
        local vb=Instance.new("Frame",h); vb.Size=UDim2.new(0,1,1,0); vb.BackgroundColor3=col; vb.BorderSizePixel=0
    end
end

local ICONS={users="rbxassetid://10747373111",navigation="rbxassetid://10747373172",swords="rbxassetid://10747383842",zap="rbxassetid://10747374061",hammer="rbxassetid://10747373307",settings="rbxassetid://10747373808",shield="rbxassetid://10747373111",package="rbxassetid://10747373731",eye="rbxassetid://10747373516",activity="rbxassetid://10747372992",wrench="rbxassetid://10747373867",home="rbxassetid://10747372702"}
local function icon(n) return ICONS[n] or ICONS.home end

local sg=Instance.new("ScreenGui"); sg.Name="SXG_GUI"; sg.ResetOnSpawn=false; sg.IgnoreGuiInset=true
local sgok=pcall(function() sg.Parent=game:GetService("CoreGui") end)
if not sgok then sg.Parent=LocalPlayer.PlayerGui end

local main=Instance.new("Frame",sg); main.Name="MainFrame"; main.Size=UDim2.new(0,760,0,500); main.Position=UDim2.new(0.5,-380,0.5,-250); main.BackgroundColor3=C.BG; main.BorderSizePixel=0
Instance.new("UICorner",main).CornerRadius=UDim.new(0,4)
local mS=Instance.new("UIStroke",main); mS.Thickness=1; mS.Color=C.BORDER
brackets(main,16,C.BRTBORDER)

local topBar=Instance.new("Frame",main); topBar.Name="TopBar"; topBar.Size=UDim2.new(1,0,0,36); topBar.BackgroundColor3=C.BG; topBar.BorderSizePixel=0
makeDraggable(topBar,main)
local topSep=Instance.new("Frame",main); topSep.Size=UDim2.new(1,0,0,1); topSep.Position=UDim2.new(0,0,0,36); topSep.BackgroundColor3=C.BORDER; topSep.BorderSizePixel=0

local function dash(par,x,y,w) local f=Instance.new("Frame",par); f.Size=UDim2.new(0,w,0,1); f.Position=UDim2.new(0,x,0,y); f.BackgroundColor3=C.BORDER; f.BorderSizePixel=0 end
dash(topBar,240,17,80); dash(topBar,340,17,40); dash(topBar,580,17,100); dash(topBar,690,17,50)

local function winBtn(lbl,xOff,hov)
    local b=Instance.new("TextButton",topBar); b.Size=UDim2.new(0,28,0,28); b.Position=UDim2.new(1,xOff,0,4); b.BackgroundColor3=C.BG3; b.Text=lbl; b.TextColor3=C.DIM; b.TextSize=13; b.Font=Enum.Font.GothamBold; b.BorderSizePixel=0
    Instance.new("UICorner",b).CornerRadius=UDim.new(0,3); local s=Instance.new("UIStroke",b); s.Thickness=1; s.Color=C.BORDER
    b.MouseEnter:Connect(function() tw(b,0.15,{BackgroundColor3=hov}) end); b.MouseLeave:Connect(function() tw(b,0.15,{BackgroundColor3=C.BG3}) end)
    return b
end
local minBtn=winBtn("-",-94,C.BTN); winBtn("[]",-62,C.BTN); local closeBtn=winBtn("X",-30,Color3.fromRGB(160,30,30))
closeBtn.MouseButton1Click:Connect(function() sg:Destroy() end)
local isMin=false
minBtn.MouseButton1Click:Connect(function()
    isMin=not isMin
    if isMin then
        tw(main,0.25,{Size=UDim2.new(0,760,0,36)})
        task.spawn(function() task.wait(0.28); local s=main:FindFirstChild("Sidebar"); local t=main:FindFirstChild("TabCont"); if s then s.Visible=false end; if t then t.Visible=false end end)
        minBtn.Text="+"
    else
        local s=main:FindFirstChild("Sidebar"); local t=main:FindFirstChild("TabCont")
        if s then s.Visible=true end; if t then t.Visible=true end
        tw(main,0.25,{Size=UDim2.new(0,760,0,500)}); minBtn.Text="-"
    end
end)

local sidebar=Instance.new("Frame",main); sidebar.Name="Sidebar"; sidebar.Size=UDim2.new(0,200,1,-37); sidebar.Position=UDim2.new(0,0,0,37); sidebar.BackgroundColor3=C.SIDEBAR; sidebar.BorderSizePixel=0
local sl=Instance.new("Frame",sidebar); sl.Size=UDim2.new(0,1,1,0); sl.Position=UDim2.new(1,-1,0,0); sl.BackgroundColor3=C.BORDER; sl.BorderSizePixel=0
local logo=Instance.new("TextLabel",sidebar); logo.Size=UDim2.new(1,0,0,58); logo.Position=UDim2.new(0,0,0,8); logo.Text="SXG"; logo.TextColor3=C.WHITE; logo.TextSize=48; logo.Font=Enum.Font.GothamBold; logo.TextXAlignment=Enum.TextXAlignment.Center; logo.BackgroundTransparency=1
local ver=Instance.new("TextLabel",sidebar); ver.Size=UDim2.new(1,0,0,14); ver.Position=UDim2.new(0,0,0,66); ver.Text="V3"; ver.TextColor3=C.DIM; ver.TextSize=11; ver.Font=Enum.Font.Gotham; ver.TextXAlignment=Enum.TextXAlignment.Center; ver.BackgroundTransparency=1
local lsep=Instance.new("Frame",sidebar); lsep.Size=UDim2.new(1,-20,0,1); lsep.Position=UDim2.new(0,10,0,84); lsep.BackgroundColor3=C.BORDER; lsep.BorderSizePixel=0
local tabList=Instance.new("ScrollingFrame",sidebar); tabList.Size=UDim2.new(1,0,1,-90); tabList.Position=UDim2.new(0,0,0,90); tabList.BackgroundTransparency=1; tabList.BorderSizePixel=0; tabList.ScrollBarThickness=0; tabList.CanvasSize=UDim2.new(0,0,0,0)
local tll=Instance.new("UIListLayout",tabList); tll.Padding=UDim.new(0,2); tll.HorizontalAlignment=Enum.HorizontalAlignment.Center; Instance.new("UIPadding",tabList).PaddingTop=UDim.new(0,6)
tll:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function() tabList.CanvasSize=UDim2.new(0,0,0,tll.AbsoluteContentSize.Y+12) end)

local tabCont=Instance.new("Frame",main); tabCont.Name="TabCont"; tabCont.Size=UDim2.new(1,-200,1,-37); tabCont.Position=UDim2.new(0,200,0,37); tabCont.BackgroundTransparency=1; tabCont.BorderSizePixel=0
local contentPanel=Instance.new("Frame",tabCont); contentPanel.Size=UDim2.new(1,-14,1,-14); contentPanel.Position=UDim2.new(0,7,0,7); contentPanel.BackgroundColor3=C.BG2; contentPanel.BorderSizePixel=0
Instance.new("UICorner",contentPanel).CornerRadius=UDim.new(0,4); local cpS=Instance.new("UIStroke",contentPanel); cpS.Thickness=1; cpS.Color=C.BORDER; brackets(contentPanel,14,C.BORDER)

local botLogo=Instance.new("TextLabel",main); botLogo.Size=UDim2.new(0,80,0,18); botLogo.Position=UDim2.new(0.5,-40,1,-20); botLogo.Text="SXG"; botLogo.TextColor3=C.BRTBORDER; botLogo.TextSize=13; botLogo.Font=Enum.Font.GothamBold; botLogo.BackgroundTransparency=1
dash(main,210,490,60); dash(main,280,490,30); dash(main,460,490,30); dash(main,500,490,60)

local activeTab=nil

local function makeCard(parent,name,desc,h)
    local card=Instance.new("Frame",parent); card.Size=UDim2.new(1,-18,0,h or 66); card.BackgroundColor3=C.BG3; card.BorderSizePixel=0
    Instance.new("UICorner",card).CornerRadius=UDim.new(0,5); local cs=Instance.new("UIStroke",card); cs.Thickness=1; cs.Color=C.BORDER
    local stripe=Instance.new("Frame",card); stripe.Size=UDim2.new(0,2,0,28); stripe.Position=UDim2.new(0,0,0.5,-14); stripe.BackgroundColor3=C.ACCENT; stripe.BorderSizePixel=0; stripe.BackgroundTransparency=0.5; Instance.new("UICorner",stripe).CornerRadius=UDim.new(0,2)
    local nt=Instance.new("TextLabel",card); nt.Size=UDim2.new(1,-150,0,18); nt.Position=UDim2.new(0,12,0,10); nt.Text=name; nt.TextColor3=C.WHITE; nt.TextSize=13; nt.Font=Enum.Font.GothamBold; nt.TextXAlignment=Enum.TextXAlignment.Left; nt.BackgroundTransparency=1
    local dt=Instance.new("TextLabel",card); dt.Size=UDim2.new(1,-150,0,14); dt.Position=UDim2.new(0,12,0,28); dt.Text=desc or ""; dt.TextColor3=C.DARK; dt.TextSize=10; dt.Font=Enum.Font.Gotham; dt.TextXAlignment=Enum.TextXAlignment.Left; dt.BackgroundTransparency=1
    card.MouseEnter:Connect(function() tw(card,0.15,{BackgroundColor3=Color3.fromRGB(26,26,26)}) end)
    card.MouseLeave:Connect(function() tw(card,0.15,{BackgroundColor3=C.BG3}) end)
    return card
end

local function CreateTab(name,iconName)
    local btn=Instance.new("TextButton",tabList); btn.Size=UDim2.new(1,-10,0,38); btn.BackgroundColor3=C.SIDEBAR; btn.Text=""; btn.BorderSizePixel=0; Instance.new("UICorner",btn).CornerRadius=UDim.new(0,4)
    local ind=Instance.new("Frame",btn); ind.Size=UDim2.new(0,3,0,22); ind.Position=UDim2.new(0,0,0.5,-11); ind.BackgroundColor3=C.ACCENT; ind.BorderSizePixel=0; ind.BackgroundTransparency=1; Instance.new("UICorner",ind).CornerRadius=UDim.new(0,2)
    local bIco=Instance.new("ImageLabel",btn); bIco.Size=UDim2.new(0,16,0,16); bIco.Position=UDim2.new(0,14,0.5,-8); bIco.Image=icon(iconName); bIco.ImageColor3=C.DARK; bIco.BackgroundTransparency=1
    local bLbl=Instance.new("TextLabel",btn); bLbl.Size=UDim2.new(1,-40,1,0); bLbl.Position=UDim2.new(0,38,0,0); bLbl.Text=name; bLbl.TextColor3=C.DIM; bLbl.TextSize=13; bLbl.Font=Enum.Font.GothamMedium; bLbl.TextXAlignment=Enum.TextXAlignment.Left; bLbl.BackgroundTransparency=1
    local page=Instance.new("ScrollingFrame",contentPanel); page.Size=UDim2.new(1,0,1,0); page.BackgroundTransparency=1; page.BorderSizePixel=0; page.Visible=false; page.ScrollBarThickness=3; page.ScrollBarImageColor3=C.BRTBORDER; page.CanvasSize=UDim2.new(0,0,0,0)
    local pl=Instance.new("UIListLayout",page); pl.Padding=UDim.new(0,8); pl.HorizontalAlignment=Enum.HorizontalAlignment.Center
    local pp=Instance.new("UIPadding",page); pp.PaddingTop=UDim.new(0,10); pp.PaddingBottom=UDim.new(0,10)
    pl:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function() page.CanvasSize=UDim2.new(0,0,0,pl.AbsoluteContentSize.Y+20) end)
    local tabObj={Page=page,Button=btn}
    local function activate()
        if activeTab then
            local op=activeTab; tw(op.Button,0.15,{BackgroundColor3=C.SIDEBAR})
            local f=op.Button:FindFirstChildOfClass("Frame"); if f then f.BackgroundTransparency=1 end
            local img=op.Button:FindFirstChildOfClass("ImageLabel"); if img then img.ImageColor3=C.DARK end
            local lbl=op.Button:FindFirstChildOfClass("TextLabel"); if lbl then lbl.TextColor3=C.DIM end
            op.Page.Visible=false
        end
        activeTab=tabObj; tw(btn,0.15,{BackgroundColor3=C.SIDE_SEL}); ind.BackgroundTransparency=0; bIco.ImageColor3=C.ACCENT; bLbl.TextColor3=C.WHITE; page.Position=UDim2.new(0,0,0,0); page.Visible=true
    end
    btn.MouseButton1Click:Connect(activate)
    btn.MouseEnter:Connect(function() if activeTab~=tabObj then tw(btn,0.15,{BackgroundColor3=Color3.fromRGB(18,18,18)}) end end)
    btn.MouseLeave:Connect(function() if activeTab~=tabObj then tw(btn,0.15,{BackgroundColor3=C.SIDEBAR}) end end)
    if not activeTab then activate() end

    function tabObj:CreateToggle(cfg)
        local card=makeCard(page,cfg.Name or "Toggle",cfg.Description or "",64); local defVal=cfg.CurrentValue or false; local cb=cfg.Callback or function() end
        local sw=Instance.new("TextButton",card); sw.Size=UDim2.new(0,46,0,24); sw.Position=UDim2.new(1,-58,0.5,-12); sw.BackgroundColor3=defVal and C.TOG_ON or C.TOG_OFF; sw.Text=""; sw.BorderSizePixel=0; Instance.new("UICorner",sw).CornerRadius=UDim.new(0,12)
        local swS=Instance.new("UIStroke",sw); swS.Thickness=1; swS.Color=defVal and C.BRTBORDER or C.BORDER
        local knob=Instance.new("Frame",sw); knob.Size=UDim2.new(0,18,0,18); knob.Position=defVal and UDim2.new(1,-21,0.5,-9) or UDim2.new(0,3,0.5,-9); knob.BackgroundColor3=C.WHITE; knob.BorderSizePixel=0; Instance.new("UICorner",knob).CornerRadius=UDim.new(0,9)
        local state=defVal
        local function upd() tw(sw,0.15,{BackgroundColor3=state and C.TOG_ON or C.TOG_OFF}); tw(swS,0.15,{Color=state and C.BRTBORDER or C.BORDER}); tw(knob,0.15,{Position=state and UDim2.new(1,-21,0.5,-9) or UDim2.new(0,3,0.5,-9)}) end
        sw.MouseButton1Click:Connect(function() state=not state; upd(); task.spawn(function() cb(state) end) end)
        return {Set=function(v) state=v; upd(); task.spawn(function() cb(state) end) end}
    end

    function tabObj:CreateSlider(cfg)
        local range=cfg.Range or {0,100}; local inc=cfg.Increment or 1; local defVal=cfg.CurrentValue or range[1]; local cb=cfg.Callback or function() end
        local card=makeCard(page,cfg.Name or "Slider",cfg.Description or "",74)
        local vLbl=Instance.new("TextLabel",card); vLbl.Size=UDim2.new(0,50,0,18); vLbl.Position=UDim2.new(1,-56,0,8); vLbl.Text=tostring(defVal); vLbl.TextColor3=C.ACCENT; vLbl.TextSize=12; vLbl.Font=Enum.Font.GothamBold; vLbl.TextXAlignment=Enum.TextXAlignment.Right; vLbl.BackgroundTransparency=1
        local track=Instance.new("TextButton",card); track.Size=UDim2.new(1,-18,0,6); track.Position=UDim2.new(0,9,0.72,-3); track.BackgroundColor3=C.BG; track.Text=""; track.BorderSizePixel=0; Instance.new("UICorner",track).CornerRadius=UDim.new(0,3); Instance.new("UIStroke",track).Color=C.BORDER
        local fill=Instance.new("Frame",track); fill.Size=UDim2.new((defVal-range[1])/(range[2]-range[1]),0,1,0); fill.BackgroundColor3=C.ACCENT; fill.BorderSizePixel=0; Instance.new("UICorner",fill).CornerRadius=UDim.new(0,3)
        local hdl=Instance.new("Frame",track); hdl.Size=UDim2.new(0,10,0,10); hdl.AnchorPoint=Vector2.new(0.5,0.5); hdl.Position=UDim2.new((defVal-range[1])/(range[2]-range[1]),0,0.5,0); hdl.BackgroundColor3=C.WHITE; hdl.BorderSizePixel=0; Instance.new("UICorner",hdl).CornerRadius=UDim.new(0,5)
        local sliding,conn=false,nil
        local function upd(i) local pct=math.clamp((i.Position.X-track.AbsolutePosition.X)/track.AbsoluteSize.X,0,1); local val=math.clamp(math.round((range[1]+pct*(range[2]-range[1]))/inc)*inc,range[1],range[2]); local vp=(val-range[1])/(range[2]-range[1]); fill.Size=UDim2.new(vp,0,1,0); hdl.Position=UDim2.new(vp,0,0.5,0); vLbl.Text=string.format("%g",val); task.spawn(function() cb(val) end) end
        track.InputBegan:Connect(function(i)
            if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then
                sliding=true; upd(i); if conn then conn:Disconnect() end
                conn=UserInputService.InputChanged:Connect(function(m) if sliding and (m.UserInputType==Enum.UserInputType.MouseMovement or m.UserInputType==Enum.UserInputType.Touch) then upd(m) end end)
            end
        end)
        UserInputService.InputEnded:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then sliding=false; if conn then conn:Disconnect(); conn=nil end end end)
        return {Set=function(v) v=math.clamp(v,range[1],range[2]); local vp=(v-range[1])/(range[2]-range[1]); fill.Size=UDim2.new(vp,0,1,0); hdl.Position=UDim2.new(vp,0,0.5,0); vLbl.Text=tostring(v); task.spawn(function() cb(v) end) end}
    end

    function tabObj:CreateButton(cfg)
        local cb=cfg.Callback or function() end; local card=makeCard(page,cfg.Name or "Button",cfg.Description or "",64)
        local b=Instance.new("TextButton",card); b.Size=UDim2.new(0,80,0,28); b.Position=UDim2.new(1,-92,0.5,-14); b.BackgroundColor3=C.BTN; b.Text="Run"; b.TextColor3=C.ACCENT; b.TextSize=12; b.Font=Enum.Font.GothamBold; b.BorderSizePixel=0; Instance.new("UICorner",b).CornerRadius=UDim.new(0,4)
        local bs=Instance.new("UIStroke",b); bs.Thickness=1; bs.Color=C.BORDER
        b.MouseButton1Click:Connect(function() tw(b,0.08,{BackgroundColor3=C.ACCENT,TextColor3=C.BG}); task.spawn(function() task.wait(0.12); tw(b,0.12,{BackgroundColor3=C.BTN,TextColor3=C.ACCENT}) end); task.spawn(cb) end)
        b.MouseEnter:Connect(function() tw(bs,0.15,{Color=C.BRTBORDER}) end); b.MouseLeave:Connect(function() tw(bs,0.15,{Color=C.BORDER}) end)
    end

    function tabObj:CreateDropdown(cfg)
        local opts=cfg.Options or {}; local isMulti=cfg.MultipleOptions or false; local cb=cfg.Callback or function() end
        local card=makeCard(page,cfg.Name or "Dropdown",isMulti and "Select multiple" or "Select an option",64)
        local selBtn=Instance.new("TextButton",card); selBtn.Size=UDim2.new(0,130,0,28); selBtn.Position=UDim2.new(1,-142,0.5,-14); selBtn.BackgroundColor3=C.BTN; selBtn.Text="Select..."; selBtn.TextColor3=C.DIM; selBtn.TextSize=11; selBtn.Font=Enum.Font.GothamMedium; selBtn.BorderSizePixel=0; selBtn.ClipsDescendants=false; Instance.new("UICorner",selBtn).CornerRadius=UDim.new(0,4); local ss=Instance.new("UIStroke",selBtn); ss.Thickness=1; ss.Color=C.BORDER
        local panel=Instance.new("Frame",card); panel.Size=UDim2.new(0,130,0,0); panel.Position=UDim2.new(1,-142,0.5,18); panel.BackgroundColor3=C.BG2; panel.BorderSizePixel=0; panel.ZIndex=20; panel.Visible=false; Instance.new("UICorner",panel).CornerRadius=UDim.new(0,4); local ps=Instance.new("UIStroke",panel); ps.Thickness=1; ps.Color=C.BRTBORDER; ps.ZIndex=21
        local iScroll=Instance.new("ScrollingFrame",panel); iScroll.Size=UDim2.new(1,0,1,0); iScroll.BackgroundTransparency=1; iScroll.BorderSizePixel=0; iScroll.ScrollBarThickness=2; iScroll.ZIndex=22
        local iLayout=Instance.new("UIListLayout",iScroll); iLayout.Padding=UDim.new(0,2); iLayout.HorizontalAlignment=Enum.HorizontalAlignment.Center
        local dropObj={CurrentOption=isMulti and {} or "Select..."}; local isOpen=false; local selMap={}
        local function displayText()
            if isMulti then local list={}; for k,v in pairs(selMap) do if v then table.insert(list,k) end end; dropObj.CurrentOption=list; selBtn.Text=#list==0 and "Select..." or (#list==1 and list[1] or tostring(#list).." Selected")
            else selBtn.Text=tostring(dropObj.CurrentOption) end
        end
        local curH=0
        local function buildList(newOpts)
            for _,c in ipairs(iScroll:GetChildren()) do if c:IsA("TextButton") then c:Destroy() end end
            for _,opt in ipairs(newOpts) do
                local ib=Instance.new("TextButton",iScroll); ib.Size=UDim2.new(1,-6,0,24); local active=isMulti and (not not selMap[opt]) or (dropObj.CurrentOption==opt); ib.BackgroundColor3=active and C.SIDE_SEL or C.BG2; ib.Text=tostring(opt); ib.TextColor3=active and C.WHITE or C.DIM; ib.TextSize=11; ib.Font=Enum.Font.GothamMedium; ib.ZIndex=23; ib.BorderSizePixel=0; Instance.new("UICorner",ib).CornerRadius=UDim.new(0,3)
                ib.MouseButton1Click:Connect(function()
                    if isMulti then selMap[opt]=not selMap[opt]; ib.BackgroundColor3=selMap[opt] and C.SIDE_SEL or C.BG2; ib.TextColor3=selMap[opt] and C.WHITE or C.DIM; displayText(); task.spawn(function() cb(dropObj.CurrentOption) end)
                    else dropObj.CurrentOption=opt; displayText(); isOpen=false; panel.Visible=false; task.spawn(function() cb(opt) end) end
                end)
            end
            local h=math.clamp(#newOpts*26+4,28,160); iScroll.CanvasSize=UDim2.new(0,0,0,#newOpts*26+4); curH=h; return h
        end
        curH=buildList(opts)
        selBtn.MouseButton1Click:Connect(function() isOpen=not isOpen; if isOpen then panel.Size=UDim2.new(0,130,0,0); panel.Visible=true; tw(panel,0.2,{Size=UDim2.new(0,130,0,curH)}) else tw(panel,0.15,{Size=UDim2.new(0,130,0,0)}); task.wait(0.15); panel.Visible=false end end)
        function dropObj:Refresh(newOpts,autoFirst) opts=newOpts; selMap={}; dropObj.CurrentOption=isMulti and {} or (autoFirst and newOpts[1] or "Select..."); curH=buildList(newOpts); displayText() end
        return dropObj
    end

    function tabObj:CreateInput(cfg)
        local cb=cfg.Callback or function() end; local card=makeCard(page,cfg.Name or "Input","Enter a value",64)
        local box=Instance.new("TextBox",card); box.Size=UDim2.new(0,120,0,28); box.Position=UDim2.new(1,-132,0.5,-14); box.BackgroundColor3=C.BTN; box.Text=cfg.CurrentValue or ""; box.PlaceholderText=cfg.PlaceholderText or "Type here..."; box.PlaceholderColor3=C.DARK; box.TextColor3=C.WHITE; box.TextSize=12; box.Font=Enum.Font.GothamMedium; box.ClearTextOnFocus=false; box.BorderSizePixel=0; Instance.new("UICorner",box).CornerRadius=UDim.new(0,4)
        local bs=Instance.new("UIStroke",box); bs.Thickness=1; bs.Color=C.BORDER
        box.Focused:Connect(function() tw(bs,0.15,{Color=C.BRTBORDER}) end)
        box.FocusLost:Connect(function() tw(bs,0.15,{Color=C.BORDER}); task.spawn(function() cb(box.Text) end) end)
        return {Set=function(v) box.Text=tostring(v); task.spawn(function() cb(box.Text) end) end}
    end

    return tabObj
end

-- ==============================================================================
-- TABS
-- ==============================================================================
local HomeTab        = CreateTab("Home",       "home")
local WhitelistTab   = CreateTab("Whitelist",  "users")
local TeleportTab    = CreateTab("Teleport",   "navigation")
local CombatTab      = CreateTab("Combat",     "swords")
local MovementTab    = CreateTab("Movement",   "zap")
local MineTab        = CreateTab("Mineing",    "hammer")
local HealTab        = CreateTab("Heals",      "shield")
local SettingsTab    = CreateTab("Settings",   "settings")
local ProtectionTab  = CreateTab("Protection", "shield")
local LootTab        = CreateTab("Loot",       "package")
local ESPTab         = CreateTab("Esp",        "eye")
local PerformanceTab = CreateTab("Performance","activity")
local SafetyTab      = CreateTab("Safty",      "wrench")

-- ==============================================================================
-- HOME
-- ==============================================================================
do
    local username=LocalPlayer.Name; local displayName=LocalPlayer.DisplayName; local userId=LocalPlayer.UserId
    local execName="Unknown"
    if identifyexecutor then pcall(function() execName=identifyexecutor() end)
    elseif getexecutorname then pcall(function() execName=getexecutorname() end) end
    local supportedText="No"
    if type(hookfunction)=="function" and type(getrawmetatable)=="function" then supportedText="Yes" end
    local avatarUrl=""
    pcall(function() avatarUrl=Players:GetUserThumbnailAsync(userId,Enum.ThumbnailType.HeadShot,Enum.ThumbnailSize.Size150x150) end)

    local profileCard=makeCard(HomeTab.Page,displayName.." (@"..username..")","User ID: "..tostring(userId),90)
    local avatarImg=Instance.new("ImageLabel",profileCard)
    avatarImg.Size=UDim2.new(0,70,0,70); avatarImg.Position=UDim2.new(0,10,0.5,-35)
    avatarImg.Image=avatarUrl; avatarImg.BackgroundTransparency=1; avatarImg.ZIndex=profileCard.ZIndex+1
    Instance.new("UICorner",avatarImg).CornerRadius=UDim.new(1,0)
    local avatarStroke=Instance.new("UIStroke",avatarImg); avatarStroke.Thickness=1; avatarStroke.Color=C.BRTBORDER
    for _,child in ipairs(profileCard:GetChildren()) do
        if child:IsA("TextLabel") then
            child.Position=UDim2.new(child.Position.X.Scale,90,child.Position.Y.Scale,child.Position.Y.Offset)
        end
    end
    local infoCard=makeCard(HomeTab.Page,"Environment Info","Executor detection and feature support",90)
    local execLabel=Instance.new("TextLabel",infoCard)
    execLabel.Size=UDim2.new(1,-20,0,18); execLabel.Position=UDim2.new(0,12,0,40)
    execLabel.Text="Executor:   "..execName; execLabel.TextColor3=C.DIM; execLabel.TextSize=12
    execLabel.Font=Enum.Font.GothamMedium; execLabel.TextXAlignment=Enum.TextXAlignment.Left
    execLabel.BackgroundTransparency=1; execLabel.ZIndex=infoCard.ZIndex+1
    local supportColor=supportedText=="Yes" and C.GREEN or C.RED
    local supportLabel=Instance.new("TextLabel",infoCard)
    supportLabel.Size=UDim2.new(1,-20,0,18); supportLabel.Position=UDim2.new(0,12,0,60)
    supportLabel.Text="Supported:  "..supportedText; supportLabel.TextColor3=supportColor; supportLabel.TextSize=12
    supportLabel.Font=Enum.Font.GothamBold; supportLabel.TextXAlignment=Enum.TextXAlignment.Left
    supportLabel.BackgroundTransparency=1; supportLabel.ZIndex=infoCard.ZIndex+1
    local tipCard=makeCard(HomeTab.Page,"Tip","",56)
    local tipLabel=Instance.new("TextLabel",tipCard)
    tipLabel.Size=UDim2.new(1,-20,1,-10); tipLabel.Position=UDim2.new(0,12,0,5)
    tipLabel.Text="SHADOW X GOATJO V3 active! Floating button toggles the hub."
    tipLabel.TextColor3=C.BRTBORDER; tipLabel.TextSize=11; tipLabel.Font=Enum.Font.Gotham
    tipLabel.TextXAlignment=Enum.TextXAlignment.Left; tipLabel.TextWrapped=true
    tipLabel.BackgroundTransparency=1; tipLabel.ZIndex=tipCard.ZIndex+1
end

-- ==============================================================================
-- SHARED STATE
-- ==============================================================================
_G.KA_ENABLED = false
local autoEatEnabled = false
local healingSpeed = 0.8
local lastHeal = 0
local dmgSettings = {FallDamage = false, DrownDamage = false, Suffocating = false, ServerKnockback = false}
local kaRange = 40
local lockOnEnabled = false
local lockOnTarget = nil
local kaConn = nil
local FLY_SPEED = 50
local flyEnabled = false
local antiDeathTP = false
local antiDeathTriggered = false

local EAT_SLOTS = {2, 3, 4, 5, 6, 7, 8, 9}

-- Remotes
local AttackRemote = nil
pcall(function()
    local sys = ReplicatedStorage:FindFirstChild("Systems", true)
    if sys then
        local actions = sys:FindFirstChild("ActionsSystem", true)
        if actions and actions:FindFirstChild("Network") then
            AttackRemote = actions.Network:FindFirstChild("Attack")
        end
    end
end)
local ConsumeRemote = nil
pcall(function()
    local sys = ReplicatedStorage:FindFirstChild("Systems", true)
    if sys then
        local actions = sys:FindFirstChild("ActionsSystem", true)
        if actions and actions:FindFirstChild("Network") then
            ConsumeRemote = actions.Network:FindFirstChild("Consume")
        end
    end
end)

-- Helpers
local function getPlayerNames()
    local list = {}
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= LocalPlayer then table.insert(list, p.Name) end
    end
    return list
end

local function validChar(c)
    if not c then return false end
    local hum = c:FindFirstChildOfClass("Humanoid")
    local hrp = c:FindFirstChild("HumanoidRootPart")
    if not hum or not hrp then return false end
    if hum.Health <= 0 then return false end
    if hum:GetState() == Enum.HumanoidStateType.Dead then return false end
    return true
end

-- ==============================================================================
-- KILL AURA (buffed + whitelist)
-- ==============================================================================
local function isWhitelistedCharacter(char)
    if not char then return false end
    local plr = Players:GetPlayerFromCharacter(char)
    if plr and isWhitelisted(plr) then return true end
    local name = char.Name
    for wl in pairs(WHITELIST) do
        if name:lower() == wl:lower() then return true end
    end
    return false
end

local function nearestTarget()
    local my = LocalPlayer.Character
    if not validChar(my) then return nil end
    local pos = my.HumanoidRootPart.Position
    local best, bestDist = nil, kaRange
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and not isWhitelisted(p) then
            local t = p.Character
            if validChar(t) then
                local dist = (t.HumanoidRootPart.Position - pos).Magnitude
                if dist < bestDist then best = t; bestDist = dist end
            end
        end
    end
    local ef = workspace:FindFirstChild("Entities")
    if ef then
        for _, e in pairs(ef:GetChildren()) do
            if validChar(e) and not isWhitelistedCharacter(e) then
                local dist = (e.HumanoidRootPart.Position - pos).Magnitude
                if dist < bestDist then best = e; bestDist = dist end
            end
        end
    end
    return best
end

local function kaHit(target)
    if not AttackRemote or not validChar(target) or isWhitelistedCharacter(target) then return end
    -- Buffed: send attack 3 times per tick instead of 1
    for _ = 1, 3 do
        pcall(function() AttackRemote:InvokeServer(target, 1) end)
    end
end

local function startKillAura()
    if kaConn then return end
    kaConn = RunService.Heartbeat:Connect(function()
        if not _G.KA_ENABLED then return end
        local target = nearestTarget()
        if target then
            kaHit(target)
            task.wait(0.05)  -- buffed from 0.1 to 0.05
        else
            task.wait(0.05)
        end
    end)
end

local function stopKillAura()
    if kaConn then kaConn:Disconnect(); kaConn = nil end
end

-- ==============================================================================
-- AUTO EAT
-- ==============================================================================
local function getInventoryFolder()
    local pg = LocalPlayer:FindFirstChild("PlayerGui")
    if not pg then return nil end
    local master = pg:FindFirstChild("MasterScreenGui")
    if not master then return nil end
    local windows = master:FindFirstChild("Windows")
    if not windows then return nil end
    local invOnly = windows:FindFirstChild("InventoryOnly")
    if not invOnly then return nil end
    return invOnly:FindFirstChild("Player")
end

local function tryAutoEat()
    if not autoEatEnabled or not ConsumeRemote then return false end
    local invFolder = getInventoryFolder()
    if not invFolder then return false end
    for _, slotNum in ipairs(EAT_SLOTS) do
        local slot = invFolder:FindFirstChild(tostring(slotNum))
        if slot then
            pcall(function() ConsumeRemote:InvokeServer(slot) end)
            Notify({Title="Auto Eat", Content="Consumed slot "..slotNum, Duration=2})
            return true
        end
    end
    return false
end

-- ==============================================================================
-- RIPTIDE HEAL
-- ==============================================================================
local RIPTIDE_MAX_IN_FLIGHT = 200
local riptideInFlight = 0

local function fireConsume(slot)
    if riptideInFlight >= RIPTIDE_MAX_IN_FLIGHT then return false end
    if not ConsumeRemote then return false end
    riptideInFlight = riptideInFlight + 1
    local ok = pcall(function()
        if ConsumeRemote:IsA("RemoteFunction") then ConsumeRemote:InvokeServer(slot)
        else ConsumeRemote:FireServer(slot) end
    end)
    riptideInFlight = riptideInFlight - 1
    return ok
end

local RIPTIDE = {
    enabled = false,
    thread = nil,
    slot = 1,
    pending = 0,
    acc = 0,
    lastFire = 0,
    baseRate = 29.4,
}
local RIPTIDE_MIN = 1
local RIPTIDE_MAX = 9

local function smoothStep(h, dt)
    if dt > 0.10 then h.acc = 0; h.lastFire = tick(); return end
    local now = tick(); if now - h.lastFire < 1/90 then return end; h.lastFire = now
    h.acc = h.acc + h.baseRate * dt * 60
    if h.acc > h.baseRate * 2 then h.acc = h.baseRate * 2 end
    local fired = 0
    while fired < math.min(35, math.floor(h.acc)) do
        if not fireConsume(h.slot) then break end
        h.slot = h.slot + 1; if h.slot > RIPTIDE_MAX then h.slot = RIPTIDE_MIN end
        h.acc = h.acc - 1; fired = fired + 1
    end
end

local function toggleRiptide()
    RIPTIDE.enabled = not RIPTIDE.enabled
    if RIPTIDE.enabled then
        RIPTIDE.slot = RIPTIDE_MIN; RIPTIDE.pending = 0; RIPTIDE.acc = 0; RIPTIDE.lastFire = 0
        RIPTIDE.thread = task.spawn(function()
            local last = tick()
            while RIPTIDE.enabled do
                local now = tick(); local dt = now - last; last = now
                smoothStep(RIPTIDE, dt)
                task.wait()
            end
        end)
        notifyToggle("Riptide Heal", true)
    else
        if RIPTIDE.thread then pcall(task.cancel, RIPTIDE.thread); RIPTIDE.thread = nil end
        notifyToggle("Riptide Heal", false)
    end
end

-- ==============================================================================
-- FLY
-- ==============================================================================
local mobileFlyVector = Vector3.zero
local mobileFlyConn = nil
local function startFly()
    if flyEnabled then return end
    flyEnabled = true
    local char = LocalPlayer.Character
    local hrp = char and char:FindFirstChild("HumanoidRootPart")
    local hum = char and char:FindFirstChild("Humanoid")
    if not hrp or not hum then flyEnabled = false; return end
    hum.WalkSpeed = 0; hum.AutoRotate = false; hum.PlatformStand = true
    local bodyGyro = Instance.new("BodyGyro", hrp); bodyGyro.P = 10000; bodyGyro.D = 500
    bodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9); bodyGyro.CFrame = hrp.CFrame
    local bodyVelocity = Instance.new("BodyVelocity", hrp); bodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9); bodyVelocity.Velocity = Vector3.zero
    mobileFlyConn = RunService.Stepped:Connect(function()
        if not flyEnabled or not hrp then return end
        local camCF = workspace.CurrentCamera.CFrame
        local dir = (camCF.LookVector * mobileFlyVector.Z) + (camCF.RightVector * mobileFlyVector.X) + Vector3.new(0, mobileFlyVector.Y, 0)
        if dir.Magnitude > 0 then bodyVelocity.Velocity = dir.Unit * FLY_SPEED else bodyVelocity.Velocity = Vector3.zero end
        bodyGyro.CFrame = camCF
    end)
    LocalPlayer.CharacterAdded:Connect(function() if flyEnabled then stopFly() end end)
end
local function stopFly()
    flyEnabled = false; mobileFlyVector = Vector3.zero
    if mobileFlyConn then mobileFlyConn:Disconnect(); mobileFlyConn = nil end
    local char = LocalPlayer.Character
    if char then
        local hrp = char:FindFirstChild("HumanoidRootPart"); local hum = char:FindFirstChild("Humanoid")
        if hrp then for _, child in ipairs(hrp:GetChildren()) do if child:IsA("BodyGyro") or child:IsA("BodyVelocity") then child:Destroy() end end end
        if hum then hum.WalkSpeed = 16; hum.AutoRotate = true; hum.PlatformStand = false end
    end
end

-- ==============================================================================
-- MOBILE CONTROLS
-- ==============================================================================
local mobileGui = Instance.new("ScreenGui")
mobileGui.Name = "SXG_MobileControls"; mobileGui.ResetOnSpawn = false; mobileGui.IgnoreGuiInset = true
pcall(function() mobileGui.Parent = game:GetService("CoreGui") end)
if not mobileGui.Parent then mobileGui.Parent = LocalPlayer.PlayerGui end
local openBtn = Instance.new("TextButton", mobileGui)
openBtn.Size = UDim2.new(0, 50, 0, 50); openBtn.Position = UDim2.new(0, 20, 0.4, 0)
openBtn.BackgroundColor3 = C.BG2; openBtn.Text = "SXG"; openBtn.TextColor3 = C.WHITE
openBtn.TextSize = 14; openBtn.Font = Enum.Font.GothamBold; openBtn.BorderSizePixel = 0
Instance.new("UICorner", openBtn).CornerRadius = UDim.new(1, 0)
local openBtnStroke = Instance.new("UIStroke", openBtn); openBtnStroke.Thickness = 1; openBtnStroke.Color = C.BRTBORDER
makeDraggable(openBtn, openBtn)
openBtn.MouseButton1Click:Connect(function() main.Visible = not main.Visible end)
local joyFrame = Instance.new("Frame", mobileGui); joyFrame.Size = UDim2.new(0, 160, 0, 160); joyFrame.Position = UDim2.new(0, 20, 1, -180); joyFrame.BackgroundTransparency = 1; joyFrame.Visible = false
local function makeDirBtn(name, text, pos, updateVec)
    local b = Instance.new("TextButton", joyFrame); b.Size = UDim2.new(0, 45, 0, 45); b.Position = pos; b.BackgroundColor3 = C.BG2; b.Text = text; b.TextColor3 = C.WHITE; b.TextSize = 16; b.Font = Enum.Font.GothamBold; b.BorderSizePixel = 0
    Instance.new("UICorner", b).CornerRadius = UDim.new(0, 8); Instance.new("UIStroke", b).Color = C.BORDER
    b.MouseButton1Down:Connect(function() mobileFlyVector = mobileFlyVector + updateVec end)
    b.MouseButton1Up:Connect(function() mobileFlyVector = mobileFlyVector - updateVec end)
    return b
end
makeDirBtn("Forward", "W", UDim2.new(0, 55, 0, 0), Vector3.new(0, 0, 1))
makeDirBtn("Left", "A", UDim2.new(0, 0, 0, 55), Vector3.new(-1, 0, 0))
makeDirBtn("Right", "D", UDim2.new(0, 110, 0, 55), Vector3.new(1, 0, 0))
makeDirBtn("Backward", "S", UDim2.new(0, 55, 0, 110), Vector3.new(0, 0, -1))
local upBtn = Instance.new("TextButton", mobileGui); upBtn.Size = UDim2.new(0, 50, 0, 50); upBtn.Position = UDim2.new(1, -70, 1, -120); upBtn.BackgroundColor3 = C.BG2; upBtn.Text = "UP"; upBtn.TextColor3 = C.WHITE; upBtn.TextSize = 12; upBtn.Font = Enum.Font.GothamBold; upBtn.BorderSizePixel = 0; upBtn.Visible = false
Instance.new("UICorner", upBtn).CornerRadius = UDim.new(0, 8); Instance.new("UIStroke", upBtn).Color = C.BORDER
upBtn.MouseButton1Down:Connect(function() mobileFlyVector = mobileFlyVector + Vector3.new(0, 1, 0) end)
upBtn.MouseButton1Up:Connect(function() mobileFlyVector = mobileFlyVector - Vector3.new(0, 1, 0) end)
local downBtn = Instance.new("TextButton", mobileGui); downBtn.Size = UDim2.new(0, 50, 0, 50); downBtn.Position = UDim2.new(1, -70, 1, -60); downBtn.BackgroundColor3 = C.BG2; downBtn.Text = "DN"; downBtn.TextColor3 = C.WHITE; downBtn.TextSize = 12; downBtn.Font = Enum.Font.GothamBold; downBtn.BorderSizePixel = 0; downBtn.Visible = false
Instance.new("UICorner", downBtn).CornerRadius = UDim.new(0, 8); Instance.new("UIStroke", downBtn).Color = C.BORDER
downBtn.MouseButton1Down:Connect(function() mobileFlyVector = mobileFlyVector + Vector3.new(0, -1, 0) end)
downBtn.MouseButton1Up:Connect(function() mobileFlyVector = mobileFlyVector - Vector3.new(0, -1, 0) end)

-- ==============================================================================
-- COMBAT TAB
-- ==============================================================================
CombatTab:CreateToggle({Name="Auto Eat",Description="Consumes food from slots 2-9.",CurrentValue=false,Callback=function(v)
    autoEatEnabled=v
    if v then
        for _,obj in ipairs(game:GetDescendants()) do
            if obj.Name=="Consume" and obj:IsA("RemoteFunction") then ConsumeRemote=obj; break end
        end
        notifyToggle("Auto Eat", true)
    else notifyToggle("Auto Eat", false) end
end})
CombatTab:CreateSlider({Name="Eat Speed",Range={0.1,2},Increment=0.1,CurrentValue=0.8,Callback=function(v) healingSpeed=v end})
CombatTab:CreateToggle({Name="Kill Aura",Description="Buffed – sends 3 hits per tick, whitelist protected.",CurrentValue=false,Callback=function(v)
    _G.KA_ENABLED=v
    if v then startKillAura() else stopKillAura() end
    notifyToggle("Kill Aura", v)
end})
CombatTab:CreateSlider({Name="Kill Aura Range",Range={5,200},Increment=5,CurrentValue=40,Callback=function(v) kaRange=v end})
local lockOnDropdown=CombatTab:CreateDropdown({Name="Lock On Target",Options=getPlayerNames(),MultipleOptions=false,Callback=function(opt)
    local p=Players:FindFirstChild(opt)
    if p then lockOnTarget=p; Notify({Title="Lock On",Content="Target: "..opt,Duration=2}) end
end})
CombatTab:CreateButton({Name="Refresh Target List",Description="Re-scans all players.",Callback=function()
    lockOnDropdown:Refresh(getPlayerNames(),true)
    Notify({Title="Lock On",Content="Refreshed.",Duration=2})
end})
CombatTab:CreateToggle({Name="Enable Lock On",Description="Teleports you behind the selected target.",CurrentValue=false,Callback=function(v)
    lockOnEnabled=v; if not v then lockOnTarget=nil end
    notifyToggle("Lock On", v)
end})

-- ==============================================================================
-- WHITELIST TAB
-- ==============================================================================
WhitelistTab:CreateDropdown({Name="Whitelisted (read-only)",Options=(function()
    local list={}; for n in pairs(WHITELIST) do table.insert(list,n) end; return list
end)(), MultipleOptions=true, Callback=function() end})
WhitelistTab:CreateButton({Name="Refresh Player List",Description="Updates list with current server players.",Callback=function()
    Notify({Title="Whitelist",Content="Refreshed.",Duration=2})
end})

-- ==============================================================================
-- HEALS TAB
-- ==============================================================================
HealTab:CreateToggle({Name="Riptide Heal",Description="Slots 1–9 · Fast smooth heal",CurrentValue=false,Callback=function(v) toggleRiptide() end})
HealTab:CreateToggle({Name="SIN Auto Eat",Description="Consumes food from slots 2–9.",CurrentValue=false,Callback=function(v)
    autoEatEnabled=v
    if v then notifyToggle("SIN Auto Eat", true) else notifyToggle("SIN Auto Eat", false) end
end})
HealTab:CreateSlider({Name="SIN Eat Speed",Range={0.1,2},Increment=0.1,CurrentValue=0.8,Callback=function(v) healingSpeed=v end})

-- ==============================================================================
-- PROTECTION TAB
-- ==============================================================================
for _,name in pairs({"FallDamage","DrownDamage","Suffocating","ServerKnockback"}) do
    ProtectionTab:CreateToggle({Name="Anti "..name,Description="Destroys the "..name.." remote.",CurrentValue=false,Callback=function(v)
        dmgSettings[name]=v
        if v then
            local remote=ReplicatedStorage:FindFirstChild(name,true) or ReplicatedStorage:FindFirstChild(name.."Remote",true)
            if remote and remote:IsA("RemoteEvent") then remote:Destroy() end
        end
        notifyToggle("Anti "..name, v)
    end})
end
ProtectionTab:CreateToggle({Name="Emergency Death TP",Description="If HP drops below 10, teleports underground.",CurrentValue=false,Callback=function(v)
    antiDeathTP=v; antiDeathTriggered=false
    notifyToggle("Emergency Death TP", v)
end})

-- ==============================================================================
-- MOVEMENT TAB
-- ==============================================================================
MovementTab:CreateSlider({Name="Fly Speed",Range={10,2000},Increment=10,CurrentValue=50,Callback=function(v) FLY_SPEED=v end})
MovementTab:CreateSlider({Name="Walk Speed",Range={16,500},Increment=1,CurrentValue=16,Callback=function(v)
    local h=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid"); if h then h.WalkSpeed=v end
end})
MovementTab:CreateSlider({Name="Jump Power",Range={50,500},Increment=10,CurrentValue=50,Callback=function(v)
    local h=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid"); if h then h.JumpPower=v end
end})
MovementTab:CreateToggle({Name="Enable Fly",Description="Camera-relative mobile touch flight.",CurrentValue=false,Callback=function(v)
    joyFrame.Visible = v; upBtn.Visible = v; downBtn.Visible = v
    if v and not flyEnabled then startFly() elseif not v and flyEnabled then stopFly() end
    notifyToggle("Fly", v)
end})
MovementTab:CreateToggle({Name="No Clip",Description="Walk through walls.",CurrentValue=false,Callback=function(v)
    _G.NOCLIP=v; notifyToggle("No Clip", v)
end})
task.spawn(function()
    RunService.Stepped:Connect(function()
        if _G.NOCLIP then
            local char=LocalPlayer.Character
            if char then for _,p in ipairs(char:GetDescendants()) do if p:IsA("BasePart") then p.CanCollide=false end end end
        end
    end)
end)

-- ==============================================================================
-- TELEPORT TAB
-- ==============================================================================
local playerDropdown=TeleportTab:CreateDropdown({Name="Select Player",Options={},MultipleOptions=false,Callback=function(opt) end})
TeleportTab:CreateButton({Name="Refresh Player List",Description="Scans server.",Callback=function()
    local names={}; for _,p in pairs(Players:GetPlayers()) do if p~=LocalPlayer then table.insert(names,p.Name) end end
    playerDropdown:Refresh(names,true)
end})
TeleportTab:CreateButton({Name="Teleport to Player",Description="Teleports to target.",Callback=function()
    local name=playerDropdown.CurrentOption
    if not name then Notify({Title="Error",Content="No player selected",Duration=3}); return end
    if type(name)=="table" then name=name[1] end
    local tp=Players:FindFirstChild(name)
    if not tp then Notify({Title="Error",Content="Player not found",Duration=3}); return end
    local targetChar=tp.Character; local targetHrp=targetChar and targetChar:FindFirstChild("HumanoidRootPart")
    local myHrp=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if targetHrp and myHrp then myHrp.CFrame=targetHrp.CFrame*CFrame.new(0,3,0); Notify({Title="Teleport",Content="Teleported to "..tp.Name,Duration=2})
    else Notify({Title="Error",Content="Missing HumanoidRootPart",Duration=3}) end
end})

-- ==============================================================================
-- LOOT TAB
-- ==============================================================================
local Drops=workspace:FindFirstChild("Drops") or workspace:WaitForChild("Drops",15)
if not Drops then Drops=Instance.new("Folder"); Drops.Name="Drops"; Drops.Parent=workspace end
local hitboxEnabled=false; local highlightEnabled=false; local descConn=nil; local hlConn=nil; local highlights={}
local function moveHitbox(obj)
    local part=obj:IsA("BasePart") and obj or obj:FindFirstChildWhichIsA("BasePart")
    if part and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        part.CFrame=LocalPlayer.Character.HumanoidRootPart.CFrame
    end
end
local function createHighlight(item)
    if not highlights[item] and (item:IsA("Model") or item:IsA("BasePart")) then
        local hl=Instance.new("Highlight",item); hl.FillColor=Color3.fromRGB(255,255,255); hl.OutlineColor=Color3.fromRGB(200,200,200); highlights[item]=hl
    end
end
LootTab:CreateToggle({Name="Teleport Drops to Me",Description="Pulls all dropped loot to your character.",CurrentValue=false,Callback=function(v)
    hitboxEnabled=v
    if v then
        for _,i in ipairs(Drops:GetChildren()) do moveHitbox(i) end
        descConn=Drops.DescendantAdded:Connect(function(obj) task.wait(0.16); if hitboxEnabled then moveHitbox(obj) end end)
    else if descConn then descConn:Disconnect(); descConn=nil end end
    notifyToggle("Teleport Drops", v)
end})
LootTab:CreateToggle({Name="Highlight Drops",Description="Draws outlines around dropped loot.",CurrentValue=false,Callback=function(v)
    highlightEnabled=v
    if v then
        for _,i in ipairs(Drops:GetChildren()) do createHighlight(i) end
        hlConn=Drops.DescendantAdded:Connect(function(obj) createHighlight(obj) end)
    else
        if hlConn then hlConn:Disconnect(); hlConn=nil end
        for _,hl in pairs(highlights) do if hl then hl:Destroy() end end
        highlights={}
    end
    notifyToggle("Highlight Drops", v)
end})

-- ==============================================================================
-- MINE TAB
-- ==============================================================================
local hookActive=false
local function enableBreakHook()
    if hookActive then return end
    repeat task.wait() until game.Players.LocalPlayer.Character
    repeat task.wait() until game.ReplicatedStorage:FindFirstChild("Systems")
    repeat task.wait() until game.Players.LocalPlayer.PlayerGui:FindFirstChild("MasterScreenGui")
    repeat task.wait() until game.Players.LocalPlayer.PlayerGui:WaitForChild("MasterScreenGui"):WaitForChild("MenuBackground").Visible == false
    task.wait(2)
    local success, err = pcall(function()
        local gbt = require(game.ReplicatedStorage.Systems.ItemsSystem.Libs.GetBreakingTime)
        hookfunction(gbt, function() return 0 end)
        hookActive = true
        notifyToggle("Instant Break", true)
    end)
    if not success then Notify({Title="Mine",Content="Failed to hook: "..tostring(err),Duration=3}) end
end
local function disableBreakHook()
    if not hookActive then return end
    hookActive = false
    notifyToggle("Instant Break", false)
end
MineTab:CreateToggle({Name="Instant Break (Hook)",Description="Hooks GetBreakingTime to return 0.",CurrentValue=false,Callback=function(v)
    if v then enableBreakHook() else disableBreakHook() end
end})

-- ==============================================================================
-- ESP TAB
-- ==============================================================================
local ESP = {}
local ESP_ENABLED = false
local Folder = workspace:FindFirstChild("LastPositionESP") or Instance.new("Folder")
Folder.Name = "LastPositionESP"; Folder.Parent = workspace
for _, child in ipairs(Folder:GetChildren()) do if child.Name:find("_ESP") then child:Destroy() end end
ESPTab:CreateToggle({Name="Enable ESP",CurrentValue=false,Description="Shows player names, health, distance",Callback=function(v) ESP_ENABLED=v; notifyToggle("ESP", v) end})
local function createESP(plr)
    if plr == LocalPlayer or ESP[plr] then return end
    local part = Instance.new("Part"); part.Name = plr.Name.."_ESP"; part.Size = Vector3.new(2,5,1); part.Transparency = 1; part.Anchored = true; part.CanCollide = false; part.Parent = Folder
    local gui = Instance.new("BillboardGui", part); gui.Name = "ESP"; gui.AlwaysOnTop = true; gui.Size = UDim2.new(0,90,0,135); gui.StudsOffsetWorldSpace = Vector3.new(0,2.8,0); gui.Enabled = ESP_ENABLED
    local container = Instance.new("Frame", gui); container.Size = UDim2.new(1,0,1,0); container.BackgroundTransparency = 1
    local nameText = Instance.new("TextLabel", container); nameText.Size = UDim2.new(1,0,0,16); nameText.Text = plr.Name; nameText.TextColor3 = Color3.new(1,1,1); nameText.TextStrokeTransparency = 0; nameText.BackgroundTransparency = 1; nameText.Font = Enum.Font.SourceSansBold; nameText.TextSize = 13
    local hpText = Instance.new("TextLabel", container); hpText.Size = UDim2.new(1,0,0,16); hpText.Position = UDim2.new(0,0,0,82); hpText.TextColor3 = Color3.fromRGB(255,255,255); hpText.TextStrokeTransparency = 0; hpText.BackgroundTransparency = 1; hpText.TextSize = 12
    local distText = Instance.new("TextLabel", container); distText.Size = UDim2.new(1,0,0,16); distText.Position = UDim2.new(0,0,0,98); distText.TextColor3 = Color3.fromRGB(255,255,255); distText.TextStrokeTransparency = 0; distText.BackgroundTransparency = 1; distText.TextSize = 11
    ESP[plr] = {Part=part, Gui=gui, NameText=nameText, HealthText=hpText, DistanceText=distText}
end
Players.PlayerRemoving:Connect(function(plr) if ESP[plr] then if ESP[plr].Part then ESP[plr].Part:Destroy() end ESP[plr]=nil end end)
task.spawn(function()
    while true do
        task.wait(0.5)
        if ESP_ENABLED then
            for _, plr in pairs(Players:GetPlayers()) do
                if plr ~= LocalPlayer then
                    if not ESP[plr] then createESP(plr) end
                    local esp = ESP[plr]
                    if esp then
                        local pos = plr:GetAttribute("LastPosition")
                        local hp = plr:GetAttribute("Health") or plr:GetAttribute("health")
                        if typeof(pos) == "Vector3" then
                            esp.Gui.Enabled = true; esp.Part.Position = pos
                            esp.HealthText.Text = typeof(hp)=="number" and math.floor(hp).." HP" or "? HP"
                            local hrp = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                            esp.DistanceText.Text = hrp and math.floor((hrp.Position-pos).Magnitude).." Stud" or "? Stud"
                        else esp.Gui.Enabled = false end
                    end
                end
            end
        else for _, esp in pairs(ESP) do if esp and esp.Gui then esp.Gui.Enabled = false end end end
    end
end)

-- ==============================================================================
-- PERFORMANCE TAB
-- ==============================================================================
PerformanceTab:CreateButton({Name="Boost FPS",Description="Disables shadows, fog, particles.",Callback=function()
    local l=game:GetService("Lighting"); l.GlobalShadows=false; l.FogEnd=999999; l.Brightness=1
    for _,o in pairs(workspace:GetDescendants()) do if o:IsA("ParticleEmitter") or o:IsA("Trail") or o:IsA("Fire") or o:IsA("Smoke") or o:IsA("Sparkles") then o.Enabled=false end end
    pcall(function() UserSettings().GameSettings.SavedQualityLevel=Enum.QualityLevel.Level01 end)
    if collectgarbage then collectgarbage("collect") end
    Notify({Title="Performance",Content="FPS Boosted.",Duration=3})
end})
PerformanceTab:CreateButton({Name="Flush Memory (GC)",Description="Triggers Lua garbage collector.",Callback=function()
    if collectgarbage then collectgarbage("collect"); Notify({Title="Performance",Content="Memory cleared.",Duration=2}) end
end})

-- ==============================================================================
-- SETTINGS TAB
-- ==============================================================================
SettingsTab:CreateToggle({Name="Anti-AFK",Description="Prevents the 20-minute idle kick.",CurrentValue=false,Callback=function(v)
    _G.ANTI_AFK=v
    if v then
        local VU=game:GetService("VirtualUser")
        _G.AFK_Conn=LocalPlayer.Idled:Connect(function() VU:CaptureController(); VU:ClickButton2(Vector2.new()) end)
    else if _G.AFK_Conn then _G.AFK_Conn:Disconnect(); _G.AFK_Conn=nil end end
    notifyToggle("Anti-AFK", v)
end})
SettingsTab:CreateToggle({Name="Hide GUI",Description="Hides the hub window.",CurrentValue=false,Callback=function(v) main.Visible=not v end})

-- ==============================================================================
-- SAFETY TAB
-- ==============================================================================
SafetyTab:CreateButton({Name="Destroy GUI",Description="Removes the hub.",Callback=function()
    sg:Destroy()
    if notifHolder and notifHolder.Parent then notifHolder.Parent:Destroy() end
    if mobileGui then mobileGui:Destroy() end
end})
SafetyTab:CreateButton({Name="Rejoin Server",Description="Reconnects.",Callback=function()
    game:GetService("TeleportService"):Teleport(game.PlaceId,LocalPlayer)
end})

-- ==============================================================================
-- WHITELIST JOIN NOTIFICATIONS
-- ==============================================================================
local function onPlayerAdded(plr)
    if isWhitelisted(plr) then
        sendChatNotification("SHADOW X GOATJO: Owner " .. plr.Name .. " joined the game! DO NOT ATTACK THEM.")
        Notify({Title="OWNER JOINED", Content=plr.Name .. " is protected.", Duration=5})
    end
end
Players.PlayerAdded:Connect(onPlayerAdded)
for _, plr in ipairs(Players:GetPlayers()) do if plr ~= LocalPlayer then onPlayerAdded(plr) end end

-- ==============================================================================
-- RUNTIME LOOP
-- ==============================================================================
RunService.Heartbeat:Connect(function()
    local char=LocalPlayer.Character
    local hrp=char and char:FindFirstChild("HumanoidRootPart")
    local hum=char and char:FindFirstChild("Humanoid")

    if autoEatEnabled and (tick()-lastHeal>=healingSpeed) then
        tryAutoEat()
        lastHeal=tick()
    end

    for name,enabled in pairs(dmgSettings) do
        if enabled then
            local remote=ReplicatedStorage:FindFirstChild(name,true) or ReplicatedStorage:FindFirstChild(name.."Remote",true)
            if remote and remote:IsA("RemoteEvent") then remote:Destroy() end
        end
    end

    if antiDeathTP and hum and hrp then
        local hp=hum.Health
        if hp>0 and hp<10 and not antiDeathTriggered then
            antiDeathTriggered=true
            hrp.CFrame=CFrame.new(hrp.Position.X,-500000,hrp.Position.Z)
            Notify({Title="Protection",Content="Emergency TP triggered! ("..math.floor(hp).." HP)",Duration=3})
            task.spawn(function() task.wait(5); antiDeathTriggered=false end)
        end
    end

    if lockOnEnabled and lockOnTarget and lockOnTarget.Character
    and lockOnTarget.Character:FindFirstChild("HumanoidRootPart") and hrp
    and not isWhitelisted(lockOnTarget) then
        hrp.CFrame=lockOnTarget.Character.HumanoidRootPart.CFrame*CFrame.new(0,0,3)
    end

    if _G.NOCLIP and char then
        for _,p in pairs(char:GetDescendants()) do if p:IsA("BasePart") then p.CanCollide=false end end
    end
end)

-- ==============================================================================
-- INIT
-- ==============================================================================
sendChatNotification("SHADOW X GOATJO V3 HUB IS LOADED")
Notify({Title="SHADOW X GOATJO V3",Content="Loaded. Welcome, "..LocalPlayer.Name.."!",Duration=4})
