# syntax=docker/dockerfile:1
FROM tiryoh/ros-desktop-vnc:noetic-amd64
LABEL maintainer="hafiidz"

# setup Python dependency
RUN echo "export PATH=Library/Frameworks/Python.framework/Versions/3.8/bin:$PATH" >> ~/.bashrc
RUN apt-get update && apt-get install -y python3-pip
RUN apt install python-is-python3
RUN pip install pandas==1.5.*
RUN pip install scipy==1.10.*

# setup catkin_ws
ADD "https://api.github.com/repos/Hafiidz/swarm/commits?per_page=1" latest_commit
RUN git clone https://github.com/Hafiidz/swarm.git ~/catkin_ws/src/swarm
RUN cd ~/catkin_ws
RUN /bin/bash -c '. /opt/ros/noetic/setup.bash; cd ~/catkin_ws; catkin_make'
RUN echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
RUN . ~/.bashrc

# launch application via roslaunch
CMD cd ~/catkin_ws/src/swarm && git pull && roslaunch swarm central.launch