# Wishark-
Using Wireshark to discover Network attacks 

Pre-requisite 
-A windowsmachine, Windows 11  , Wireshark has to be installed 
-Another windows machine 
-A Kali machine (optional)
-all three machine are running on the same network 

Description: First, we will use Wireshark to capture FTP credentials. Next, we will use Wireshark to determine details from a network traffic capture, such as MAC addresses, the destination IP address of a website, and whether HTTP traffic is encrypted. Finally, we will use Wireshark to discover evidence of a password-guessing attack.


Log  into machine, Open terminal and then identify the name of the network adapter that has an IPv4 Address in the 192.168.10.x range. 
<img width="828" height="277" alt="image" src="https://github.com/user-attachments/assets/0cb2a4dd-5457-45ed-8a15-74cb07eaba9b" />

Take note of Ip 192.168.10.100 

Launch Wireshark 
<img width="1174" height="724" alt="image" src="https://github.com/user-attachments/assets/a8f39878-63d7-403e-ac6c-4f4e1730b768" />

Next we are going to initiate a network packet capture on the network interface identified earlier by using a Capture filter to capture only traffic related to FTP ports 20 or 21.
On the Wireshark menu bar, select Capture, and then select Options.
In the Wireshark - Capture Options window, select the network interface with the IPv4 Address we recorded earlier.
In the Enter a capture filter… field, enter tcp port 20 or tcp port 21, and then select Start.
<img width="1277" height="615" alt="image" src="https://github.com/user-attachments/assets/e5133217-5198-467a-8af7-a048e5362d11" />
<img width="1719" height="443" alt="image" src="https://github.com/user-attachments/assets/e8ea4c48-85bb-419d-93ee-134afa07fbfd" />


Switch to the Terminal window, connect to 192.168.10.27 (WinLAMP) by using ftp, and then attempt to log on using Administrator as the Name and WrongPassw0rd as the password; the attempt should fail.
<img width="712" height="251" alt="image" src="https://github.com/user-attachments/assets/29017ad6-de91-4a2e-b949-49c9102b919c" />

confirm that a login error message is displayed; this is not the valid password for this account.
<img width="1906" height="406" alt="image" src="https://github.com/user-attachments/assets/6dcb139f-01b4-44b7-a4f2-0a2736b3a918" />

Stop the Wireshark capture.
-Switch to the Wireshark window.
On the Wireshark command bar, select the Stop capturing packets button; it looks like a red square.

Note: Some captured frames are labeled with a Protocol of TCP and others are labeled with FTP. The TCP segments are those related to the establishment of the TCP session on ports 20 or 21.

Apply a display filter that contains tcp contains "USER" to find the frame that has a source address of 192.168.10.100 and represents the transmission of the name that was used to attempt to sign in to the FTP server.
-Select the Apply a display filter field, enter tcp contains "USER", and then either press Enter or select the Apply display filter button that looks like an arrow on the far-right side of the field.
Select the frame that has a source address matching the IP address you recorded earlier; there should only be one or two frames that include USER in the payload.
Review the ASCII interpretation in the bottom pane to confirm that the username contained in the packet immediately after USER matches what you entered in the previous task; this information is also displayed in the Info column in the top pane.
<img width="1110" height="423" alt="image" src="https://github.com/user-attachments/assets/ccf83b5b-a61b-4194-833e-c4faaa9685fc" />
<img width="1108" height="428" alt="image" src="https://github.com/user-attachments/assets/7bcd7a71-581b-461f-97c6-0c20f0d702e2" />

remove the current filter and  Apply a display filter that contains tcp contains "PASS" to find the frame that has a source address of 192.168.10.100 and then review the ASCII interpretation in the bottom pane to confirm that WrongPassw0rd! was the password used to attempt to authenticate the FTP session.
<img width="1114" height="300" alt="image" src="https://github.com/user-attachments/assets/5684aaf5-4a6c-465d-8dd7-537ff8b62627" />

Save the capture in the Documents folder as capture01.
-On the Wireshark menu bar, select File, and then select Save As.
In the Wireshark - Save Capture File As dialog, in Look in, ensure that C:\Users\Administrator\Documents is displayed.
In File name, enter capture01; there is no need to include the file extension, as that is added automatically by the Save As function.
In the Wireshark - Save Capture File As dialog, select Save.
<img width="1169" height="744" alt="image" src="https://github.com/user-attachments/assets/58f49dc2-05cc-45f4-81c4-024984a039f2" />












