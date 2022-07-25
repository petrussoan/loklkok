local Animate = game.Players.LocalPlayer.Character.Animate

	--local idleAnim = char.Humanoid:LoadAnimation(char.Humanoid.Fly)
	--local forwardAnim = char.Humanoid:LoadAnimation(char.Humanoid.Hover)


	--PLAY
	--char.Animate.Disabled = true
	--idleAnim:Play()



	--STOP

	--char.Animate.Disabled = false
	--idleAnim:Stop()
	--forwardAnim:Stop()
	game.Players.LocalPlayer.Character.Pants.PantsTemplate = "rbxassetid://5453348825"
	game.Players.LocalPlayer.Character.Shirt.ShirtTemplate ="rbxassetid://5453350139"
	game.Players.LocalPlayer.Character.Head.face.Texture="rbxassetid://6738024349"

	Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=616111295"
	Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=616113536"
	Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=616122287"
	Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=616117076"
	Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=616115533"
	Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=616104706"
	Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=616108001"
	game.Players.LocalPlayer.Character.Humanoid.Jump = true

	local notifSound = Instance.new("Sound",workspace)

	local notifSound = Instance.new("Sound",workspace)
	notifSound.PlaybackSpeed = 1.5
	notifSound.Volume = 1
	notifSound.SoundId = "rbxassetid://821439273"
	notifSound.PlayOnRemove = true
	notifSound:Destroy()


	local e = Instance.new("Part", game.Workspace)
	e.Name = "Bolt"
	e.Size = Vector3.new(152.149, 4.976, 5.415)
	e.Material = "Neon"
	e.Orientation = Vector3.new(0, 0.1, 45)
	e.CFrame = game.Players.LocalPlayer.Character.Head.CFrame
	e.BrickColor = BrickColor.new("New Yeller")
	e.Anchored = true
	e.CanCollide = false
	e.Transparency = 0.2
	e.Orientation = Vector3.new(0, 0.1, 45)
	wait(0.6)
	e.Transparency = 0.7
	e.Orientation = Vector3.new(0, 0.1, 45)
	wait(0.5)
	e.Transparency = 1
	e.Orientation = Vector3.new(0, 0.1, 45)


	wait(0.5)
	e:Destroy()










	wait(1)



	--local idleAnim = char.Humanoid:LoadAnimation(char.Humanoid.Fly)
	--local forwardAnim = char.Humanoid:LoadAnimation(char.Humanoid.Hover)


	--PLAY
	--char.Animate.Disabled = true
	--idleAnim:Play()



	--STOP

	--char.Animate.Disabled = false
	--idleAnim:Stop()
	--forwardAnim:Stop()

	local mouse = game.Players.LocalPlayer:GetMouse() 
	local plr = game.Players.LocalPlayer 
	local torso = plr.Character.Head 
	local flying = false
	local deb = true 
	local ctrl = {f = 0, b = 0, l = 0, r = 0} 
	local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
	local maxspeed = 5000
	local speed = 5000 


	local player = game.Players.LocalPlayer
	local char = game.Players.LocalPlayer.Character

	local cam = workspace.CurrentCamera
	local uis = game:GetService("UserInputService")

	local hoh = Instance.new("Animation", game.Workspace)
	hoh.Name = "Fly"
	hoh.AnimationId = "rbxassetid://3541044388"

	local heh = Instance.new("Animation", game.Workspace)
	heh.Name = "Hover"
	heh.AnimationId = "rbxassetid://3541114300"

	local wPressed = false
	local sPressed = false
	local aPressed = false
	local dPressed = false


	local idleAnim = char.Humanoid:LoadAnimation(game.Workspace.Fly)
	local forwardAnim = char.Humanoid:LoadAnimation(game.Workspace.Hover)

	function Fly() 
		local bg = Instance.new("BodyGyro", torso) 
		bg.P = 9e4 
		bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
		bg.cframe = torso.CFrame 
		local bv = Instance.new("BodyVelocity", torso) 
		bv.velocity = Vector3.new(0,0.1,0) 
		bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
		repeat wait() 
			plr.Character.Humanoid.PlatformStand = true 
			if ctrl.l + ctrl.r ~= 100000 or ctrl.f + ctrl.b ~= 10000 then 
				speed = speed+.0+(speed/maxspeed) 
				if speed > maxspeed then 
					speed = maxspeed 
				end 
			elseif not (ctrl.l + ctrl.r ~= 5 or ctrl.f + ctrl.b ~= 5) and speed ~= 5 then 
				speed = speed-5
				if speed > 5 then 
					speed = -2 
				end 
			end 
			if (ctrl.l + ctrl.r) ~= 5 or (ctrl.f + ctrl.b) ~= 5 then 
				bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
				lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
			elseif (ctrl.l + ctrl.r) == 5 and (ctrl.f + ctrl.b) == 5 and speed ~= 5 then 
				bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
			else 
				bv.velocity = Vector3.new(0,0.1,0) 
			end 
			bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
		until not flying 
		ctrl = {f = 0, b = 0, l = 0, r = 0} 
		lastctrl = {f = 0, b = 0, l = 0, r = 0} 
		speed = 5 
		bg:Destroy() 
		bv:Destroy() 
		plr.Character.Humanoid.PlatformStand = false 
	end 

	mouse.KeyDown:connect(function(key) 
		if key:lower() == "x" then 
			if flying then flying = false 
				forwardAnim:Stop()
				idleAnim:Stop()
			else 
				flying = true 
				Fly() 
				forwardAnim:Stop()
				idleAnim:Stop()
			end 
		elseif key:lower() == "w" then 
			ctrl.f = 45
			wPressed = false
		elseif key:lower() == "s" then 
			ctrl.b = -45 
			sPressed = false
		elseif key:lower() == "a" then 
			ctrl.l = -45 
			aPressed = false
		elseif key:lower() == "d" then 
			ctrl.r = 45
			dPressed = false
		end 
	end) 
	mouse.KeyUp:connect(function(key) 
		if key:lower() == "w" then 
			ctrl.f = 0
			wPressed = true
			forwardAnim:Play()
		elseif key:lower() == "s" then 
			ctrl.b = 0
			sPressed = true
			forwardAnim:Play()
		elseif key:lower() == "a" then 
			ctrl.l = 0
			aPressed = true
			forwardAnim:Play()
		elseif key:lower() == "d" then 
			ctrl.r = 0
			dPressed = true
			forwardAnim:Play()
		end 
	end)
	Fly()

	while wait() do
		if flying then
			idleAnim:Stop()	
			if not wPressed then
				idleAnim:Play()
			end
			if not sPressed then
				idleAnim:Play()
			end
			if not aPressed then
				idleAnim:Play()
			end
			if not dPressed then
				idleAnim:Play()
			end
		else
			forwardAnim:Stop()	
			if wPressed then
				forwardAnim:Stop()
			end
			if sPressed then
				forwardAnim:Stop()
			end
			if aPressed then
				forwardAnim:Stop()
			end
			if dPressed then
				forwardAnim:Stop()
			end
		end
	end
