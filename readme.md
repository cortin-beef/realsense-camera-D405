---


---

<p>本安装测试用于ubuntu24.03.live-server-amd端<br>
<strong>#Installation on Ubuntu</strong><br>
##Step 1:Install the ROS2 distribution*</p>
<ul>
<li>Ubuntu 24.04
<ul>
<li><a href="https://docs.ros.org/en/rolling/Installation/Ubuntu-Install-Debs.html">ROS2 Rolling</a></li>
<li><a href="https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html">ROS2 Jazzy</a></li>
</ul>
</li>
</ul>
<p>在ubuntu终端中输入<code>printenv ROS_DISTRO</code><br>
若输出为<code>rolling</code>则证明安装成功。</p>
<p>##Step 2:Install latest Intel® RealSense™ SDK 2.0</p>
<ul>
<li><strong>Option 1: Install librealsense2 debian package from Intel servers</strong>
<ul>
<li>Jetson user - use the <a href="https://github.com/IntelRealSense/librealsense/blob/master/doc/installation_jetson.md"> Jetson Installation Guide</a></li>
<li>Otherwise, install from[<a href="https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md#installing-the-packages">Linux Debian Installation Guide</a>]
<ul>
<li>In this case treat yourself as a developer: make sure to follow the instructions to also install librealsense2-dev and librealsense2-dkms packages</li>
</ul>
</li>
</ul>
</li>
<li><strong>Option 2: Install librealsense2 (without graphical tools and examples) debian package from ROS servers (Foxy EOL distro is not supported by this option)</strong>:</li>
<li>Configure your Ubuntu repositories</li>
<li>Install all realsense ROS packages by <code>sudo apt install ros-&lt;ROS_DISTRO&gt;-librealsense2*</code>
<ul>
<li>For example, for Humble distro: sudo apt install ros-humble-librealsense2*</li>
</ul>
</li>
<li>Option 3: Build from source</li>
<li>Download the latest <a href="https://github.com/IntelRealSense/librealsense">Intel® RealSense™ SDK 2.0</a></li>
<li>Follow the instructions under [<a href="https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md">Linux Installation</a>]</li>
<li><strong>注意：执行到Run Intel Realsense permissions script from <em>librealsense2</em> root directory<br>
cd librealsense<br>
./scripts/setup_udev_rules.sh<br>
时会出现<code>v4l2-ctl not found, install with: sudo apt install v4l-utils问题</code>，继续输入<code>sudo apt install v4l-utils</code></strong><br>
<strong>在终端输入realsense-viewer以测试成功安装。</strong></li>
</ul>
<p>##Step 3: Install ROS Wrapper for Intel® RealSense™ cameras</p>
<p>Install from source</p>
<pre><code>mkdir -p ~/ros2_ws/src
</code></pre>
<p>cd ~/ros2_ws/src/</p>
<ul>
<li>
<p>Clone the latest ROS Wrapper for Intel® RealSense™ cameras from here into ‘~/ros2_ws/src/’</p>
<pre><code> git clone https://github.com/IntelRealSense/realsense-ros.git -b ros2-master
 cd ~/ros2_ws
</code></pre>
</li>
<li>
<p>Install dependencies</p>
<pre><code>   sudo apt-get install python3-rosdep -y
   sudo rosdep init # "sudo rosdep init --include-eol-distros" for Foxy        and earlier
   rosdep update # "sudo rosdep update --include-eol-distros" for          Foxy and earlier
   rosdep install -i --from-path src --rosdistro $ROS_DISTRO --skip-keys=librealsense2 -y
</code></pre>
</li>
<li>
<p>Build</p>
<pre><code>   colcon build
</code></pre>
</li>
<li>
<p>Source environment</p>
<pre><code>    ROS_DISTRO=&lt;YOUR_SYSTEM_ROS_DISTRO&gt;  # set your    ROS_DISTRO: kilted, jazzy, iron, humble, foxy
    source /opt/ros/$ROS_DISTRO/setup.bash
    cd ~/ros2_ws
    . install/local_setup.bash
</code></pre>
</li>
<li>
<p>验证：</p>
<p><code>rviz2</code></p>
<p>观察pointclouds信息</p>
</li>
</ul>
<hr>

