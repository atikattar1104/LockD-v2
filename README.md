
# Lockd v2

Abbreviation For `Lock Daemon`. 

Unix-Style Lock Written In Bash. A Complete Rewrite Of Older Version Of LockD. Now With Credential Obfuscation. Best Suitable For Termux. Highly Compatible With Various Linux Environments. 

## Principles :- (From The Perspective Of System) 

1. Host Identification :- Who Am I (System) To You (User)? 

2. User Identification :- Who Are You (User) To Me (System)? 

3. Password Authentication :- What Do You (User) Know (Password) That I (System) Also Know (Password)? 

## Features :- 

1. Open Source. 

2. Single-File Daemon. 

3. Embeddable. 

4. Robust. 

5. Complex Architecture. 

6. 3 Factor Authentication (3FA) ( `Hostname` -> `Username` -> `Password` ). 

7. Uses Different Hostnames, Usernames, And Passwords, Than Actual System Hostnames, Usernames, And Passwords. No Need To Expose Confidential Details! 

8. Multi-Level Classification Possible For Multi-User Systems. 

9. Built-In Enabling/Disabling Feature For Entire Lock, By Setting Value Of `loggedin` Variable To Any Number Greater Than `0`, And For Specific Authentication Factors, By Commenting Out Specific Factor Checking Conditional Statements Using `#`. 

10. Custom Commands Can Be Embedded For Each Hostname And/Or User And/Or Password For Internal Mechanism Customization, As Well As User Desired Customization. 

11. Highly Compatible With Termux, And Various Linux Environments. 

12. Cannot Interrupt With `CTRL+C` Or Any Type Of Interrupt Signal. 

13. Can Be Customized To Greet Individual Users With Individual Welcome Messages, And Run Various Commands Specifically As Per Individual User's Choice, As Desired. 

14. Easy To Understand, For `Features -> 9.`. 

15. Can Increase And/Or Decrease The Number Of Attempts Of Failed Authentication Factors, By Changing The Values Of `failhnamecount` And/Or `failunamecount` And/Or `failpwordcount` To Desired Number Of Attempts. 

16. `NEW` Credential Obfuscation Using Obfuscation Chaining Mechanism, Inspired By Various Ransomwares' Encryption Mechanisms. 

17. `NEW` Uses Switch-Case Based Function Calling For Simplicity And Ease Of Understanding. 

18. `NEW` Built-In Credential Creation Mechanism. 

19. `NEW` Built-In Credential Modification Mechanism. 

20. `NEW` Built-In Credential Storage Directory Migration Mechanism. 

21. `NEW` `WIP` Built-In Individual Credential Migration Mechanism. 

22. `NEW` `WIP` Built-In Hidden Storage Made Using Existing Credential Storage Mechanism, Can Be Used As A Hidden Space For Confidential Data Storage. 

23. `NEW` POSIX-Compliant, Filesystem Hierarchy Standard `FHS` Compliant, XDG-Base Directory Specification `BDS` Compliant, UNIX Filesystem's Conventional Directory Layout `CDL` Compliant, Centralized Directory-Based Credential Storage Mechanism. 

24. Can Use Docker-Based, uDocker-Based, Proot-Based, Externally Installed Package(s)' Command(s), If Any Of The Required Package(s) Of Dependencies Is/Are Not Available For User's System. 

25. Noob, Script-Kiddie Safe. Since Cannot Be Locked By Just Calling The Daemon File. 

## Drawbacks :- 

1. Doesn't Uses Real Hostnames, Usernames, And Real Passwords For Classification. 

2. Can Bypass If :- 

	1. External Access To Daemon File Is Possible. 

	2. If Any Time-Consuming Process Is Running Before LockD, And That Process Is Interrupted Manually. E.g. :- `Time-Consuming_Process && lockd` Or `Time-Consuming_Process ; lockd`. 

3. Malicious Actors Can Create Backdoors, If, External Access To Daemon File Is Possible. 

4. Doesn't Natively Work On Shells Other Than Bash ( Might Work On Shells Based On Bash ). For Making It Work On Other Shells, Entire Code Of The `LockD` Mechanism Needs To Be Re-Written Using The Target Shell Scripting Language. 

5. If `Drawback -> 3` Is Possible, Then :- 

	1. Any External Access To Filesystem Can Lead To Credential Leaks, If, Path To Centralized Credential Storage Directory Is Known By The Attacker/Malicious Threat Actor. 

	2. Any External Access To Filesystem Can Lead To Data Stored In Credential Storage Directory, To Be Leaked, If, Path To Centralized Credential Storage Directory Is Known By The Attacker/Malicious Threat Actor. 

## Dependencies :- 

In The Previous Version Of LockD, There Was Only One Requirement :- A Fully Functional Bash Shell. In This Version, There Are Various. 

Note :- The Packages Must Not Need To Be Distro-Supported, Since Can Be Used Using Methods Mentioned In `Features -> 23`. 

1. GNU Coreutils (For Commands `basenc` `md5sum` `cksum` `b2sum` ) 

2. SHAsum (For Command `shasum` ) 

3. XXHsum (For Command `xxhsum` ) 

4. Hashdeep (For Command `hashdeep` ) 

5. Blake3B (For Command `b3sum` ) 

## Install :- 

0. Read LockD Daemon File To See If It Meets Your Requirements And Expectations For The Use Case. If Yes, Then Read It Again, To Understand How It Works. 

1. Install All The Packages For The Dependencies Section. 

	Note :- If Any Package(s) Is/Are Not Available For Your Linux Distro, But Is/Are Available For Other Distro(s), You Can Use Methods Mentioned In `Features -> 23`, To Use Those Distro(s), And Install Those Not Available Package(s) On Those Distro(s), And Use Their Individual Methods (Like `docker exec`) To Run Those Specific Command(s) (You May Need To Look Into Their Documentations, In Order To Run Those Commands Without Logging Into Those Distros), And Also Modify The Obfuscation Chain To Include The Docker Exec Command(s) For The Lock To Work. 

2. Download The LockD File `lockd`. 

	1. Using `git clone`. 

	2. Using `Download File` Feature Of This Repository. 

3. Move The Downloaded `lockd` File In The Same Directory Where `.bashrc` Or `.profile` Is Stored, Or, In Any Directory That Is Specified In `$PATH`. Prefer `$PREFIX/bin`.

4. Provide `Execute` Permission Using `chmod +x path/to/lockd`. 

5. Append This New Line In `.bashrc` For Calling LockD Everytime A New Shell Is Called, Or In `.profile` For Calling LockD Everytime The System Starts :- 

	1. If Moved LockD File Is In Same Directory As In `.bashrc` Or `.profile` :- 

		```
		./lockd -i
		```

	2. If Moved LockD File Is In One Of The Directories In `$PATH` :- 

		```
		lockd -i
		``` 

6. Create A Blank Directory Anywhere Within The System, And Give Read Permission To The Entire Path Of Created Blank Directory. 

7. Open The LockD File, And Change The Value Of `LOCKDPASSWDPATH` Variable To The Newly Created Blank Directory's Path. 

8. Add New Hostname(s), Usernames(s) Using, And Password Using Built-In Flag Arguments Of `lockd` File, As You Desire. Once The Lockd File Is Called With Appropriate Flag Argument, Follow On Screen Instructions. 

Note :- You Can Add As Many Hostnames, Usernames Per Single Hostname, Password Variables Per Single Username, As You Desire. 

## Security :- 

### To Avoid `Drawback -> 2 -> 2` :- 

	1. Make Sure That The `lockd` File Is Starting First, Before Any Time-Consuming Process Or Any Process That Cannot Be Interrupted ( E.g. :- Neofetch, Which Takes Time To Print System Information ). 

	2. If `.bashrc` Or `.profile` Contains Important System Commands, Give Them First Priority, Then Second Priority To `lockd`, Then To Any Other Non-System Interruptable Process. 

### To Avoid `Drawback -> 2 -> 2` After Embedding LockD Inside An Application Software :- 

	1. Make Sure That The `lockd` File Is Starting First, Before Any Time-Consuming Process Or Any Process That Cannot Be Interrupted. 

### Code-Level Security Is Provided, For System-Level Security, You Are On Your Own! 

### If Any Issue/Defect/Bug/Error/Exception/Etc. Occurs And/Or Found, Leaving Your Device(s)/Computer(s)/Machine(s)/System(s) Vulnerable, STOP USING LockD AS SOON AS POSSIBLE! 

## Responsibility And Liability :- 

1. If Any Loss ( Data/System/Etc. ) Occurs, I, The Creator Of This `LockD` Mechanism, Am Neither Responsible, Nor Liable. 

2. If Any Issue/Defect/Bug/Error/Exception/Etc. Occured And/Or Found In This `LockD` Mechanism, And Can Be Avoided By Modifying The Code Of This `LockD` Mechanism, :- 

	1. If The Issue/Defect/Bug/Error/Exception/Etc. Is Locally Occured And/Or Found On A Single Device/Computer/Machine/System, Feel Free To Modify The Code Of This `LockD` Mechanism Locally In The Device/Computer/Machine/System, To Avoid The Occured And/Or Found Issue/Defect/Bug/Error/Exception/Etc, BUT, Then That Modifier/Person Who Modified The Code Of This `LockD` Mechanism Locally, And/Or The Organization/Company/Group Of Companies/Etc. Under Which The Modifier/Person Who Modified The Code Of This `LockD` Mechanism Locally, Is Working And/Or Contributing For, Is Entirely Responsible For Any Loss ( Data/System/Etc. ) Caused By The Locally Modified Code Of This `LockD` Mechanism. 

	2. If The Issue/Defect/Bug/Error/Exception/Etc. Is Globally Occured And/Or Found On Multiple Devices/Computers/Machines/Systems, Feel Free To Raise Issue(s) Or Pull Request(s) On This Repository, BUT, If Any Loss ( Data/System/Etc. ) Occurs Before And/Or After The Issue/Defect/Bug/Error/Exception/Etc. Is Occured And/Or Found, I, The Creator Of This `LockD` Mechanism, Am ( STILL ) Neither Responsible, Nor Liable. 

# Made In Nano On Termux. 

Heck! Even This README Is Made in Nano On Termux. 
Modified This README In Acode IDE On Android

# `Thanks!`

