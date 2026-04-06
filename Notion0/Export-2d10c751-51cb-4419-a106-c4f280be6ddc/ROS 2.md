[https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries.html](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries.html)

[https://youtube.com/playlist?list=PLLSegLrePWgJudpPUof4-nVFHGkB62Izy&si=mBOCv8BS9ea57ROA](https://youtube.com/playlist?list=PLLSegLrePWgJudpPUof4-nVFHGkB62Izy&si=mBOCv8BS9ea57ROA)

- **Installation** Ubuntu Linux - Jammy Jellyfish (22.04) - [deb packages](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)
    
    ## Set locale
    
    - 確保語言環境支援`UTF-8`。
        
        ```Shell
        locale  # check for UTF-8
        ```
        
    
    ---
    
    ## Setup Sources
    
    - 安裝 ros2-apt-source 軟體包將為您的系統設定 ROS 2 倉庫。
        
        ```Shell
        sudo apt update && sudo apt install curl -y
        export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')
        curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo $VERSION_CODENAME)_all.deb" # If using Ubuntu derivates use $UBUNTU_CODENAME
        sudo apt install /tmp/ros2-apt-source.deb
        ```
        
    
    ---
    
    ## Install ROS 2 packages
    
    - 設定儲存庫後更新您的 apt 儲存庫快取。
        
        ```Shell
        sudo apt update
        ```
        
    
    - ROS 2 軟體套件是基於頻繁更新的 Ubuntu 系統建置。建議您在安裝新軟體包之前，請確保系統已更新至最新版本。
        
        ```Shell
        sudo apt upgrade
        ```
        
    
    - 桌面安裝（建議）：ROS, RViz, demos, tutorials.
        
        ```Shell
        sudo apt install ros-humble-desktop
        ```
        
    
    ---
    
    ## Environment setup
    
    - 透過取得以下文件來設定您的環境。
        
        ```Shell
        gedit ~/.bashrc
        
        source /opt/ros/humble/setup.bash # 加入到文件尾端
        ```
        
    
      
    

---

- **Start First ROS2 Node (**Demo)
    
    ```Shell
    ros2 run demo_nodes_cpp talker
    
    ros2 run demo_nodes_cpp listener
    ```
    
    ```Shell
    rqt_graph
    ```
    
    ![[Attachments/image 6.png|image 6.png]]
    
    ```Shell
    ros2 run turtlesim turtle_teleop_key
    
    ros2 run turtlesim turtlesim_node
    ```
    
    ![[Attachments/image 1 2.png|image 1 2.png]]
    

---

- **Create and Set Up a ROS2 Workspace**
    
    Installation Build Tool
    
    ```Shell
    sudo apt install python3-colcon-common-extensions
    ```
    
    ```Shell
    gedit ~/.bashrc
    
    source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash # 加入到文件尾端
    ```
    
    ---
    
    ```Shell
    mkdir ros2_ws
    cd ros2_ws/
    mkdir src
    colcon build
    ```
    
    ```Shell
    gedit ~/.bashrc
    
    source ~/ros2_ws/install/setup.bash # 加入到文件尾端
    ```
    

---

- **Create a ROS2 Python Package**
    
    ```Shell
    ros2 pkg create my_robot_controller --build-type ament_python --dependencies rcply
    ```
    
    ```Shell
    sudo snap install code --classic
    code .
    ```
    
    ![[2b96a491-63f2-4432-ac58-56f6e96ba306.png]]
    

---

- **Create a ROS2 Node with Python**
    
    ```Shell
    cd ros2_ws/src/my_robot_controller/my_robot_controller/
    touch my_first_node.py
    chmod +x my_first_node.py
    ```
    
    Install ROS extension on VS Code
    
    ```Python
    #!/usr/bin/env python3
    import rclpy
    from rclpy.node import Node
    
    class MyNode(Node):
    
        def __init__(self):
            super().__init__("first_node")
            self.get_logger().info("Hello from ROS2")
    
    def main(args=None):
        rclpy.init(args=args)
        node = MyNode()
        rclpy.spin(node)
        rclpy.shutdown()
    
    if __name__ == "__main__":
        main()
    ```
    
    ```Python
    from setuptools import find_packages, setup
    
    package_name = 'my_robot_controller'
    
    setup(
        name=package_name,
        version='0.0.0',
        packages=find_packages(exclude=['test']),
        data_files=[
            ('share/ament_index/resource_index/packages',
                ['resource/' + package_name]),
            ('share/' + package_name, ['package.xml']),
        ],
        install_requires=['setuptools'],
        zip_safe=True,
        maintainer='test',
        maintainer_email='test@todo.todo',
        description='TODO: Package description',
        license='TODO: License declaration',
        tests_require=['pytest'],
        entry_points={
            'console_scripts': [
            "test_node = my_robor_controller.my_first_node:main"
            ],
        },
    )
    ```
    
    ```Shell
    colcon build -> 
    colcon build --symlink-install
    
    source ~/.bashrc
    
    ros2 run my_robot_controller test_node
    ```
    
    ```Python
    #!/usr/bin/env python3
    import rclpy
    from rclpy.node import Node
    
    class MyNode(Node):
    
        def __init__(self):
            super().__init__("first_node")
            self.counter_ = 0
            self.create_timer(1.0 , self.timer_callback)
    
        def timer_callback(self):
            self.get_logger().info("Hello " + str(self.counter_ ))
            self.counter_  += 1
    
    def main(args=None):
        rclpy.init(args=args)
        node = MyNode()
        rclpy.spin(node)
        rclpy.shutdown()
    
    if __name__ == "__main__":
        main()
    ```
    
    ```Shell
    test@test:~$ ros2 node list 
    /first_node
    test@test:~$ ros2 node info /first_node
    ```
    

---

- **What is a ROS2 Topic?**
    
    ![[9087dc94-c988-4581-9250-cf299cec46fe.png]]
    
    ```Shell
    test@test:~$ ros2 topic list 
    /chatter
    /parameter_events
    /rosout
    
    test@test:~$ ros2 topic info /chatter 
    Type: std_msgs/msg/String
    Publisher count: 1
    Subscription count: 1
    
    test@test:~$ ros2 interface show std_msgs/msg/String 
    # This was originally provided as an example message.
    # It is deprecated as of Foxy
    # It is recommended to create your own semantically meaningful message.
    # However if you would like to continue using this please use the equivalent in example_msgs.
    
    string data
    
    test@test:~$ ros2 topic echo /chatter 
    data: 'Hello World: 23'
    ---
    data: 'Hello World: 24'
    ---
    
    test@test:~$ ros2 topic info /chatter 
    Type: std_msgs/msg/String
    Publisher count: 1
    Subscription count: 2
    ```
    
    ![[Attachments/image 2 2.png|image 2 2.png]]
    
    ---
    
    ![[Attachments/image 3 2.png|image 3 2.png]]
    
    ```Shell
    test@test:~$ ros2 topic list 
    /parameter_events
    /rosout
    /turtle1/cmd_vel
    /turtle1/color_sensor
    /turtle1/pose
    
    test@test:~$ ros2 topic info /turtle1/cmd_vel 
    Type: geometry_msgs/msg/Twist
    Publisher count: 1
    Subscription count: 1
    
    test@test:~$ ros2 interface show geometry_msgs/msg/Twist
    # This expresses velocity in free space broken into its linear and angular parts.
    
    Vector3  linear
    	float64 x
    	float64 y
    	float64 z
    Vector3  angular
    	float64 x
    	float64 y
    	float64 z
    ```
    

---

- **Write a ROS2 Publisher with Python**
    
    ```Shell
    cd ros2_ws/src/my_robot_controller/my_robot_controller/
    touch draw_circle.py
    chmod +x draw_circle.py
    ```
    
    ```XML
    <?xml version="1.0"?>
    <?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
    <package format="3">
      <name>my_robot_controller</name>
      <version>0.0.0</version>
      <description>TODO: Package description</description>
      <maintainer email="test@todo.todo">test</maintainer>
      <license>TODO: License declaration</license>
    
      <depend>rcply</depend>
      <depend>geometry_msgs</depend>
      <depend>turtlesim</depend>
    
      <test_depend>ament_copyright</test_depend>
      <test_depend>ament_flake8</test_depend>
      <test_depend>ament_pep257</test_depend>
      <test_depend>python3-pytest</test_depend>
    
      <export>
        <build_type>ament_python</build_type>
      </export>
    </package>
    ```
    
    ```Python
    #!/usr/bin/env python3
    import rclpy
    from rclpy.node import Node
    from  geometry_msgs.msg import Twist
    
    class DrawCircleNode(Node):
    
        def __init__(self):
            super().__init__("draw_circle")
            self.cmd_vel_pub_ = self.create_publisher(Twist, "/turtle1/cmd_vel", 10)
            self.timer_ = self.create_timer(0.5, self.send_velocity_command)
            self.get_logger().info("Draw circle node has been started")
    
        def send_velocity_command(self):
            msg = Twist()
            msg.linear.x = 2.0
            msg.angular.z = 1.0
            self.cmd_vel_pub_.publish(msg)
    
    def main(args=None):
        rclpy.init(args=args)
        node = DrawCircleNode()
        rclpy.spin(node)
        rclpy.shutdown()
    ```
    
    ```Python
    from setuptools import find_packages, setup
    
    package_name = 'my_robot_controller'
    
    setup(
        name=package_name,
        version='0.0.0',
        packages=find_packages(exclude=['test']),
        data_files=[
            ('share/ament_index/resource_index/packages',
                ['resource/' + package_name]),
            ('share/' + package_name, ['package.xml']),
        ],
        install_requires=['setuptools'],
        zip_safe=True,
        maintainer='test',
        maintainer_email='test@todo.todo',
        description='TODO: Package description',
        license='TODO: License declaration',
        tests_require=['pytest'],
        entry_points={
            'console_scripts': [
                "test_node = my_robot_controller.my_first_node:main",
                "draw_circle = my_robot_controller.draw_circle:main"
            ],
        },
    )
    ```
    
    ```Shell
    colcon build --symlink-install
    
    ros2 run turtlesim turtlesim_node
    
    ros2 run my_robot_controller draw_circle
    ```
    

---

- **Write a ROS2 Subscriber with Python**
    
    ![[Attachments/image 4 2.png|image 4 2.png]]
    
    ```Shell
    test@test:~$ ros2 topic list 
    /parameter_events
    /rosout
    /turtle1/cmd_vel
    /turtle1/color_sensor
    /turtle1/pose
    
    test@test:~$ ros2 topic info /turtle1/pose 
    Type: turtlesim/msg/Pose
    Publisher count: 1
    Subscription count: 0
    
    test@test:~$ ros2 interface show turtlesim/msg/Pose 
    float32 x
    float32 y
    float32 theta
    
    float32 linear_velocity
    float32 angular_velocity
    ```
    
    ```Shell
    cd ros2_ws/src/my_robot_controller/my_robot_controller/
    touch pose_subscriber.py
    chmod +x pose_subscriber.py
    ```
    
    ```Python
    #!/usr/bin/env python3
    import rclpy
    from rclpy.node import Node
    from turtlesim.msg import Pose
    
    class PoseSubscriberNode(Node):
    
        def __init__(self):
            super().__init__("pose_subscribers")
            self.pose_subscriber_ = self.create_subscription(
                Pose, "/turtle1/pose", self.pose_callback, 10)
    
        def pose_callback(self, msg: Pose):
            self.get_logger().info("(" + str(msg.x) + ", " + str(msg.y) + ")")
    
    def main(args=None):
        rclpy.init(args=args)
        node = PoseSubscriberNode()
        rclpy.spin(node)
        rclpy.shutdown()
    ```
    
    ```Python
    from setuptools import find_packages, setup
    
    package_name = 'my_robot_controller'
    
    setup(
        name=package_name,
        version='0.0.0',
        packages=find_packages(exclude=['test']),
        data_files=[
            ('share/ament_index/resource_index/packages',
                ['resource/' + package_name]),
            ('share/' + package_name, ['package.xml']),
        ],
        install_requires=['setuptools'],
        zip_safe=True,
        maintainer='test',
        maintainer_email='test@todo.todo',
        description='TODO: Package description',
        license='TODO: License declaration',
        tests_require=['pytest'],
        entry_points={
            'console_scripts': [
                "test_node = my_robot_controller.my_first_node:main",
                "draw_circle = my_robot_controller.draw_circle:main",
                "pose_subscriber = my_robot_controller.pose_subscriber:main"
            ],
        },
    )
    ```
    
    ```Shell
    colcon build --symlink-install
    
    ros2 run my_robot_controller pose_subscriber
    
    ros2 run turtlesim turtlesim_node
    
    ros2 run my_robot_controller draw_circle
    ```
    
    ![[Attachments/image 5 2.png|image 5 2.png]]
    
    ![[Attachments/image 6 2.png|image 6 2.png]]
    

---

- Create a Closed Loop System with a Publisher and a Subscriber
    
    ```Shell
    cd ros2_ws/src/my_robot_controller/my_robot_controller/
    touch turtle_controller.py
    chmod +x turtle_controller.py
    ```
    
    ```Python
    #!/usr/bin/env python3
    import rclpy
    from rclpy.node import Node
    from turtlesim.msg import Pose
    from geometry_msgs.msg import Twist
    
    class TurtleControllerNode(Node):
    
        def __init__(self):
            super().__init__("turtle_controller")
            self.cmd_vel_publisher_ = self.create_publisher(
                Twist, "/turtle1/cmd_vel", 10)
            self.pose_subscriber_ = self.create_subscription(
                Pose, "/turtle1/pose", self.pose_callback, 10)
            self.get_logger().info("Turtle controller has been started")
    
        def pose_callback(self, pose: Pose):
            cmd = Twist()
            if pose.x > 9.0 or pose.x < 2.0 or pose.y > 9.0 or pose.y < 2.0:
                cmd.linear.x = 1.0
                cmd.angular.z = 0.9
            else:
                cmd.linear.x = 5.0
                cmd.angular.z = 0.0
            self.cmd_vel_publisher_.publish(cmd)
            
    
    def main(agrs=None):
        rclpy.init(args=agrs)
        node = TurtleControllerNode()
        rclpy.spin(node)
        rclpy.shutdown()
    ```
    
    ```Python
    from setuptools import find_packages, setup
    
    package_name = 'my_robot_controller'
    
    setup(
        name=package_name,
        version='0.0.0',
        packages=find_packages(exclude=['test']),
        data_files=[
            ('share/ament_index/resource_index/packages',
                ['resource/' + package_name]),
            ('share/' + package_name, ['package.xml']),
        ],
        install_requires=['setuptools'],
        zip_safe=True,
        maintainer='test',
        maintainer_email='test@todo.todo',
        description='TODO: Package description',
        license='TODO: License declaration',
        tests_require=['pytest'],
        entry_points={
            'console_scripts': [
                "test_node = my_robot_controller.my_first_node:main",
                "draw_circle = my_robot_controller.draw_circle:main",
                "pose_subscriber = my_robot_controller.pose_subscriber:main",
                "turtle_controller = my_robot_controller.turtle_controller:main"
                
            ],
        },
    )
    ```
    
    ```Shell
    colcon build --symlink-install
    
    ros2 run turtlesim turtlesim_node
    
    ros2 run my_robot_controller turtle_controller.py
    ```
    
    ![[image 7.png]]
    

---

- **What is a ROS2 Service?**
    
    ```Shell
    test@test:~$ ros2 run demo_nodes_cpp add_two_ints_server
    [INFO] [1751016991.496232701] [add_two_ints_server]: Incoming request
    a: 2 b: 5
    ```
    
    ```Shell
    test@test:~$ ros2 node list 
    /add_two_ints_server
    
    test@test:~$ ros2 service list 
    /add_two_ints
    /add_two_ints_server/describe_parameters
    /add_two_ints_server/get_parameter_types
    /add_two_ints_server/get_parameters
    /add_two_ints_server/list_parameters
    /add_two_ints_server/set_parameters
    /add_two_ints_server/set_parameters_atomically
    
    test@test:~$ ros2 service type /add_two_ints
    example_interfaces/srv/AddTwoInts
    
    test@test:~$ ros2 interface show example_interfaces/srv/AddTwoInts
    int64 a
    int64 b
    ---
    int64 sum
    
    test@test:~$ ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts "{'a': 2, 'b': 5}"
    waiting for service to become available...
    requester: making request: example_interfaces.srv.AddTwoInts_Request(a=2, b=5)
    
    response:
    example_interfaces.srv.AddTwoInts_Response(sum=7)
    ```
    
    ---
    
    ```Shell
    test@test:~$ ros2 run turtlesim turtlesim_node 
    
    test@test:~$ ros2 service list 
    /clear
    /kill
    /reset
    /spawn
    /turtle1/set_pen
    /turtle1/teleport_absolute
    /turtle1/teleport_relative
    /turtlesim/describe_parameters
    /turtlesim/get_parameter_types
    /turtlesim/get_parameters
    /turtlesim/list_parameters
    /turtlesim/set_parameters
    /turtlesim/set_parameters_atomically
    
    test@test:~$ ros2 service type /turtle1/set_pen
    turtlesim/srv/SetPen
    
    test@test:~$ ros2 interface show turtlesim/srv/SetPen
    uint8 r
    uint8 g
    uint8 b
    uint8 width
    uint8 off
    ---
    
    test@test:~$ ros2 service call /turtle1/set_pen turtlesim/srv/SetPen "{'r': 255, 'g': 0, 'b': 0, 'width': 3, 'off': 0}" 
    waiting for service to become available...
    requester: making request: turtlesim.srv.SetPen_Request(r=255, g=0, b=0, width=3, off=0)
    
    response:
    turtlesim.srv.SetPen_Response()
    ```
    
    ![[274841ed-468f-4d2e-a7ff-66758eea8c88.png]]
    

---

- **Write a ROS2 Service Client with Python**
    
    ```Shell
    test@test:~$ ros2 topic hz /turtle1/pose
    WARNING: topic [/turtle1/pose] does not appear to be published yet
    average rate: 62.408
    min: 0.014s max: 0.018s std dev: 0.00067s window: 64
    average rate: 62.471
    min: 0.014s max: 0.018s std dev: 0.00061s window: 127
    average rate: 62.497
    min: 0.014s max: 0.018s std dev: 0.00061s window: 190
    ```
    
    ```Python
    #!/usr/bin/env python3
    import rclpy
    from rclpy.node import Node
    from turtlesim.msg import Pose
    from geometry_msgs.msg import Twist
    from turtlesim.srv import SetPen
    from functools import partial
    
    class TurtleControllerNode(Node):
    
        def __init__(self):
            super().__init__("turtle_controller")
            self.previous_x_ = 0
            self.cmd_vel_publisher_ = self.create_publisher(
                Twist, "/turtle1/cmd_vel", 10)
            self.pose_subscriber_ = self.create_subscription(
                Pose, "/turtle1/pose", self.pose_callback, 10)
            self.get_logger().info("Turtle controller has been started")
    
        def pose_callback(self, pose: Pose):
            cmd = Twist()
            if pose.x > 9.0 or pose.x < 2.0 or pose.y > 9.0 or pose.y < 2.0:
                cmd.linear.x = 1.0
                cmd.angular.z = 0.9
            else:
                cmd.linear.x = 5.0
                cmd.angular.z = 0.0
            self.cmd_vel_publisher_.publish(cmd)
    
            if pose.x > 5.5 and self.previous_x_ <= 5.5:
                self.previous_x_ = pose.x
                self.get_logger().info("Set color to red!")
                self.call_set_pen_service(255, 0, 0, 3, 0)
            elif pose.x <= 5.5 and self.previous_x_ > 5.5:
                self.previous_x_ = pose.x
                self.get_logger().info("Set color to green!")
                self.call_set_pen_service(0, 255, 0, 3, 0)
    
        def call_set_pen_service(self, r, g, b, width, off):
            client = self.create_client(SetPen, "/turtle1/set_pen")
            while not client.wait_for_service(1.0):
                self.get_logger().warn("Waiting for service...")
    
            request = SetPen.Request()
            request.r = r
            request.g = g
            request.b = b
            request.width = width
            request.off = off
    
            future = client.call_async(request)
            future.add_done_callback(partial(self.callback_set_pen))
    
        def callback_set_pen(self, future):
            try:
                response = future.result()
            except Exception as e:
                self.get_logger().error("Service call failed: %r" %(e,))
    
    def main(agrs=None):
        rclpy.init(args=agrs)
        node = TurtleControllerNode()
        rclpy.spin(node)
        rclpy.shutdown()
    ```
    
    ![[image 8.png]]
    

---

  

# Isaac Sim

```PowerShell
rviz2
ros2 param set /rviz use_sim_time true
```

```PowerShell
ros2 run teleop_twist_keyboard teleop_twist_keyboard
# ros2 run turtlebot3_teleop teleop_keyboard
```

「turtlebot3_cartographer」與「SLAM Toolbox」

- A. 一邊建圖一邊導航（SLAM mode）

- B. 先建圖 → 存檔 → 之後用 **AMCL / 或 SLAM 的定位模式** 來導航（Localization mode）

- turtlebot3_cartographer 版
    
    Cartographer 比較適合「B. 先建圖 → 再導航」。
    
    要「邊建圖邊導航」也能做，但整合沒有 slam_toolbox 順手。
    
    B-1) 先建圖
    
    ```PowerShell
    ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
    # 開 RViz，遙控跑一圈，建圖結束後存檔
    ros2 run nav2_map_server map_saver_cli -f ~/map
    # 會得到 ~/maps/tb3_map.yaml / tb3_map.pgm
    ```
    
    B-2) 用 AMCL + Nav2 導航
    
    ```PowerShell
    # 使用 TurtleBot3 預設的 Nav2 參數（含 costmap、planner 等）
    ros2 launch turtlebot3_navigation2 navigation2.launch.py \
      use_sim_time:=True \
      map:=$HOME/tb3_map.yaml
    ```
    
    ```PowerShell
    # 用 nav2_bringup 原生啟動
    ros2 launch nav2_bringup bringup_launch.py \
      use_sim_time:=True \
      map:=$HOME/tb3_map.yaml \
      params_file:=$HOME/nav2_params.yaml
    ```
    

- SLAM Toolbox 版
    
    A) 邊建圖邊導航
    
    一行帶起 SLAM + Nav2
    
    ```PowerShell
    ros2 launch nav2_bringup bringup_launch.py \
      use_sim_time:=True \
      slam:=True \
      params_file:=$HOME/nav2_params.yaml
    ```
    
    B) 先建圖 → 存檔 → 之後導航
    
    B-1) 建圖與存檔
    
    ```PowerShell
    ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True
    # 建完圖後
    ros2 run nav2_map_server map_saver_cli -f ~/map
    ```
    
    B-2) 載入地圖，以「定位模式」導航
    
    ```PowerShell
    # 1) 啟動 SLAM Toolbox 的定位模式（不再修改地圖）
    ros2 launch slam_toolbox localization_launch.py \
      use_sim_time:=True \
      slam_params_file:=/PATH/TO/slam_toolbox_localization.yaml \
      map_file:=$HOME/tb3_map.yaml
    
    # 2) 啟動 Nav2
    ros2 launch nav2_bringup bringup_launch.py \
      use_sim_time:=True \
      params_file:=$HOME/nav2_params.yaml \
      map:=$HOME/tb3_map.yaml
    ```
    

```PowerShell
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=$HOME/turtlebot3_ws/src/turtlebot3/turtlebot3_navigation2/map/h_map.yaml
```

---

  

# URDF 、 MJCF

- `**mujoco**`：書皮。
    
    - 這是整個檔案的根節點（Root），就像是這本書的封面。
        
        - **功能**：告訴程式「這是一個 MuJoCo 模型檔案」。
        
        - **範例**：`<mujoco model="crazydog_urdf">` 代表這隻機器人的名字叫 crazydog。
        
    

- `**compiler**`：閱讀規則。
    
    - 這是寫給 MuJoCo 的「編譯器」看的設定，告訴它該如何解讀這份檔案。
        
        - **功能**：設定全域的單位或路徑。
        
        - **範例**：
            
            - `angle="radian"`：告訴系統這裡面的角度單位是「弧度」不是「度」。
            
            - `meshdir="../meshes/"`：告訴系統「如果要找模型檔 (.STL)，請去上一層的 meshes 資料夾找」。這非常重要，設錯了就會找不到檔案。
            
        
    

- `**default**`：偷懶用的樣板（設定一次，重複使用）。
    
    - 用來**「減少重複寫程式碼」**。可以把它想像成 Word 裡面的「樣式設定」。
        
        - **功能**：可以先定義好一套標準（例如：所有的輪子摩擦力都是 0.8），之後只要說「這是一個輪子」，它就會自動套用這些設定，不用每個輪子都重寫一遍。
        
        - **範例** (`crazydog` 裡面用很多)：
            
            - 它定義了一個 `<default class="thigh">`，裡面設定好了大腿關節的範圍和馬達出力。
            
            - 之後在建立大腿時，只要加上 `childclass="thigh"` 或類似引用，就會自動擁有這些屬性。
            
        
    

- `**asset**`：倉庫（放模型檔）。
    
    - 這裡是存放所有「素材」的地方。在把東西放進世界之前，要先在這裡註冊。
        
        - **功能**：列出所有會用到的 3D 模型網格 (Mesh)、貼圖 (Texture) 或材質 (Material)。
        
        - **範例**：
            
            - `<mesh name="base_link" file="base_link.STL"/>`。
            
            - 這句話的意思是：「我有個模型檔案叫 `base_link.STL`，我把它取名為 `base_link` 放在倉庫備用」。之後在世界裡要用時，就呼叫這個名字。
            
        
    

- `**worldbody**`：舞台（把倉庫的東西搬出來，組裝成機器人）。
    
    - 定義了**物理世界中實際存在的物體**。
        
        - **功能**：所有看得到的機器人、地板、燈光，全部都要寫在這裡面。這裡是「父子階層」結構的起點。
        
        - **結構**：
            
            - 通常第一層會有 `<light>` (燈光) 或 `<geom name="floor">` (地板)。
            
            - 接著就是機器人的 `<body name="base_link">`，然後一層一層往下長出零件。
            
        
    

- `**actuator**`：馬達。
    
    - 如果只有 `worldbody`，機器人只是個不會動的木偶。這裡定義了驅動關節的力量來源。
        
        - **功能**：將「關節 (Joint)」與「控制器」連結起來。
        
        - **範例** (`biped_wheel` 比較清楚)：
            
            - `<motor name="r_wheel" joint="R4" ctrlrange="-5 5"/>`。
            
            - 意思是：「建立一個叫 `r_wheel` 的馬達，去驅動 `R4` 這個關節，控制訊號範圍是 -5 到 5」。
            
        
    

- `**sensor**`：感測器。
    
    - 這裡定義機器人如何感知世界。
        
        - **功能**：模擬真實的感測器數據，如編碼器、IMU、相機等。
        
        - **範例** (`biped_wheel` 才有)：
            
            - `<jointpos name="right1_pos" joint="R1" />`：這是「關節角度感測器」，用來讀取 R1 關節現在轉了幾度。
            
            - `<accelerometer name="imu_acc" site="imu" />`：這是「加速度計」，安裝在 `imu` 這個標記點上。
            
        
    

  

- `**<body ...>**` **(剛體/部位)**：
    
    - 這代表機器人的一個「部位」，例如：軀幹、大腿、小腿。
    
    - MuJoCo 是**父子結構 (Hierarchy)**，就像大腿連在軀幹上，小腿連在大腿上。如果父物體移動，子物體也會跟著動。
    

- `**<joint ...>**` **(關節)**：
    
    - 這是連接兩個部位的樞紐。沒有 Joint，兩個部位就會黏死在一起。
    
    - Joint 定義了這個部位「怎麼動」（例如：旋轉軸向 `axis`、活動範圍 `range`）。
    

- `**<geom ...>**` **(外型/幾何)**：
    
    - Body 是概念上的「骨架」，Geom 才是你看得到的「肉」或「外殼」。
    
    - 它決定了物體的形狀（如 `.STL` 模型檔）、顏色、以及**碰撞體積**（會不會穿過別的東西）。
    

- `**<site ...>**` **(標記點)**：
    
    - 這是一個看不見的標記，通常用來安裝感測器（如 IMU）或當作攝影機的焦點。
    

  
`crazydog_urdf`

**🟪 軀幹 (Base Link)**

- 這是機器人的核心，也是飄浮在空中的基準點。

- 裡面裝了電池 (`battery`) 和慣性測量單元 (`site name="imu"`)。

- **⬇ 連接右腿 (Right Leg Chain)**：
    
    - **大腿 (R_thigh)**：透過 `R_hip2thigh` 關節連接軀幹（負責大腿擺動）。
        
        - **小腿 (R_calf)**：透過 `R_thigh2calf` 關節連接大腿（負責膝蓋彎曲）。
            
            - **輪子 (R_wheel)**：透過 `R_calf2wheel` 關節連接小腿（負責滾動）。
            
        
    

- **⬇ 連接左腿 (Left Leg Chain)**：
    
    - 結構與右腿完全對稱 (`L_thigh` -> `L_calf` -> `L_wheel`)。