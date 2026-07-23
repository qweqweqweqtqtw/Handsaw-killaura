--[[
 .____                  ________ ___.    _____                           __                
 |    |    __ _______   \_____  \\_ |___/ ____\_ __  ______ ____ _____ _/  |_  ___________ 
 |    |   |  |  \__  \   /   |   \| __ \   __\  |  \/  ___// ___\\__  \\   __\/  _ \_  __ \
 |    |___|  |  // __ \_/    |    \ \_\ \  | |  |  /\___ \\  \___ / __ \|  | (  <_> )  | \/
 |_______ \____/(____  /\_______  /___  /__| |____//____  >\___  >____  /__|  \____/|__|   
         \/          \/         \/    \/                \/     \/     \/                   
          \_Welcome to LuaObfuscator.com   (Alpha 0.10.9) ~  Much Love, Ferib 

]]--

bit32 = {};
local N = 32;
local P = 2 ^ N;
bit32.bnot = function(x)
	x = x % P;
	return (P - 1) - x;
end;
bit32.band = function(x, y)
	if (y == 255) then
		return x % 256;
	end
	if (y == 65535) then
		return x % 65536;
	end
	if (y == 4294967295) then
		return x % 4294967296;
	end
	x, y = x % P, y % P;
	local r = 0;
	local p = 1;
	for i = 1, N do
		local a, b = x % 2, y % 2;
		x, y = math.floor(x / 2), math.floor(y / 2);
		if ((a + b) == 2) then
			r = r + p;
		end
		p = 2 * p;
	end
	return r;
end;
bit32.bor = function(x, y)
	if (y == 255) then
		return (x - (x % 256)) + 255;
	end
	if (y == 65535) then
		return (x - (x % 65536)) + 65535;
	end
	if (y == 4294967295) then
		return 4294967295;
	end
	x, y = x % P, y % P;
	local r = 0;
	local p = 1;
	for i = 1, N do
		local a, b = x % 2, y % 2;
		x, y = math.floor(x / 2), math.floor(y / 2);
		if ((a + b) >= 1) then
			r = r + p;
		end
		p = 2 * p;
	end
	return r;
end;
bit32.bxor = function(x, y)
	x, y = x % P, y % P;
	local r = 0;
	local p = 1;
	for i = 1, N do
		local a, b = x % 2, y % 2;
		x, y = math.floor(x / 2), math.floor(y / 2);
		if ((a + b) == 1) then
			r = r + p;
		end
		p = 2 * p;
	end
	return r;
end;
bit32.lshift = function(x, s_amount)
	if (math.abs(s_amount) >= N) then
		return 0;
	end
	x = x % P;
	if (s_amount < 0) then
		return math.floor(x * (2 ^ s_amount));
	else
		return (x * (2 ^ s_amount)) % P;
	end
end;
bit32.rshift = function(x, s_amount)
	if (math.abs(s_amount) >= N) then
		return 0;
	end
	x = x % P;
	if (s_amount > 0) then
		return math.floor(x * (2 ^ -s_amount));
	else
		return (x * (2 ^ -s_amount)) % P;
	end
end;
bit32.arshift = function(x, s_amount)
	if (math.abs(s_amount) >= N) then
		return 0;
	end
	x = x % P;
	if (s_amount > 0) then
		local add = 0;
		if (x >= (P / 2)) then
			add = P - (2 ^ (N - s_amount));
		end
		return math.floor(x * (2 ^ -s_amount)) + add;
	else
		return (x * (2 ^ -s_amount)) % P;
	end
end;
local v0 = string.char;
local v1 = string.byte;
local v2 = string.sub;
local v3 = bit32 or bit;
local v4 = v3.bxor;
local v5 = table.concat;
local v6 = table.insert;
local function v7(v15, v16)
	local v17 = {};
	for v18 = 1, #v15 do
		v6(v17, v0(v4(v1(v2(v15, v18, v18 + 1)), v1(v2(v16, 1 + (v18 % #v16), 1 + (v18 % #v16) + 1))) % 256));
	end
	return v5(v17);
end
local v8 = game:GetService(v7("\225\207\218\60\227\169\212", "\126\177\163\187\69\134\219\167"));
local v9 = game:GetService(v7("\17\200\58\201\245\32\204\62\192\248\16\217\37\215\253\36\200", "\156\67\173\74\165"));
local v10 = v8.LocalPlayer;
local v11 = v9:WaitForChild(v7("\23\184\68\20\189\50", "\38\84\215\41\118\220\70"));
local v12 = 14.4;
local v13 = 0.29;
local v14 = v13 / 1.3;
_G.HandsawAura = true;
task.spawn(function()
	while _G.HandsawAura do
		task.wait(v14);
		local v19 = v10.Character;
		local v20 = v19 and v19:FindFirstChild(v7("\120\23\44\22\237\81\1", "\158\48\118\66\114"));
		local v21 = v19 and v19:FindFirstChild(v7("\131\49\29\55\125\170\242\175\22\31\57\103\149\250\185\48", "\155\203\68\112\86\19\197"));
		if (v19 and v20 and v21) then
			for v22, v23 in ipairs(v8:GetPlayers()) do
				if ((v23 ~= v10) and v23.Character) then
					local v24 = v23.Character;
					local v25 = v24:FindFirstChild(v7("\114\210\36\239\79", "\152\38\189\86\156\32\24\133")) or v24:FindFirstChild(v7("\212\66\170\71\242\88\174\66\206\88\168\82\204\86\181\82", "\38\156\55\199"));
					local v26 = v24:FindFirstChildOfClass(v7("\128\104\113\41\29\123\243\71", "\35\200\29\28\72\115\20\154"));
					if (v25 and v26 and (v26.Health > 0)) then
						local v27 = (v21.Position - v25.Position).Magnitude;
						if (v27 <= v12) then
							pcall(function()
								local v28 = v21.CFrame;
								v21.CFrame = CFrame.new(v25.Position - (v25.CFrame.LookVector * 1.8));
								local v30 = {v19,v25,v20};
								v11:FireServer(unpack(v30));
								v21.CFrame = v28;
							end);
							break;
						end
					end
				end
			end
		end
	end
end);
