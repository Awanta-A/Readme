# Deepstream Setup 
## Jetson Setup
_Use NVIDIA SDK Manager for install JetPack and Deepstream_

_After installed Open terminal and run command_
```bash
$ sudo apt update
$ sudo apt install python3-pip
$ sudo pip3 install -U jetson-stats
```
_Restart and run_
```bash
$ jtop
```

**Migrate glib to newer version**

_In order to migrate to newer glib version (e.g. 2.76.6) follow below steps:_
    
1. Prerequisites: Install below packages:
    ```bash
    $ sudo pip3 install meson
    $ sudo pip3 install ninja
    ```
2. Compilation and installation steps:

    ```bash
    $ git clone https://github.com/GNOME/glib.git
    $ cd glib
    $ git checkout <glib-version-branch>
    # recommend : main
    $ meson build --prefix=/usr
    $ ninja -C build/
    $ cd build/
    $ sudo ninja install
    ```
3. Check and confirm the newly installed glib version:
    ```bash
    $ pkg-config --modversion glib-2.0
    ```
**Install prerequisite packages**
```bash
$ sudo apt install \
libssl3 \
libssl-dev \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstreamer-plugins-base1.0-dev \
libgstrtspserver-1.0-0 \
libjansson4 \
libyaml-cpp-dev
```
**Install librdkafka (to enable Kafka protocol adaptor for message broker)**
1. Clone the librdkafka repository from GitHub:
    ```bash
    $ git clone https://github.com/confluentinc/librdkafka.git
    ```
2. Configure and build the library:
    ```bash
    $ cd librdkafka
    $ git checkout tags/v2.2.0
    $ ./configure --enable-ssl
    $ make
    $ sudo make install
    ```
3. Copy the generated libraries to the deepstream directory:
    ```bash
    $ sudo mkdir -p /opt/nvidia/deepstream/deepstream/lib
    $ sudo cp /usr/local/lib/librdkafka* /opt/nvidia/deepstream/deepstream/lib
    $ sudo ldconfig
    ```
**Run deepstream-app example**
1. Navigate to the configs/deepstream-app directory on the development kit.
    ```bash
    $ cd /opt/nvidia/deepstream/deepstream-7.1/samples/configs/deepstream-app
    ```
2. Enter the following command to run the reference application:
    ```bash
    # deepstream-app -c <path_to_config_file>
    $ deepstream-app -c source30_1080p_dec_infer-resnet_tiled_display_int8.txt
    ```
    _Where <path_to_config_file> is the pathname of one of the reference application’s configuration files, found in **configs/deepstream-app/**. See Package Contents in **configs/deepstream-app/** for a list of the available files._
   
    _Config files that can be run with deepstream-app:_
    * source30_1080p_dec_infer-resnet_tiled_display_int8.txt

    * source30_1080p_dec_preprocess_infer-resnet_tiled_display_int8.txt

    * source4_1080p_dec_infer-resnet_tracker_sgie_tiled_display_int8.txt

    * source1_usb_dec_infer_resnet_int8.txt

    * source1_csi_dec_infer_resnet_int8.txt

    * source2_csi_usb_dec_infer_resnet_int8.txt

    * source6_csi_dec_infer_resnet_int8.txt

    * source2_1080p_dec_infer-resnet_demux_int8.txt

    * source4_1080p_dec_infer-resnet_tracker_sgie_tiled_display_int8.yml

    * source30_1080p_dec_infer-resnet_tiled_display_int8.yml

    * source4_1080p_dec_preprocess_infer-resnet_preprocess_sgie_tiled_display_int8.txt

    * source2_dewarper_test.txt

