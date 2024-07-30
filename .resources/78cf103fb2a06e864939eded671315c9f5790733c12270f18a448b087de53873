SELECT 
	audit_events_id, 
	DATE_FORMAT(event_timestamp, '%c/%e/%y %h:%i:%s %p') event_timestamp,
	actor, 
	action,
	action_target,
	action_value,
	actor_host,
	status_code,
	originating_system,
	originating_context
FROM 
	AUDIT_EVENTS
WHERE 
	event_timestamp BETWEEN :startDate AND :endDate AND 
	(:search = '' OR (:search != '' AND (actor LIKE :search OR action LIKE :search OR action_target LIKE :search)))
ORDER BY 
	audit_events_id DESC
	
