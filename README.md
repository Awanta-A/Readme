# Deepstream Setup 
## Jetson Setup
_Open terminal and run command_
```bash
$ sudo apt update
$ sudo apt install python3-pip
$ sudo pip3 install -U jetson-stats
```
_Restart and run_
```bash
$ jtop
```

**Install Glib**
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
