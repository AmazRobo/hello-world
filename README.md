local tool = script.Parent
local canDamage = false
local canSwing = true

local Handle = script.Parent:WaitForChild("Handle")

Sounds = {
	Slash = Handle:WaitForChild("SlashSound"),
	Lunge = Handle:WaitForChild("LungeSound"),
	Unsheath = Handle:WaitForChild("EquipSound"),
	HitSound1 = Handle:WaitForChild("HitSound1")
}



local function onTouch(otherPart)
	local humanoid = otherPart.Parent:FindFirstChild("Humanoid")
	if not humanoid then 
		return 
	end
	if humanoid.Parent ~= tool.Parent and canDamage then 
		humanoid:TakeDamage(5)
	else
		return
	end
	canDamage = false
end



local function slash()
	local Character = tool.Parent
	local Humanoid = Character.Humanoid
	local Sword_Slash_Animation = Instance.new("Animation")
	Sword_Slash_Animation.AnimationId = "rbxassetid://9404404634"
	local AnimationTrack = Humanoid:LoadAnimation(Sword_Slash_Animation)
	AnimationTrack:Play()
	canDamage = true
end

tool.Activated:Connect(slash)
tool.Handle.Touched:Connect(onTouch)
