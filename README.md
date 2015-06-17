It's easy to use. There are 4 steps.

Step 1.
Just copy modified QtMultimedia.jar and QtMultimedia-bundled.jar files into your C:\Qt\5.4\android_armv7\jar directory. If you did this before go to next step.

Step 2.
Copy libanw.14.so, libanw.18.so, libanw.21.so, libiomx.14.so, libvlcjni.so files into your project directory.

Step 3.
Add these lines to your .pro file

QT += multimedia

contains(ANDROID_TARGET_ARCH,armeabi-v7a) {
    ANDROID_EXTRA_LIBS = \
$$PWD/libanw.14.so \
$$PWD/libanw.18.so \
$$PWD/libanw.21.so \
$$PWD/libiomx.14.so \
$$PWD/libvlcjni.so
}

Step 4.
You must add ":VLC" suffix to MediaPlayer source string. Otherwise you use default Android MediaPlayer class. So, QML file seems like this:

import QtQuick 2.4
import QtQuick.Controls 1.3
import QtQuick.Window 2.2
import QtQuick.Dialogs 1.2
import QtMultimedia 5.4

ApplicationWindow {
    title: qsTr("Hello World")
    width: 640
    height: 480
    visible: true

    MediaPlayer{
        id: vlcMediaPlayer
        source: "rtsp://blablabla:VLC"
        autoPlay: true
    }
    VideoOutput{
        source: vlcMediaPlayer
        anchors.fill: parent
        fillMode: VideoOutput.Stretch
    }
}


