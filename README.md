```python
def on_response_received(event: ResponseReceivedEvent, session_id: str | None) -> None:
    response = event.get('response', {})
    url = response.get('url', '')
    content_type = response.get('mimeType', '').lower()
    headers = {k.lower(): v for k, v in response.get('headers', {}).items()}
    content_disposition = str(headers.get('content-disposition', '')).lower()

    suggested_filename = None
    if 'filename=' in content_disposition:
        filename_match = re.search(r'filename[^;=\n]*=(([\'"]).*?\2|[^;\n]*)', content_disposition)
        if filename_match:
            suggested_filename = filename_match.group(1).strip('\'"')

    # Trigger download asynchronously in background (don't block event handler)
    async def download_in_background():
        # Don't permanently block re-processing this URL if download fails
        try:
            download_path = await self.download_file_from_url(
                url=url,
                target_id=event_target_id,  # Use target_id from session_id lookup
                content_type=content_type,
                suggested_filename=suggested_filename,
            )
```
