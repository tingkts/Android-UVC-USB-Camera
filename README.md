

<font size="3"> For Android, there are two ways to make USB Camera app, </font>


1. by android standard [Camera2 API](https://developer.android.com/training/camera2), e.g. [Camera2Basic](https://github.com/android/camera-samples/tree/main/Camera2Basic)

2. by 3rd party libuvc, e.g. [jiangdongguo/AndroidUSBCamera](https://github.com/jiangdongguo/AndroidUSBCamera), [Google Play/USB Camera Viewer](https://play.google.com/store/apps/details?id=com.homesoft.usb.camera&hl=zh_TW&gl=US)


ref. : &nbsp; [Android USB Camera](https://blog.csdn.net/andytian1991/article/details/118082662)

</br>

---

<font size="3"> Android External Camera HAL  </font>

 [Android Open Source Project / External USB Cameras](https://source.android.com/docs/core/camera/external-usb-cameras)


```
e.g. mt8395 android 13

vintf

	           FM               android.frameworks.cameraservice.service@2.2::ICameraService/default

	      DM                    android.hardware.camera.provider@2.4::ICameraProvider/external/0   // aosp external camera hidl
	      DM                    android.hardware.camera.provider@2.4::ICameraProvider/hdmirx/0
	      DM                    android.hardware.camera.provider@2.6::ICameraProvider/internal/0   // mtk isp camera hidl

	      DM        FCM         vendor.mediatek.hardware.camera.atms@1.0::IATMs/default
	      DM        FCM         vendor.mediatek.hardware.camera.isphal@1.1::IISPModule/internal/0


ps

    u:r:kernel:s0                  root           571     2       0      0 rescuer_thread      0 I [16000000.camisp]
    u:r:kernel:s0                  root           572     2       0      0 rescuer_thread      0 I [16000000.camisp]
    u:r:kernel:s0                  root           578     2       0      0 rescuer_thread      0 I [fbt_cam_recycle]
    u:r:kernel:s0                  root           579     2       0      0 rescuer_thread      0 I [fbt_cam_jerk]

    u:r:hal_camera_default:s0      cameraserver   620     1   39516  16060 binder_thread_read  0 S android.hardware.camera.provider@2.4-external-service    // aosp external camera hidl service (usb camera)
    u:r:mtk_hal_cameraprovider_hdmirx:s0 cameraserver 621 1   38912  15208 binder_thread_read  0 S android.hardware.camera.provider@2.4-hdmirx-service
    u:r:mtk_hal_camera:s0          cameraserver   905     1 12538960 98140 binder_thread_read  0 S camerahalserver        // mtk isp camera hidl service

    u:r:cameraserver:s0            cameraserver   866     1 11405892 25480 binder_thread_read  0 S cameraserver

    u:r:platform_app:s0:c512,c768  u0_a94        2626   608 15234796 95468 ep_poll             0 S com.mediatek.camera    // mtk camera app


```

- AOSP external camera HIDL service : &nbsp; [hardware/interfaces/camera/provider/2.4/default](https://android.googlesource.com/platform/hardware/interfaces/+/refs/tags/android-13.0.0_r1/camera/provider/2.4/default/android.hardware.camera.provider%402.4-external-service.rc)
- MTK ISP camera HIDL service : &nbsp; [vendor/mediatek/proprietary/hardware/mtkcam-android/main/hal/hidl/depend/instance.cpp](vendor/mediatek/proprietary/hardware/mtkcam-android/main/hal/hidl/depend/instance.cpp)



</br>

---

<font size="3"> UVC driver </font>


  [kernel/drivers/media/usb/uvc/](https://android.googlesource.com/kernel/arm64/+/refs/tags/android-tv-13.0.0_r0.5/drivers/media/usb/uvc/)



  ```
  debug function/class:

  uvc_dbg()       /sys/module/uvcvideo/parameters

  uvc_debugfs     /sys/kernel/debug/usb/uvcvideo/4-3-1/stats
  ```




</br>
</br>
</br>





 <p align="right"> mtk mt8395 / android-13.0.0_r1 / linux kernel 5.15 </p>
