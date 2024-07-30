import java.lang.Exception
import json

# SFC Monitor utilities #

LOGGER_NAME = 'SFCMonitor'
DB_TABLE_NAME = 'SFC_EVENTS'
PROJECT_NAME = system.project.getProjectName()

logger = DBLogger.Logger(LOGGER_NAME)


def insert_data(chart):
	
	parent = json.dumps(chart.get('parent')) if chart.get('parent') else None
	params = {
		'table_name': DB_TABLE_NAME,
		'parent': parent,
		'running_time': chart.get('runningTime'),
		'state': chart.get('state'),
		'active_steps': json.dumps(chart.get('activeSteps')),
		'instance_id': chart.get('instanceId'),
		'chart_path': chart.get('chartPath'),
		'start_date': chart.get('startTime')
	}

	try:
		system.db.runNamedQuery(PROJECT_NAME, "SFCMonitor/SQLSERVER_Insert", params)
		logger.logger.info("Row inserted: %s" % str(params))
	except java.lang.Exception as e:
		logger.logger.error("%s" % e)
		

def get_charts_running(chart_path = None):
	charts = system.sfc.getRunningCharts(chart_path) if chart_path else system.sfc.getRunningCharts()
	return charts

	
def get_chart_information(instance_id):
	if instance_id is None or instance_id == '':
		return ''
	return system.sfc.getVariables(instance_id)
	

def dict_to_string(dictionary, skip_key = []):
    keys = []
    values = []
    
    if dictionary is None or dictionary == '':
    	return ['', '']
    else:
    	for key, value in dictionary.items():
    		if key in skip_key:
    			continue
    		keys.append(key)
    		values.append(str(value))
    	return ["\n".join(keys), "\n".join(values)]
    	
	
def active_steps_to_list(data):
	active = data['activeSteps']
	return [step for step in active.values()]
	

def create_instances(active_steps, steps):
	act_steps = [active['name'] for active in active_steps if active['runningTime'] > 0]
	return [{'name':step['name'], 'description': step['description'],'active':step['name'] in act_steps} for step in steps]	