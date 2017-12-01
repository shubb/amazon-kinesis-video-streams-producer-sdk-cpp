Amazon Kinesis Video Streams Producer SDK Cpp

## License

This library is licensed under the Amazon Software License.

## Introduction
Amazon Kinesis Video Streams makes it easy to securely stream video from connected devices to AWS for analytics, machine learning (ML), and other processing. 

Amazon Kinesis Video Streams Producer SDK for C/C++ makes it easy to build an on-device application that securely connects to a video stream, and reliably publishes video and other media data to Kinesis Video Streams. It takes care of all the underlying tasks required to package the frames and fragments generated by the device's media pipeline. The SDK also handles stream creation, token rotation for secure and uninterrupted streaming, processing acknowledgements returned by Kinesis Video Streams, and other tasks.  

Amazon Kinesis Video Streams Producer SDK for C/C++ contains the following sub-directories/projects:
* kinesis-video-pic - The Platform Independent Codebase which is the basic building block for the C++/Java producer SDK. The project includes multiple sub-projects for each sub-component with unit tests.
* kinesis-video-producer - The C++ Producer SDK with unit test.
* kinesis-video-producer-jni - The C++ wrapper for JNI to expose the functionality to Java/Android.
* kinesis-video-gst-demo - C++ GStreamer sample application.
* kinesis-video-native-build - Native build directory with a build script for Mac OS. This is the directory that will contain the artifacts after the build.

## Building from Source
After you've downloaded the code from GitHub, you can build it on Mac OS or Ubuntu using /kinesis-video-native-build/install-script script. This will produce the core library, the JNI library, unit tests executable and the sample GStreamer application. The script will download and build the dependent open source components in the 'downloads' directory and link against it. 

The bulk of the install script is building the open source dependencies. The project is based on CMake so the open source components building can be skipped if the system versions can be used for linking.

## Open Source Dependencies
The projects depend on the following open source components. Running install-script will download and build the necessary components automatically.

* curl lib - https://curl.haxx.se/docs/copyright.html
* openssl (crypto and ssl) - https://github.com/openssl/openssl/blob/master/LICENSE
* log4cplus - https://github.com/log4cplus/log4cplus/blob/master/LICENSE
* jsoncpp - https://github.com/open-source-parsers/jsoncpp/blob/master/LICENSE

### Build Dependencies 
Please install the following additional build tools before running install-script.
* autoconf 2.69 (License GPLv3+/Autoconf: GNU GPL version 3 or later) http://www.gnu.org/software/autoconf/autoconf.html
* cmake 3.7/3.8 https://cmake.org/
* bison 2.4 (GNU License)
* automake 1.15.1 (GNU License)
* libtool (Apple Inc. version cctools-898)
* xCode (Mac OS) / clang / gcc (xcode-select version 2347)
* Java jdk (for Java JNI compilation)

## Certificate store integration
Kinesis Video Streams Produicer SDK for C++ needs to establish trust with the backend service through TLS. This is done through validating the CAs in the public certificate store. On Linux-based models, this store is located in /etc/ssl/ directory by default. 

Please download the PEM file from 
https://www.amazontrust.com/repository/SFSRootCAG2.pem
 
to '/stc/ssl/cert.pem'. Append to the end of the file if it exists.

Many platforms come with a cert file with a lot of the well-known public certs in them.


### Launching the sample application / unit test
Define AWS_ACCESS_KEY_ID and AWS_SECRET_KEY_ID environment variables with the AWS access key id and secret key:
`export AWS_ACCESS_KEY_ID={AccessKeyId}`
`export AWS_SECRET_ACCESS_KEY={SecretAccessKey}`

#### C++ Unit tests
* The executable will be built in kinesis-video-native-build/start. Launch it and it will run the unit test and kick off dummy frame streaming.

#### GStreamer demo app
* The GStreamer demo app will be built in kinesis-video-native-build/kinesis_video_gstreamer_sample_app. Launch it with a stream name and it will start streaming from the camera.

### Enabling verbose logs
Define HEAP_DEBUG and LOG_STREAMING C-defines by uncommenting the appropriate lines in CMakeList.txt

## Release Notes
### Release 1.0.0 (November 2017)
* First release of the Amazon Kinesis Video Producer SDK for Cpp.
* Known issues:
    * Missing build scripts for Linux-based and Windows-based systems.
    * Missing cross-compile option.
    * Sample application/unit tests can't handle buffer pressures properly - simple print in debug log.
