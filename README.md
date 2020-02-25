# Kinesis Video Streams Producer Docker Builds

*Updated as of 25 Feb, 2020*

Docker builds are for two different deployment modes: (1) on AmazonLinux instances (on cloud), and (2) on Raspberry Pi or other ARM-architecture devices (on edge).

For each deployment mode, there are respective Dockerfiles with different default commands that would stream either (1) RTSP feed, or (2) webcam feed into KVS.

## How to run

For RTSP Streaming, the following variables are required: (1) `RTSP_STREAM_URL`, (2) `KVS_STREAM_NAME`, (3) `VIDEO_FORMAT`.

For Webcam Streaming, the following variables are required: (1) `DEVICE_LOCATION` (e.g. `/dev/video0`), (2) `KVS_STREAM_NAME`.

If you are running in AWS, the instance that is running on should have the IAM role that allows for pushing into KVS. If not, and only for testing purposes, you should have the following variables: (1) `AWS_DEFAULT_REGION`, (2) `AWS_ACCESS_KEY_ID`, (3) `AWS_SECRET_ACCESS_KEY`.

Once you have those variables, you can fill them in using the relevant docker-compose-examples YAML file:
1. `docker-compose-examples/amazonlinux_rtsp.yml` - config for AmazonLinux RTSP 
2. `docker-compose-examples/amazonlinux_webcam.yml` - config for AmazonLinux Webcam
3. `docker-compose-examples/raspbian_rtsp.yml` - config for Raspbian RTSP
4. `docker-compose-examples/raspbian_webcam.yml` - config for AmazonLinux Webcam

```
git clone <this library>
cd kvs-producer
docker build . -t kvs-producer:amazonlinux_rtsp -f amazonlinux/Dockerfile_rtsp
docker-compose -f docker-compose-examples/amazonlinux_rtsp.yml up
```