getgenv().Settings = {
    ["Auto Click Keybind"] = "B", 
    ["Lock Mouse Position Keybind"] = "",
    ["Right Click"] = false,
    ["GUI"] = true, 
    ["Delay"] = 0 
}
loadstring(game:HttpGet("https://raw.githubusercontent.com/BimbusCoder/Script/main/Auto%20Clicker.lua"))()

local player = game.Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")
local teleporting = false 

local function getNearestNPC(character)
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
    local npcNames = {"Vampire", "Skeleton"}
    local nearestNPC = nil
    local shortestDistance = math.huge 

    for _, npcName in ipairs(npcNames) do
        local npc = game.Workspace:FindFirstChild(npcName)
        if npc and npc.PrimaryPart then
            local distance = (humanoidRootPart.Position - npc.PrimaryPart.Position).magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                nearestNPC = npc
            end
        end
    end

    return nearestNPC 
end

local function teleportToNearestNPC(character)
    while teleporting do
        local nearestNPC = getNearestNPC(character)
        if nearestNPC then
            character:SetPrimaryPartCFrame(nearestNPC.PrimaryPart.CFrame)
        else
            print("Ближайший NPC не найден!")
        end
        wait(0.1) 
    end
end

local function onCharacterAdded(character)
    character:WaitForChild("HumanoidRootPart")

    if teleporting then
        teleportToNearestNPC(character)
    end
end

UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if input.KeyCode == Enum.KeyCode.F1 and not gameProcessedEvent then
        teleporting = not teleporting
        if teleporting then
            teleportToNearestNPC(player.Character or player.CharacterAdded:Wait())
        end
    end
end)

player.CharacterAdded:Connect(onCharacterAdded)
