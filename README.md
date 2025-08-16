local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- posição do seu stand (ajusta aí)
local standPos = Vector3.new(0, 0, 0)

-- Função principal
local function OnFakeDonation(donor)
    local char = player.Character or player.CharacterAdded:Wait()
    local hrp = char:WaitForChild("HumanoidRootPart")

    local donorChar = donor.Character
    if donorChar then
        local donorHRP = donorChar:WaitForChild("HumanoidRootPart")
        -- teleporta pra perto do doador
        hrp.CFrame = CFrame.new(donorHRP.Position + Vector3.new(2,0,0))
    end

    -- manda mensagem no chat
    game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(
        "hey, can i have some robux? follow me.",
        "All"
    )

    -- espera 5 segundos
    task.wait(5)

    -- volta pro stand
    hrp.CFrame = CFrame.new(standPos)
end

-- Simulação: se alguém digitar "!doar", ativa a função
Players.PlayerAdded:Connect(function(plr)
    plr.Chatted:Connect(function(msg)
        if msg:lower() == "!doar" then
            OnFakeDonation(plr)
        end
    end)
end)
