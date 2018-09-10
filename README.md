# flutter_umpush

Flutter ��������
���ڿ����С�Ŀǰ��׿ƽ̨������ɡ�

## ROADMAP

* [ ] ios
* [x] android
* [x] ����notification
* [x] ����message
* [x] ����alias
* [x] ����tags
* [x] �������е�����
* [ ] �û����໥��������


## ���ɹ���

### ׼������

�� pubspec.yaml �м��� flutter-umpush 

### ����key

����[����](http://message.umeng.com/list/new/app)�������������Ӧ�á�Ȼ�������Ӧ����Ϣ�п��� Appkey��Umeng Message Secret
ͬʱ��Ӧ����Ϣ�п������ð���Ϊ���app������
��ϸ��Ϣ�ο������ĵ�(https://developer.umeng.com/?refer=UPush)

#### ios ֤������

ͬ��׿һ�����루http://message.umeng.com/list/apps���½�Ӧ�á�
����ο�iOS�����ĵ�(https://developer.umeng.com/docs/66632/detail/66734)

### ios ����


### Android ����

1. �����ػ���SDK�У�����Ŀexample���� push �ļ��и��Ƶ�����Ŀ�� android Ŀ¼�С�
2. �� push �� libs �н�ȱ�ٵ�so��jar��ȫ���ο���ͼ

![image](https://github.com/yangyxd/flutter_umpush/blob/master/raw/img001.png)

3. �޸� android\settings.gradle �ļ�������include ':push'
```
include ':app',':push'

def flutterProjectRoot = rootProject.projectDir.parentFile.toPath()
...
```

4. �޸� android\app\build.gradle ���� android ��������� manifestPlaceholders �� ndk

```

android {
  ...
  
         // ��ӵ�����
  
         manifestPlaceholders = [
                UMPUSH_PKGNAME : applicationId,
                UMPUSH_APPKEY : "5b8c9800f29d9836ac000017", //Push��ע��İ�����Ӧ��appkey.
                UMPUSH_CHANNEL : "umpush",
                UMENG_MESSAGE_SECRET : "b11af04a78ddc9c6ca246a7dc8c275d7",
        ]

        ndk {
            //ѡ��Ҫ��ӵĶ�Ӧcpu���͵�.so�⡣
            abiFilters 'x86', 'x86_64',  'armeabi-v7a'
            // abiFilters 'armeabi-v7a'
            // ��������� 'x86', 'x86_64', 'mips', 'mips64', 'armeabi', 'armeabi-v7a', 'arm64-v8a'
        }
 
  
  ...
}

```

5. �޸� AndroidManifest.xml

```
�� application �е� 

android:name="io.flutter.app.FlutterApplication" 

�޸�Ϊ 

android:name="com.yangyxd.flutterumpush.MainApplication"

```

## ʹ�ò��

�� initState() �г�ʼ������Ӽ���

```
    await FlutterUmPush.startup();

    FlutterUmPush.addConnectionChangeListener((bool connected) {
      setState(() {
        /// �Ƿ����ӣ������˲ſ�������
        print("����״̬�ı�:$connected");
        this.isConnected = connected;
        if (connected) {
          FlutterUmPush.getRegistrationID().then((String regId) {
            print("������ȡ�豸��:$regId");
            setState(() {});
          });
        }
      });
    });

    FlutterUmPush.addnetworkDidLoginListener((String registrationId) {
      setState(() {
        /// ��������
        print("�յ��豸��:$registrationId");
      });
    });

    FlutterUmPush
        .addReceiveNotificationListener((PushMessage notification) {
      setState(() {
        /// �յ�����
        print("�յ���������: $notification");
      });
    });

    FlutterUmPush
        .addReceiveOpenNotificationListener((PushMessage notification) {
      setState(() {
        print("������������: $notification");
      });
    });

    FlutterUmPush.addReceiveCustomMsgListener((PushMessage msg) {
      setState(() {
        print("�յ�������Ϣ����: $msg");
      });
    });
    
```

## License MIT

## ��л
����Ŀֱ������ѩ���ļ������Ϳ�����ĵģ�ʡ�˲���ʱ�䣬�ڴ˱�ʾ��л��
�������ͣ�https://github.com/best-flutter/flutter_jpush

## ��ӭ�ύissue���߼���QQȺ325337654

