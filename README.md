# doorbell
Open source iot video doorbell with Chromecast support

This is an open source project to avoid big-tech home securitry products which may include audio and video of the home. Recent stories have highlighted the problems with only a handfull of monoliths looking after such personal information, whether it is [employees looking at our feeds](https://www.vice.com/en_us/article/y3mdvk/ring-fired-employees-abusing-video-data), [being hacked](https://www.wired.com/story/nest-cameras-pew-die-pie-north-korea-passwords/) or [flawed](https://www.theverge.com/2020/2/25/21152534/nest-cameras-outage-google-security) and the [risks turning our communities into CCTV police state](https://www.washingtonpost.com/technology/2019/08/28/doorbell-camera-firm-ring-has-partnered-with-police-forces-extending-surveillance-reach/?arc404=true), all makes me uncomfortable. Further reading below.   

This is not intended to be an intercom security system.   

## Notes

RPi to recieve, transcode and broadcast video
Something like
`raspivid -fps 25 -o - -t 0 -w 600 -h 400 | cvlc stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/}' :demux=h264`

`raspivid -fps 25 -o - -t 0 -w 600 -h 400` by setting `-o` (output) to `-`, this buffers the output to stdout
`cvlc stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/}' :demux=h264`, then pipe the stdout to vlc stdin and broadcast

## Scenarios

When a doorbell `event` is received, a number of `reactions` can be handled to notifify a service.

## 1 - Doorbell
The doorbell is pressed creating an `Doorbell.start` and `Doorbell.end` events.
This causes 3 reactions
- A chromecast event is sent to the HomeHub to connect a live video from the RPi.
- A photo is sent to an s3 bucket so that it can be viewed on a users device and a sms sent with the url for a image preview on the users phone.



## Events

### Camera.on('motion')
### Mic.on('sound');
### Doorbell.on('start')
### Doorbell.on('end')
### DoorSensor.on('open')
### DoorSensor.on('closed')

## Reactions

### Webhook
### SNS or other queue system
### Stream from camera to Chromecast
### Send photo from camera to service
### Send clip from camera to service

## Hardware

RaspberryPi   
Camera Module    
Mic    
Magnetic sensor 
Doorbell   
Chromecast/ NestHub.  

## Read more
https://www.nytimes.com/2020/02/19/technology/personaltech/ring-doorbell-camera-spying.html.  

### Employees
https://theintercept.com/2019/01/10/amazon-ring-security-camera/.  
https://www.vice.com/en_us/article/y3mdvk/ring-fired-employees-abusing-video-data.  

### Law enforcment
https://www.washingtonpost.com/news/the-switch/wp/2018/05/22/amazon-is-selling-facial-recognition-to-law-enforcement-for-a-fistful-of-dollars/.  
https://www.washingtonpost.com/technology/2019/08/28/doorbell-camera-firm-ring-has-partnered-with-police-forces-extending-surveillance-reach.  
https://gizmodo.com/ring-s-hidden-data-let-us-map-amazons-sprawling-home-su-1840312279.  

### Security
https://www.vice.com/en_uk/article/epg4xm/we-tested-rings-security-its-awful   
https://www.wired.com/story/nest-cameras-pew-die-pie-north-korea-passwords/   
https://www.theverge.com/2020/2/25/21152534/nest-cameras-outage-google-security    
https://www.zdnet.com/article/vulnerabilities-in-google-nest-cam-iq-can-be-used-to-hijack-your-camera/   
