This is a fork of jhuckaby/Cronicle, which adds some more UI features to original project. 

## install
```bash
git clone https://github.com/mikeTWC1984/Cronicle-X; cd Cronicle-X
npm install; node bin/build.js dist
# configure config.json now if needed
bin/control.sh setup; bin/control.sh start
# optional - create symlink for control.sh
ln -s $PWD/bin/control.sh /usr/bin/cronx
```
you can install it in any folder if needed (not only /opt/cronicle). To uninstall: ```rm -rf Cronicle-X```


# New Features

## shell plugin - code editor

![image](https://user-images.githubusercontent.com/31977106/87238642-49afdf80-c3d3-11ea-86fc-a99ea25200ce.png)

## job details - ansi colors fixed, console style view
You can also capture terminal colors using terminal emulator checkbox on shell plugin.
It requires **script** tool which is typically included in the most linux distros. On alpine add **util-linux** package to get it.
Script tool will not redirect stderr (exit code only) and will hang on interactive prompts, so it's not recommended for jobs running on regular schedules.

![image](https://user-images.githubusercontent.com/31977106/87238676-b62ade80-c3d3-11ea-8450-51f7172d5088.png)

## Warning state
use exit code -1 (or 255) to emulate warning. E.g.
```bash
echo 'some warning' > &2
exit -1
```
![image](https://user-images.githubusercontent.com/31977106/87238751-90520980-c3d4-11ea-9b49-d0d1abbb2d85.png)

## Active Directory / External authentication
You can let user to use alternative authentication (username/password verification) mechanism. While creating a user check **external authentication** check box.
![image](https://user-images.githubusercontent.com/31977106/87841063-afd3b100-c870-11ea-8e73-2c5274bc3e4e.png)
If that option is set user's password/username check will be routed to external mechanism (standard mechanism compares password hashes) and all password updated option will be locked. All other steps (user status check/incorrect password handling/session generation) are the same for both methods
The default external mechanism is Active Directory. In order to enable it:
1.   install activedirectory2 module: ```npm install activedirectory2```
2.   in config.json specify ad_domain setting (a.k.a. kerberos realm)
   if not sure what it is try to ping localhost (you'll likely see domain name added to your hostname), or in powershell run this ```[adsi]""```, then you if you get something like ``` {DC=CORP,DC=MYCOMPANY,DC=com}``` the domain name will be corp.mycompany.com (assuming you do it from a windows machine that s logged to your domain)
3. create a new user with external auth box checked. Now that user should be able to login using his ad credentials.

To set up a custom authentication (e.g. http post request) 
- open this file: **_node_modules/pixl-server-user/user.js_**  (or  **_plugins/user.ad.js_** before installing cronicle)
- locate **startup** function and require any extra modules you need (e.g. request)
- then locate **api_login** function and replace **ad.authenticate** method with your custom one (e.g. request.post )


## Minor updates:
- **edit** button added on completed job detail page (for easy back and forth navigation)
- control.sh setup returns 0 exit code (no error) if setup already completed (useful for docker entrypoints)
- control.sh - works properly as symlink (thanks to https://github.com/jhuckaby/Cronicle/pull/153 )
- if using Gitlab's webhooks to trigger job - api key can be used as secret 
- aws-sdk added to dependencies ( for s3 support)

# Original Project:
https://github.com/jhuckaby/Cronicle