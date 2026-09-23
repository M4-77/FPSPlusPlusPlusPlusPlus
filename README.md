# FPSPlusPlusPlusPlusPlus
People playground was hacked and i was infected at 6:03:10pm BST, this pissed me off so heres the entire malware decompiled / decoded and all info i could gather about it

// WARNING //

Potentially harmful code, this is for malware analysis purposes unless youre a security engineer or you know what youre doing DO NOT DOWNLOAD FROM THIS REPO!!!! just read the stuff below
I REPEAT DO NOT DOWNLOAD ANY OF THE FILES 
i'm saying this so i'm not morally or ethically responsible if any of you do, legally i should be fine as github allows this type of stuff for malware analysis purposes which it is for, 
the malware also doesn't work anymore due to updates which is the only reason why i'm comfortable putting it out there like this

after looking at the virus' code it looks vibecoded by a 9 year old, nothing truly serious just mildly annoying

# What did the virus do EXACTLY?

Read red's blog at https://redthefirst.github.io/SteamWorkshopMalware/ which utilized this repo, thank you red

Does it steal passwords? kinda
there is no password theft in this payload, i've checked the decompiled code for it.
- No saved-password extraction. It never touches any credential store.
- No keylogger. user32.dll is only used for the MessageBox in the fake-crash routine, there is also no clipboard capture
- it does steal the discord token so reset your password on discord

This payload is hard-coded for Windows, Linux devices are unaffected with the exception of steam operations such as workshop publishing.
The payload has no persistance meaning your device is safe once you reinstall ppg with no mods

- collects info and steam config and publishes it, dont worry too much about it just reset discord passwords


TLDR it infects the game then wipes in game content then it destroys all contraptions and stats then it kills discord processes and deletes discord cache folders then it copies entire steam config folder to %APPDATA%\discord\STEAM_CONFIG before deleting steam config files, it then uploads your discord folder to the workshop (includes token) so reset discord password, it then destroys browser and personal data like pictures. videos, chrome profiles etc then it has a scare payload that gives a BSOD at some point if you relaunch the game
