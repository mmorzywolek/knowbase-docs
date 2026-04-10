---
description: All the ways to add content to your knowledge base
---

# Uploading Files

## Upload methods

### Drag and drop
Go to the **New File** tab and drag files directly onto the drop zone. You can drop up to 50 files at once.

<!-- screenshot: upload-drag-and-drop -->

### YouTube links
Paste a YouTube URL into the upload area. Knowbase downloads the transcript and makes it searchable.

<!-- screenshot: upload-youtube-url -->

### From connectors
If you've connected Google Drive, Notion, or Dropbox, you can import files directly from those services. See [Connectors](../connectors/README.md).

## Supported formats

| Category       | Formats                                        | Max size |
| -------------- | ---------------------------------------------- | -------- |
| Documents      | PDF, DOCX, DOC, TXT, MD, PPTX, PPT            | 3 GB     |
| Audio          | MP3, WAV, M4A, AAC, OGG, FLAC                 | 3 GB     |
| Video          | MP4, MOV, WEBM, AVI, MKV                      | 3 GB     |
| Web            | YouTube links                                  | —        |

## Processing pipeline

After upload, each file goes through several stages:

1. **Uploaded** — file received
2. **Processing** — text extraction, transcription, or OCR in progress
3. **Ready** — file is searchable and available for chat

<!-- screenshot: file-status-indicators -->

{% hint style="warning" %}
**Processing time** depends on the file type. Documents take seconds; long videos may take several minutes for transcription.
{% endhint %}

## Storage limits

Storage depends on your plan:

| Plan    | Storage |
| ------- | ------- |
| Free    | 50 MB   |
| Starter | 2 GB    |
| Pro     | 25 GB   |
| Team    | 100 GB  |

Check your usage in **Account > Plans & Billing**.
