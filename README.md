```python
async def download_file_from_url(
		self, url: str, target_id: TargetID, content_type: str | None = None, suggested_filename: str | None = None
	) -> str | None:
    if suggested_filename:
        filename = suggested_filename
    ...
    final_filename = filename
    existing_files = os.listdir(downloads_dir)
    if filename in existing_files:
        base, ext = os.path.splitext(filename)
        counter = 1
        while f'{base} ({counter}){ext}' in existing_files:
            counter += 1
        final_filename = f'{base} ({counter}){ext}'
    if download_result and download_result.get('data') and len(download_result['data']) > 0:
        download_path = os.path.join(downloads_dir, final_filename)
        async with await anyio.open_file(download_path, 'wb') as f:
            await f.write(bytes(download_result['data']))
```
