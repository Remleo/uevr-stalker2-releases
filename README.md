# S.T.A.L.K.E.R. 2 in full VR

Play STALKER 2 in VR with your own hands. Pull guns from over your shoulder, raise them to your eye to aim,
check your wrist for the bolt, put the scanner up with your left hand. No buttons for any of it, just gestures.

It's built on a fork of [praydog's UEVR](https://github.com/praydog/UEVR) with fixes for STALKER 2 on Unreal Engine 5.5,
plus a profile made for this game. Everything you need is in one archive.

**It's an alpha.** Very playable, but expect rough edges. If something breaks, see [Troubleshooting](#troubleshooting)
and tell us about it.

## Getting started

1. **Unzip the archive** anywhere you like, e.g. `D:\Stalker2VR`. Keep the folder structure as it is.
2. **Start your VR runtime.** Best is **Virtual Desktop with VDXR**: in the **Virtual Desktop Streamer** app on your
   PC, go to **Options** and set **OpenXR Runtime** to **VDXR**. Then connect from the headset as usual. Anything else
   that provides OpenXR should work too (Quest Link, SteamVR), but SteamVR in particular costs you frames.
3. **Run `UEVRInjector.exe`** from that folder and leave it open.
4. **Start the game.** A few seconds later VR switches on by itself.
5. **Put the headset on.** The main menu floats in front of you. Load a save and have fun.

## Gestures

Hold the controllers like you'd hold your hands. Most things are "put your hand there and squeeze".

**Drawing anything = squeeze the grip and keep holding it.** The weapon (or grenade, or scanner) stays in your hand for
as long as you hold the grip. Let go and it's put away. There's no separate "holster" button.

### Right hand: weapons

| what | how |
|---|---|
| **Primary weapon** | reach over your **right shoulder** and squeeze the grip |
| **Secondary weapon** | reach over your **left shoulder** with your right hand, squeeze the grip |
| **Pistol** | reach **under your left armpit** (like a shoulder holster), squeeze the grip |
| **Grenade** | right hand at the **middle of your chest**, squeeze the grip |
| **Keep it** | keep holding the grip. **Let go and the weapon goes away.** |
| **Shoot** | right trigger |
| **Aim down the sights** | raise the gun to your eye and look along it, like a real one. Lower it to stop. Scopes zoom in. |
| **Throw a grenade** | right hand at your chest, squeeze and **keep holding the grip** (that's the draw), then pull the trigger to wind up and let go of the trigger to throw |
| **Ammo type, fire mode, attachments** | turn the gun **side-on to your eyes**, like you're checking it out. The game's weapon menu opens and shows them; use the buttons it shows. Look away to close it. |

### Left hand: gear

| what | how |
|---|---|
| **Bolt and knife** | look at the **back of your left wrist**, like checking a watch. The bolt and the knife show up there. Grab one with your right hand (squeeze the grip near it). |
| **Anomaly scanner** | reach over your **left shoulder** with your left hand, squeeze the grip. Hold it up to read it; let go to put it away. |
| **Head lamp** | left hand to your **left temple**, pull the left trigger. The light follows your head. |

### Everything else

- **Walk** with the left stick, in the direction you're looking. **Turn** with the right stick. You can also just
  walk around your room.
- **Jump, crouch, reload, use, inventory** and the rest are the game's normal gamepad buttons, on your controllers.
- **Buttons match their labels.** On Quest controllers this profile puts the Xbox buttons where the letters say:
  **A and B on the right controller, X and Y on the left**. Stock UEVR swaps two of them (Xbox B ends up on the left X
  and Xbox X on the right B), so if you've played other UEVR games, that's why it feels different here. Prefer the
  stock layout? Just delete `UnrealVRMod\Stalker2\_interaction_profiles_oculus_touch_controller.json` and restart the
  game.
- **Pause menu**: a short press of the **menu button** on the left controller.
- **PDA**: a **long press** of that same menu button (Quest controllers have only one menu button, so UEVR gives a
  short press and a long press different jobs).
- **Things you can interact with** get their marker floating right on them in the world.
- **Menus** stay put where they open, so you can look around them.

## Troubleshooting

### `UEVRInjector.exe` disappeared

Windows Defender sometimes deletes it right after unzipping. Injectors look scary to antivirus software. Add the folder
to Defender's exclusions (Windows Security → Virus & threat protection → Manage settings → Exclusions) and unzip
again.

### VR didn't switch on

Make sure `UEVRInjector.exe` is still open. In its window, pick the game in the list and click **Inject**.

### The hands go weird

Sometimes after a load or a crazy moment the hands or the weapon can get stuck, float off or vanish. Easy fix, no
restart needed:

1. Open the UEVR menu: **click both sticks at the same time** (L3 + R3), or press **Insert** on the keyboard.
2. Go to **LuaLoader** → **Main**.
3. Hit **Reset scripts**.

Everything gets rebuilt in a second. Close the menu the same way you opened it.

### The game is in a window when I play without VR

That's on purpose. In VR the profile switches the game to windowed mode so the HUD fits the headset, and the game
remembers that when you quit. For flat play, just switch it back to fullscreen in the game's display settings.

## Settings

The profile has a few settings of its own, in the same UEVR menu under **LuaLoader** → **Stalker2**:

- **Interface**: how far away and how big the HUD is, and how high it sits; the same three for menus. Plus a
  slider that moves just the HUD down inside its frame.
- **Aiming**: how far the view shifts to your right eye when you look through a scope. Tweak it if the scope doesn't
  line up with your eye.
- **Debug**: **Write the log**, for when you're sending us a bug report.

Changes apply right away and are saved for next time.

## What's under the hood

This isn't stock UEVR. It's [our fork](https://github.com/remleo/UEVR) with a bunch of fixes, most of them made for
STALKER 2 on UE 5.5.

**First and most important: it actually runs.** Stock UEVR doesn't cope with STALKER 2 Update 2: the game's move to
Unreal Engine 5.5 left it without a UI, with broken console settings, and crashing on save loads. This build starts,
plays and loads saves without crashing.

### Things you'll see

- **Both eyes see the same lighting.** Stock UEVR gives each eye its own copy of the game's far lighting, and one
  eye's copy goes stale, so distant shading differed between your eyes. Now they share one. Up close, walls at an angle
  used to get darker patches in one eye; a new "canted" projection fixes that and costs no FPS.
- **No more squeezed right eye.** Dynamic resolution squashed the right eye's picture whenever it kicked in. It's
  off now, and a small plugin fixes another case of the same squeeze.
- **Distant buildings are lit properly.** The game stopped lighting buildings past its streaming range, so it now
  streams them further out.
- **Guns and hands at their real size.** The game draws first-person stuff with a trick that looks fine on a monitor
  but flattens it in VR. That's off, so a rifle looks like a rifle.
- **Real scopes.** You look through the actual scope, the hole lines up with your eye, and your shots land where the
  sights say.
- **No fake weapon sway.** Your hands are the sway now.
- **HUD locked to your head, crosshair out in the world** where your gun is actually pointing.
- **Cutscenes and dialogues don't yank your view around**, and you won't walk through the scene by leaning.

### Fixes in UEVR itself

- **Unreal Engine 5.5 support.** The UI shows up again, and console variables are read and set correctly on UE 5.4+
  (they came back as garbage before, and reading one could reset it).
- **No crashes on save loads.** UEVR now learns when objects are destroyed from the engine itself, and stops calling
  into ones that are gone.
- **Games whose frame counter freezes or restarts** don't break head tracking anymore.
- **Shared lighting between the eyes** and the **canted projection** (above), with zoom that stays centred on your eye.
- **A second UI layer**, so the crosshair can live in the world while the HUD stays on your head.
- **Menus that stay where they open**, and a camera freeze for cutscenes.
- **More for scripts**: where the controller really points, where the UI is drawn, reloading scripts on a key.
- **One profile for every store.** Steam (`-Win64-`) and Game Pass (`-WinGDK-`) builds use the same folder, and a
  profile next to UEVR wins over the one in AppData, so a release is just a folder you unzip.
- **The injector defaults to OpenXR** and keeps its auto-inject settings in the profile.

## How it was tested

- **Game:** STALKER 2: Heart of Chornobyl, **Update 2** (Unreal Engine 5.5), **Steam** version.
- **Headset:** Meta Quest with Touch controllers, over **Virtual Desktop** with its **VDXR** OpenXR runtime.
- **SteamVR** works too, but runs noticeably slower than VDXR.
- **Not tested yet:** the Game Pass version (it should pick up the same profile), Quest Link, other headsets and
  controllers. If you try one, let us know how it went.

## Something broke?

Open an issue and attach `UnrealVRMod\Stalker2\log.txt` from the archive folder. Tell us what you were doing when it
happened.

## License

The STALKER 2 profile is © remleo, licensed under
[CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/). Play it, share the unchanged archive, credit
remleo. No selling it, no modified versions.

That license covers the profile only. UEVR is © praydog under its own terms, and our fork of it lives at
[remleo/UEVR](https://github.com/remleo/UEVR). Lua and sol2 are MIT-licensed. All of their notices are in the archive.

Huge thanks to **praydog** for UEVR. None of this exists without it.
