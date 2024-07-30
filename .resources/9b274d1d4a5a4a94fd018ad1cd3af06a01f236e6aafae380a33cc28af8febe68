import time

#on cart argument use PressIF for infeed tarnsfer cart or PressOF for outfeed tranfer cart
def move_to_source_car(path,cart):
	sourcePos=system.tag.read(path+'/Coordinate/X_Location').value
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/ActualPosition_PLCTOSM',sourcePos)
	time.sleep(10)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/InSourcePos_PLCTOSM',1)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/SourceRollRun_PLCTOSM',1)
	system.tag.write(path+'/TransComm/SourceRollRun_PLCTOSM',1)
	time.sleep(10)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/InSourcePos_PLCTOSM',0)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/SourceRollRun_PLCTOSM',0)
	system.tag.write(path+'/TransComm/SourceRollRun_PLCTOSM',0)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/LocOccupied_PLCTOSM',1)
	system.tag.write(path+'/LocOccupied_PLCTOSM',0)
	

	
def move_to_dest_car(path,cart):
	sourcePos=system.tag.read(path+'/Coordinate/X_Location').value
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/ActualPosition_PLCTOSM',sourcePos)
	system.tag.write(path+'/LocOccupied_PLCTOSM',0)
	time.sleep(10)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/InDestPos_PLCTOSM',1)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/DestRollRun_PLCTOSM',1)
	system.tag.write(path+'/TransComm/DestRollRun_PLCTOSM',1)
	time.sleep(10)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/InDestPos_PLCTOSM',0)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/DestRollRun_PLCTOSM',0)
	system.tag.write(path+'/TransComm/DestRollRun_PLCTOSM',0)
	system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/LocOccupied_PLCTOSM',0)
	system.tag.write(path+'/LocOccupied_PLCTOSM',1)

def park_location_simul(cart):
	actual_loc=system.tag.read('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/ParkLocation_SMTOPLC').value
	if actual_loc != 0:
		system.tag.write('[default]'+cart+'_TransferCart/TC_AGTC/TransComm/ActualPosition_PLCTOSM', actual_loc)
	
	
	