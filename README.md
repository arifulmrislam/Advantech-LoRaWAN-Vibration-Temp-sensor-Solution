# Advantech-LoRaWAN-Vibration-Temp-sensor-Solution
WISE-2410 is a LoRaWAN wireless conditional monitoring sensor integrated with ARM Cortex-M4 Processor, LoRa transceiver, 3-axis accelerometer and temperature sensor. 
Battery life cycle is 2years with IP66 enclosure.

Brief Solution Step by Step:

If we connect WISE-2410 with our computer and the Advantech WISE Studio shows it cannot recognize the com port, then please install the driver from the following link:

https://www.advantech.com/support/details/driver?id=1-13U9QTV

Step1.

Enter the WISE-6610 gateway. Default IP: 192.168.1.1

  Account: root
  
  Password: root
  
<img src= "Gateway WISE-6610.png" width=800>

Step2.

Go to user mode.

Step3.

Click LoRaWAN Gateway to enter the setting page. Make sure all of these parameters are matching with the RF module setting on WISE-2410 Sensor.
Or click on quick setup for default setting.

Step4.

A new tab will pop up after click on network server > enable > network > server (http).

  Account: root
  
  Password: root

Step5.

Create an end node device according the OTAA or ABP method.

   I f select commissioned ””, which means the node will use OTAA mode for connecting with a gateway.
  
   I f select active nodes ””, which means the node will use ABP mode for connecting with a gateway.

Click on create in devices in activated because this project is using ABP mode for connection.

A.DevAddr: the device address of an end node.
   Copy pate from WISE-2410 RF module tab.
  
B.Profile: select the model name of the WISE-6610 which used for Network Server role.
   In this demo, a EUR version is used to connect with WISE-2410NA version.
  
C.App Arguments: the I/O board of the end node.
   In this project, a WISE-2410 is used.
  
D.NwkSKey: the network service key address of an end node.
   Copy pate from WISE-2410 RF module tab.
  
E.AppSK ey: the application service key of an end node.
   Copy pate from WISE-2410 RF module tab.
  
F.Click on save to finish the setting.

Select LoRaWAN for RF operation mode setting on WISE-2410.

<img src= "Sensor WISE-2410.png" width=800>

Step6.

Create a network server gateway. Copy paste the MAC address from LoRaWAN radio > LoRaWAN Gateway Identifier. Then click on submit.

Connection results:

1. Click application server > status. Here we will see the end nodes if packets are received by gateway from an end node.

2. The gateway will help to pre parsing the data payload if the app arguments input correctly.

3. Received frames page shows the received results. The FCnt shows the frame sequence. If this sequence is in continuously , means some of the packets were lost.

Continue with setting up:

Step7. (optional)

Connect WISE-6610 through WinSCP (FileZilla cannot connect with it). Modify the “setting.js” file of WISE 6610. So, we can insert image into dashboard. 
Put the “title.jpg” file under folder “opt/nodered /node red/” of WISE-6610. Need to reboot Node-Red service if modify the setting.js file. If we don't
want an image, we can simply delete this node. Add a line httpStatic: '/opt/nodered/node red/',

Step8.

Enable the Node-Red function on WISE-6610. Go to Customization / User Modules / Node Red webpage and enable automatic start function with the port number we prefer. 
Default port number 1880 is recommended.

Step9.

Open a new tab on a browser. Type in the IP address of the WISE-6610 and port number of the Node Red.

Step11.

Modify all of the device MAC addresses in WISE-2410 UpLink node, and Device function into the MAC of ours. Then click on deploy,

<img src= "Node-red flow.png" width=1200>

Click dashboard / open. There will be the dashboard created by the program copy pasted from the notepad.

<img src= "Dashboard.png" width=1000>

## Example

### Here is an example you can import demonstrating many of these formats and capabilities

# [Node-Red flow](Node-red flow.json)

[{"id":"767cefce.350ad","type":"ui_template","z":"99ff3a85.459e88","group":"df4ee2b8.4e152","name":"","order":0,"width":"23","height":"2","format":"<img src=\"/title.jpg\"/> ","storeOutMessages":false,"fwdInMessages":false,"x":195,"y":82.00000095367432,"wires":[[]]},{"id":"ab73b4d0.9025e8","type":"ui_template","z":"99ff3a85.459e88","group":"38fb1afd.32f896","name":"table for Device","order":2,"width":"10","height":"4","format":"<style>\n    th{\n      border-bottom: 3px solid white;\n    }\n    caption, th, td {\n      padding: 5px;\n      text-align: left;    \n    }\n</style>\n<table style=\"width:100%\">\n    <tr>\n    <!--    <th>Events</th> -->\n        <th>Device<br>address</th>\n        <th>Power<br>source</th>\n        <th>Battery<br>voltage (V)</th> \n        <th colspan=\"2\">Timestamp</th>\n    </tr>\n    <tr>\n    <!--    <td>{{msg.payload[0]}}</td>-->\n        <td>{{msg.payload[1]}}</td>\n        <td>{{msg.payload[2]}}</td>\n        <td>{{msg.payload[3]}}</td>\n            <td colspan=\"2\">{{msg.payload[7]}}<br>\n            {{msg.payload[8]}}</td> \n     </tr>\n     <tr>\n        <th>Fcnt</th>\n        <th>U/L SNR</th>\n        <th>U/L RSSI</th>\n        <tr>\n        <td>{{msg.payload[4]}}</td>\n        <td>{{msg.payload[5]}}</td>\n        <td>{{msg.payload[6]}}</td> \n        </tr>\n     </tr>\n</table>","storeOutMessages":true,"fwdInMessages":true,"x":954.0000076293945,"y":134.00000095367432,"wires":[[]]},{"id":"153aa170.0406df","type":"mqtt in","z":"99ff3a85.459e88","name":"WISE-2410_UpLink","topic":"uplink/#","qos":"2","broker":"a79e3eb.160c7c","x":222,"y":136.00000190734863,"wires":[["59e0b161.add16"]]},{"id":"35d09517.fdee7a","type":"mqtt in","z":"99ff3a85.459e88","name":"WISE-2410","topic":"Advantech/#","qos":"0","broker":"a79e3eb.160c7c","x":203,"y":195.00000476837158,"wires":[["dcb389f8.d6a868"]]},{"id":"dcb389f8.d6a868","type":"json","z":"99ff3a85.459e88","name":"","x":440.00000381469727,"y":196.0000057220459,"wires":[["36311167.8ea56e","66b2ba4b.c35be4","b9c83a74.f3b578","275c5a37.76a356","49c9b27e.ac0c7c"]]},{"id":"59e0b161.add16","type":"json","z":"99ff3a85.459e88","name":"","x":443,"y":137.00000190734863,"wires":[["275c5a37.76a356"]]},{"id":"36311167.8ea56e","type":"function","z":"99ff3a85.459e88","name":"TempHumi","func":"var TempHumi = [2];\ntempEvents = msg.payload.TempHumi.Event\nTempHumi[1] = msg.payload.TempHumi.SenVal/1000;\ntempRange = msg.payload.TempHumi.Range;\n\nswitch (tempEvents){\n    case 0:\n        TempHumi[0] = (\"Status normal\");\n        break;\n    case 1:\n        TempHumi[0] = (\"High alarm!\");\n        break;\n    default:\n        TempHumi[0] = (\"Reading error!\");\n}\n\nmsg.color = ((TempHumi[0]===\"Status normal\")? \"White\" : \"Red\");\n\nswitch (tempRange){\n    case 0:\n        tempRange = (\" \\'C\");\n        break;\n    default:\n        tempRange = (\"\\nRange parsing error!\");\n}\n\nTempHumi[1] = TempHumi[1] + tempRange;\nmsg.payload = TempHumi;\nreturn msg;\n","outputs":"1","noerr":0,"x":625.0000076293945,"y":337.0000057220459,"wires":[["aee2ef2.64efa1","1049ee8a.48c541","89b6e936.af0ff8"]]},{"id":"fc30ff27.c6a08","type":"ui_template","z":"99ff3a85.459e88","group":"7dc459ba.028e38","name":"table for Accelerometer","order":0,"width":"10","height":"4","format":"<table style=\"width:100%\">\n  <tr>\n    <th></th>\n    <th>Sensor Event</th>\n    <th>Velocity RMS (mm/s)</th> \n    <th>Acceloratioin RMS (g)</th> \n    <th>Acceloratioin Peak (g)</th> \n  </tr>\n  <tr>\n    <td>X-Axis</td>\n    <td>{{msg.payload[0]}}</td>\n    <td>{{msg.payload[1]}}</td> \n    <td>{{msg.payload[2]}}</td> \n    <td>{{msg.payload[3]}}</td> \n  </tr>\n  <tr>\n    <td>Y-Axis</td>\n    <td>{{msg.payload[4]}}</td>\n    <td>{{msg.payload[5]}}</td> \n    <td>{{msg.payload[6]}}</td> \n    <td>{{msg.payload[7]}}</td> \n  </tr>\n  <tr>\n    <td>Z-Axis</td>\n    <td>{{msg.payload[8]}}</td>\n    <td>{{msg.payload[9]}}</td> \n    <td>{{msg.payload[10]}}</td> \n    <td>{{msg.payload[11]}}</td> \n  </tr>\n</table>","storeOutMessages":true,"fwdInMessages":true,"x":853.0000076293945,"y":179.00000095367432,"wires":[[]]},{"id":"49c9b27e.ac0c7c","type":"function","z":"99ff3a85.459e88","name":"Accelerometer","func":"var aryAccel=[12];\nvar aryAccelColor=[3];\n\n//X-axis\naryAccel [0] = msg.payload.Accelerometer['X-Axis'].SenEvent;\n\nswitch (aryAccel [0]){\n    case 0:\n        aryAccel[0] = (\"Status normal\");\n        break;\n    case 1:\n        aryAccel[0] = (\"High alarm!!!\");\n        break;\n    default:\n        aryAccel[0] = (\"Reading error!!!\");\n}\n\naryAccelColor[0] = ((aryAccel[0]===\"Status normal\")? \"White\" : \"Red\");\naryAccel [1] = msg.payload.Accelerometer['X-Axis'].OAVelocity/100;\naryAccel [2] = msg.payload.Accelerometer['X-Axis'].Peakmg/1000;\naryAccel [3] = msg.payload.Accelerometer['X-Axis'].RMSmg/1000;\n\n//Y-axis\naryAccel [4] = msg.payload.Accelerometer['Y-Axis'].SenEvent;\nswitch (aryAccel [4]){\n    case 0:\n        aryAccel[4] = (\"Status normal\");\n        break;\n    case 1:\n        aryAccel[4] = (\"High alarm!!!\");\n        break;\n    default:\n        aryAccel[4] = (\"Reading error!!!\");\n}\n\naryAccelColor[1] = ((aryAccel[4]===\"Status normal\")? \"White\" : \"Red\");\naryAccel [5] = msg.payload.Accelerometer['Y-Axis'].OAVelocity/100;\naryAccel [6] = msg.payload.Accelerometer['Y-Axis'].Peakmg/1000;\naryAccel [7] = msg.payload.Accelerometer['Y-Axis'].RMSmg/1000;\n\n//Z-axis\naryAccel [8] = msg.payload.Accelerometer['Z-Axis'].SenEvent;\nswitch (aryAccel [8]){\n    case 0:\n        aryAccel[8] = (\"Status normal\");\n        break;\n    case 1:\n        aryAccel[8] = (\"High alarm!!!\");\n        break;\n    default:\n        aryAccel[8] = (\"Reading error!!!\");\n}\n\naryAccelColor[2] = ((aryAccel[8]===\"Status normal\")? \"White\" : \"Red\");\naryAccel [9] = msg.payload.Accelerometer['Z-Axis'].OAVelocity/100;\naryAccel [10] = msg.payload.Accelerometer['Z-Axis'].Peakmg/1000;\naryAccel [11] = msg.payload.Accelerometer['Z-Axis'].RMSmg/1000;\n\nmsg.payload = aryAccel;\nmsg.color = aryAccelColor;\nreturn msg;","outputs":1,"noerr":0,"x":632.0000076293945,"y":216.00000190734863,"wires":[["fc30ff27.c6a08","a709d0e5.3041b","9113901c.9c237","ccf023f6.08002"]]},{"id":"aee2ef2.64efa1","type":"ui_template","z":"99ff3a85.459e88","group":"d0ad8b2b.552848","name":"table for Temparature","order":0,"width":"7","height":"2","format":"<table style=\"width:100%\">\n    <tr>\n        <th>Event</th>\n        <th>Temparature</th>\n    </tr>\n    <tr>\n        <td>{{msg.payload[0]}}</td>\n        <td>{{msg.payload[1]}}  <i class=\"fa fa-thermometer-three-quarters fa-2x\" aria-hidden=\"true\"></i></td>\n    </tr>\n</table>\n","storeOutMessages":true,"fwdInMessages":true,"x":835.0000038146973,"y":284.0000057220459,"wires":[[]]},{"id":"66b2ba4b.c35be4","type":"function","z":"99ff3a85.459e88","name":"OAVelocityChart","func":"var msg1 = {};\nvar msg2 = {};\nvar msg3 = {};\n\nmsg1.payload = msg.payload.Accelerometer['X-Axis'].OAVelocity/100;\nmsg1.topic = 'X-Axis';\n\nmsg2.payload = msg.payload.Accelerometer['Y-Axis'].OAVelocity/100;\nmsg2.topic = 'Y-Axis';\n\nmsg3.payload = msg.payload.Accelerometer['Z-Axis'].OAVelocity/100;\nmsg3.topic = 'Z-Axis';\nreturn [msg1, msg2, msg3];","outputs":"3","noerr":0,"x":488.00000762939453,"y":976.9999289512634,"wires":[["e52c7f12.fc8eb","902013fd.23b45","b9cab876.0e07a8","9f215fe4.b1ad2","f6d5e1a0.8554e"],["e52c7f12.fc8eb"],["e52c7f12.fc8eb"]]},{"id":"e52c7f12.fc8eb","type":"ui_chart","z":"99ff3a85.459e88","name":"","group":"8efeb247.9f6df","order":0,"width":"10","height":"4","label":"Velocity RMS (Root-Mean-Squar)","chartType":"line","legend":"true","xformat":"HH:mm","interpolate":"linear","nodata":"","ymin":"","ymax":"","removeOlder":"1","removeOlderPoints":"1000","removeOlderUnit":"3600","cutout":0,"colors":["#ffc107","#e80000","#9c27b0","#2ca02c","#98df8a","#d62728","#ff9896","#9467bd","#c5b0d5"],"x":749.0000038146973,"y":877.0000200271606,"wires":[[],[]]},{"id":"b9c83a74.f3b578","type":"function","z":"99ff3a85.459e88","name":"TempHumiChart","func":"msg.payload = msg.payload.TempHumi.SenVal/1000;\n\nreturn msg;","outputs":1,"noerr":0,"x":632.0000076293945,"y":438.00001335144043,"wires":[["85da81b2.f7fa9","bcef5420.bb3398","57eaa699.e81418"]]},{"id":"85da81b2.f7fa9","type":"ui_chart","z":"99ff3a85.459e88","name":"","group":"ca8a3d6d.ef27","order":0,"width":"10","height":"4","label":"Temperature","chartType":"line","legend":"false","xformat":"HH:mm","interpolate":"linear","nodata":"","ymin":"","ymax":"","removeOlder":"1","removeOlderPoints":"1000","removeOlderUnit":"3600","cutout":0,"colors":["#4caf50","#aec7e8","#ff7f0e","#2ca02c","#98df8a","#d62728","#ff9896","#9467bd","#c5b0d5"],"x":799.0000076293945,"y":415.0000066757202,"wires":[[],[]]},{"id":"275c5a37.76a356","type":"join","z":"99ff3a85.459e88","name":"","mode":"custom","build":"object","property":"payload","propertyType":"msg","key":"topic","joiner":"\\n","timeout":"","count":"2","x":628.0000038146973,"y":138.00000095367432,"wires":[["8217c159.7c9ff"]]},{"id":"88ac455f.3d2b48","type":"ui_text","z":"99ff3a85.459e88","group":"d36c051a.aabae8","order":0,"width":"4","height":"1","name":"","label":"","format":"<font color= \"{{msg.color}}\">{{msg.payload}}</font>","layout":"col-center","x":1103.0000076293945,"y":1156.9999656677246,"wires":[]},{"id":"18052121.5f88df","type":"ui_text","z":"99ff3a85.459e88","group":"5034141b.fce75c","order":0,"width":"4","height":"1","name":"","label":"","format":"<font color= \"{{msg.color}}\">{{msg.payload}}</font>","layout":"col-center","x":1131.0000076293945,"y":1544.9999837875366,"wires":[]},{"id":"902013fd.23b45","type":"debug","z":"99ff3a85.459e88","name":"","active":true,"console":"false","complete":"payload","x":771.1666717529297,"y":994.6667957305908,"wires":[]},{"id":"c6046a40.ebc688","type":"trigger","z":"99ff3a85.459e88","op1":"1","op2":"0","op1type":"str","op2type":"str","duration":"1","extend":false,"units":"s","reset":"","name":"","x":732.0000076293945,"y":1105.5555458068848,"wires":[["ed463776.d78598","f74ae6e1.cab958"]]},{"id":"ed463776.d78598","type":"function","z":"99ff3a85.459e88","name":"Logic","func":"if (msg.payload == \"off\")\n\tcontext.state = 0;\nif (msg.payload == \"error\")\n\tcontext.state = 0;\nif (msg.payload == \"on\")\n\tcontext.state = 1;\n\nif (context.state == 1)\n{\n\tif (msg.payload == 0)\n\t\treturn msg;\n\telse\n\t\treturn;\n}\nelse\n\treturn;","outputs":1,"noerr":0,"x":731.0000076293945,"y":1164.5555458068848,"wires":[["c37165d0.a2e988"]]},{"id":"c37165d0.a2e988","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"1","timeoutUnits":"seconds","rate":"1","nbRateUnits":"","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":871.0000076293945,"y":1164.5555992126465,"wires":[["c6046a40.ebc688"]]},{"id":"44dac2d6.9633ec","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":725.1666717529297,"y":1061.5555906295776,"wires":[["bf82d418.65d0d8"]]},{"id":"f74ae6e1.cab958","type":"function","z":"99ff3a85.459e88","name":"HIGH ALARM","func":"payload = msg.payload;\nvar name = \"HIGH ALARM\";\nvar color1 = \"red\";\nvar color2 = \"black\";\n\nvar count;\n\nif(payload===\"1\"){\n    msg.payload = name;\n    msg.color = color2;\n    return msg;\n}else{\n    msg.payload = name;\n    msg.color = color1;\n    return msg;\n}","outputs":1,"noerr":0,"x":926.166675567627,"y":1107.2221493721008,"wires":[["88ac455f.3d2b48"]]},{"id":"bf82d418.65d0d8","type":"function","z":"99ff3a85.459e88","name":"NORMAL","func":"msg.payload = \"NORMAL\";\nmsg.color = \"green\";\nreturn msg;\n\n\n","outputs":1,"noerr":0,"x":909.0000076293945,"y":1061.555591583252,"wires":[["88ac455f.3d2b48"]]},{"id":"ed6e8b4b.5fcd68","type":"function","z":"99ff3a85.459e88","name":"READING ERROR","func":"msg.payload = \"ERROR\";\nmsg.color = \"orange\";\nreturn msg;\n","outputs":1,"noerr":0,"x":909.0000076293945,"y":1211.4444522857666,"wires":[["88ac455f.3d2b48"]]},{"id":"380c94d6.89b8fc","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":730.0000038146973,"y":1208.4444522857666,"wires":[["ed6e8b4b.5fcd68"]]},{"id":"a709d0e5.3041b","type":"function","z":"99ff3a85.459e88","name":"X-Axis","func":"var payload = msg.payload;\n\n\n\nif(payload[0] === \"Status normal\")\n{\n    msg.payload = \"off\";\n    return msg; \n}\nif(payload[0] === \"High alarm!!!\")\n{\n    msg.payload = \"on\";\n    return msg; \n}\nif(payload[0] === \"Reading error!!!\")\n{\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":1071.166675567627,"y":199.88879585266113,"wires":[[]]},{"id":"9113901c.9c237","type":"function","z":"99ff3a85.459e88","name":"Y-Axis","func":"var payload = msg.payload;\nif(payload[4] === \"Status normal\")\n{\n    msg.payload = \"off\";\n    return msg; \n}\nif(payload[4] === \"High alarm!!!\")\n{\n    msg.payload = \"on\";\n    return msg; \n}\nif(payload[4] === \"Reading error!!!\")\n{\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":1074.0000076293945,"y":238.55555725097656,"wires":[[]]},{"id":"ccf023f6.08002","type":"function","z":"99ff3a85.459e88","name":"Z-Axis","func":"var payload = msg.payload;\n\nif(payload[8] === \"Status normal\")\n{\n    msg.payload = \"off\";\n    return msg; \n}\nif(payload[8] === \"High alarm!!!\")\n{\n    msg.payload = \"on\";\n    return msg; \n}\nif(payload[8] === \"Reading error!!!\")\n{\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":1076.0000076293945,"y":277.55555725097656,"wires":[[]]},{"id":"474df036.158c4","type":"ui_text","z":"99ff3a85.459e88","group":"d03f58be.bb93c8","order":0,"width":"4","height":"1","name":"","label":"","format":" <font color= \"{{msg.color}}\">{{msg.payload}}</font>","layout":"col-center","x":1123.0000076293945,"y":1356.9999828338623,"wires":[]},{"id":"e0227ed7.5faf3","type":"switch","z":"99ff3a85.459e88","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"},{"t":"eq","v":"error","vt":"str"}],"checkall":"true","outputs":3,"x":542.1666679382324,"y":1136.2222576141357,"wires":[["c6046a40.ebc688","ed463776.d78598"],["ed463776.d78598","44dac2d6.9633ec"],["ed463776.d78598","380c94d6.89b8fc"]]},{"id":"af06cc11.231c2","type":"trigger","z":"99ff3a85.459e88","op1":"1","op2":"0","op1type":"str","op2type":"str","duration":"1","extend":false,"units":"s","reset":"","name":"","x":744.8333892822266,"y":1315.8888244628906,"wires":[["2f396ac1.0cc606","cbbf70dc.d46b3"]]},{"id":"2f396ac1.0cc606","type":"function","z":"99ff3a85.459e88","name":"Logic","func":"if (msg.payload == \"off\")\n\tcontext.state = 0;\nif (msg.payload == \"error\")\n\tcontext.state = 0;\nif (msg.payload == \"on\")\n\tcontext.state = 1;\n\nif (context.state == 1)\n{\n\tif (msg.payload == 0)\n\t\treturn msg;\n\telse\n\t\treturn;\n}\nelse\n\treturn;","outputs":1,"noerr":0,"x":743.8333892822266,"y":1374.8888244628906,"wires":[["b54f946b.2b95b8"]]},{"id":"b54f946b.2b95b8","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"1","timeoutUnits":"seconds","rate":"1","nbRateUnits":"","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":883.8333892822266,"y":1374.8888778686523,"wires":[["af06cc11.231c2"]]},{"id":"10a0a316.9b80ad","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":738.0000534057617,"y":1271.8888692855835,"wires":[["97d3c89a.011a08"]]},{"id":"cbbf70dc.d46b3","type":"function","z":"99ff3a85.459e88","name":"HIGH ALARM","func":"payload = msg.payload;\nvar name = \"HIGH ALARM\";\nvar color1 = \"red\";\nvar color2 = \"black\";\n\nvar count;\n\nif(payload===\"1\"){\n    msg.payload = name;\n    msg.color = color2;\n    return msg;\n}else{\n    msg.payload = name;\n    msg.color = color1;\n    return msg;\n}","outputs":1,"noerr":0,"x":939.000057220459,"y":1317.5554280281067,"wires":[["474df036.158c4"]]},{"id":"97d3c89a.011a08","type":"function","z":"99ff3a85.459e88","name":"NORMAL","func":"msg.payload = \"NORMAL\";\nmsg.color = \"green\";\nreturn msg;\n\n\n","outputs":1,"noerr":0,"x":921.8333892822266,"y":1271.8888702392578,"wires":[["474df036.158c4"]]},{"id":"f0bc5959.b0e1b8","type":"function","z":"99ff3a85.459e88","name":"READING ERROR","func":"msg.payload = \"ERROR\";\nmsg.color = \"orange\";\nreturn msg;\n","outputs":1,"noerr":0,"x":921.8333892822266,"y":1421.7777309417725,"wires":[["474df036.158c4"]]},{"id":"5ebf4274.43012c","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":742.8333854675293,"y":1418.7777309417725,"wires":[["f0bc5959.b0e1b8"]]},{"id":"8daf8447.cbe168","type":"switch","z":"99ff3a85.459e88","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"},{"t":"eq","v":"error","vt":"str"}],"checkall":"true","outputs":3,"x":548,"y":1346.5555381774902,"wires":[["af06cc11.231c2","2f396ac1.0cc606"],["2f396ac1.0cc606","10a0a316.9b80ad"],["2f396ac1.0cc606","5ebf4274.43012c"]]},{"id":"819390a5.84eae","type":"trigger","z":"99ff3a85.459e88","op1":"1","op2":"0","op1type":"str","op2type":"str","duration":"1","extend":false,"units":"s","reset":"","name":"","x":757.0000076293945,"y":1516.1111574172974,"wires":[["4ef0e086.4af3d","cd28d1fa.59e21"]]},{"id":"4ef0e086.4af3d","type":"function","z":"99ff3a85.459e88","name":"Logic","func":"if (msg.payload == \"off\")\n\tcontext.state = 0;\nif (msg.payload == \"error\")\n\tcontext.state = 0;\nif (msg.payload == \"on\")\n\tcontext.state = 1;\n\nif (context.state == 1)\n{\n\tif (msg.payload == 0)\n\t\treturn msg;\n\telse\n\t\treturn;\n}\nelse\n\treturn;","outputs":1,"noerr":0,"x":756.0000076293945,"y":1575.1111574172974,"wires":[["e2d6265b.878d88"]]},{"id":"e2d6265b.878d88","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"1","timeoutUnits":"seconds","rate":"1","nbRateUnits":"","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":896.0000076293945,"y":1575.111210823059,"wires":[["819390a5.84eae"]]},{"id":"d2ed6afd.c506a8","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":750.1666717529297,"y":1472.1112022399902,"wires":[["11caa41d.0c56ec"]]},{"id":"cd28d1fa.59e21","type":"function","z":"99ff3a85.459e88","name":"HIGH ALARM","func":"payload = msg.payload;\nvar name = \"HIGH ALARM\";\nvar color1 = \"red\";\nvar color2 = \"black\";\n\nvar count;\n\nif(payload===\"1\"){\n    msg.payload = name;\n    msg.color = color2;\n    return msg;\n}else{\n    msg.payload = name;\n    msg.color = color1;\n    return msg;\n}","outputs":1,"noerr":0,"x":951.166675567627,"y":1517.7777609825134,"wires":[["18052121.5f88df"]]},{"id":"11caa41d.0c56ec","type":"function","z":"99ff3a85.459e88","name":"NORMAL","func":"msg.payload = \"NORMAL\";\nmsg.color = \"green\";\nreturn msg;\n\n\n","outputs":1,"noerr":0,"x":934.0000076293945,"y":1472.1112031936646,"wires":[["18052121.5f88df"]]},{"id":"e3b33e7e.be989","type":"function","z":"99ff3a85.459e88","name":"READING ERROR","func":"msg.payload = \"ERROR\";\nmsg.color = \"orange\";\nreturn msg;\n","outputs":1,"noerr":0,"x":934.0000076293945,"y":1622.0000638961792,"wires":[["18052121.5f88df"]]},{"id":"e10ce827.090998","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":755.0000038146973,"y":1619.0000638961792,"wires":[["e3b33e7e.be989"]]},{"id":"b5e9ab6e.f70ef8","type":"switch","z":"99ff3a85.459e88","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"},{"t":"eq","v":"error","vt":"str"}],"checkall":"true","outputs":3,"x":553.1666679382324,"y":1549.7777614593506,"wires":[["819390a5.84eae","4ef0e086.4af3d"],["4ef0e086.4af3d","d2ed6afd.c506a8"],["4ef0e086.4af3d","e10ce827.090998"]]},{"id":"1049ee8a.48c541","type":"debug","z":"99ff3a85.459e88","name":"","active":true,"console":"false","complete":"payload","x":813.1666717529297,"y":361.00003242492676,"wires":[]},{"id":"4e8f9dd7.108624","type":"trigger","z":"99ff3a85.459e88","op1":"1","op2":"0","op1type":"str","op2type":"str","duration":"1","extend":false,"units":"s","reset":"","name":"","x":738.8333396911621,"y":626.9999933242798,"wires":[["d8aa290d.004018","a5c3487b.fea188"]]},{"id":"d8aa290d.004018","type":"function","z":"99ff3a85.459e88","name":"Logic","func":"if (msg.payload == \"off\")\n\tcontext.state = 0;\nif (msg.payload == \"error\")\n\tcontext.state = 0;\nif (msg.payload == \"on\")\n\tcontext.state = 1;\n\nif (context.state == 1)\n{\n\tif (msg.payload == 0)\n\t\treturn msg;\n\telse\n\t\treturn;\n}\nelse\n\treturn;","outputs":1,"noerr":0,"x":737.8333396911621,"y":685.9999933242798,"wires":[["d0e07a8d.ba2a68"]]},{"id":"d0e07a8d.ba2a68","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"1","timeoutUnits":"seconds","rate":"1","nbRateUnits":"","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":877.8333396911621,"y":686.0000467300415,"wires":[["4e8f9dd7.108624"]]},{"id":"48f14c82.2d44d4","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":732.0000038146973,"y":583.0000381469727,"wires":[["a2c660a0.455f4"]]},{"id":"a5c3487b.fea188","type":"function","z":"99ff3a85.459e88","name":"HIGH ALARM","func":"payload = msg.payload;\nvar name = \"HIGH ALARM\";\nvar color1 = \"red\";\nvar color2 = \"black\";\n\nvar count;\n\nif(payload===\"1\"){\n    msg.payload = name;\n    msg.color = color2;\n    return msg;\n}else{\n    msg.payload = name;\n    msg.color = color1;\n    return msg;\n}","outputs":1,"noerr":0,"x":933.0000076293945,"y":628.6665968894958,"wires":[["a79a004b.23dca"]]},{"id":"a2c660a0.455f4","type":"function","z":"99ff3a85.459e88","name":"NORMAL","func":"msg.payload = \"NORMAL\";\nmsg.color = \"green\";\nreturn msg;\n\n\n","outputs":1,"noerr":0,"x":915.8333396911621,"y":583.000039100647,"wires":[["a79a004b.23dca"]]},{"id":"3895947f.e8e8cc","type":"function","z":"99ff3a85.459e88","name":"READING ERROR","func":"msg.payload = \"ERROR\";\nmsg.color = \"orange\";\nreturn msg;\n","outputs":1,"noerr":0,"x":915.8333396911621,"y":732.8888998031616,"wires":[["a79a004b.23dca"]]},{"id":"2a3f1761.af1e28","type":"delay","z":"99ff3a85.459e88","name":"","pauseType":"delay","timeout":"2","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":736.8333358764648,"y":729.8888998031616,"wires":[["3895947f.e8e8cc"]]},{"id":"89b6e936.af0ff8","type":"function","z":"99ff3a85.459e88","name":"Temp-Alarm","func":"var payload = msg.payload;\n\n\n\nif(payload[0] === \"Status normal\")\n{\n    msg.payload = \"off\";\n    return msg; \n}\nif(payload[0] === \"High alarm!!!\")\n{\n    msg.payload = \"on\";\n    return msg; \n}\nif(payload[0] === \"Reading error!!!\")\n{\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":812.0000076293945,"y":324.7777843475342,"wires":[[]]},{"id":"b491352.7630ac8","type":"switch","z":"99ff3a85.459e88","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"},{"t":"eq","v":"error","vt":"str"}],"checkall":"true","outputs":3,"x":553.0000038146973,"y":657.6666507720947,"wires":[["4e8f9dd7.108624","d8aa290d.004018"],["d8aa290d.004018","48f14c82.2d44d4"],["d8aa290d.004018","2a3f1761.af1e28"]]},{"id":"a79a004b.23dca","type":"ui_text","z":"99ff3a85.459e88","group":"c47baf96.4fa88","order":0,"width":"7","height":"2","name":"","label":"","format":"<font color= \"{{msg.color}}\">{{msg.payload}}</font>","layout":"row-center","x":1093.0000076293945,"y":677.4444360733032,"wires":[]},{"id":"bcef5420.bb3398","type":"debug","z":"99ff3a85.459e88","name":"","active":true,"console":"false","complete":"payload","x":819.0000076293945,"y":456.22222900390625,"wires":[]},{"id":"57eaa699.e81418","type":"function","z":"99ff3a85.459e88","name":"Temp-Alarm","func":"var payload = msg.payload;\n\nif (payload > 20 ){\n    msg.payload = \"on\";\n    return msg; \n}\nelse if (payload < 13){\n    msg.payload = \"off\";\n    return msg; \n}\nelse if(payload ===  undefined){\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":364,"y":664.222207069397,"wires":[["b491352.7630ac8","d4c3b67f.b79ee8","83b1185f.64e6b8"]]},{"id":"d4c3b67f.b79ee8","type":"debug","z":"99ff3a85.459e88","name":"","active":true,"console":"false","complete":"payload","x":362.00000381469727,"y":718.3333168029785,"wires":[]},{"id":"b9cab876.0e07a8","type":"function","z":"99ff3a85.459e88","name":"X-Axis","func":"var payload = msg.payload;\n\nif (payload > 2.5){ \n    msg.payload = \"on\";\n    return msg; \n}\nelse if (payload < 2.5){\n    msg.payload = \"off\";\n    return msg; \n}\nelse if(payload ===  undefined){\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":369,"y":1325.555700302124,"wires":[["e0227ed7.5faf3","8daf8447.cbe168","b5e9ab6e.f70ef8","e67314c.20139e8","200fbcf1.485214"]]},{"id":"9f215fe4.b1ad2","type":"function","z":"99ff3a85.459e88","name":"Y-Axis","func":"var payload = msg.payload;\n\nif (payload > 1.5){ \n    msg.payload = \"on\";\n    return msg; \n}\nelse if (payload > 1){\n    msg.payload = \"off\";\n    return msg; \n}\nelse if(payload ===  undefined){\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":752.0000038146973,"y":915.7777976989746,"wires":[[]]},{"id":"f6d5e1a0.8554e","type":"function","z":"99ff3a85.459e88","name":"Z-Axis","func":"var payload = msg.payload;\n\nif (payload > 2){ \n    msg.payload = \"on\";\n    return msg; \n}\nelse if (payload > 1){\n    msg.payload = \"off\";\n    return msg; \n}\nelse if(payload ===  undefined){\n    msg.payload = \"error\";\n    return msg; \n}\n","outputs":1,"noerr":0,"x":751.0000038146973,"y":955.1111316680908,"wires":[[]]},{"id":"5a10e468.6eccdc","type":"binaryOutput","z":"99ff3a85.459e88","pin":"P3","inverting":false,"defaultState":"0","name":"","x":1011.1666717529297,"y":817.7778778076172,"wires":[]},{"id":"83b1185f.64e6b8","type":"function","z":"99ff3a85.459e88","name":"Error","func":"payload = msg.payload;\nif (payload == \"on\"){\n    msg.payload = true;\n    return msg;}\nif (payload == \"off\"){\n    msg.payload = false;\n    return msg;}","outputs":1,"noerr":0,"x":593.1666717529297,"y":790.1112117767334,"wires":[["5a10e468.6eccdc"]]},{"id":"9cf2e48b.09f598","type":"inject","z":"99ff3a85.459e88","name":"Manually Temp_Alarm_create","topic":"","payload":"20","payloadType":"num","repeat":"","crontab":"","once":false,"x":202,"y":591.5555667877197,"wires":[["57eaa699.e81418"]]},{"id":"9814ca1d.c3c2e8","type":"inject","z":"99ff3a85.459e88","name":"Manually Axis_Alarm_create","topic":"","payload":"1.1","payloadType":"num","repeat":"","crontab":"","once":false,"x":155,"y":1325.666784286499,"wires":[["b9cab876.0e07a8"]]},{"id":"3d4ef04a.4857c","type":"ui_button","z":"99ff3a85.459e88","name":"","group":"caabfdbe.1355","order":0,"width":"7","height":"1","label":"Reset Alarm","color":"White","bgcolor":"Red","icon":"","payload":"false","payloadType":"bool","topic":"","x":75,"y":1083.7777690887451,"wires":[["57eaa699.e81418","b9cab876.0e07a8"]]},{"id":"4fabb3d6.940a8c","type":"function","z":"99ff3a85.459e88","name":"Random velocity","func":"var random = Math.random()*3;\nmsg.payload = random;\nreturn msg;","outputs":1,"noerr":0,"x":277.1666564941406,"y":306.33334255218506,"wires":[["b3b850af.859d9"]]},{"id":"ab8f3bb3.28f358","type":"inject","z":"99ff3a85.459e88","name":"","topic":"","payload":"","payloadType":"date","repeat":"300","crontab":"","once":false,"x":104.16667175292969,"y":305.1111145019531,"wires":[["4fabb3d6.940a8c"]]},{"id":"b3b850af.859d9","type":"debug","z":"99ff3a85.459e88","name":"","active":true,"console":"false","complete":"false","x":194.16669464111328,"y":338.00003719329834,"wires":[]},{"id":"e2ccc2d.292934","type":"function","z":"99ff3a85.459e88","name":"Random Temp","func":"var random = Math.random()*20;\nmsg.payload = random;\nreturn msg;","outputs":1,"noerr":0,"x":271.99997329711914,"y":370.3333387374878,"wires":[[]]},{"id":"fdacc880.7268c8","type":"inject","z":"99ff3a85.459e88","name":"","topic":"","payload":"","payloadType":"date","repeat":"300","crontab":"","once":false,"x":102,"y":371.1111173629761,"wires":[["e2ccc2d.292934"]]},{"id":"565c914c.637ba","type":"inject","z":"99ff3a85.459e88","name":"","topic":"","payload":"off","payloadType":"str","repeat":"","crontab":"","once":false,"x":291.1666564941406,"y":837.5555725097656,"wires":[["83b1185f.64e6b8"]]},{"id":"e67314c.20139e8","type":"function","z":"99ff3a85.459e88","name":"Error","func":"payload = msg.payload;\nif (payload == \"on\"){\n    msg.payload = true;\n    return msg;}\nif (payload == \"off\"){\n    msg.payload = false;\n    return msg;}","outputs":1,"noerr":0,"x":590,"y":843.5555419921875,"wires":[["5a10e468.6eccdc"]]},{"id":"200fbcf1.485214","type":"debug","z":"99ff3a85.459e88","name":"","active":true,"console":"false","complete":"payload","x":549.1666870117188,"y":1266.6666870117188,"wires":[]},{"id":"8217c159.7c9ff","type":"function","z":"99ff3a85.459e88","name":"Device","func":"var aryDevice = [];\n\nvar tempEvents = msg.payload['Advantech/FF504B7A/data'].Device.Events;\nswitch (tempEvents){\n    case 0:\n        aryDevice[0] = (\"Status normal\");\n        break;\n    case 1:\n        aryDevice [0] = (\"High alarm!!!\");\n        break;\n    default:\n        aryDevice [0] = (\"Reading error!!!\");\n}\naryDevice[1] = msg.payload['uplink/FF504B7A'].devaddr;\nvar tempPowerSrc = msg.payload['Advantech/FF504B7A/data'].Device.PowerSrc;\nswitch (tempPowerSrc){\n    case 0:\n        aryDevice [2] = (\"NA\");\n        break;\n    case 1:\n        aryDevice [2] = (\"Line power\");\n        break;\n    case 2:\n        aryDevice [2] = (\"Device battery\");\n        break;\n    case 3:\n        aryDevice [2] = (\"Line power+Device battery\");\n        break;\n    default:\n        aryDevice [2] = (\"Reading error!!!\");\n}\naryDevice[3] = msg.payload['Advantech/FF504B7A/data'].Device.BatteryVolt/1000;\naryDevice[4] = msg.payload['uplink/FF504B7A'].fcnt;\naryDevice[5] = msg.payload['uplink/FF504B7A'].lsnr;\naryDevice[6] = msg.payload['uplink/FF504B7A'].rssi;\naryDevice[7] = msg.payload['Advantech/FF504B7A/data'].Device.Time;\nvar today = new Date();\n// aryDevice[8] = tempDate.toGMTString(aryDevice[7]);\naryDevice[8] = today.getHours() + \":\" + today.getMinutes() + \":\" + today.getSeconds() +\" GMT\";\naryDevice[7] = aryDevice[7] + \" UTC\";\n\nmsg.payload = aryDevice;\nreturn msg;\n\n\n\n","outputs":1,"noerr":0,"x":793.0000114440918,"y":121.00000095367432,"wires":[["ab73b4d0.9025e8","ed92de9f.28515"]]},{"id":"ed92de9f.28515","type":"debug","z":"99ff3a85.459e88","name":"","active":true,"console":"false","complete":"false","x":1028.1666259765625,"y":52.763893127441406,"wires":[]},{"id":"df4ee2b8.4e152","type":"ui_group","z":"","name":"Reset","tab":"9c5e40f.219d0c","order":1,"disp":false,"width":"27"},{"id":"38fb1afd.32f896","type":"ui_group","z":"","name":"Device: WISE-2410","tab":"9c5e40f.219d0c","order":2,"disp":true,"width":"10"},{"id":"a79e3eb.160c7c","type":"mqtt-broker","z":"","broker":"127.0.0.1","port":"1883","clientid":"","usetls":false,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willPayload":"","birthTopic":"","birthQos":"0","birthPayload":""},{"id":"7dc459ba.028e38","type":"ui_group","z":"","name":"Accelerometer","tab":"9c5e40f.219d0c","order":3,"disp":true,"width":"10"},{"id":"d0ad8b2b.552848","type":"ui_group","z":"","name":"Temperature of the target","tab":"9c5e40f.219d0c","order":4,"disp":true,"width":"7"},{"id":"8efeb247.9f6df","type":"ui_group","z":"","name":"History Charts","tab":"9c5e40f.219d0c","order":9,"disp":true,"width":"10"},{"id":"ca8a3d6d.ef27","type":"ui_group","z":"","name":"History Charts","tab":"9c5e40f.219d0c","order":10,"disp":true,"width":"10"},{"id":"d36c051a.aabae8","type":"ui_group","z":"","name":"X-Axis Alarm","tab":"9c5e40f.219d0c","order":5,"disp":true,"width":"2"},{"id":"5034141b.fce75c","type":"ui_group","z":"","name":"Z-Axis Alarm","tab":"9c5e40f.219d0c","order":7,"disp":true,"width":"2"},{"id":"d03f58be.bb93c8","type":"ui_group","z":"","name":"Y-Axis Alarm","tab":"9c5e40f.219d0c","order":6,"disp":true,"width":"2"},{"id":"c47baf96.4fa88","type":"ui_group","z":"","name":"Temperature Alarm","tab":"9c5e40f.219d0c","order":8,"disp":true,"width":"7"},{"id":"caabfdbe.1355","type":"ui_group","z":"","name":"Button","tab":"9c5e40f.219d0c","order":11,"disp":true,"width":"7"},{"id":"9c5e40f.219d0c","type":"ui_tab","z":"","name":"Advantech LoRaWAN Vibration/Temp sensor Solution ","icon":"dashboard","order":1}]

Visit our official website: https://polisea.ro/aiot/ 

🚩 Connect with me on social
- LinkedIn: https://www.linkedin.com/in/ariful-islam-arif-2987b51a3/
- Twitter: https://twitter.com/arifulislam301
- Instagram: https://www.instagram.com/ariful_mr_islam/

🔔 Subscribe to my YouTube channel
https://www.youtube.com/channel/UCED68cm6nHaAlAk0h9I3yAQ

