getgenv().script_key = getgenv()['script_key']

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/notjohnnylol/Azusidian/refs/heads/main/UILoader"))()
local api = loadstring(game:HttpGet("https://sdkapi-public.luarmor.net/library.lua"))()
local Window = Library:CreateWindow({Title = "Azure ", Footer = "Key System", Icon = 112280917739514, NotifySide = "Left", ShowCustomCursor = false})
local Tabs = {Key = Window:AddTab("Azure Keysystem", "key")}

local key = Tabs.Key:AddLeftGroupbox("Key Input")
local keyLinks = Tabs.Key:AddRightGroupbox("Key System Links")
local UnloadUI = Tabs.Key:AddRightGroupbox("UI Unloading")

if not game:GetService("Players").LocalPlayer then
    game:GetService("Players").PlayerAdded:Wait()
end

api.script_id = "c6a488fafed9291db97ad2202b349825"

local function load_script(key)
    local dec_key = key:gsub("%s+", "")
    getgenv().script_key = dec_key
    local success, err = pcall(function()
        local script_content = game:HttpGet("https://api.luarmor.net/files/v3/loaders/c6a488fafed9291db97ad2202b349825.lua")
        loadstring(script_content)()
    end)
    if success then
        task.wait()
        Library:Unload()
    else
        Library:Notify({Title = "Azure Keysystem", Description = "something fucking went wrong: " .. tostring(err), Time = 4})
    end
end

key:AddInput("AzureKey", {
    Default = "",
    Numeric = false,
    Finished = true,
    ClearTextOnFocus = false,
    Text = "Enter Key",
    Placeholder = "Paste your key here",
    Callback = function(Value)
        local status = api.check_key(Value)
        if status.code == "KEY_VALID" then
            writefile("savedazurekey", Value)
            Library:Notify({Title = "Azure Keysystem", Description = "Welcome! Key: " .. Value .. " accepted and saved.", Time = 4})
            load_script(Value)
        elseif status.code == "KEY_HWID_LOCKED" then
            Library:Notify({Title = "Azure Keysystem", Description = "Key linked to a different HWID. Please reset it using our bot.", Time = 4})
        elseif status.code == "KEY_INCORRECT" then
            Library:Notify({Title = "Azure Keysystem", Description = "Key is wrong or deleted!", Time = 4})
        else
            Library:Notify({Title = "Azure Keysystem", Description = "Key is invalid! " .. status.message .. " (Code: " .. status.code .. ")", Time = 4})
        end
    end
})

keyLinks:AddButton({Text = "Linkvertise", Func = function()
    setclipboard("https://ads.luarmor.net/get_key?for=Azure_Hub_KEY-otfjcauwUgdh")
    Library:Notify({Title = "Azure Keysystem", Description = "Linkvertise link copied to clipboard!", Time = 2})
end})

keyLinks:AddButton({Text = "Lootlabs", Func = function()
    setclipboard("https://ads.luarmor.net/get_key?for=Azure_Hub_Lootlabs-nRjyMTOmyBby")
    Library:Notify({Title = "Azure Keysystem", Description = "Lootlabs link copied to clipboard!", Time = 2})
end})

UnloadUI:AddButton({Text = "Unload UI", Func = function()
    Library:Unload()
end})

if isfile("savedazurekey") then
    task.spawn(function()
        local saved_key = readfile("savedazurekey"):gsub("%s+", "")
        local status = api.check_key(saved_key)
        if status.code == "KEY_VALID" then
            getgenv().script_key = saved_key
            Library:Notify({Title = "Azure Keysystem", Description = "Loaded saved key: " .. saved_key, Time = 4})
            load_script(saved_key)
        end
    end)
end
