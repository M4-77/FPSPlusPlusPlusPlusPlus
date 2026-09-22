# FPSPlusPlusPlusPlusPlus
People playground was hacked and i was infected at 6:03:10pm BST, this pissed me off so heres the entire malware decompiled / decoded and all info i could gather about it

after looking at the virus' code it looks vibecoded by a 9 year old, nothing truly serious just mildly annoying

# What did the virus do EXACTLY?

# RESET YOUR DISCORD PASSWORD IF YOU WERE INFECTED, IT PUBLISHES YOUR TOKEN TO THE WORKSHOP!!!!!!!!!

fear not, heres a list of exactly what it does 

1. Injects/infects the game install (InfectMods)
- Uses the embedded Mono.Cecil (stage 3_0) to rewrite assembly code; generates new mod source (```namespace {0} ... class ... OnLoad  templates, resetConfig.bat, TEMPORARY_, .outline marker), and writes malicious DLLs straight into People Playground_Data\Managed\{1}.dll via a UnityEvent<string,byte[]>/BinaryFormatter trick so the payload survives restarts (kind of persistent but you can just reinstall the game with no mods and youll be fine)

2. Wipes in-game content
- DestroyAllPPGContraptions — deletes every *.jaap contraption save.
- DestroyPPGStats — resets your stat manager (StatManager/NonSteamStatManager, SaveToFile, integers/floats).

3. publishes your private information (PublishDiscordData)
- kills all Discord processes, deletes Discord's *Cache folders in %APPDATA%\discord.
- collects a fingerprint: public IP (via https://api.ipify.org), windows username, hostname, motherboard model, CPU, RAM, GPU, VRAM, MAC address → writes %APPDATA%\discord\myprivatedata.txt.
- Locates your running Steam client, copies the entire Steam config folder (account names, SteamIDs, loginusers.vdf, registry.vdf, client settings) into %APPDATA%\discord\STEAM_CONFIG\, then deletes the original Steam config.
- Publishes the whole %APPDATA%\discord folder as a PUBLIC Steam Workshop item via Steamworks.Ugc.Editor — title "My Data", description "This is my data!", tag "Mods", WithPublicVisibility. Anyone can view it.

4. Destroys browser + personal data
- DestroyCookies — kills chrome, msedge, firefox, then deletes entire profile folders: %LOCALAPPDATA%\Google\Chrome, %LOCALAPPDATA%\Microsoft\Edge, %LOCALAPPDATA%\Mozilla\Firefox, and %APPDATA%\Mozilla\Firefox.
- DestroyPictures — deletes every file in your Pictures folder (+ .outline variants).
- DestroyVideos — deletes every file in your Videos folder.

5. destroys Steam data (via Facepunch.Steamworks + direct file ops)
- DestroySteamApps — enumerates every installed game from appmanifest_*.acf, maps each appid → installDir, then processes each installed game folder (with SteamClient.Shutdown() first).
- DestroySteamUGC/DestroySteamCloud/DestroySteamFriends/DestroySteamInventory/DestroySteamMatchmaking — Steamworks calls + userdata/remote/config deletions.
  
- BSOD: RtlAdjustPrivilege(SeShutdownPrivilege) + NtRaiseHardError(0xC0000022) (winnt class) — hard-error/blue-screen the machine; wired to fire on game unfocus (BSOD.OnApplicationFocus), plus a fake PPG Mod Compiler Protection Service scare dialog ("Suspicious activity was noticed…").
- Writes Documents\FPS+++++ authors.txt with racist slurs ("THIS IS ME, FUCK YOU, I HATE YOU, N**GER…"). (i censored the last word there as im not sure if i can say it in this context)
- Squats in-game chat commands (/optimized!, /auto update, /show hitboxes, FPS+++, /Geneva's Graphics Mod) to masquerade as a legit FPS mod.

Does it steal passwords? kinda
there is no password theft in this payload, i've checked the decompiled code for it.
- No saved-password extraction. It never touches any credential store.
- No keylogger. user32.dll is only used for the MessageBox in the fake-crash routine, there is also no clipboard capture
- it does steal the discord token so reset your password on discord

This payload is hard-coded for Windows, Linux devices are unaffected with the exception of steam operations such as workshop publishing.
The payload has no persistance meaning your device is safe once you reinstall ppg with no mods

- collects info and steam config and publishes it, dont worry too much about it just reset discord passwords


TLDR it infects the game then wipes in game content then it destroys all contraptions and stats then it kills discord processes and deletes discord cache folders then it copies entire steam config folder to %APPDATA%\discord\STEAM_CONFIG before deleting steam config files, it then uploads your discord folder to the workshop (includes token) so reset discord password, it then destroys browser and personal data like pictures. videos, chrome profiles etc then it has a scare payload that gives a BSOD at some point if you relaunch the game
