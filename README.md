# TAPO-Robovac-Dev
TAPO Robovac Development with login protocol and validated methods and responses

## Communications Notes
* HTTPS, you will need to ignore SSL Issues.
* Command transmitted as JSON.  In hubitat I use a Hubitat command httpPostJson (so they handle headers)
* Parameters for https command (packaged as MAP)
  
  a.  uri - see lower notes
  
  b.  ignoerSSLIssues (Hubitat specific nomenclature)
  
  c.  body (in Hubitat, JSON data)
  
* Hubitat command: httpPostJson(parameters)
  
## Login Notes
* username: no encoding.
* password: encoded MD5, converted to Hex, converted to UPPERCASE
* uri: "https://${deviceIp}:4433"
* body: [method: "login", params: [hashed: true, password: encodedPassword, username: username]]
* Return Data includes the TOKEN, used in device commands

## Device Commands Notes
* uri:   https://IP_ADDRESS:4433/?token=TOKEN
* example body: [method: "get_device_info"]

## Inital test results
Below are some initial test results of methods with the output data.  Format is METHOD, HTTP STATUS, DEVICE RESPONES.
* If the HTTP Status is 200, and device response error_code is 0, the response if OK.
* If the response error_code is 9999, login again.

### Explicit results

[command:[method:get_device_info], data:[status:200, response:[result:[device_id:80374FB4607598FCD43E7F738B6A4378206F816C, fw_ver:1.0.9 Build 230612 Rel.170558, hw_ver:1.0, type:SMART.TAPOROBOVAC, model:RV10, mac:AC-15-A2-2D-A9-40, hw_id:472DEE7C094077B944FB5C60F60EA7B7, fw_id:00000000000000000000000000000000, oem_id:9F92BF137602D0E1386F0E86F709EF72, overheated:false, ip:192.168.50.63, time_diff:-360, ssid:REpHXzIuNEc=, rssi:-49, signal_level:3, latitude:331351, longitude:-968918, lang:, avatar:, region:America/Chicago, specs:, nickname:Um9ib3QgVmFjdXVt, location:, has_set_location_info:true], error_code:0]]]

[command:[method:set_device_info, params:[nickname:vacuum]], data:[status:200, response:[error_code:0]]]	//NOTE:  You can typically change many of the get_device_info values.  This is the most useful here.

[command:[method:get_device_time], data:[status:200, response:[result:[time_diff:-360, timestamp:1698931331, region:America/Chicago], error_code:0]]]

[command:[method:get_connect_cloud_state], data:[status:200, response:[result:[status:0], error_code:0]]]

[command:[method:get_countdown_rules], data:[status:200, response:[result:[enable:false, countdown_rule_max_count:1, rule_list:[]], error_code:0]]]	//NOTE:  Indicates that rules are supported.  I will not investigate this further.

[command:[method:get_device_running_info], data:[status:200, response:[result:[device_id:80374FB4607598FCD43E7F738B6A4378206F816C, fw_ver:1.0.9 Build 230612 Rel.170558, overheated:false, ip:192.168.50.63, signal_level:3, rssi:-49, latitude:331351, longitude:-968918, lang:, avatar:, region:America/Chicago, specs:, nickname:vacuum, location:, has_set_location_info:true], error_code:0]]]

[command:[method:get_fw_download_state], data:[status:200, response:[result:[status:0, download_progress:0, reboot_time:5, upgrade_time:5, auto_upgrade:false], error_code:0]]]

[command:[method:get_inherit_info], data:[status:200, response:[result:[inherit_status:false], error_code:0]]]

[command:[method:getCleanMode], data:[status:200, response:[result:[clean_mode:3], error_code:0]]]

TO DO: setCleanMode

[command:[method:getCleanInfo], data:[status:200, response:[result:[clean_time:1, clean_area:2], error_code:0]]]

TO DO: setCleanInfo

[command:[method:getRobotPauseTime], data:[status:200, response:[result:[pause_min:0], error_code:0]]]

[command:[method:getSwitchClean], data:[status:200, response:[result:[clean_on:false], error_code:0]]]

TO DO: setSwitchClean

[command:[method:getVacStatus], data:[status:200, response:[result:[status:6, err_status:[], errorCode_id:[], prompt:[], promptCode_id:[]], error_code:0]]]

TO DO: setVacStatus

[command:[method:getCleanStatus], data:[status:200, response:[result:[clean_status:0, is_working:false], error_code:0]]]

TO DO: setCleanStatus

[command:[method:getCleanRecords], data:[status:200, response:[result:[record_list:[], lastest_day_record:[0, 0, 0, 0], total_time:0, total_area:0, total_number:0, record_list_num:0], error_code:0]]]

[command:[method:device_reboot], data:[status:200, response:[error_code:0]]]

[command:[method:getCarpetClean], data:[status:200, response:[result:[carpet_clean_prefer:boost], error_code:0]]]

[command:[method:setCarpetClean, params:[carpet_clean_prefer:normal]], data:[status:200, response:[error_code:0]]]	//Note: carpet_clean_prefer = boost, normal

[command:[method:getCleanNumber], data:[status:200, response:[result:[suction:2, clean_number:2, cistern:2], error_code:0]]]

[command:[method:setCleanNumber, params:[clean_number:2]], data:[status:200, response:[error_code:0]]]	//clean_number = 1,2,3.  Is number of clean passes for vac.

[command:[method:getChildLockInfo], data:[status:200, response:[result:[child_lock_status:false], error_code:0]]]










