```python
@app.post('/execute_action')
async def execute_action(action_request: ActionRequest):
	assert client is not None
	try:
		action = event_from_dict(action_request.action)
		if not isinstance(action, Action):
			raise HTTPException(status_code=400, detail='Invalid action type')
		client.last_execution_time = time.time()
		observation = await client.run_action(action)
		return event_to_dict(observation)
	except Exception as e:
		logger.error(f'Error while running /execute_action: {str(e)}')
		raise HTTPException(
			status_code=500,
			detail=traceback.format_exc(),
		)
	finally:
		update_last_execution_time()
```
