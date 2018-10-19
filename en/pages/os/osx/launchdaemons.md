# LaunchDaemons (from Yosemite, v 10.10.5)

## Essential

|`.plist` file | Action| 
|--------------|-------|
|`/System/Library/LaunchDaemons/com.apple.taskgated.plist`|Vital to link processes to mach ports|
|`/System/Library/LaunchDaemons/com.apple.configd.plist` | reads `/Library/Preferences/*` and manages systemconfiguration|
|`/System/Library/LaunchDaemons/com.apple.coreservices.launchservicesd.plist` | launchservices tracks/determines XPC, process signaling, which applications open different types, etc.|
|`/System/Library/LaunchDaemons/com.apple.coreservicesd.plist` | proooobably important |
|`/System/Library/LaunchDaemons/com.apple.kextd.plist` |  handles kext loading/unloading
|`/System/Library/LaunchDaemons/com.apple.networkd.plist` | bring up network|
|`/System/Library/LaunchDaemons/com.apple.networkd_privileged.plist` | same as above|
|`/System/Library/LaunchDaemons/com.apple.opendirectoryd.plist` | requires for user authentication and authorization|
|`/System/Library/LaunchDaemons/com.apple.usbd.plist` | usb device communication|
|`/System/Library/LaunchDaemons/com.apple.wifid.plist` | needed for wireless networking|
|`/System/Library/LaunchDaemons/com.apple.wirelessproxd.plist` | probably keep this|
|`/System/Library/LaunchDaemons/com.apple.xpc.smd.plist` | xpc and such|
|`/System/Library/LaunchDaemons/com.apple.xpc.uscwoap.plist` | xpc done be important|
|`/System/Library/LaunchDaemons/org.ntp.ntpd.plist` | ntp is useful|

## Probably should keep active?

|`.plist` file | Action| 
|--------------|-------|
|`/System/Library/LaunchDaemons/com.apple.MobileFileIntegrity.plist` | starts amfid to check file integrity & enforce code signing. unsure whether the kernel will allow it to be disabled. panics on unload|
|`/System/Library/LaunchDaemons/com.apple.SCHelper.plist` | presumably bridges UNIX settings & System Preferences.app, like scutil|
|`/System/Library/LaunchDaemons/com.apple.TrustEvaluationAgent.system.plist` | root cert verification? XPC? can't tell|
|`/System/Library/LaunchDaemons/com.apple.UserEventAgent-System.plist` | 'The UserEventAgent utility is a daemon that loads system-provided plugins to handle |high-level system events which cannot be monitored directly by launchd.'|
|`/System/Library/LaunchDaemons/com.apple.bsd.dirhelper.plist` | relates mach and bsd layers|
|`/System/Library/LaunchDaemons/com.apple.diskarbitrationd.plist` | governs the mounting of filesystems|
|`/System/Library/LaunchDaemons/com.apple.diskmanagementd.plist` | updates boot files, kernel cache?|
|`/System/Library/LaunchDaemons/com.apple.diskmanagementstartup.plist` | updates boot files, kernel cache?|
|`/System/Library/LaunchDaemons/com.apple.dspluginhelperd.plist` | support for legacy directoryservice calls|
|`/System/Library/LaunchDaemons/com.apple.kuncd.plist` | relays notifications from kernel to user|
|`/System/Library/LaunchDaemons/com.apple.logind.plist` | login!|
|`/System/Library/LaunchDaemons/com.apple.lsd.plist` | launchservices|
|`/System/Library/LaunchDaemons/com.apple.mDNSResponder.plist` | multicast DNS|
|`/System/Library/LaunchDaemons/com.apple.mDNSResponderHelper.plist` | multicast DNS|
|`/System/Library/LaunchDaemons/com.apple.nehelper.plist` | 'network extensions' - vpn and stuff?|
|`/System/Library/LaunchDaemons/com.apple.nesessionmanager.plist` | same as above|
|`/System/Library/LaunchDaemons/com.apple.rootless.init.plist` | enforces rootless restrictions? new in elcap|
|`/System/Library/LaunchDaemons/com.apple.sandboxd.plist` | enforces sandbox restrictions|
|`/System/Library/LaunchDaemons/com.apple.storagekitd.plist` | no clue, probably LVM related|
|`/System/Library/LaunchDaemons/com.apple.sysmond.plist` | system monitor|
|`/System/Library/LaunchDaemons/com.apple.systemkeychain.plist` | unlocks system keychain?|
|`/System/Library/LaunchDaemons/com.apple.taskgated-helper.plist` | communicates tasks ports from PIDs to kernel|
|`/System/Library/LaunchDaemons/com.apple.taskgated.plist` | communicates tasks ports from PIDs to kernel|
|`/System/Library/LaunchDaemons/com.apple.thermald.plist` | thermal management|
|`/System/Library/LaunchDaemons/com.apple.ucupdate.plist` | patches buggy cpu microcode|
|`/System/Library/LaunchDaemons/com.apple.warmd.plist` | manages caches during startup|
|`/System/Library/LaunchDaemons/com.vix.cron.plist` | cron is enabled by default??|

## Probably safe to disable.

|`.plist` file | Action| 
|--------------|-------|
|`/System/Library/LaunchDaemons/com.apple.IOAccelMemoryInfoCollector.plist` | no clue. manages gpumemd?|
|`/System/Library/LaunchDaemons/com.apple.IOBluetoothUSBDFU.plist` | update firmware of bluetooth devices?|
|`/System/Library/LaunchDaemons/com.apple.SCHelper.plist` | presumably bridges UNIX settings & System Preferences.app, like scutil|
|`/System/Library/LaunchDaemons/com.apple.logkextloadsd.plist` | logs kexts that are loaded|
|`/System/Library/LaunchDaemons/com.apple.netauth.sys.auth.plist` | no clue|
|`/System/Library/LaunchDaemons/com.apple.netauth.sys.gui.plist` | no clue|
|`/System/Library/LaunchDaemons/com.apple.notifyd.plist` | apparently breaks some GUI apps|
|`/System/Library/LaunchDaemons/com.apple.periodic-daily.plist` | periodic shell scripts for log/cache cleanup|
|`/System/Library/LaunchDaemons/com.apple.periodic-monthly.plist` | periodic shell scripts for log/cache cleanup|
|`/System/Library/LaunchDaemons/com.apple.periodic-weekly.plist` | periodic shell scripts for log/cache cleanup|
|`/System/Library/LaunchDaemons/com.apple.symptomsd.plist` | no fucking clue - probably logging|
|`/System/Library/LaunchDaemons/com.apple.AirPlayXPCHelper.plist` | airplay inter-process communication|
|`/System/Library/LaunchDaemons/com.apple.AssetCacheLocatorService.plist` | looks for server with cached updates|
|`/System/Library/LaunchDaemons/com.apple.CommCenterRootHelper.plist` | should be ios only, afaik?|
|`/System/Library/LaunchDaemons/com.apple.CoreRAID.plist` | don't need unless you're using raid|
|`/System/Library/LaunchDaemons/com.apple.CrashReporterSupportHelper.plist` | don't need crash reporting in SUM|
|`/System/Library/LaunchDaemons/com.apple.DesktopServicesHelper.plist` | creates .DS_Store files|
|`/System/Library/LaunchDaemons/com.apple.DumpGPURestart.plist` | def need this if you have a failing GPU :O|
|`/System/Library/LaunchDaemons/com.apple.DumpPanic.plist` | dumps KP info to NVRAM on panic|
|`/System/Library/LaunchDaemons/com.apple.FileCoordination.plist` |'filecoordinationd is used by the Foundation framework's NSFileCoordinator class to coordinate access to|
|`/System/Library/LaunchDaemons/com.apple.FontWorker.plist` | Registers and validates fonts for the UI|
|`/System/Library/LaunchDaemons/com.apple.GSSCred.plist` | controls GSSAPI interface (required for Kerberos, i'd imagine)|
|`/System/Library/LaunchDaemons/com.apple.GameController.gamecontrollerd.plist` | definitely not required|
|`/System/Library/LaunchDaemons/com.apple.IFCStart.plist` | ifcstart is the daemon responsible for rebuilding the file caches used by International components of Mac OS X.|
|`/System/Library/LaunchDaemons/com.apple.Kerberos.digest-service.plist` | all for kerberos authentication, safe to disable in this context|
|`/System/Library/LaunchDaemons/com.apple.Kerberos.kadmind.plist` |all for kerberos authentication, safe to disable in this context|
|`/System/Library/LaunchDaemons/com.apple.Kerberos.kcm.plist` |all for kerberos authentication, safe to disable in this context|
|`/System/Library/LaunchDaemons/com.apple.Kerberos.kdc.plist` |all for kerberos authentication, safe to disable in this context|
|`/System/Library/LaunchDaemons/com.apple.Kerberos.kpasswdd.plist` | all for kerberos authentication, safe to disable in this context|
|`/System/Library/LaunchDaemons/com.apple.KernelEventAgent.plist` | 'The KernelEventAgent utility is responsible for displaying disk full and unresponsive file server messages.'|
|`/System/Library/LaunchDaemons/com.apple.MRTd.plist` | `strings` contains a list of known OSX malware, guessing it's for XProtect framework|
|`/System/Library/LaunchDaemons/com.apple.ManagedClient.cloudconfigurationd.plist` | all for enterprise MDM/profiles|
|`/System/Library/LaunchDaemons/com.apple.ManagedClient.enroll.plist` | all for enterprise MDM/profiles|
|`/System/Library/LaunchDaemons/com.apple.ManagedClient.plist` | all for enterprise MDM/profiles|
|`/System/Library/LaunchDaemons/com.apple.ManagedClient.startup.plist` | all for enterprise MDM/profiles|
|`/System/Library/LaunchDaemons/com.apple.NetBootClientStatus.plist` | only matters if running netboot|
|`/System/Library/LaunchDaemons/com.apple.NetworkDiagnostics.plist` | allows wifi diags|
|`/System/Library/LaunchDaemons/com.apple.NetworkLinkConditioner.plist` | simulate shitty network connection (for devs and masochists)|
|`/System/Library/LaunchDaemons/com.apple.NetworkSharing.plist` | creates tunnels to route multiple network interfaces together|
|`/System/Library/LaunchDaemons/com.apple.PCIELaneConfigTool.plist` | mac pro expansion slot config utility helper|
|`/System/Library/LaunchDaemons/com.apple.RFBEventHelper.plist` | registers VNC as a bonjour service and sends events from client to server|
|`/System/Library/LaunchDaemons/com.apple.RemoteDesktop.PrivilegeProxy.plist` | something something VNC something|
|`/System/Library/LaunchDaemons/com.apple.ReportCrash.Root.plist` | exactly what it says|
|`/System/Library/LaunchDaemons/com.apple.ReportPanicService.plist` | samesies|
|`/System/Library/LaunchDaemons/com.apple.SubmitDiagInfo.plist` | what it says|
|`/System/Library/LaunchDaemons/com.apple.TMCacheDelete.plist` | what it says|
|`/System/Library/LaunchDaemons/com.apple.UserNotificationCenter.plist` | manages notification center|
|`/System/Library/LaunchDaemons/com.apple.WindowServer.plist` | serves windows. not rocket science|
|`/System/Library/LaunchDaemons/com.apple.WirelessRadioManagerd-osx.plist` | new in 10.11; likely for wifi calling/handoff|
|`/System/Library/LaunchDaemons/com.apple.afpfs_afpLoad.plist` | afp init|
|`/System/Library/LaunchDaemons/com.apple.afpfs_checkafp.plist` | afp setup|
|`/System/Library/LaunchDaemons/com.apple.airplaydiagnostics.server.mac.plist` | obvious from the name|
|`/System/Library/LaunchDaemons/com.apple.airport.wps.plist` | for configuring wifi protected setup devices|
|`/System/Library/LaunchDaemons/com.apple.akd.plist` | undoubtedly for enforcing code signing|
|`/System/Library/LaunchDaemons/com.apple.alf.agent.plist` | application firewall|
|`/System/Library/LaunchDaemons/com.apple.appleseed.fbahelperd.plist` | appleseed is internal testing|
|`/System/Library/LaunchDaemons/com.apple.applessdstatistics.plist` | ssd statistics would be a good guess|
|`/System/Library/LaunchDaemons/com.apple.apsd.plist` | apple push notification service daemon|
|`/System/Library/LaunchDaemons/com.apple.aslmanager.plist` | apple system log manager|
|`/System/Library/LaunchDaemons/com.apple.atrun.plist` | starts the at unix daemon|
|`/System/Library/LaunchDaemons/com.apple.audio.coreaudiod.plist` | initializes audio|
|`/System/Library/LaunchDaemons/com.apple.audio.systemsoundserverd.plist` | soundserver, probably akin to linuxs' pulseaudio|
|`/System/Library/LaunchDaemons/com.apple.auditd.plist` | audit and rotate log files|
|`/System/Library/LaunchDaemons/com.apple.autofsd.plist` | automatic mounting for local/remote drives, kinda like fstab, except it won't shit itself if drive is missing or offline|
|`/System/Library/LaunchDaemons/com.apple.automountd.plist` | same as previous|
|`/System/Library/LaunchDaemons/com.apple.avbdeviced.plist` | implements IEEE standard for sending audio/video info over network link|
|`/System/Library/LaunchDaemons/com.apple.awacsd.plist` | apple wide area connectivity service daemon -- BTMM helper|
|`/System/Library/LaunchDaemons/com.apple.awdd.plist` | apple wireless diagnostic daemon|
|`/System/Library/LaunchDaemons/com.apple.backupd.plist` | time machine|
|`/System/Library/LaunchDaemons/com.apple.blued.plist` | bluetooth HCI|
|`/System/Library/LaunchDaemons/com.apple.bluetoothReporter.plist` | bluetooth event reporter|
|`/System/Library/LaunchDaemons/com.apple.bluetoothaudiod.plist` | BT ADSP|
|`/System/Library/LaunchDaemons/com.apple.bnepd.plist` | low level BT protocol (L2CAP)|
|`/System/Library/LaunchDaemons/com.apple.cache_delete.plist` | deletes caches?|
|`/System/Library/LaunchDaemons/com.apple.cfprefsd.xpc.daemon.plist` | manages CFPreferences/NSUserDefaults (i.e. `defaults` command)|
|`/System/Library/LaunchDaemons/com.apple.cloudfamilyrestrictionsd-mac.plist` | family sharing?|
|`/System/Library/LaunchDaemons/com.apple.cmio.AVCAssistant.plist` | all for video capture|
|`/System/Library/LaunchDaemons/com.apple.cmio.AppleCameraAssistant.plist` | all for video capture|
|`/System/Library/LaunchDaemons/com.apple.cmio.IIDCVideoAssistant.plist` | all for video capture|
|`/System/Library/LaunchDaemons/com.apple.cmio.VDCAssistant.plist` | all for video capture|
|`/System/Library/LaunchDaemons/com.apple.cmio.iOSScreenCaptureAssistant.plist` | all for video capture|
|`/System/Library/LaunchDaemons/com.apple.colorsyncd.plist` | implements colorsync calibration|
|`/System/Library/LaunchDaemons/com.apple.configureLocalKDC.plist` | sets up kerberos domain controller|
|`/System/Library/LaunchDaemons/com.apple.corecaptured.plist` | no clue, strings only contains 'SIGBUS DEATH'. new in elcap?|
|`/System/Library/LaunchDaemons/com.apple.coreduetd.osx.plist` | maintains a sqlite3 DB in /var/db/CoreDuet. has a bunch of event tables like screen lock, power management, etc. probably logging|
|`/System/Library/LaunchDaemons/com.apple.coreservices.appleevents.plist` | relays appleevents for UI automation|
|`/System/Library/LaunchDaemons/com.apple.coreservices.sharedfilelistd.plist` | seems to be about sandbox implementation|
|`/System/Library/LaunchDaemons/com.apple.corestorage.corestoraged.plist` | required only if FV is on? or if disk utility needs to manipulate CS volumes|
|`/System/Library/LaunchDaemons/com.apple.corestorage.corestoragehelperd.plist` | see above|
|`/System/Library/LaunchDaemons/com.apple.coresymbolicationd.plist` | for debugging and crash reporting|
|`/System/Library/LaunchDaemons/com.apple.csrutil.report.plist` | CSR is the userspace component of the new rootless security component of the 10.11+ kernel|
|`/System/Library/LaunchDaemons/com.apple.ctkd.plist` | crypto token kit. probably for SSL/HTTPS or kerberos.|
|`/System/Library/LaunchDaemons/com.apple.cvmsServ.plist` | part of OpenGL framework - 'Core Virtual Machine'? probably for OpenCL|
|`/System/Library/LaunchDaemons/com.apple.diagnostic.uuidpathd.plist` | diags|
|`/System/Library/LaunchDaemons/com.apple.diagnosticd.plist` | diags|
|`/System/Library/LaunchDaemons/com.apple.displaypolicyd.plist` | reads EDID/monitor information, displayport/hdmi/dvi?|
|`/System/Library/LaunchDaemons/com.apple.distnoted.xpc.daemon.plist` | distributed notification services?|
|`/System/Library/LaunchDaemons/com.apple.dpaudiothru.plist` | displayport audio out|
|`/System/Library/LaunchDaemons/com.apple.dpd.plist` | 'displayport daemon' - responsible for target display mode and whatnot.|
|`/System/Library/LaunchDaemons/com.apple.dvdplayback.setregion.plist` | pffft|
|`/System/Library/LaunchDaemons/com.apple.dynamic_pager.plist` | responsible for managing virtual memory and swapping to disk|
|`/System/Library/LaunchDaemons/com.apple.eapolcfg_auth.plist` | only needed if 802.1x is required|
|`/System/Library/LaunchDaemons/com.apple.efilogin-helper.plist` | i have no idea. FV login management?|
|`/System/Library/LaunchDaemons/com.apple.familycontrols.plist` | i have disgraced my family (sharing)|
|`/System/Library/LaunchDaemons/com.apple.findmymac.plist` | what it sounds like|
|`/System/Library/LaunchDaemons/com.apple.findmymacmessenger.plist` | ditto|
|`/System/Library/LaunchDaemons/com.apple.firmwaresyncd.plist` | copies firmware updates to the ESP from softwareupdate|
|`/System/Library/LaunchDaemons/com.apple.fontd.plist` | only required by GUI afaik|
|`/System/Library/LaunchDaemons/com.apple.fontmover.plist` | ditto|
|`/System/Library/LaunchDaemons/com.apple.fseventsd.plist` | watches file(systems) for changes and notifies processes. usually spotlight.|
|`/System/Library/LaunchDaemons/com.apple.gkreport.plist` | 'reports gatekeeper status to messsagetracer'|
|`/System/Library/LaunchDaemons/com.apple.gssd.plist` | enables access to GSSAPI|
|`/System/Library/LaunchDaemons/com.apple.hdiejectd.plist` | helper for .dmg files|
|`/System/Library/LaunchDaemons/com.apple.hidd.plist` | interfaces HIDs with high level system processes|
|`/System/Library/LaunchDaemons/com.apple.icloud.findmydeviced.plist` | see title|
|`/System/Library/LaunchDaemons/com.apple.iconservices.iconservicesagent.plist` | gui only|
|`/System/Library/LaunchDaemons/com.apple.iconservices.iconservicesd.plist` | gui only|
|`/System/Library/LaunchDaemons/com.apple.ifdreader.plist` | smart card authentication|
|`/System/Library/LaunchDaemons/com.apple.installandsetup.systemmigrationd.plist` | probably only runs on setup assistant or migration assistant?|
|`/System/Library/LaunchDaemons/com.apple.installd.plist` | responsible for installing .pkg/.mpkg files|
|`/System/Library/LaunchDaemons/com.apple.kcproxy.plist` | keychain proxy - unless using keychain for CLI key management, unnecessary|
|`/System/Library/LaunchDaemons/com.apple.locationd.plist` | location services|
|`/System/Library/LaunchDaemons/com.apple.lockd.plist` | NFS lock daemon|
|`/System/Library/LaunchDaemons/com.apple.logd.plist` | logging|
|`/System/Library/LaunchDaemons/com.apple.loginwindow.LFVTracer.plist` | only needed for legacy FV1|
|`/System/Library/LaunchDaemons/com.apple.loginwindow.plist` | loginwindow (probably launches the GUI itself)|
|`/System/Library/LaunchDaemons/com.apple.mbsystemadministration.plist` | setup assistant|
|`/System/Library/LaunchDaemons/com.apple.mbusertrampoline.plist` | setup assistant|
|`/System/Library/LaunchDaemons/com.apple.mdmclient.daemon.plist` | mdm|
|`/System/Library/LaunchDaemons/com.apple.metadata.mds.index.plist` |  all spotlight stuff|
|`/System/Library/LaunchDaemons/com.apple.metadata.mds.plist` | all spotlight stuff|
|`/System/Library/LaunchDaemons/com.apple.metadata.mds.scan.plist` | all spotlight stuff|
|`/System/Library/LaunchDaemons/com.apple.metadata.mds.spindump.plist` | all spotlight stuff|
|`/System/Library/LaunchDaemons/com.apple.msrpc.lsarpc.plist` | presumably all stuff for AD/Samba/Windows integration|
|`/System/Library/LaunchDaemons/com.apple.msrpc.mdssvc.plist` | presumably all stuff for AD/Samba/Windows integration|
|`/System/Library/LaunchDaemons/com.apple.msrpc.netlogon.plist` | presumably all stuff for AD/Samba/Windows integration|
|`/System/Library/LaunchDaemons/com.apple.msrpc.srvsvc.plist` | presumably all stuff for AD/Samba/Windows integration|
|`/System/Library/LaunchDaemons/com.apple.msrpc.wkssvc.plist` | presumably all stuff for AD/Samba/Windows integration|
|`/System/Library/LaunchDaemons/com.apple.mtmd.plist` | mobile time machine|
|`/System/Library/LaunchDaemons/com.apple.newsyslog.plist` | logging|
|`/System/Library/LaunchDaemons/com.apple.nfsconf.plist` | nfs|
|`/System/Library/LaunchDaemons/com.apple.nfsd.plist` | nfs|
|`/System/Library/LaunchDaemons/com.apple.nis.ypbind.plist` | nis|
|`/System/Library/LaunchDaemons/com.apple.noticeboard.state.plist` | something to do with MAS|
|`/System/Library/LaunchDaemons/com.apple.nsurlsessiond.plist` | background NSURLSession (probably for spotlight online searching)|
|`/System/Library/LaunchDaemons/com.apple.nsurlstoraged.plist` | manages http storage (probably the same as above)|
|`/System/Library/LaunchDaemons/com.apple.ocspd.plist` | checks for revoked certificates|
|`/System/Library/LaunchDaemons/com.apple.pfd.plist` | manages pf firewall|
|`/System/Library/LaunchDaemons/com.apple.platform.ptmd.plist` | thermal monitor daemon|
|`/System/Library/LaunchDaemons/com.apple.powerd.plist` | manages assertions for power management|
|`/System/Library/LaunchDaemons/com.apple.powerd.swd.plist` | manages assertions for power management|
|`/System/Library/LaunchDaemons/com.apple.preferences.timezone.admintool.plist` | timezone configuration|
|`/System/Library/LaunchDaemons/com.apple.preferences.timezone.auto.plist` | see above|
|`/System/Library/LaunchDaemons/com.apple.racoon.plist` | VPN configuration|
|`/System/Library/LaunchDaemons/com.apple.remotepairtool.plist` | apple remote pairing|
|`/System/Library/LaunchDaemons/com.apple.rpcbind.plist` | for nfs or smb, either way i don't care|
|`/System/Library/LaunchDaemons/com.apple.scsid.plist` | scsi devices|
|`/System/Library/LaunchDaemons/com.apple.secinitd.plist` | initialized security policies. TrustedBSD?|
|`/System/Library/LaunchDaemons/com.apple.security.agent.login.plist` | access to keychain and gui prompt for pw, etc|
|`/System/Library/LaunchDaemons/com.apple.security.authhost.plist` | access to keychain and gui prompt for pw, etc|
|`/System/Library/LaunchDaemons/com.apple.securityd.plist` | access to keychain and gui prompt for pw, etc|
|`/System/Library/LaunchDaemons/com.apple.securityd_service.plist` | access to keychain and gui prompt for pw, etc|
|`/System/Library/LaunchDaemons/com.apple.sessionlogoutd.plist` | handles user logout?|
|`/System/Library/LaunchDaemons/com.apple.smb.preferences.plist` | samba|
|`/System/Library/LaunchDaemons/com.apple.softwareupdate_download_service.plist` | softwareupdate|
|`/System/Library/LaunchDaemons/com.apple.softwareupdate_firstrun_tasks.plist` | ditto|
|`/System/Library/LaunchDaemons/com.apple.softwareupdated.plist` | ditto|
|`/System/Library/LaunchDaemons/com.apple.speech.speechsynthesisd.plist` | speech synthesis|
|`/System/Library/LaunchDaemons/com.apple.spindump.plist` | reports hanging ui events|
|`/System/Library/LaunchDaemons/com.apple.statd.notify.plist` | rpc related|
|`/System/Library/LaunchDaemons/com.apple.storeaccountd.daemon.plist` | MAS/itunes auth|
|`/System/Library/LaunchDaemons/com.apple.storeagent.daemon.plist` | same|
|`/System/Library/LaunchDaemons/com.apple.storeassetd.daemon.plist` | same|
|`/System/Library/LaunchDaemons/com.apple.storedownloadd.daemon.plist` | same|
|`/System/Library/LaunchDaemons/com.apple.storereceiptinstaller.plist` | same|
|`/System/Library/LaunchDaemons/com.apple.suhelperd.plist` | software update|
|`/System/Library/LaunchDaemons/com.apple.sysdiagnose.plist` | handles sysdiagnose events (to send to support)|
|`/System/Library/LaunchDaemons/com.apple.syslogd.plist` | system logging|
|`/System/Library/LaunchDaemons/com.apple.system_installd.plist` | installing stuff. probably system updates|
|`/System/Library/LaunchDaemons/com.apple.systempreferences.installer.plist` | installs system preferences?|
|`/System/Library/LaunchDaemons/com.apple.systemstats.analysis.plist` | stats|
|`/System/Library/LaunchDaemons/com.apple.systemstats.daily.plist` | stats|
|`/System/Library/LaunchDaemons/com.apple.systemstatsd.plist` | stats|
|`/System/Library/LaunchDaemons/com.apple.tccd.system.plist` | no clue. google suggests localization|
|`/System/Library/LaunchDaemons/com.apple.trustd.plist` | radius or kerberos?|
|`/System/Library/LaunchDaemons/com.apple.uninstalld.plist` | installd's evil twin|
|`/System/Library/LaunchDaemons/com.apple.unmountassistant.sysagent.plist` | guessing helps unmount things.|
|`/System/Library/LaunchDaemons/com.apple.updateEFIDesktopPicture.plist` | updates EFI background for FV2 login|
|`/System/Library/LaunchDaemons/com.apple.usbmuxd.plist` | communciates with ios devices over usb|
|`/System/Library/LaunchDaemons/com.apple.var-db-dslocal-backup.plist` | let's play with fire|
|`/System/Library/LaunchDaemons/com.apple.vsdbutil.plist` | volume status database for unique drive identification -- seemingly no longer needed except for legacy|
|`/System/Library/LaunchDaemons/com.apple.watchdogd.plist` | reboots system in case of user & kernel both locking up|
|`/System/Library/LaunchDaemons/com.apple.wdhelper.plist` | wireless diags helper|
|`/System/Library/LaunchDaemons/com.apple.wwand.plist` | only need if using usb WAN device|
|`/System/Library/LaunchDaemons/com.apple.xscertd-helper.plist` | certs, probably kerberos or https|
|`/System/Library/LaunchDaemons/org.cups.cupsd.plist` | printing, who cares|
|`/System/Library/LaunchDaemons/org.postfix.master.plist` | don't need a mail server|
|`/System/Library/LaunchDaemons/org.postfix.newaliases.plist` | same as above|
||