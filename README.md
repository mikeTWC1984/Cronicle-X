This is a fork of jhuckaby/Cronicle, which adds some more UI features to original project. 

## install
```bash
git clone https://github.com/mikeTWC1984/Cronicle-X; cd Cronicle-X
npm install; node bin/build.js dist
# configure config.json now if needed
bin/control.sh setup; bin/control.sh start
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

## Minor updates:
- **edit** button added on completed job detail page (for easy back and forth navigation)
- control.sh setup returns 0 exit code (no error) if setup already completed (useful for docker entrypoints)
- if using Gitlab's webhooks to trigger job - api key can be used as secret 
- aws-sdk added to dependencies ( for s3 support)

# Original Project:
https://github.com/jhuckaby/Cronicle