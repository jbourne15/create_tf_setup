#include <ros/ros.h>
#include <tf/transform_listener.h>
#include <iostream>
#include <geometry_msgs/Twist.h>

int main(int argc, char** argv){
  ros::init(argc, argv, "create_tf_listener");
  ros::NodeHandle node;
  tf::TransformListener listener;

  ros::Publisher create_vel = node.advertise<geometry_msgs::Twist>("/cmd_vel", 1);

  ros::Rate rate(10.0);
  while (node.ok()){
    tf::StampedTransform transform;
    try{
      ros::Time now = ros::Time::now();
      listener.waitForTransform("/world", "/create0",
				now, ros::Duration(1.0));
      listener.lookupTransform("/world", "/create0",
			       now, transform);
    }
    catch (tf::TransformException ex){
      ROS_ERROR("%s",ex.what());
      ros::Duration(1.0).sleep();
    }

    geometry_msgs::Twist vel_msg;
    vel_msg.angular.z = 0.0;
      //4.0 * atan2(transform.getOrigin().y(),transform.getOrigin().x());
    vel_msg.linear.x = .25;
      //0.5 * sqrt(pow(transform.getOrigin().x(), 2) + pow(transform.getOrigin().y(), 2));
    create_vel.publish(vel_msg);

    /*
    ROS_INFO_STREAM("x");
    ROS_INFO_STREAM(transform.getOrigin().x());
    ROS_INFO_STREAM("y");
    ROS_INFO_STREAM(transform.getOrigin().y());
    ROS_INFO_STREAM("z");
    ROS_INFO_STREAM(transform.getOrigin().z());
    */
    rate.sleep();
  }
  return 0;
};
