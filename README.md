
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
