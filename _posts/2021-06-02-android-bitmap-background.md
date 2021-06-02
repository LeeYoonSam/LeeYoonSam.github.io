---
layout: post
title:  "[Android] 글라이드(Glide) 를 사용해서 png 이미지 일때 배경색 지정하기"
categories: android
---

> 이미지를 보여줄때 png 이미지로 배경이 없는 이미지가 나왔을때 문제가 생겨서 png 파일일 경우 흰색 배경을 지정 하였다.

<br>

처음에 떠 오른 생각은 단순하게 .png 로 끝나는 문자열이면 ImageView 의 backgroudColor 만 지정해주면 될것이라고 예상했다.
<br>

하지만, 이미지 확대, 축소 기능이 있었기 때문에 ImageView 는 화면을 꽉채운 크기로 지정해야했고, 이 조건에서 백그라운드를 지정했더니 화면 전체 영역이 하얀색 배경으로 지정되어 원하지 않는 현상이 발상했다.
<br>

이런저런 고민을 해보다가 ImageView 의 크기를 Glide 에서 제공하는 override 함수를 사용해서 디바이스 크기만큼 리사이즈 되도록 지정하고 뒤에는 검은색 투명이 보이게 했다.
<br>

이미지도 잘 보이고 그럴싸하게 잘 되는듯 했지만, 확대를 해보니 ImageView 의 크기가 고정되어 화면 전체를 사용해서 확대가 되지 않았다.
<br>

여러가지로 고민해보고 구글링을 해본 결과 Glide 의 CustomTarget 을 사용해서 Drawable resource 를 전달받아서 BitmapDrawable 로 변환하고 Canvas 를 사용해서 해당 캔버스만큼만 배경색을 지정하도록 해서 해결했다.
<br>

{% highlight kotlin %}
Glide.with(view.context)
    .load(imageUrl)
    .addListener(requestListener)
    .into(object : CustomTarget<Drawable?>() {
        override fun onLoadCleared(placeholder: Drawable?) {}
        override fun onResourceReady(
            resource: Drawable,
            transition: Transition<in Drawable?>?
        ) {
            // png 파일이면 흰배경색을 추가
            if (imageUrl.endsWith(".png")) {
                val bitmap = (resource as BitmapDrawable).bitmap
                val outBitmap = Bitmap.createBitmap(
                    bitmap.width,
                    bitmap.height,
                    Bitmap.Config.ARGB_8888
                )
                val canvas = Canvas(outBitmap)
                canvas.drawColor(-0x1)
                canvas.drawBitmap(bitmap, 0f, 0f, null)
                targetImageView.setImageBitmap(outBitmap)
                return
            }

            targetImageView.setImageDrawable(resource)
        }
    })
{% endhighlight %}