adb shell am start-activity \
-n com.android.dynsystem/com.android.dynsystem.VerificationActivity  \
-a android.os.image.action.START_INSTALL  \
-d file:///storage/emulated/0/Download/system_raw.gz  \
--el KEY_SYSTEM_SIZE $(du -b system_raw.img|cut -f1)  \
--el KEY_USERDATA_SIZE 8589934592
