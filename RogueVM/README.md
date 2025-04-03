# How to create a rogue virtual machine 

1., Create a virtual MacOS machine using the scripts at: https://github.com/kholia/OSX-KVM 

2., After installation shut down the machine and edit the config.plist file in the Opencore folder and replace the SerialNumber value with the target serial number. After that run the following command:
```
rm -f OpenCore.qcow2; sudo ./opencore-image-ng.sh --cfg config.plist --img OpenCore.qcow2
```

If you want to know more about obtaining valid serial numbers and the MDM process in general check out:

https://www.blackhat.com/asia-25/briefings/schedule/#impostor-syndrome---hacking-apple-mdms-using-rogue-device-enrolments-44052

https://duo.com/labs/research/mdm-me-maybe

3., Start up the virtual machine using: 
```
./Opencore-boot.sh
```
4., Log into the machine and run:
```
sudo profiles renew -type enrollment
```

+1., To test for potential SSO bypasses, after running the command in step 4, do not click on the popup, instead go to: 

```
/var/db/ConfigurationProfiles/Settings/.cloudConfigProfileFound
```
Remove the entry for CloudConfigurationWebURL if there is a CloudConfigurationURL present as well the MDM agent will attempt to connect to that instead.
