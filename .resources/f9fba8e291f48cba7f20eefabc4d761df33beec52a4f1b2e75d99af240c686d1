

import java.lang.Exception
from datetime import datetime


# DBLogger utilities #

DB_TABLE_NAME = 'EVENT_LOGS'
PROJECT_NAME = system.project.getProjectName()


class Logger:
	
    def __init__(self, name):
    	
    	self.name = name
    	self.logger = system.util.getLogger(self.name)
    
    def to_db(self, level, message):
    	
    	log_method = getattr(self.logger, level.lower(), None)
    	
    	if log_method:
    		log_method(message)
    		
    		params = {
    			'table_name': DB_TABLE_NAME,
    			'logger': self.name, 
    			'message': message, 
    			'level_': level.upper(),
    			'project': PROJECT_NAME, 
    			'time_stamp': datetime.now()
    			}
    		try:
    			system.db.runNamedQuery(PROJECT_NAME, "DBLogger/Insert", params)
    		except java.lang.Exception as e:
				self.logger.error("%s" % e)
	else:
			self.logger.error("Level is not valid")

#in this function name is a string, valor int, tc should be 'infeed' or 'outfeed'
def script_monitor(logger,level,project):
	params={'logger':logger,'level':level,'project':project}
	system.db.runNamedQuery('DBLogger/Update',params)

def reset_script_steps():
	system.db.runNamedQuery('DBLogger/Update_0')

def get_charts_running(chart_path):
	charts = system.sfc.getRunningCharts(chart_path)
	return charts