# 打造高效的图片加载框架

![预览图片](https://github.com/Demigirlz/network_imageloader_with_diskcache/blob/master/a.gif "预览图片")

### 1、本地图片的压缩

   a、获得imageview想要显示的大小
   想要压缩，我们第一步应该是获得imageview想要显示的大小，没大小肯定没办法压缩？
   那么如何获得imageview想要显示的大小呢？

    /**
         * 根据ImageView获适当的压缩的宽和高
         *
         * @param imageView
         * @return
         */
        public static ImageSize getImageViewSize(ImageView imageView)
        {

            ImageSize imageSize = new ImageSize();
            DisplayMetrics displayMetrics = imageView.getContext().getResources()
                    .getDisplayMetrics();

            LayoutParams lp = imageView.getLayoutParams();

            int width = imageView.getWidth();
    // 获取imageview的实际宽度
            if (width <= 0)
            {
                width = lp.width;
    // 获取imageview在layout中声明的宽度
            }
            if (width <= 0)
            {

    // width = imageView.getMaxWidth();// 检查最大值
                width = getImageViewFieldValue(imageView, "mMaxWidth");
            }
            if (width <= 0)
            {
                width = displayMetrics.widthPixels;
            }

            int height = imageView.getHeight();
    // 获取imageview的实际高度
            if (height <= 0)
            {
                height = lp.height;
    // 获取imageview在layout中声明的宽度
            }
            if (height <= 0)
            {
                height = getImageViewFieldValue(imageView, "mMaxHeight");
    // 检查最大值
            }
            if (height <= 0)
            {
                height = displayMetrics.heightPixels;
            }
            imageSize.width = width;
            imageSize.height = height;

            return imageSize;
        }

        public static class ImageSize
        {
            int width;
            int height;
        }

