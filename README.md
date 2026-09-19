```python

async def evaluate(code: str, browser_session: BrowserSession):
    # Execute JavaScript with proper error handling and promise support
    cdp_session = await browser_session.get_or_create_cdp_session()

    try:
        # Validate and potentially fix JavaScript code before execution
        validated_code = self._validate_and_fix_javascript(code)

        # Always use awaitPromise=True - it's ignored for non-promises
        result = await cdp_session.cdp_client.send.Runtime.evaluate(
            params={'expression': validated_code, 'returnByValue': True, 'awaitPromise': True},
            session_id=cdp_session.session_id,
        )
```
