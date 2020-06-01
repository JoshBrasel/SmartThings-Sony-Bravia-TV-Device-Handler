/*
* Sony Bravia TV SmartThings Device Handler
*
* Based on Steve Abratt's example:
* 	https://gist.githubusercontent.com/steveAbratt/43133bf9011febf6437a662eb5998ec8/raw/4c9f61c7822ba944192862d6a56a9c1a0b81d1bf/bravia.groovy
*
* Configuration Steps:
*   1. Enable Remote Start on the TV: [Settings] → [Network] → [Home Network Setup] → [Remote Start] → [On]
*	2. Enable Pre-Shared Key on the TV: [Settings] → [Network] → [Home Network Setup] → [IP Control] → [Authentication] → [Normal and Pre-Shared Key]
*   3. Set Pre-Shared Key on the TV: [Settings] → [Network] → [Home Network Setup] → [IP Control] → [Pre-Shared Key] → [sony] *Note: You can select any Pre-Shared Key you want
*   4. Assign the TV a static IP address
*   5. Add this Device Handler on your SmartThings HUB and publish it
*	6. Ensure the TV is ON
*   7. Add the Device to SmartThings
*		Type = Sony Bravia XBR TV
*		Device Network ID = (Hex of IP address and port in the form of 00000000:0000 and must be in ALL CAPS) (i.e. 10.0.1.220:80 is 0A0001DC:0050)
*			*Note: You can find a converter on the Internet
*   8. Set the Preferences in this Device Handler
*		tvIP = IP Address of the TV (with decimals)
*		tvPSK = passphrase for your TV
*		tvPort = 80 (typically 80, only enter a different value if you know it is different)
*
*	WOLC (Wake on LAN) functionality is only necessary if the TV is in ECO mode and is NOT included in this version.
*/
 
metadata {
  definition (name: "Sony Bravia TV", namespace: "Brasel", author: "Josh Brasel") {
    capability "Switch"
    capability "Polling"
    capability "Refresh"
    capability "Switch Level"

    command "powerButton"
    command "refreshButton"
    command "volumeUpButton"
    command "volumeDownButton"	
	command "muteButton"
    command "channelUpButton"	
    command "channelDownButton"
    command "sleepTimerButton"
    command "applicationLauncherButton"
    command "discoverButton"
    command "homeButton"
    command "returnButton"
    command "exitButton"	    
	command "upButton"
	command "rightButton"
    command "downButton"
    command "leftButton"
    command "centerButton"
    command "inputButton"
    command "analogButton"
    command "hdmi1Button"
    command "hdmi2Button"
    command "hdmi3Button"
    command "hdmi4Button"
    command "video1Button"
    command "video2Button"
    command "tvButton"	
	command "playButton"    
    command "pauseButton"    
    command "rewindButton"
    command "fastforwardButton"
    command "previousButton"
	command "nextButton"
	command "stopButton"
	command "netflixButton"
	command "vuduButton"
    command "hboButton"
	command "youTubeButton"
    command "wweButton"
    command "disneyButton"
  }

  tiles(scale:2) {
    multiAttributeTile(name:"mainTile", type:"generic", width:6, height:4) {
		tileAttribute("device.switch", key: "PRIMARY_CONTROL") {
            attributeState "off", label: '${currentValue}', action: "switch.on", icon: "st.Electronics.electronics18", backgroundColor: "#ffffff", nextState: "on"
            attributeState "on", label: '${currentValue}', action: "switch.off", icon: "st.Electronics.electronics18", backgroundColor: "#00a0dc", nextState: "off"}
        tileAttribute("device.input", key: "SECONDARY_CONTROL") {
        	attributeState "input", label: '${currentValue}'}
        tileAttribute("device.level", key: "SLIDER_CONTROL") {
            attributeState "level", action:"setLevel", icon: 'st.Entertainment.entertainment15',  defaultState: "true"}
	}
	standardTile("powerButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Power", action:"powerButton", icon:"st.samsung.da.RC_ic_power"}
	standardTile("refreshButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Refresh", action:"refresh", icon:"st.secondary.refresh-icon"}
	standardTile("volumeUpButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"volumeUpButton", icon:"st.samsung.da.oven_ic_plus"}
	standardTile("volumeDownButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"volumeDownButton", icon:"st.samsung.da.oven_ic_minus"}
    valueTile("muteButton", "device.mute", inactiveLabel: false, height: 1, width: 1, decoration: "flat") {
        state "true", label:"Mute", action:"muteButton", icon: "st.custom.sonos.muted",  nextState: "false"
        state "false", label:"Mute", action:"muteButton", icon: "st.custom.sonos.unmuted",  nextState: "true"}
	standardTile("channelUpButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"channelUpButton", icon:"st.samsung.da.oven_ic_up"}
    standardTile("channelDownButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"channelDownButton", icon:"st.samsung.da.oven_ic_down"}
	standardTile("sleepTimerButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Sleep Timer", action:"sleepTimerButton", icon:"st.Office.office6"}
	standardTile("applicationLauncherButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Apps", action:"applicationLauncherButton", icon:""}
	standardTile("discoverButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Discover", action:"discoverButton", icon:""}
	standardTile("homeButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Home", action:"homeButton", icon:"st.Home.home2"} 
    standardTile("returnButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Return", action:"returnButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Return.png"}
	standardTile("exitButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Exit", action:"exitButton", icon:"st.samsung.da.washer_ic_cancel"}        
	standardTile("upButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"upButton", icon:"st.thermostat.thermostat-up"}
	standardTile("rightButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"rightButton", icon:"st.thermostat.thermostat-right"}
    standardTile("downButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"downButton", icon:"st.thermostat.thermostat-down"}
	standardTile("leftButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"leftButton", icon:"st.thermostat.thermostat-left"}
	standardTile("centerButton", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"centerButton", icon:"st.illuminance.illuminance.dark"}
    standardTile("inputButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Input", action:"inputButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Input.png"}
	standardTile("analogButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Analog", action:"analogButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Analog.png"}
	standardTile("hdmi1Button", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"HDMI 1", action:"hdmi1Button", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/GoogleFiber.png"}
	standardTile("hdmi2Button", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"HDMI 2", action:"hdmi2Button", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/XBOX.png"}
	standardTile("hdmi3Button", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"HDMI 3", action:"hdmi3Button", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Switch.png"}
	standardTile("hdmi4Button", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"HDMI 4", action:"hdmi4Button", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/HDMI.png"}
	standardTile("video1Button", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Video 1", action:"video1Button", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/RCA.png"}
	standardTile("video2Button", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"Video 2", action:"video2Button", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Component.png"}
	standardTile("tvButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"TV", action:"tvButton", icon:""}
	standardTile("playButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"playButton", icon:"st.sonos.play-btn"}   
	standardTile("pauseButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"pauseButton", icon:"st.sonos.pause-btn"}
	standardTile("rewindButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"rewindButton", icon:"st.sonos.previous-btn"}
	standardTile("fastforwardButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"fastforwardButton", icon:"st.sonos.next-btn"}
	standardTile("previousButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"previousButton", icon:"st.sonos.previous-btn"}      
	standardTile("nextButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"nextButton", icon:"st.sonos.next-btn"}   
	standardTile("stopButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"stopButton", icon:"st.sonos.stop-btn"}        
    standardTile("netflixButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"netflixButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Netflix.png"}
	standardTile("vuduButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"vuduButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Vudu.png"}
	standardTile("hboButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"hboButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/HBOMax.png"}
	standardTile("youTubeButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"youTubeButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/YouTube.png"}
	standardTile("disneyButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"disneyButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/Disney.png"}      
	standardTile("wweButton", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"wweButton", icon:"https://raw.githubusercontent.com/joshbrasel/SmartThingsCustomIcons/master/WWE.png"}	
    standardTile("emptyButtonLarge", "device.switch", inactiveLabel: false, height: 2, width: 2, decoration: "flat"){
		state "default", label:"", action:"", icon:""}     
    standardTile("emptyButtonSmall", "device.switch", inactiveLabel: false, height: 1, width: 1, decoration: "flat"){
		state "default", label:"", action:"", icon:""} 
        
    main("mainTile")

    details(["mainTile",
        "powerButton",
        "refreshButton",
        "homeButton",
        "muteButton",
        "sleepTimerButton",
        "exitButton",
        "volumeUpButton",
        "hdmi1Button",
        "video1Button",
        "channelUpButton",
        "hdmi2Button",
        "video2Button",
        "volumeDownButton",
        "hdmi3Button",
        "analogButton",
        "channelDownButton",
        "hdmi4Button",
        "inputButton",
        "netflixButton",
        "vuduButton",
        "hboButton",
        "youTubeButton",
        "disneyButton",
        "wweButton",
        "playButton",
        "pauseButton",
        "upButton",
        "stopButton",
        "returnButton",
        "rewindButton",
		"fastforwardButton",
        "emptyButtonSmall",
        "emptyButtonSmall",
        "leftButton",
        "centerButton",
        "rightButton",
        "emptyButtonLarge",
        "downButton",
        "emptyButtonLarge"
        ])
        /* Not used
        "discoverButton",
        "previousButton",
		"nextButton",
        "tvButton"
        "applicationLauncherButton",
        */
  	}

    preferences {
        input("tvIP", "string", title:"TV IP Address", description: "", required: true, displayDuringSetup: false)
        input("tvPort", "string", title:"TV Port", description: "", required: true, displayDuringSetup: false)
        input("tvPSK", "string", title:"TV PSK Passphrase", description: "", required: true, displayDuringSetup: false)
	}
}

/* Method is called automatically when installed */
def installed() {
	resetState()
    refresh()
}

/* Method is called automatically when preferences are updated */
def updated(){
	resetState()
    refresh()
}

/* Method is called automatically approximately every 5 minutes */
def poll() {
    state.tvPollCount = (state.tvPollCount + 1)
    
	getPowerStatus([callback: pollGetPowerStatusCallBack])

    // If the TV has been polled more than once without a response, assume it is off
  	if (state.tvPollCount > 1 ) {
        state.tvStatus = "off"
        sendEvent(name: "switch", value: state.tvStatus)
    }
}

/*Method is called automatically as a result of calling HubAction(), unless a callback is assigned*/
def parse(description) {
    Map response = parseLanMessage(description)

    if (response){
    	parseResponse(response)
    }
}

def refresh() {
	setConfiguration()
    poll()
}

def on() {
    state.tvStatus = "on"
    sendEvent(name: "switch", value: state.tvStatus)
    setPowerStatus("true", [callback: sendCommandCallBack])
}

def off() {
    state.tvStatus = "off"
  	sendEvent(name: "switch", value: state.tvStatus)
    setPowerStatus("false", [callback: sendCommandCallBack])
}

def setLevel(level){
    // Maximum volume level to prevent damage
    if (level > 70){
    	level = 70
    }
    
    state.tvVolumeLevel = level.intValue()
    state.tvMuteStatus = "false"
    
    sendEvent(name: "level", value: state.tvVolumeLevel)
    sendEvent(name: "mute", value: state.tvMuteStatus)
    setSpeakerVolume(level.intValue(),[callback: sendCommandCallBack])
}

private setConfiguration(){
    state.tvIP = "${tvIP}"
	state.tvPort = "${tvPort}"
    state.tvPSK = "${tvPSK}"
    state.tvIPHex = state.tvIP.tokenize('.').collect{String.format('%02x', it.toInteger())}.join()
    state.tvPortHex = state.tvPort.tokenize('.').collect {String.format('%04x', it.toInteger())}.join()
    state.tvDeviceNetworkID = ("${state.tvIPHex}:${state.tvPortHex}")
    
    if (device.currentValue("switch") == "on"){
    	getCurrentExternalInputsStatus([:])
    	getApplicationList([:])
    }
}

private parseResponse(Map response){
	Map responseJSON = [:]
    int responseID = 0
    
    if(response.status == 200){
    	if (response.json?.id){
        	responseID = response.json.id.toInteger()
       		responseJSON =  response.json

            if (responseID == getGetPowerStatusCommandID()) {
                parseGetPowerStatusResponseJSON(responseJSON)
            }
            
            if (responseID == getSetPowerStatusCommandID()) {
                parseSetPowerStatusResponseJSON(responseJSON)
            }

            if (responseID == getGetVolumeInformationCommandID()) {
                parseGetVolumeInformationResponseJSON(responseJSON)
            }

            if (responseID == getGetPlayingContentCommandID()) {
                parseGetPlayingContentResponseJSON(responseJSON)
            }

            if (responseID == getGetCurrentExternalInputsStatusCommandID()) {  
                parseGetCurrentExternalInputsStatusResponseJSON(responseJSON)
            }

            if (responseID == getGetApplicationListCommandID()){
                parseGetApplicationListResponseJSON(responseJSON)
            }

            if (responseID == getSetSpeakerVolumeCommandID()){
                parseSetSpeakerVolumeResponseJSON(responseJSON)
            }

            if (responseID == getSetActiveAppCommandID()){
                parseSetActiveAppResponseJSON(responseJSON)
            }   
        }
    } else{
    	log.debug("ERROR:response:{$response}")
    }
}

def sendCommandCallBack(physicalgraph.device.HubResponse hubResponse){
    Map response = transformHubResponse(hubResponse)
    parseResponse(response)
    poll()  
}

def pollGetPowerStatusCallBack(physicalgraph.device.HubResponse hubResponse){
    Map response = transformHubResponse(hubResponse)
    parseResponse(response)
    
    if (device.currentValue("switch") == "on"){
        getVolumeInformation([:])
        getPlayingContentInformation([:])
    } else{
        state.tvVolumeLevel = 0
    	state.tvMuteStatus = "false"
        state.playingContentURI = ""
        state.playingContent = "TV Off"
    	sendEvent(name: "level", value: state.tvVolumeLevel)
    	sendEvent(name: "mute", value: state.tvMuteStatus)
        sendEvent(name: "input", value: state.playingContent)
    }
}

private transformHubResponse(physicalgraph.device.HubResponse hubResponse){
    Map response = [:]
	response.put("status", hubResponse.status)
    response.put("json", hubResponse.json)
    return response
}

private getPowerStatus(Map callBack){
  	String messageBody = "{\"id\":${getGetPowerStatusCommandID()},\"method\":\"getPowerStatus\",\"version\":\"1.0\",\"params\":[]}" 
  	sendSystemCommand(messageBody, callBack)
}

private setPowerStatus(String powerStatus, Map callBack){
  	String messageBody = "{\"id\":${getSetPowerStatusCommandID()},\"method\":\"setPowerStatus\",\"version\":\"1.0\",\"params\":[{\"status\":${powerStatus}}]}"
  	sendSystemCommand(messageBody, callBack)
}   

private parseGetPowerStatusResponseJSON(Map powerStatusInformationJSON){
    ArrayList powerStatusInformation = powerStatusInformationJSON.result
    
    state.tvPollCount = 0
	if (powerStatusInformation){
        if (powerStatusInformation[0].status == "active"){
            state.tvStatus = "on"
        } else{
            state.tvStatus = "off"
        }
        sendEvent(name: "switch", value: state.tvStatus)
    }
}

private parseSetPowerStatusResponseJSON(Map responseJSON){
	// No response parsing required
}

private sendSystemCommand(String messageBody, Map callBack) {
    def hubActionResult = new physicalgraph.device.HubAction(
    		method: 	"POST",
    		path: 		"/sony/system",
    		body: 		messageBody,
    		headers: 	[
						"Host":			"${state.tvIP}:${state.tvPort}", 
						"Content-Type": "application/json",
                        "X-Auth-PSK":	"${state.tvPSK}"
						], null, callBack
	)     
    sendHubCommand(hubActionResult)
}

private getVolumeInformation(Map callBack){
  	String messageBody = "{\"id\":${getGetVolumeInformationCommandID()},\"method\":\"getVolumeInformation\",\"version\":\"1.0\",\"params\":[]}" 
  	sendAudioCommand(messageBody, callBack)
}

private setSpeakerVolume(int volumeLevel, Map callBack){
	String messageBody = "{\"id\":${getSetSpeakerVolumeCommandID()},\"method\":\"setAudioVolume\",\"version\":\"1.2\",\"params\":[{\"volume\":\"${volumeLevel}\",\"ui\":\"on\",\"target\":\"speaker\"}]}" 
	sendAudioCommand(messageBody, callBack)
}

private parseGetVolumeInformationResponseJSON(Map volumeInformationJSON){
    int volumeInformationLength = 0
    ArrayList volumeInformation = volumeInformationJSON.result
  
    if (volumeInformation){
        volumeInformationLength = volumeInformation[0].target.size()

        for (int i = 0; i < volumeInformationLength; i++){
            if (volumeInformation[0].target[i] == "speaker"){
                state.tvVolumeLevel = volumeInformation[0].volume[i]
                state.tvMuteStatus = volumeInformation[0].mute[i]
            }
        }
    } else{
        state.tvVolumeLevel = 0
        state.tvMuteStatus = "false"
    }
    
    sendEvent(name: "level", value: state.tvVolumeLevel)
    sendEvent(name: "mute", value: state.tvMuteStatus)
}

private parseSetSpeakerVolumeResponseJSON(Map responseJSON){
	// No response parsing required
}

private sendAudioCommand(String messageBody, Map callBack) {
    def hubActionResult = new physicalgraph.device.HubAction(
    		method: 	"POST",
    		path: 		"/sony/audio",
    		body: 		messageBody,
    		headers: 	[
						"Host":			"${state.tvIP}:${state.tvPort}", 
						"Content-Type": "application/json",
                        "X-Auth-PSK":	"${state.tvPSK}"
						], null, callBack
	)     
    sendHubCommand(hubActionResult)
}

private getPlayingContentInformation(Map callBack){
  	String messageBody = "{\"id\":${getGetPlayingContentCommandID()},\"method\":\"getPlayingContentInfo\",\"version\":\"1.0\",\"params\":[]}" 
  	sendAVCommand(messageBody, callBack)
}

private getCurrentExternalInputsStatus(Map callBack){
	String messageBody = "{\"id\":${getGetCurrentExternalInputsStatusCommandID()},\"method\":\"getCurrentExternalInputsStatus\",\"version\":\"1.1\",\"params\":[]  }" 
 	sendAVCommand(messageBody, callBack)
}

private parseGetPlayingContentResponseJSON(Map activeSourceInformationJSON){
	ArrayList activeSourceInformation = activeSourceInformationJSON.result

    if (activeSourceInformation)
    {
        // Analog URI is not returned from GetCurrentExternalInputsStatus so it has to be handled directly 
        if (activeSourceInformation[0].uri.startsWith("tv:analog?channel="))
        {
            state.playingContentURI = ""
            state.playingContent = "Analog"
        } else{
            state.playingContentURI = activeSourceInformation[0].uri 
            state.playingContent = state.externalInput["${state.playingContentURI}"]
        }
    } else{
        state.playingContentURI = ""
        state.playingContent = "Android TV"
    }
    
    sendEvent(name: "input", value: state.playingContent)
}

private parseGetCurrentExternalInputsStatusResponseJSON(Map externalInputInformationJSON){
    int externalInputInformationLength = 0
    String externalInputLabel = ""
	ArrayList externalInputInformation = externalInputInformationJSON.result
    Map externalInput = [:]
	
    if (externalInputInformation)
    {
        externalInputInformationLength = externalInputInformation[0].uri.size()

        for (int i = 0; i < externalInputInformationLength; i++){
            if (externalInputInformation[0].label[i])
            {
                externalInputLabel = externalInputInformation[0].label[i]
            } else{
                externalInputLabel = externalInputInformation[0].title[i]
            }
            externalInput.put(externalInputInformation[0].uri[i], externalInputLabel)
        }

        state.externalInput = externalInput
    }
}
    
private sendAVCommand(String messageBody, Map callBack) {
    def hubActionResult = new physicalgraph.device.HubAction(
    		method: 	"POST",
    		path: 		"/sony/avContent",
    		body: 		messageBody,
    		headers: 	[
						"Host":			"${state.tvIP}:${state.tvPort}", 
						"Content-Type": "application/json",
                        "X-Auth-PSK":	"${state.tvPSK}"
						], null, callBack
	)     
    sendHubCommand(hubActionResult)
}

private getApplicationList(Map callBack){
    String messageBody = "{\"id\":${getGetApplicationListCommandID()},\"method\":\"getApplicationList\",\"version\":\"1.0\",\"params\":[]  }" 
    sendAppControlCommand(messageBody, callBack)	
}

private setActiveApp(String applicationURI, Map callBack){
    String messageBody = "{\"id\":${getSetActiveAppCommandID()},\"method\":\"setActiveApp\",\"version\":\"1.0\",\"params\":[{\"uri\":\"${applicationURI}\"}]}" 
    sendAppControlCommand(messageBody, callBack)
}

private parseGetApplicationListResponseJSON(Map applicationListInformationJSON){
    int applicationListInformationLength = 0
    Map applicationList = [:]
    ArrayList applicationListInformation = applicationListInformationJSON.result

    if (applicationListInformation)
    {
        applicationListInformationLength = applicationListInformation[0].uri.size()

        for (int i = 0; i < applicationListInformationLength; i++){
            if (applicationListInformation[0].title[i] == "WWE" || applicationListInformation[0].title[i] == "HBO Max" || applicationListInformation[0].title[i] == "VUDU" || applicationListInformation[0].title[i] == "Disney+"){
                applicationList.put(applicationListInformation[0].title[i],applicationListInformation[0].uri[i])
            }
        }
        state.applicationList = applicationList
    } 
}

private parseSetActiveAppResponseJSON(Map activeAppInformation){
	// No response parsing required
}

private sendAppControlCommand(String messageBody, Map callBack) {
    def hubActionResult = new physicalgraph.device.HubAction(
    		method: 	"POST",
    		path: 		"/sony/appControl",
    		body: 		messageBody,
    		headers: 	[
						"Host":			"${state.tvIP}:${state.tvPort}", 
						"Content-Type": "application/json",
                        "X-Auth-PSK":	"${state.tvPSK}"
						], null, callBack
	)
    sendHubCommand(hubActionResult)
}

private sendIRCCCommand(rawCommand, Map callBack){
	String body = "<?xml version=\"1.0\" encoding=\"utf-8\"?><s:Envelope xmlns:s=\"http://schemas.xmlsoap.org/soap/envelope/\" s:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\"><s:Body><u:X_SendIRCC xmlns:u=\"urn:schemas-sony-com:service:IRCC:1\"><IRCCCode>${rawCommand}</IRCCCode></u:X_SendIRCC></s:Body></s:Envelope>"
    
    def hubActionResult = new physicalgraph.device.HubAction(
    		method: 	"POST",
    		path: 		"/sony/IRCC",
    		body: 		body,
    		headers: 	[
						"Host":				"${state.tvIP}:${state.tvPort}", 
						"Content-Type": 	"text/xml; charset=\"utf-8\"",
                        "X-Auth-PSK":		"${state.tvPSK}",
                        "SOAPAction":		"\"urn:schemas-sony-com:service:IRCC:1#X_SendIRCC\"",
                        "Content-Length":	body.length(),
						], null, callBack
	)
    sendHubCommand(hubActionResult)
}

private resetState() {
    state.tvPollCount = 0
    state.tvVolumeLevel = 0
    state.tvMuteStatus = "false"
	state.tvStatus = "off"
	state.tvMacAddress = ""
	state.playingContentURI = ""
    state.playingContent= ""
	state.externalInput = [:]
	state.applicationList = [:]	    
    state.tvIP = ""
	state.tvPort = ""
    state.tvPSK = ""
    state.tvIPHex = ""
    state.tvPortHex = ""
    state.tvDeviceNetworkID = ""
}

/* Message ID constants */
private getSetPowerStatusCommandID(){
	return 1
}

private getGetPowerStatusCommandID() {
    return 2
}

private getGetVolumeInformationCommandID() {
    return 3
}

private getGetPlayingContentCommandID() {
    return 4
}

private getGetCurrentExternalInputsStatusCommandID(){
	return 5
}

private getGetApplicationListCommandID(){
	return 6
}

private getSetSpeakerVolumeCommandID(){
	return 7
}

private getSetActiveAppCommandID(){
	return 8
}

def powerButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAAVAw==", [callback: sendCommandCallBack])
}

def volumeUpButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAASAw==", [callback: sendCommandCallBack])
}

def volumeDownButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAATAw==", [callback: sendCommandCallBack])
}

def muteButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAAUAw==", [callback: sendCommandCallBack])
}

def channelUpButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAAQAw==", [:])
}

def channelDownButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAARAw==", [:])
}

def sleepTimerButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAA2Aw==", [:])
}

def applicationLauncherButton(){
	sendIRCCCommand("AAAAAgAAAMQAAAAqAw==", [:])
}

def discoverButton(){
	sendIRCCCommand("AAAAAgAAABoAAABzAw==", [:])
}

def homeButton(){
	sendIRCCCommand("AAAAAQAAAAEAAABgAw==", [:])
}

def returnButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAAjAw==", [:])
}

def exitButton(){
	sendIRCCCommand("AAAAAQAAAAEAAABjAw==", [:])
}

def upButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAB0Aw==", [:])
}

def rightButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAAzAw==", [:])
}

def downButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAB1Aw==", [:])
}

def leftButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAA0Aw==", [:])
}

def centerButton(){
	sendIRCCCommand("AAAAAgAAAJcAAABKAw==", [:])
}

def inputButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAAlAw==", [:])
    
    // Unable to handle refreshing UI on a callback because the input command is a menu that has multiple ways to change the input (center button, no button, etc).  Assume user makes selection within 10 seconds.
    runIn(10,poll)
}

def analogButton(){
	sendIRCCCommand("AAAAAgAAAHcAAAANAw==", [callback: sendCommandCallBack])
}

def hdmi1Button(){
	sendIRCCCommand("AAAAAgAAABoAAABaAw==", [callback: sendCommandCallBack])
}

def hdmi2Button(){
	sendIRCCCommand("AAAAAgAAABoAAABbAw==", [callback: sendCommandCallBack])
}

def hdmi3Button(){
	sendIRCCCommand("AAAAAgAAABoAAABcAw==", [callback: sendCommandCallBack])
}

def hdmi4Button(){
	sendIRCCCommand("AAAAAgAAABoAAABdAw==", [callback: sendCommandCallBack])
}

def video1Button(){
	sendIRCCCommand("AAAAAQAAAAEAAABAAw==", [callback: sendCommandCallBack])
}

def video2Button(){
	sendIRCCCommand("AAAAAQAAAAEAAABBAw==", [callback: sendCommandCallBack])
}

def tvButton(){
	sendIRCCCommand("AAAAAQAAAAEAAAAkAw==", [callback: sendCommandCallBack])
}

def playButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAAaAw==", [:])
}

def pauseButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAAZAw==", [:])
}

def rewindButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAAbAw==", [:])
}

def fastforwardButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAAcAw==", [:])
}

def previousButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAA8Aw==", [:])
}

def nextButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAA9Aw==", [:])
}

def stopButton(){
	sendIRCCCommand("AAAAAgAAAJcAAAAYAw==", [:])
}

def netflixButton(){
	sendIRCCCommand("AAAAAgAAABoAAAB8Aw==", [callback: sendCommandCallBack])
}

def youTubeButton(){
	sendIRCCCommand("AAAAAgAAAMQAAABHAw==", [callback: sendCommandCallBack])
}

def vuduButton(){
   	setActiveApp(state.applicationList["VUDU"], [callback: sendCommandCallBack])
}

def hboButton(){
   	setActiveApp(state.applicationList["HBO Max"], [callback: sendCommandCallBack])
}

def disneyButton(){
	setActiveApp(state.applicationList["Disney+"], [callback: sendCommandCallBack])
}

def wweButton(){
    setActiveApp(state.applicationList["WWE"], [callback: sendCommandCallBack])
}