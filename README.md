# Rosbags2 NodeJS wrapper

Simple CDR deserializer that can be used in NodeJS (CDR is the default serializer format used for Rosbags2). Deserialize Rosbag2 messages into objects/strings to be used in NodeJS.

Features:
- Deserialize Ros2 std_msgs::msg::String messages.
- Deserialize Ros2 sensor_msgs::msg::Image messages.
- Deserialize Ros2 sensor_msgs::msg::CompressedImage messages.
- Deserialize Ros2 sensor_msgs::msg::NavSatFix messages.
  - Outputs latitude, longitude and altitude
- Deserialize Ros2 sensor_msgs::msg::Imu messages.
  - Outputs quaternion x, y, z, w (geometry_msgs/Quaternion) part of the message.
- Base64 encodes deserialization results.

Future:
- Generalize message deserialization to easier add other message types
- Full output of message data
- Support arbitrary JSON objects results to be returned (either buffer or base64 encoded)


See the examples folder for usage. Basically what the approach would be is to read a SQLite3 DB from your Rosbag2 recording
and you pass the message type (from the metafile or the DB row) and pass this to the deserializer function. It will deserialize the binary
CDR formatted message payload, and pass pack a base64 encoded string with the message payload (see features for some limitations to some message types)

## Installation
First make sure to source your ROS2 environment. 
`. install/setup.bash`

If Rosbag2 is not installed as part of your base Ros2 environment, make sure you activate the Rosbag2 workspace as well.

Then run:

`yarn build`

You might need to change some paths in binding.gyp, 

## Usage

Make sure that your ROS2 environment is sourced before running the module, since some dependencies are dynamically linked.

See examples folder for an example on how to use the module.

The `sample.db3` is just a rosbag2 file containing:
 - one String message 
 - one Image message
 - one CompressedImage message
 - one NavSatFix message
 - one Imu message
 
 All for testing the deserialization of them and how its done.

`node examples/deserialize.js`
## Other

Please feel free to add a PR for improving the code, it's not ideal at the moment, since I'm a beginner C++ programmer at best. 



