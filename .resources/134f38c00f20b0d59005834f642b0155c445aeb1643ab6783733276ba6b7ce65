#Libraries
import time



# Function to find the value of 'Serial' for each door using tag path
def find_serial(tag_path):
	#Amount of doors to check for serial number
    doors = ["Door_0", "Door_1", "Door_2", "Door_3", "Door_4", "Door_5", "Door_6", "Door_7", "Door_8", "Door_9", "Door_10",
             "Door_11", "Door_12", "Door_13", "Door_14", "Door_15", "Door_16", "Door_17", "Door_18", "Door_19", "Door_20",
             "Door_21", "Door_22", "Door_23", "Door_24", "Door_25", "Door_26", "Door_27", "Door_28", "Door_29", "Door_30",
             "Door_31", "Door_32", "Door_33", "Door_34", "Door_35", "Door_36", "Door_37", "Door_38", "Door_39", "Door_40",
             "Door_41", "Door_42", "Door_43", "Door_44", "Door_45", "Door_46", "Door_47", "Door_48", "Door_49"]
    tag_values_list = []
    for door in doors:
        door_tag_path = "%s/Door/%s" %(tag_path, door)
        serial_tag_path = "%s/Serial" %door_tag_path
        serial_value = system.tag.read(serial_tag_path).value
        if serial_value != '':
        	tag_values_list.append(serial_value)
    return tag_values_list
    
    
    
def find_serial_kepware(tag_path):
	#Amount of doors to check for serial number
	doors = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 
		18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 
		35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50]
	
	tag_values_list = []
	for door in doors:
		door_tag_path = "%s/Door/%s" %(tag_path, door)
		serial_tag_path = "%s/Serial" %door_tag_path
		serial_value = system.tag.read(serial_tag_path).value
		if serial_value != '':
			tag_values_list.append(serial_value)
	return tag_values_list



def Perform_SP_Query(serial, location, sequence, pile, pileSequence):
	params = {'pile':pile, 'serial':serial, 'sequence':sequence, 'location':location, 'pileSequence':pileSequence}
	results = system.db.runNamedQuery('Press_Infeed/UpdatePileLocation', params)
	
	
	
def Perform_SP_TagLog_Query(triggerGroup, ipAddress, tagName, tagValue):
	params = {'group':triggerGroup, 'ip':ipAddress, 'name':tagName, 'value':tagValue}
	results = system.db.runNamedQuery('AGTC_TagLogging/AGTC_TagLogging', params)
	
	
	
def getSplit(tagpath):
	import re
	sec_a = 'Press_Infeed'
	sec_b = 'DET_Rollerbeds'
	sec_c = 'Manual_Rollerbeds'
	sec_d = 'Press_2'
	sec_e = 'Press_3'
	sec_f = 'Press_Auxiliary_Conveyors'
	sec_g = 'Press_Backfill_RB'
	sec_h = 'PressIF_TransferCart'
	sec_i = 'PressOF_TransferCart'

	aMatch = re.search(sec_a, tagpath, re.IGNORECASE)
	bMatch = re.search(sec_b, tagpath, re.IGNORECASE)
	cMatch = re.search(sec_c, tagpath, re.IGNORECASE)
	dMatch = re.search(sec_d, tagpath, re.IGNORECASE)
	eMatch = re.search(sec_e, tagpath, re.IGNORECASE)
	fMatch = re.search(sec_f, tagpath, re.IGNORECASE)
	gMatch = re.search(sec_g, tagpath, re.IGNORECASE)
	hMatch = re.search(sec_h, tagpath, re.IGNORECASE)
	iMatch = re.search(sec_i, tagpath, re.IGNORECASE)
	if aMatch:
		original = tagpath.split('[default]Press_Infeed/AGTC_')
		return original[1]
	elif bMatch:
		original = tagpath.split('[default]DET_Rollerbeds/AGTC_')
		return original[1]
	elif cMatch:
		original = tagpath.split('[default]Manual_Rollerbeds/')
		return original[1]
	elif dMatch:
		original = tagpath.split('[default]Press_2/AGTC_')
		return original[1]
	elif eMatch:
		original = tagpath.split('[default]Press_3/AGTC_')
		return original[1]
	elif fMatch:
		original = tagpath.split('[default]Press_Auxiliary_Conveyors/AGTC_')
		return original[1]
	elif gMatch:
		original = tagpath.split('[default]Press_Backfill_RB/AGTC_')
		return original[1]
	elif hMatch:
		original = tagpath.split('[default]PressIF_TransferCart/')
		return original[1]
	elif iMatch:
		original = tagpath.split('[default]PressOF_TransferCart/')
		return original[1]
		
		
#this funtion takes a rollerbed name like 'AGTC_FPA10_1' and returns the area wehre it belongs. 
def getArea(name):
	query='TC_Setttings/TC_Settings_Read'	
	params={
		'name':name
	}
	result=system.db.runNamedQuery(query,params)
	if result.getRowCount() > 0:
		area=result.getValueAt(0,"Area")
		return str(area)
	else:
		raise Exception("No area found for the given name: " + name)
		
def getFullPath(partialpath):
	filterpath = '*' + partialpath + '*'
	filter ={'name':filterpath, 'recursive':True}
	findpath = system.tag.browse('[default]', filter)
	for path in findpath:
		fullpath = str(path['fullPath'])
		return fullpath
		
		
		
# Function to check if a tag is ready to load
def is_ready_load(tag_path):
	import system
	return system.tag.read(tag_path + '/TransComm/ReadyToLoad_PLCTOSM').value



# Function to check if a tag is ready to unload
def is_ready_unload(tag_path):
	import system
	return system.tag.read(tag_path + '/TransComm/ReadyToUnload_PLCTOSM').value



# Function to check if the transfer cart is ready
def is_TC_ready():
	import system
	return system.tag.read('[default]LSPF_TransferCart/TC_AGTC/TransComm/ReadyToLoad_PLCTOSM').value

def is_TC_ready_test():
	import system
	return system.tag.read('[default]testcarReady').value
	
	
# Function to log auto transfers
def transfer_test(source, sourcex, sourcey, destination, destinationx, destinationy,source_is_auto,dest_is_auto,s_path,d_path):
	parameters = {
	'source_path':source, 
	'sourcex':sourcex, 
	'sourcey':sourcey, 
	'destination_path':destination, 
	'destinationx':destinationx, 
	'destinationy':destinationy,
	'dest_is_auto':dest_is_auto,
	'source_is_auto':source_is_auto,
	's_path':s_path,
	'd_path':d_path
	}
	system.db.runNamedQuery('Transfer_Carts/TRANSFER_TEST', parameters)
	

# Function to get next o previous id given a ids list
def get_position(ids_list, id_, mov = "up"):
	current_index = ids_list.index(id_)
	first_id = ids_list[0]
	last_id = ids_list[len(ids_list) -1]
	
	if mov == "up" and id_ != first_id:
		return ids_list[current_index - 1]
	elif mov == "down" and id_ != last_id:
		return ids_list[current_index + 1]
	else:
		return None


def destination_state():
	results = system.db.runNamedQuery('Transfer_Carts/Queue/Infeed_Queue')
	for row in range(results.rowCount):
		dest1 = results.getValueAt(row, 'Destination1')
		if dest1 != '':
			return True
	return False	



#This function is used in timer scrip TC carts to get the first ready movement with a destination ready to load.
def queue_select(result):
	lista=[]
	for i in range(len(result)):
		dest1=result.getValueAt(i,'Destination1')
		dest2=result.getValueAt(i,'Destination2')
		if dest1 or dest2:
			lista.append(i)
	if lista:
		return lista[0] #Ensure there's at leat one item
	else:
		return None #Return None if no items meets the condition

#Function to get destination movement
	
def get_destination_path(path1,path2):
	if path2 is None or path2 == ' ' or '':
		if system.tag.exists(path1+'/TransComm/ReadyToLoad_PLCTOSM') is False:
			return path1
		elif system.tag.exists(path1+'/TransComm/ReadyToLoad_PLCTOSM') == True and system.tag.read(path1+'/TransComm/ReadyToLoad_PLCTOSM').value == True:
			return path1
		else:
			return None
	else:	
		if system.tag.exists(path2+'/TransComm/ReadyToLoad_PLCTOSM') is False:
		 	return path2 
		elif system.tag.exists(path1+'/TransComm/ReadyToLoad_PLCTOSM') and system.tag.exists(path2+'/TransComm/ReadyToLoad_PLCTOSM') is False:
			return path1
		elif system.tag.read(path1+'/TransComm/ReadyToLoad_PLCTOSM').value == False and system.tag.read(path2+'/ready_load').value == False:
			data= None
		elif system.tag.read(path1+'/TransComm/ReadyToLoad_PLCTOSM').value == True:
			return path1
		elif system.tag.read(path2+'/TransComm/ReadyToLoad_PLCTOSM').value == True:
			return path2
	

#check if source is ready to load this apply for manual an auto movements
def source_ready(path):
	auto=system.tag.read(path + '/Coordinate/Auto_State').value
	tagValue=system.tag.read(path + '/TransComm/ReadyToUnload_PLCTOSM').value
	if auto is False or tagValue is True:
		data = True
	else:
		data = False
	return data
	
#Get chart Parameter Pos_error
def pos_error(name):
	params={
	'name':name
	}
	result=system.db.runNamedQuery('TC_Setttings/TC_Pos_error_Read',params)
	Pos_error=result.getValueAt(0,'Semi_mode')
	return Pos_error
	
#Function to reset the SMTOPLC tags	
def reset_TC_tags(tc_path):
	lista =['/TransComm/InDestPos_SMTOPLC','/TransComm/InSourcePos_SMTOPLC','/TransComm/DestRollRun_SMTOPLC','/TransComm/SourceRollRun_SMTOPLC',
			'/TransComm/SourceXLocation_SMTOPLC', '/TransComm/SourceYDirection_SMTOPLC', '/TransComm/DestXLocation_SMTOPLC', 
			'/TransComm/DestYDirection_SMTOPLC','/TransComm/SourceIsAuto_SMTOPLC','/TransComm/DestIsAuto_SMTOPLC','/TransComm/ParkLocation_SMTOPLC']
	new_list=[tc_path+tag for tag in lista]
	values=[0] * len(new_list)
	system.tag.writeBlocking(new_list, values)

def reset_source(path):
	lista = ['/TransComm/SourceRollRun_SMTOPLC','/TransComm/InSourcePos_SMTOPLC']
	new_list=[path+tag for tag in lista]
	values=[0] * len(new_list)
	system.tag.writeBlocking(new_list, values)	

def reset_dest(path):
	lista = ['/TransComm/DestRollRun_SMTOPLC','/TransComm/InDestPos_SMTOPLC']
	new_list=[path+tag for tag in lista]
	values=[0] * len(new_list)
	system.tag.writeBlocking(new_list, values)
	
#*START****** functions for transfer array at SFC*************************
#if press 3 area = 3    other than that area = 1, array's number of elments,path from reading data
#Get the roller bed area to have the right paths 
def get_area_code(path):
	try:
		path_name=getSplit(path)
		path_area=getArea(path_name)
		if path_area == 'Press_3':
			return 3
		else:
			return 1
	except:
		return "This element was not found on TC area"

#read an array from source and create two list to transfer 
def read_array(area,items,path):
	lst_pile=[]
	lst_serial=[]
	for i in range(items):
		if area == 1:
			second_path='/Door/Door_'+str(i)
		elif area == 3:
			second_path='/Door/'+str(i+1)
		else:
			raise ValueError('Unsupported area value:' + str(area))
		
		pile_tag_path = path+second_path+'/PileNumber'
		serial_tag_path = path+second_path+'/Serial'
		pile_value = system.tag.read(pile_tag_path).value
		serial_value = system.tag.read(serial_tag_path).value
		lst_pile.append(pile_value)
		lst_serial.append(serial_value)
	if lst_pile[0]=='':
		lst_pile[0]=-1
		data={'pile_list':lst_pile,'serial_list':lst_serial}
	else:
		data={'pile_list':lst_pile,'serial_list':lst_serial}
	return data

#if press 3 area = 3    other than that area = 1,array's number of elments,path from reading data,data shoul come from read_array function.
def write_array(area,items,path,data):
	for i in range(items):
		if area == 1:
			second_path='/Door/Door_'+str(i)
		elif area == 3:
			second_path='/Door/'+str(i+1)
		pile_tag_path = path+second_path+'/PileNumber'
		serial_tag_path = path+second_path+'/Serial'
		system.tag.write(pile_tag_path, data['pile_list'][i])
		system.tag.write(serial_tag_path, data['pile_list'][i])
	
#if press 3 area = 3    other than that area = 1,array's number of elments,path from reading data,data should come from read_array function.
def write_array_zero(area,items,path):
	for i in range(items):
		if area == 1:
			second_path='/Door/Door_'+str(i)
		elif area == 3:
			second_path='/Door/'+str(i+1)
		pile_tag_path = path+second_path+'/PileNumber'
		serial_tag_path = path+second_path+'/Serial'
		system.tag.write(pile_tag_path,'')
		system.tag.write(serial_tag_path,'')

#this is main script for transfer the array from RB to TC or TC to RB works with fucntions get_area_code,read_array,write_array,write_array_zero
def transfer_array_data(source_path,dest_path,items):
	source_area=get_area_code(source_path)
	dest_area=get_area_code(dest_path)
	data=read_array(source_area,items,source_path)
	write_array(dest_area,items,dest_path,data)
	write_array_zero(source_area,items,source_path)
	
# Check pilenumber on first door of transfer cart to make sure its populated
def is_populated(tag_path):
    area = get_area_code(tag_path)
    if area == 1:
        return system.tag.read(tag_path + '/Door/Door_0/PileNumber').value != ''
    elif area == 3:
        return system.tag.read(tag_path + '/Door/Door_1/PileNumber').value != ''
    else:
        return 
   
	
#Back to empty if the array was written -1 by transfer_array_data function we need to have the array empty again  
def clean_array_1(path,no):
	area=Functions.get_area_code(path)
	if area == 1:
		valor=int(system.tag.read(path +'/Door/Door_0/PileNumber').value)
		if valor == '-1':
			Functions.write_array_zero(area,no,path)
		else:
			pass
	elif area == 3:
		valor=int(system.tag.read(path +'/Door/1/PileNumber').value)
		if valor == '-1':
			Functions.write_array_zero(area,no,path)
		else:
			pass
#*FINISH******functions for transfer array at SFC*************************


#*START****** functions ffor select movement ready on Infeed timer script*************************

#auxilary functions 
def is_auto(name):
	name_area = getArea(name)
	name_full_path = ('[default]'+name_area + '/AGTC_'+ name)
	is_auto=system.tag.read(name_full_path+'/Coordinate/Auto').value
	return is_auto
	
def is_dest_auto(dest1,dest2):
	dest1_area = getArea(dest1)
	dest1_full_path = ('[default]'+dest1_area + '/AGTC_'+ dest1)
	is_dest1_auto = system.tag.read(dest1_full_path+'/Coordinate/Auto').value
	if dest2 == None or dest2 == ' ' or dest2=='':
		is_dest2_auto = False
	else:
		dest2_area = getArea(dest2)
		dest2_full_path = ('[default]'+dest2_area + '/AGTC_'+ dest2)
		is_dest2_auto = system.tag.read(dest2_full_path+'/Coordinate/Auto').value
	return is_dest1_auto or is_dest2_auto


#secondary fucntions.
def check_auto_dest(dest1,dest2=None):
	dest1_area = getArea(dest1)
	dest1_full_path = ('[default]'+dest1_area + '/AGTC_'+ dest1)
	is_dest1_auto = system.tag.read(dest1_full_path+'/Coordinate/Auto').value
	dest1_ready=system.tag.read(dest1_full_path+'/TransComm/ReadyToLoad_PLCTOSM').value
	
	if dest2 == None:
		return (is_dest1_auto and dest1_ready)
		
	else:
		dest2_area = getArea(dest2)
		dest2_full_path = ('[default]'+dest2_area + '/AGTC_'+ dest2)
		is_dest2_auto = system.tag.read(dest2_full_path+'/Coordinate/Auto').value
		dest2_ready = system.tag.read(dest2_full_path+'/TransComm/ReadyToLoad_PLCTOSM').value
		return (is_dest1_auto and dest1_ready) or (is_dest2_auto and dest2_ready)

def check_ready_unload(source):
	source_area = getArea(source)
	if source_area == 'Manual_Rollerbeds':
		return True
	else:
		source_full_path = ('[default]'+source_area + '/AGTC_'+ source)
		source_ready=system.tag.read(source_full_path+'/TransComm/ReadyToUnload_PLCTOSM').value
		return source_ready

def check_ready_load(dest1,dest2):
	dest1_area = getArea(dest1)
	if dest1_area == 'Manual_Rollerbeds':
		return True
	else:
		dest1_full_path = ('[default]'+dest1_area + '/AGTC_'+ dest1)
		dest1_ready=system.tag.read(dest1_full_path+'/TransComm/ReadyToLoad_PLCTOSM').value
		if dest2 == None or dest2 == ' ' or dest2=='':
			dest2_ready = False
			return dest2_ready or dest1_ready
		else:
			dest2_area = getArea(dest2)
			if dest2_area == 'Manual_Rollerbeds':
				return True
			else:
				dest2_full_path = ('[default]'+dest2_area + '/AGTC_'+ dest2)
				dest2_ready = system.tag.read(dest2_full_path+'/TransComm/ReadyToLoad_PLCTOSM').value
				return dest2_ready or dest1_ready
		
	
#Main function to movements ready.
def get_movement_ready(result):
	for element in range(len(result)):
		#get source, dest1 and dest2 values
		source=result.getValueAt(element,'Source')
		dest1=result.getValueAt(element,'Destination1')
		dest2 = result.getValueAt(element,'Destination2')
		Pile=result.getValueAt(element,'PileNumber')
		
		#Apply Fucntions to check if auto is ready
		if Pile == "SEMI":
			source_ready=check_ready_unload(source)
			dest_ready=check_ready_load(dest1,dest2)
			if source_ready and dest_ready:
				return element
				break
		else:# we are not using the dest_ready funtion here because it is already included on auto_ready Function.
			if dest1 and dest2:
				auto_dest_ready=check_auto_dest(dest1, dest2)
			else:
				auto_dest_ready=check_auto_dest(dest1)
			
			source_ready=check_ready_unload(source)
			if auto_dest_ready and source_ready:
				return element
				break
				
#*FINISH****** functions for select movement ready on Infeed timer script*************************

def get_step_name(chart_path):
	chart_instance=system.sfc.getRunningCharts(chart_path)
	chart_id=chart_instance.getValueAt(0, "instanceId")
	variables = system.sfc.getVariables(chart_id)
	allSteps=variables["activeSteps"]
	for step in allSteps:
		currStep=allSteps[step]['name']
	return str(currStep)
	

#to log errors from SFC chart
def sfc_add_log(error, step):
	#stringify error message
	log_error = str(error)
	#log to db table
	parameters = {'log': log_error,'step':step}
	system.db.runNamedQuery('SFCMonitor/Step_Logs/InsertStepLogs', parameters)