Desctiption: Make Alexa Call People Out for Leaving the Toilet Seat Up! (Node-RED Tutorial)

Link to YouTube video: https://youtu.be/HoYak0LTelg

This is the code for the Node-Red process flow

- Copy the below code to the clipboard then from Node-Red cick the 3 horizontal lines
- Select Import
- Paste the code into the Window and Select Import
- Configure the 2 Nodes referencing your door sensors
- Confugure the Alexa node to reference your Amazon account and Alexa device
- Deploy the changes to apply

- **Full Code for Alexa-Toilet-Seat-Alert**
```
[{"id":"03578a0971389483","type":"function","z":"3d5bd8efbb0e55d5","name":"Bathroom Door is Closed","func":"flow.set (\"bathroom_door_open\",false);\nvar bathroom_door_open_status = flow.get (\"bathroom_door_open\");\nmsg.topic= bathroom_door_open_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":209.0994415283203,"y":178.2465991973877,"wires":[[]]},{"id":"bb2a7b6dbf43b099","type":"function","z":"3d5bd8efbb0e55d5","name":"Bathroom Door is Open","func":"flow.set(\"bathroom_door_open\",true);\nvar bathroom_door_open_status = flow.get(\"bathroom_door_open\");\nmsg.topic = bathroom_door_open_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":209.0994415283203,"y":216.95177555084229,"wires":[[]]},{"id":"13315ba210e9200b","type":"function","z":"3d5bd8efbb0e55d5","name":"Toilet Seat is Down","func":"flow.set (\"toilet_seat_up\",false);\nvar toilet_seat_up_status = flow.get (\"toilet_seat\");\nmsg.topic= toilet_seat_up_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":606.4435234069824,"y":183.84813563028968,"wires":[[]]},{"id":"2383fc3b9fa1f618","type":"function","z":"3d5bd8efbb0e55d5","name":"Toilet Seat is Up","func":"flow.set (\"toilet_seat_up\",true);\nvar toilet_seat_up_status = flow.get (\"toilet_seat\");\nmsg.topic= toilet_seat_up_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":371.2293014526367,"y":906.236668586731,"wires":[[]]},{"id":"c2963ae7febe2462","type":"comment","z":"3d5bd8efbb0e55d5","name":"Change Entity to Your Toilet Seat Sensor","info":"","x":676.4435234069824,"y":76.73544502258301,"wires":[]},{"id":"3394896ecf437625","type":"comment","z":"3d5bd8efbb0e55d5","name":"Run when bathroom door opens","info":"","x":184.31948852539062,"y":1114.2576351165771,"wires":[]},{"id":"e83ad8aa4e44bee2","type":"function","z":"3d5bd8efbb0e55d5","name":"Get Toilet Seat Up Status","func":"var ObtainedData = flow.get (\"toilet_seat_up\");\nmsg.topic= ObtainedData;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":397.73639187812796,"y":1157.490240573883,"wires":[["99e6ede146b6ab03"]]},{"id":"99e6ede146b6ab03","type":"switch","z":"3d5bd8efbb0e55d5","name":"If toilet Seat is Up","property":"topic","propertyType":"msg","rules":[{"t":"true"},{"t":"false"},{"t":"else"}],"checkall":"true","repair":false,"outputs":3,"x":624.093986940384,"y":1164.990240573883,"wires":[["71acce01c9acbaf3"],[],[]]},{"id":"71acce01c9acbaf3","type":"function","z":"3d5bd8efbb0e55d5","name":"Check if Nagging is Enabled","func":"var ObtainedData = flow.get (\"nagging_on\");\nmsg.topic= ObtainedData;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":860.45158200264,"y":1157.490240573883,"wires":[["b185c74e29898018"]]},{"id":"b185c74e29898018","type":"switch","z":"3d5bd8efbb0e55d5","name":"If nagging_on_status is true","property":"topic","propertyType":"msg","rules":[{"t":"false"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":1126.8091770648957,"y":1157.490240573883,"wires":[[],["bc525db6acd0b039"]]},{"id":"314df8167ee0db87","type":"switch","z":"3d5bd8efbb0e55d5","name":"If bathroom door is open","property":"topic","propertyType":"msg","rules":[{"t":"true"},{"t":"false"},{"t":"else"}],"checkall":"true","repair":false,"outputs":3,"x":714.6466522216797,"y":1033.8475341796875,"wires":[["2dfc39ced1eaacd1"],[],[]]},{"id":"1185d145fd575666","type":"function","z":"3d5bd8efbb0e55d5","name":"Check if Nagging is Enabled","func":"var ObtainedData = flow.get (\"nagging_on\");\nmsg.topic= ObtainedData;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":1663.1016235351562,"y":1026.3475341796875,"wires":[["3bc5ad5368671636"]]},{"id":"3bc5ad5368671636","type":"switch","z":"3d5bd8efbb0e55d5","name":"If nagging_on_status is true","property":"topic","propertyType":"msg","rules":[{"t":"false"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":1929.2532806396484,"y":1026.3475341796875,"wires":[[],["a6934912a1387b10"]]},{"id":"bfaf498440b488c1","type":"function","z":"3d5bd8efbb0e55d5","name":"Get toilet door open / closed status","func":"var ObtainedData = flow.get (\"bathroom_door_open\");\nmsg.topic= ObtainedData;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":438.4949951171875,"y":1026.3475341796875,"wires":[["314df8167ee0db87"]]},{"id":"9d44049b3d6d2edc","type":"comment","z":"3d5bd8efbb0e55d5","name":"Run when toilet seat is down","info":"","x":160.15807342529297,"y":981.9508781433105,"wires":[]},{"id":"8b0134eb376b300d","type":"server-state-changed","z":"3d5bd8efbb0e55d5","name":"Bathroom Door Status","server":"67fb9d0f.36c644","version":6,"outputs":2,"exposeAsEntityConfig":"","entities":{"entity":["binary_sensor.sensor_bathroom_door_contact"],"substring":[],"regex":[]},"outputInitially":false,"stateType":"str","ifState":"off","ifStateType":"str","ifStateOperator":"is","outputOnlyOnStateChange":true,"for":"0","forType":"num","forUnits":"minutes","ignorePrevStateNull":false,"ignorePrevStateUnknown":false,"ignorePrevStateUnavailable":false,"ignoreCurrentStateUnknown":true,"ignoreCurrentStateUnavailable":true,"outputProperties":[{"property":"payload","propertyType":"msg","value":"","valueType":"entityState"},{"property":"data","propertyType":"msg","value":"","valueType":"eventData"},{"property":"topic","propertyType":"msg","value":"","valueType":"triggerId"}],"x":199.0994415283203,"y":124.45069980621338,"wires":[["03578a0971389483"],["bb2a7b6dbf43b099","5abf3813c78bdd25"]]},{"id":"fdb2f60fca260fb6","type":"server-state-changed","z":"3d5bd8efbb0e55d5","name":"Toilet Seat Status","server":"67fb9d0f.36c644","version":6,"outputs":2,"exposeAsEntityConfig":"","entities":{"entity":["binary_sensor.sensor_toilet_seat_contact"],"substring":[],"regex":[]},"outputInitially":false,"stateType":"str","ifState":"on","ifStateType":"str","ifStateOperator":"is","outputOnlyOnStateChange":true,"for":"0","forType":"num","forUnits":"minutes","ignorePrevStateNull":false,"ignorePrevStateUnknown":false,"ignorePrevStateUnavailable":false,"ignoreCurrentStateUnknown":true,"ignoreCurrentStateUnavailable":true,"outputProperties":[{"property":"payload","propertyType":"msg","value":"","valueType":"entityState"},{"property":"data","propertyType":"msg","value":"","valueType":"eventData"},{"property":"topic","propertyType":"msg","value":"","valueType":"triggerId"}],"x":596.4435234069824,"y":130.45083236694336,"wires":[["13315ba210e9200b","0ed5e8dff453c147"],["df668f7776b517b5"]]},{"id":"44d63d0aeefee542","type":"function","z":"3d5bd8efbb0e55d5","name":"Get Bathroom Door Open / Closed Status","func":"var ObtainedData = flow.get(\"bathroom_door_open\");\nmsg.topic= ObtainedData;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":448.92860412597656,"y":863.5379095077515,"wires":[["03d7c27d340cf1c1"]]},{"id":"03d7c27d340cf1c1","type":"switch","z":"3d5bd8efbb0e55d5","name":"If bathroom door is open","property":"topic","propertyType":"msg","rules":[{"t":"true"},{"t":"false"},{"t":"else"}],"checkall":"true","repair":false,"outputs":3,"x":748.1349487304688,"y":861.9506711959839,"wires":[["b3eabfbd84976231"],["81a5d7695fd5a764"],["81a5d7695fd5a764"]]},{"id":"b3eabfbd84976231","type":"function","z":"3d5bd8efbb0e55d5","name":"set \"seat lifted_when door open\" to true","func":"flow.set (\"seat_lifted_when_door_open\",true);\nvar seat_lifted_when_door_open_status = flow.get (\"seat_lifted_when_door_open\");\nmsg.topic= seat_lifted_when_door_open_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":1061.626937866211,"y":830.0459356307983,"wires":[[]]},{"id":"81a5d7695fd5a764","type":"function","z":"3d5bd8efbb0e55d5","name":"set \"seat lifted_when door open\" to false","func":"flow.set (\"seat_lifted_when_door_open\",false);\nvar seat_lifted_when_door_open_status = flow.get (\"seat_lifted_when_door_open\");\nmsg.topic= seat_lifted_when_door_open_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":1061.9443969726562,"y":883.220458984375,"wires":[[]]},{"id":"2dfc39ced1eaacd1","type":"function","z":"3d5bd8efbb0e55d5","name":"Get \"seat_lifted_when_door_open\" status","func":"var ObtainedData = flow.get (\"seat_lifted_when_door_open\");\nmsg.topic= ObtainedData;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":1010.7983093261719,"y":1026.3475341796875,"wires":[["908b4dda78ffe55a"]]},{"id":"908b4dda78ffe55a","type":"switch","z":"3d5bd8efbb0e55d5","name":"If \"seat_lifted_when_door_open\" is false","property":"seat_lifted_when_door_open","propertyType":"flow","rules":[{"t":"true"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":1356.949966430664,"y":1026.3475341796875,"wires":[[],["1185d145fd575666"]]},{"id":"c8e99e71f9f77912","type":"function","z":"3d5bd8efbb0e55d5","name":"Random Nagging For Leaving Toilet Seat Up","func":"var line1 = [\n        \"Hey!, \",\n        \"Oi!, \",\n        \"Mate!, \",\n        \"Did I really just witness this?,\",\n        \"oh for crying out loud,\",\n        \"Excuse me, \"\n        ]\n        \nvar line2 = [\n        \"you've left the toilet seat up. \",\n        \"you didn't put the seat down. \",\n        \"the toilet seat is still up. \"\n        ]\n        \nvar line3 = [\n        \"go back and close it \",\n        \"Turn around and shut it! \",\n        \"close it now \"\n        ]\n        \nvar line4 = [\n        \"you \",\n        \"you \"\n        ]\n        \nvar line5 = [\n        \"dirty \",\n        \"lazy \",\n        \"disgusting \",\n        \"revolting \",\n        \"phile \",\n        \"despicable \",\n        \"pathetic\",\n        \"filthy \"\n        ]\n        \nvar line6 = [\n        \"git\",\n        \"walking embarrassment\",\n        \"individual\",\n        \"human\",\n        \"creature\",\n        \"animal\",\n        \"beast\",\n        \"excuse of a human being\",\n        \"slob \"\n        ]        \n\nmsg.payload =\n\nline1[Math.floor(Math.random() * line1.length)]+\nline2[Math.floor(Math.random() * line2.length)]+\nline3[Math.floor(Math.random() * line3.length)]+\nline4[Math.floor(Math.random() * line4.length)]+\nline5[Math.floor(Math.random() * line5.length)]+\nline6[Math.floor(Math.random() * line6.length)]\n\nreturn msg","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":1993.83345413208,"y":468.4903202056885,"wires":[["81ef895f9ce6d3af"]]},{"id":"2f29bd7234fdf66f","type":"alexa-remote-routine","z":"3d5bd8efbb0e55d5","name":"Broadcast Announcement to Alexa Device","account":"d52478f1.087f58","routineNode":{"type":"speak","payload":{"type":"regular","text":{"type":"msg","value":"payload"},"devices":["G0014C0594551CG2"]}},"x":1063.502082824707,"y":134.84744834899902,"wires":[[]]},{"id":"09bd25ad12a68ecc","type":"function","z":"3d5bd8efbb0e55d5","name":"Random Response after Closing Toilet Seat","func":"var line1 = [\n        \"Thankyou!, \",\n        \"Thanks, \",\n        \"good, \"\n        ]\nvar line2 = [\n        \"dont \",\n        \"you better not \"\n        ]\nvar line3 = [\n        \"make me \",\n        \"cause me to \",\n        \"make this a habbit and force me to \",\n        \"repeat this so that I have to \"\n        ]\nvar line4 = [\n        \"shout \",\n        \"complain \",\n        \"yell \"\n        ]\nvar line5 = [\n        \"again\",\n        \"once again\",\n        \"another time\"\n        ]        \n\nmsg.payload =\n\nline1[Math.floor(Math.random() * line1.length)]+\nline2[Math.floor(Math.random() * line2.length)]+\nline3[Math.floor(Math.random() * line3.length)]+\nline4[Math.floor(Math.random() * line4.length)]+\nline5[Math.floor(Math.random() * line4.length)]\n\nreturn msg","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":2017.5476722717285,"y":652.6332302093506,"wires":[["98b27b5333e947c5"]]},{"id":"627a6b58642d2d78","type":"delay","z":"3d5bd8efbb0e55d5","name":"","pauseType":"delay","timeout":"1","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"outputs":1,"x":1738.2619895935059,"y":468.06179332733154,"wires":[["c8e99e71f9f77912"]]},{"id":"4448a1f5fbe48648","type":"switch","z":"3d5bd8efbb0e55d5","name":"Null?","property":"payload","propertyType":"msg","rules":[{"t":"cont","v":"undefined","vt":"str"}],"checkall":"true","repair":false,"outputs":1,"x":1638.3835716247559,"y":467.4787244796753,"wires":[["627a6b58642d2d78"]],"l":false},{"id":"f110a8f9509a8708","type":"catch","z":"3d5bd8efbb0e55d5","name":"Alexa errors","scope":["2f29bd7234fdf66f"],"uncaught":false,"x":1531.3834495544434,"y":467.58974742889404,"wires":[["4448a1f5fbe48648"]]},{"id":"4c5634011335047e","type":"delay","z":"3d5bd8efbb0e55d5","name":"","pauseType":"delay","timeout":"1","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"outputs":1,"x":1751.2619895935059,"y":653.0617933273315,"wires":[["09bd25ad12a68ecc"]]},{"id":"7aa2feda932e47bd","type":"switch","z":"3d5bd8efbb0e55d5","name":"Null?","property":"payload","propertyType":"msg","rules":[{"t":"cont","v":"undefined","vt":"str"}],"checkall":"true","repair":false,"outputs":1,"x":1628.3835697174072,"y":653.4787034988403,"wires":[["4c5634011335047e"]],"l":false},{"id":"2ddc0505d9249b36","type":"catch","z":"3d5bd8efbb0e55d5","name":"Alexa errors","scope":["e1dd64f4204d8773"],"uncaught":false,"x":1509.3834495544434,"y":654.589747428894,"wires":[["7aa2feda932e47bd"]]},{"id":"7460be0f17637104","type":"link in","z":"3d5bd8efbb0e55d5","name":"Link in_Post Toilet Seat Close Nag","links":["a6934912a1387b10"],"x":1579.5476722717285,"y":705.6331691741943,"wires":[["09bd25ad12a68ecc"]],"l":true},{"id":"a6934912a1387b10","type":"link out","z":"3d5bd8efbb0e55d5","name":"Link out","mode":"link","links":["7460be0f17637104"],"x":2135.4049377441406,"y":1026.3475341796875,"wires":[],"l":true},{"id":"3d6b49429e273f4d","type":"link in","z":"3d5bd8efbb0e55d5","name":"Link in_Toilet Seat Up Nag","links":["bc525db6acd0b039"],"x":1565.118984222412,"y":512.9188842773438,"wires":[["c8e99e71f9f77912"]],"l":true},{"id":"bc525db6acd0b039","type":"link out","z":"3d5bd8efbb0e55d5","name":"Link out 2","mode":"link","links":["3d6b49429e273f4d"],"x":1333.1667721271515,"y":1157.490240573883,"wires":[],"l":true},{"id":"c8b7d92035f5cd8c","type":"comment","z":"3d5bd8efbb0e55d5","name":"Turn Nagging On / Off","info":"","x":140.98614764213562,"y":457.9383382797241,"wires":[]},{"id":"53c50e9fded7e46e","type":"inject","z":"3d5bd8efbb0e55d5","name":"Nagging on","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":129.03970336914062,"y":502.8436117172241,"wires":[["37ebfe3c2f0d81c3"]]},{"id":"7155810452cbace4","type":"inject","z":"3d5bd8efbb0e55d5","name":"Nagging off","repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":128.4047622680664,"y":552.9003467559814,"wires":[["6c255af3aaaa4020"]]},{"id":"37ebfe3c2f0d81c3","type":"function","z":"3d5bd8efbb0e55d5","name":"Turn on Nagging","func":"flow.set (\"nagging_on\",true);\nvar nagging_on_status = flow.get (\"nagging_on\");\nmsg.topic= nagging_on_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":309.94457244873047,"y":502.8436117172241,"wires":[["e73e204d5362542b"]]},{"id":"6c255af3aaaa4020","type":"function","z":"3d5bd8efbb0e55d5","name":"Turn off Nagging","func":"flow.set (\"nagging_on\",false);\nvar nagging_on_status = flow.get (\"nagging_on\");\nmsg.topic= nagging_on_status;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":309.62710189819336,"y":552.9003467559814,"wires":[["a2b449c4128956b0"]]},{"id":"f3d9bf7771dbad32","type":"switch","z":"3d5bd8efbb0e55d5","name":"Check if Nagging is Enabled","property":"topic","propertyType":"msg","rules":[{"t":"true"},{"t":"false"},{"t":"cont","v":"undefined","vt":"str"}],"checkall":"true","repair":false,"outputs":3,"x":527.0968227386475,"y":695.9323263168335,"wires":[["d8ad7e056b20e46c"],["154a05cf1eb9323f"],["0e9fbc33dc2f7ef5"]]},{"id":"813a9132fbf6d3e2","type":"function","z":"3d5bd8efbb0e55d5","name":"Get Nagging Status","func":"var ObtainedData = flow.get (\"nagging_on\");\nmsg.topic= ObtainedData;\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":289.7635555267334,"y":688.4324245452881,"wires":[["f3d9bf7771dbad32"]]},{"id":"a244668b3ba8653d","type":"inject","z":"3d5bd8efbb0e55d5","name":"","repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"check nagging status","payload":"","payloadType":"date","x":117.84915351867676,"y":688.4324245452881,"wires":[["813a9132fbf6d3e2"]]},{"id":"75dc54a63570004b","type":"comment","z":"3d5bd8efbb0e55d5","name":"Get Nagging Status","info":"","x":130.98614764213562,"y":642.1656303405762,"wires":[]},{"id":"11dd0e77a27025da","type":"comment","z":"3d5bd8efbb0e55d5","name":"NAG Toilet seat is up!","info":"","x":1559.412452697754,"y":420.8470678329468,"wires":[]},{"id":"e5ef5b77f5c7209b","type":"comment","z":"3d5bd8efbb0e55d5","name":"POST NAG after closing toilet seat","info":"","x":1577.983814239502,"y":606.5613393783569,"wires":[]},{"id":"5abf3813c78bdd25","type":"link out","z":"3d5bd8efbb0e55d5","name":"If Bathroom Door Open","mode":"link","links":["1d72bb22afb23829"],"x":209.0994415283203,"y":255.65695190429688,"wires":[],"l":true},{"id":"1d72bb22afb23829","type":"link in","z":"3d5bd8efbb0e55d5","name":"If Bathroom Door Open","links":["5abf3813c78bdd25"],"x":161.3787968158722,"y":1157.490240573883,"wires":[["e83ad8aa4e44bee2"]],"l":true},{"id":"df2fb175c370bdbc","type":"link in","z":"3d5bd8efbb0e55d5","name":"If Toilet Seat if Down (IN)","links":["0ed5e8dff453c147"],"x":162.3433380126953,"y":1026.3475341796875,"wires":[["bfaf498440b488c1"]],"l":true},{"id":"0ed5e8dff453c147","type":"link out","z":"3d5bd8efbb0e55d5","name":"If Toilet Seat if Down (OUT)","mode":"link","links":["df2fb175c370bdbc"],"x":636.4435234069824,"y":220.3645270665487,"wires":[],"l":true},{"id":"df668f7776b517b5","type":"link out","z":"3d5bd8efbb0e55d5","name":"If Toilet Seat is Up (OUT)","mode":"link","links":["ae3de188f9f355ab"],"x":626.4435234069824,"y":256.8809185028076,"wires":[],"l":true},{"id":"ae3de188f9f355ab","type":"link in","z":"3d5bd8efbb0e55d5","name":"If Toilet Seat is Up (IN)","links":["df668f7776b517b5"],"x":152.91470336914062,"y":879.6826238632202,"wires":[["44d63d0aeefee542","2383fc3b9fa1f618"]],"l":true},{"id":"81ef895f9ce6d3af","type":"link out","z":"3d5bd8efbb0e55d5","name":"Broadcast Announcement to Alexa Device (OUT)","mode":"link","links":["f5555ca4a8dffee5"],"x":2366.9898262023926,"y":470.1388626098633,"wires":[],"l":true},{"id":"f5555ca4a8dffee5","type":"link in","z":"3d5bd8efbb0e55d5","name":"Broadcast Announcement to Alexa Device (IN)","links":["81ef895f9ce6d3af","98b27b5333e947c5","67be4625a10077f8","c4666c5e44d21258"],"x":1073.502082824707,"y":237.02770900726318,"wires":[["5723e2effaa7b432"]],"l":true},{"id":"98b27b5333e947c5","type":"link out","z":"3d5bd8efbb0e55d5","name":"Broadcast Announcement to Alexa Device (OUT)","mode":"link","links":["f5555ca4a8dffee5"],"x":2389.4086952209473,"y":653.7041606903076,"wires":[],"l":true},{"id":"ed1cc8d0e60762c6","type":"comment","z":"3d5bd8efbb0e55d5","name":"Change Entity to Your Bathroom Door Sensor","info":"","x":269.0994415283203,"y":76.73544502258301,"wires":[]},{"id":"2bef44b3be4b305c","type":"comment","z":"3d5bd8efbb0e55d5","name":"Change Device to your Amazon Echo","info":"","x":1040.6448822021484,"y":76.73544502258301,"wires":[]},{"id":"4655bbd13e6f27fa","type":"comment","z":"3d5bd8efbb0e55d5","name":"########### Do Not Edit the Below!!! ###########","info":"","x":674.0994644165039,"y":391.09375,"wires":[]},{"id":"364398de9f64b631","type":"comment","z":"3d5bd8efbb0e55d5","name":"This part prevents the routine from working if the bathroom door open","info":"","x":280.9861476421356,"y":814.2354001998901,"wires":[]},{"id":"e73e204d5362542b","type":"function","z":"3d5bd8efbb0e55d5","name":"Nagging Enabled","func":"msg.payload = \"Nagging enabled\";\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":510.8494415283203,"y":502.8436117172241,"wires":[["67be4625a10077f8"]]},{"id":"67be4625a10077f8","type":"link out","z":"3d5bd8efbb0e55d5","name":"Broadcast Announcement to Alexa Device (OUT)","mode":"link","links":["f5555ca4a8dffee5"],"x":812.8494491577148,"y":526.5709056854248,"wires":[],"l":true},{"id":"a2b449c4128956b0","type":"function","z":"3d5bd8efbb0e55d5","name":"Nagging Disabled","func":"msg.payload = \"Nagging disabled\";\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":510.8494415283203,"y":552.9003467559814,"wires":[["67be4625a10077f8"]]},{"id":"d8ad7e056b20e46c","type":"function","z":"3d5bd8efbb0e55d5","name":"Nagging Enabled","func":"msg.payload = \"Nagging enabled\";\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":776.8494663238525,"y":662.3887710571289,"wires":[["c4666c5e44d21258"]]},{"id":"c4666c5e44d21258","type":"link out","z":"3d5bd8efbb0e55d5","name":"Broadcast Announcement to Alexa Device (OUT)","mode":"link","links":["f5555ca4a8dffee5"],"x":1172.8494873046875,"y":695.3890190124512,"wires":[],"l":true},{"id":"154a05cf1eb9323f","type":"function","z":"3d5bd8efbb0e55d5","name":"Nagging Disabled","func":"msg.payload = \"Nagging disabled\";\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":776.8494663238525,"y":697.3887701034546,"wires":[["c4666c5e44d21258"]]},{"id":"0e9fbc33dc2f7ef5","type":"function","z":"3d5bd8efbb0e55d5","name":"Undefined So Nagging is Enabled","func":"msg.payload = \"undefined so nagging is enabled\";\nreturn msg;","outputs":1,"timeout":"","noerr":0,"initialize":"","finalize":"","libs":[],"x":826.8494663238525,"y":733.3888912200928,"wires":[["c4666c5e44d21258"]]},{"id":"dc4c8bbb22d2a8da","type":"comment","z":"3d5bd8efbb0e55d5","name":"########### Do Not Edit the Below!!! ###########","info":"","x":1108.0994873046875,"y":391.09375,"wires":[]},{"id":"b2531c80bc2c0d36","type":"comment","z":"3d5bd8efbb0e55d5","name":"########### Do Not Edit the Below!!! ###########","info":"","x":240.0994415283203,"y":391.09375,"wires":[]},{"id":"5723e2effaa7b432","type":"delay","z":"3d5bd8efbb0e55d5","name":"","pauseType":"delay","timeout":"1.5","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"allowrate":false,"outputs":1,"x":973.502082824707,"y":184.70535373687744,"wires":[["2f29bd7234fdf66f"]]},{"id":"67fb9d0f.36c644","type":"server","name":"Home Assistant","version":5,"addon":true,"rejectUnauthorizedCerts":true,"ha_boolean":"y|yes|true|on|home|open","connectionDelay":true,"cacheJson":true,"heartbeat":false,"heartbeatInterval":30,"areaSelector":"friendlyName","deviceSelector":"friendlyName","entitySelector":"friendlyName","statusSeparator":"at: ","statusYear":"hidden","statusMonth":"short","statusDay":"numeric","statusHourCycle":"h23","statusTimeFormat":"h:m","enableGlobalContextStore":true},{"id":"d52478f1.087f58","type":"alexa-remote-account","name":"","authMethod":"proxy","proxyOwnIp":"192.168.1.113","proxyPort":"3456","cookieFile":"/config/alexa_cookies12.txt","refreshInterval":"3","alexaServiceHost":"alexa.amazon.co.uk","amazonPage":"amazon.co.uk","acceptLanguage":"en-UK","userAgent":"","useWsMqtt":"on","autoInit":"on"}]
```
