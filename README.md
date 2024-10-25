# Roblox-Script-For-PvP-Zone
# What Is Roblox
Roblox is an online platform that allows users to create and play games made by other users. It combines elements of a game creation tool and a multiplayer gaming environment, where players can use Roblox Studio to build games using Lua scripting and share them on the platform. 

Use This Script For A PvP Zone Circle in You Roblox Game

# SCRIPT
-- Settings

local zonePart = workspace:WaitForChild("BattleZone") -- Rename this to the name of your circular part

local zoneRadius = zonePart.Size.X / 2 -- Radius based on the part's size

local playersInZone = {} -- Track players in the zone

-- Function to check if a player is inside the circle

local function isPlayerInZone(player)

    local character = player.Character
    
    if character and character:FindFirstChild("HumanoidRootPart") then
    
        local distance = (character.HumanoidRootPart.Position - zonePart.Position).magnitude
        
        return distance <= zoneRadius
        
    end
    
    return false
    
end

-- Enable or disable attack based on location

local function updateAttackPermission()

    for _, player in pairs(game.Players:GetPlayers()) do
    
        if isPlayerInZone(player) then
        
            playersInZone[player] = true
            
        else
        
            playersInZone[player] = nil
            
        end
        
    end
    
end

-- Monitor when a player joins or leaves the zone

game.Players.PlayerAdded:Connect(function(player)

    player.CharacterAdded:Connect(function(character)
    
        while true do
        
            wait(1) -- Adjust frequency if needed
            
            updateAttackPermission()
            
        end
        
    end)
    
end)

-- Attack Script (use this in the sword tool)

local function onAttack(hitPlayer, attackerPlayer)

    if playersInZone[hitPlayer] and playersInZone[attackerPlayer] then
    
        -- Allow attack logic here, such as dealing damage
        
        local humanoid = hitPlayer.Character:FindFirstChild("Humanoid")
        
        if humanoid then
        
            humanoid:TakeDamage(20) -- Adjust damage as needed
            
        end
        
    else
    
        -- Deny attack, could show a message or sound for feedback
        
        attackerPlayer:SendNotification({Title = "Can't Attack!", Text = "Only attack inside the battle zone!"})
        
    end
    
end

-- Connect the function to swords/tools that players use to attack

-- Example: tool.Activated:Connect(function() onAttack(hitPlayer, attackerPlayer) end)

# ( THE LINES STARTING WITH "--" ARE THE LINES EXPLAINING THE SCRIPT YOU NEED TO REMOVE THOSE LINES )

# ( THE SHORT LINE IS AFTER SOME LINES IS THE LINE THAT TELLS WHAT TO BE EDITED IN YOUR SCRIPT ACCORDING TO YOUR GAME )

