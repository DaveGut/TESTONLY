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
* If the HTTP Status is 200, and device response error_code is 0, the response is OK.
* If the response error_code is 9999, login again.

### Explicit results

[command:[method:multipleRequest, params:[requests:[[method:setCleanSuction, params:[suction_level:2, clean_number:2, cistern:1]], [method:getCleanSuction]]]], data:[status:200, response:[result:[responses:[[method:setCleanSuction, error_code:0], [method:getCleanSuction, result:[suction:2, clean_number:2, cistern:1], error_code:0]]], error_code:0]]]

[command:[method:multipleRequest, params:[requests:[[method:setCleanNumber, params:[suction_level:1, clean_number:1, cistern:2]], [method:getCleanNumber]]]], data:[status:200, response:[result:[responses:[[method:setCleanNumber, error_code:0], [method:getCleanNumber, result:[suction:1, clean_number:1, cistern:2], error_code:0]]], error_code:0]]

[command:[method:setDoNotDisturb, params:[s_min:1300, e_min:510, do_not_disturb:true]], data:[status:200, response:[result:[:], error_code:0]]]

[command:[method:getDoNotDisturb], data:[status:200, response:[result:[s_min:1300, e_min:510, do_not_disturb:true], error_code:0]]]

[command:[method:getWirelessConnectedStatus], data:[status:200, response:[result:[status:connected, ssid:ABCDEF, key_type:none, signal_level:3], error_code:0]]]

[command:[method:getVolume], data:[status:200, response:[result:[volume:0], error_code:0]]]
(No volume on my device)

[command:[method:setCliffDetectMode, params:[cliff_detect_mode:1]], data:[status:200, response:[error_code:0]]]

[command:[method:getCliffDetectMode], data:[status:200, response:[result:[cliff_detect_mode:1], error_code:0]]]

[command:[method:getConsumablesInfo], data:[status:200, response:[result:[edge_brush_time:11, roll_brush_time:3, filter_time:3, sensor_time:11], error_code:0]]]

[command:[method:getDustCollectionInfo], data:[status:200, response:[result:[auto_dust_collection:true, dust_collection_mode:0], error_code:0]]]

[command:[method:getMopState], data:[status:200, response:[result:[mop_state:false], error_code:0]]]

[command:[method:setSwitchCharge, params:[switch_charge:true]], data:[status:200, response:[error_code:0]]]

[command:[method:getSwitchCharge], data:[status:200, response:[result:[switch_charge:false], error_code:0]]]
(VAC was already fully charged)

[command:[method:setSwitchDustCollection, params:[switch_dust_collection:true]], data:[status:200, response:[error_code:-3013]]]

[command:[method:getSwitchDustCollection], data:[status:200, response:[result:[switch_dust_collection:false], error_code:0]]]
(No BIN on my device)

[command:[method:setAreaUnit, params:[area_unit:1]], data:[status:200, response:[error_code:0]]]

[command:[method:getAreaUnit], data:[status:200, response:[result:[area_unit:1], error_code:0]]]

[command:[method:getBatteryInfo], data:[status:200, response:[result:[battery_percentage:100], error_code:0]]]

[command:[method:get_device_info], data:[status:200, response:[result:[device_id:80377598FCD43E7F738B6A4378206, fw_ver:1.0.9 Build 230612 Rel.170558, hw_ver:1.0, type:SMART.TAPOROBOVAC, model:RV10, mac:AC-15-A2-2D-A9-40, hw_id:472DEE7C094077B944FB5C60F60EA7B7, fw_id:00000000000000000000000000000000, oem_id:9F92BF137602D0E1386F0E86F709EF72, overheated:false, ip:192.168.50.63, time_diff:-360, ssid:REpHXzIuNEc=, rssi:-49, signal_level:3, latitude:331351, longitude:-968918, lang:, avatar:, region:America/Chicago, specs:, nickname:Um9ib3QgVmFjdXVt, location:, has_set_location_info:true], error_code:0]]]

[command:[method:set_device_info, params:[nickname:vacuum]], data:[status:200, response:[error_code:0]]]	//NOTE:  You can typically change many of the get_device_info values.  This is the most useful here.

[command:[method:get_device_time], data:[status:200, response:[result:[time_diff:-360, timestamp:1698931331, region:America/Chicago], error_code:0]]]

[command:[method:get_connect_cloud_state], data:[status:200, response:[result:[status:0], error_code:0]]]

[command:[method:get_countdown_rules], data:[status:200, response:[result:[enable:false, countdown_rule_max_count:1, rule_list:[]], error_code:0]]]	//NOTE:  Indicates that rules are supported.  I will not investigate this further.

[command:[method:get_device_running_info], data:[status:200, response:[result:[device_id:80374FB4607598FCD43E7F738B6A4378206F816C, fw_ver:1.0.9 Build 230612 Rel.170558, overheated:false, ip:192.168.50.63, signal_level:3, rssi:-49, latitude:331351, longitude:-968918, lang:, avatar:, region:America/Chicago, specs:, nickname:vacuum, location:, has_set_location_info:true], error_code:0]]]

[command:[method:get_fw_download_state], data:[status:200, response:[result:[status:0, download_progress:0, reboot_time:5, upgrade_time:5, auto_upgrade:false], error_code:0]]]

[command:[method:get_inherit_info], data:[status:200, response:[result:[inherit_status:false], error_code:0]]]

[command:[method:setCleanMode, params:[clean_mode:3]], data:[status:200, response:[error_code:0]]]

[command:[method:getCleanMode], data:[status:200, response:[result:[clean_mode:3], error_code:0]]]

[command:[method:getCleanInfo], data:[status:200, response:[result:[clean_time:1, clean_area:2], error_code:0]]]

[command:[method:getRobotPauseTime], data:[status:200, response:[result:[pause_min:0], error_code:0]]]

[command:[method:setSwitchClean, params:[clean_on:false, clean_mode:2, forceClean:true]], data:[status:200, response:[error_code:0]]]

[command:[method:getSwitchClean], data:[status:200, response:[result:[clean_on:false], error_code:0]]]

[command:[method:getVacStatus], data:[status:200, response:[result:[status:6, err_status:[], errorCode_id:[], prompt:[], promptCode_id:[]], error_code:0]]]

[command:[method:getCleanStatus], data:[status:200, response:[result:[clean_status:0, is_working:false], error_code:0]]]

[command:[method:getCleanRecords], data:[status:200, response:[result:[record_list:[[error:1, clean_time:1, clean_area:0, dust_collection:false, timestamp:1699020294, start_type:0, task_type:2, record_index:0]], lastest_day_record:[1699020294, 1, 0, 1], total_time:1, total_area:0, total_number:1, record_list_num:1], error_code:0]]]

[command:[method:device_reboot], data:[status:200, response:[error_code:0]]]

[command:[method:getCarpetClean], data:[status:200, response:[result:[carpet_clean_prefer:boost], error_code:0]]]

[command:[method:setCarpetClean, params:[carpet_clean_prefer:normal]], data:[status:200, response:[error_code:0]]]	//Note: carpet_clean_prefer = boost, normal

[command:[method:getChildLockInfo], data:[status:200, response:[result:[child_lock_status:false], error_code:0]]]

