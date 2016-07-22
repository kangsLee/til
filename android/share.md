# 공유하기 

## 페이스북 공유하기
```java
 boolean facebookAppFound = false;

        List<ResolveInfo> matches = getPackageManager().queryIntentActivities(intent, 0);
        for (ResolveInfo info : matches) {
            if (info.activityInfo.packageName.toLowerCase().startsWith("com.facebook.katana")) {
                intent.setPackage(info.activityInfo.packageName);
                facebookAppFound = true;
                break;
            }
        }

        if (!facebookAppFound) {
            String shareUrl = "https://www.facebook.com/sharer/sharer.php?u=" + imageUri;
            intent = new Intent(Intent.ACTION_VIEW, Uri.parse(shareUrl));
        }

        startActivityForResult(intent, 0);
    }
```
- 공유하기에서 package name을 필터링하여 해당 package name과 일치하는 app만 뽑아준다.  
facebook은 com.faceook.katana 라는 패키지로 시작하기 때문에 페이스북 관련 앱만 나타나게 된다.
## SDK를 이용한 페이스북 공유하기

```java
 shareDialog = new ShareDialog(this);
            ShareLinkContent content = new ShareLinkContent.Builder()
                    .setContentUrl(Uri.parse("https://developers.facebook.com"))
                    .setShareHashtag(new ShareHashtag.Builder()
                            .setHashtag("#아티즘 #Artism")
                            .build())
                    .build();

            shareDialog.show(content);
```
- Facebook SDK를 이용한 공유하는 것, ShareDialog를 띄우며 원하는 정보를 추가할 수 있다.  
위 코드는 해시태그와 링크정보를 추가하는 내용이며 더 추가할 정보가 있다면 아래 링크를 참조한다.
- https://developers.facebook.com/docs/sharing/android