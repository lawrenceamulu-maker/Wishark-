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

On the Wireshark menu bar, select File, and then select Save As.
In the Wireshark - Save Capture File As dialog, in Look in, ensure that C:\Users\Administrator\Documents is displayed.
In File name, enter capture01; there is no need to include the file extension, as that is added automatically by the Save As function.
In the Wireshark - Save Capture File As dialog, select Save.
On the Wireshark menu bar, select Capture, and then select Options.
In the Wireshark-Capture Options window, select the X at the right end of the Capture filter field; this button functions as a clear capture filter.
In the Wireshark-Capture Options window, select Close.
<img width="920" height="527" alt="image" src="https://github.com/user-attachments/assets/40564fc5-92f2-451d-b548-ccf14d40c4bf" />

//Find details in a network traffic capture

On the Wireshark toolbar, select the Start capturing packets icon; it looks like a shark fin and is the left-most icon on the toolbar.
If prompted by an Unsaved packets dialog, select Continue without Saving.
<img width="916" height="435" alt="image" src="https://github.com/user-attachments/assets/202af513-f1b8-48b5-b249-c7bb190d5d91" />

Open Microsoft Edge and then go to http://info.cern.ch/.

Switch to Wireshark and then stop the network capture.

Apply ip.src == 192.168.10.100 as a display filter.

Review the captured traffic to determine the MAC address of the computer that uses 192.168.10.100 as its IP address.
<img width="867" height="928" alt="image" src="https://github.com/user-attachments/assets/e2978231-3e78-4c00-9748-9e3db699ebb4" />
<img width="843" height="366" alt="image" src="https://github.com/user-attachments/assets/93dd1214-ae0d-4b5b-bafe-a9ba5aac5cef" />
<img width="799" height="333" alt="image" src="https://github.com/user-attachments/assets/c656f543-f8b7-4d52-8078-a529550c61d2" />

<img width="923" height="384" alt="image" src="https://github.com/user-attachments/assets/13874bf6-ab3c-4211-b22a-6e18f33c615e" />


Review the captured traffic to determine the MAC address of the computer that uses 192.168.10.100 as its IP address
-In the Packet List pane, select the first packet that is displayed based on this display filter; be sure to scroll to the top of the capture or press Home on your keyboard to ensure you are at the first packet.
In the Packet Details pane, select the arrow next to Ethernet II to expand its contents.
In Ethernet II, locate the Ethernet header value labeled Source:; this is the MAC address of the source of this packet.
<img width="562" height="233" alt="image" src="https://github.com/user-attachments/assets/1dca0a86-cb4e-4660-840a-43764d4dd6ed" />

Remove the existing display filter.

Apply http.host=="info.cern.ch" as a display filter.

Review the captured traffic to locate and select a packet that displays 192.168.10.100 in the Source column, HTTP in the Protocol column, and GET / HTTP/1.1 in the Info column and then determine the IP Address value displayed in the Destination column.

The IP address in the Destination column is the IP address of the info.cern.ch website.

Record the IP address obtained in the previous task in the following Dest IP Addr text box:
<img width="900" height="226" alt="image" src="https://github.com/user-attachments/assets/5f87fa08-dd71-410b-9625-d8e05aedfee9" />

Ip dest is 188.184.67.127

Remove the existing display filter.

Apply ip.dst == 188.184.67.127 as a display filter.
<img width="930" height="353" alt="image" src="https://github.com/user-attachments/assets/3c7fa7f0-7419-4148-b8ee-0207cbd4ccc3" />

In the top Packet List pane, review the displayed packets to determine if there are any TLS labeled packets in the Protocol column; there can be various TLS versions listed, such as TLSv1.3.
In the top Packet List pane, select any packet.
In the Packet Details pane, expand Transmission Control Protocol, and then select the Destination Port.
Right-click Destination Port, and then select Apply as Column.
In the top Packet List pane between the Length and Info columns, confirm that a new column labeled Destination Port is displayed.
Review the contents of the new column.

<img width="1118" height="727" alt="image" src="https://github.com/user-attachments/assets/3768726d-6433-4a78-88f3-d9d8b4f221c8" />

<img width="678" height="271" alt="image" src="https://github.com/user-attachments/assets/7d1c8578-6285-4bd2-ae7f-bf58f80b68ae" />


//Discover a password-guessing attack

Note: WinLAMP, at 192.168.10.27, already runs an FTP service through IIS, so it will also serve as the target of the password-guessing attack in this requirement. KaliLinux is accessed only through a terminal connection in this Virtual Lab-there is no desktop available.\

Switch to WinLAMP

 install WinPcap and then run an rpcap server using the following commands:
 <img width="1143" height="321" alt="image" src="https://github.com/user-attachments/assets/253382bf-a55d-4c41-b018-4c49741deb24" />

 


























