# demonstrate code signing

### BINARIES

- Make a duplicate copy of a binary

`$ cp /sbin/md5 /var/tmp/`

- Verify its' integrity:
    + ` $ codesign --verify -vv /sbin/md5 `

- Modify the copied version in some way:
    + ` $ echo '0101' >> /var/tmp/md5 ` # this will add half a byte at the end of `/var/tmp/md5`

- Retest your modified one for codesigning: 
    + ` $ codesign --verify -vv /var/tmp/md5 `
    + It should fail now and give you an error message. 

### KEXTS

- Verify the integrity of an existing, known-signed kext:

`$ codesign --no-strict -vv /System/Library/Extensions/ALF.kext`
- It should tell you it satisfies its designated requirement.

- Duplicate/modify same kext:
`$ cp -r /System/Library/Extensions/ALF.kext /var/tmp`
`$ sed -i .bak s/Apple/Affle/g /var/tmp/ALF.kext/Contents/Info.plist # changes all instances of 'Apple' to 'Affle'`

- Retest copied kext:
`$ codesign --no-strict -vv /var/tmp/ALF.kext`
- Should fail, and even tell you which file has been modified. 
  
