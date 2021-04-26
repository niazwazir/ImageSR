# Demosaicing_SuperResolution

## Testing Result

01. 2021/04/16 在固定各種參數后，以Set5為基準測資
   -  使用bilinear的結果: ``PSNR:28.73``, ``SSIM:0.753``
   -  使用bicubic的結果 ：``PSNR:28.58``, ``SSIM:0.744``

02. 2021/04/16 把patch_size從64改成32，label_size從128改成64
   - ``PSNR:28.65``, ``SSIM:0.757``

03. 2021/04/16 把coarse_output拿掉
   - ``PSNR:28.98``, ``SSIM:0.787``

04. reduce_lr callbacks
   - 把reduce_lr加進去:``PSNR:28.72``, ``SSIM:0.724``
   - 把reduce_lr撤回去: ``PSNR:28.87``, ``SSIM:0.738``

05. 同上設定，batch_size改成16,Model_output只有Residual_Output
   - ``PSNR:29.31``, ``SSIM:0.805``

06. 64，128，30，T91，/255.0，6 residual_block, output=Residual_Output, without reduce_lr
   - ``PSNR:29.29``, ``SSIM:0.821``

07. 把koda也加入training data set中，training_dataset(koda, T91, origin)
   - original ``PSNR:29.29``, ``SSIM:0.821``
   - current  ``PSNR:27.96``, ``SSIM:0.421``

08. 2021/04/21 做bayer_reverse

09. 2021/04/21 計算RGB和BGR的PSNR

10. 2021/04/21 testing的圖加上preprocessing (bayer_reverse + resize)

11. 加入BSD200

12. 2021/04/24 創立一個縮小版本的BSD200，稱為BSD，裡面有隨機從BSD200選出30張的圖片，目的是使用輕量版的dataset測試程式碼的正確性

13. 2021/04/24 **重要！ image.load_image這個method會使到讀進來的圖片強制變成3通道！ 所以應該要用Image.open來讀取patch image**

14. 2021/04/24 稍微調整了bayer_reverse里的 R和B通道的寫法，晚點可以調回來

15. 2021/04/24 通道對調的寫法很重要 label[:,:,0] = tmp2]:,:,2]， 沒有這個部分的處理的話，藍色和紅色的色域會調換，所以不能

16. 2021/04/26 TODO, 使用bicubic

17. 2021/04/26 TODO, upsampling interpolation use 'bilinear'
   - original ``PSNR:28.82``, ``SSIM:0.774``
   - current  ``PSNR:28.95``, ``SSIM:0.784``

