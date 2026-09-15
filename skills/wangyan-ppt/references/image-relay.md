# Wangyan Image Relay Reference

Use this reference for every AI image row in a Wangyan PPT project. The default
route is the OpenAI-compatible `hfsyapi.cn` relay already used by this checkout.

## 1. Configuration

Resolve configuration with the existing PPT Master lookup order: process
environment first, then the first available `.env` in the current directory,
skill directory, repository root, or `~/.ppt-master/.env`.

Required values:

| Variable | Value |
|---|---|
| `IMAGE_BACKEND` | `openai` |
| `OPENAI_MODEL` | `gpt-image-2` |
| `OPENAI_BASE_URL` | `https://www.hfsyapi.cn/v1` |
| `OPENAI_API_KEY` | user-provided secret; never print or commit |
| `OPENAI_OUTPUT_FORMAT` | `png` |
| `OPENAI_BACKGROUND` | `auto` |
| `OPENAI_MODERATION` | `auto` |
| `IMAGE_CONCURRENCY` | `3` unless the relay rate-limits, then reduce to `1` |

Do not use deprecated `IMAGE_API_KEY`, `IMAGE_MODEL`, or `IMAGE_BASE_URL` keys.

## 1.1 Windows network rule: IPv4 first

For this relay on Windows, prefer IPv4. A previous successful run required an
IPv4 connection after the default dual-stack request failed with a socket
permission/connection error (`WinError 10013`). This is a network-path recovery
rule, not a reason to change providers.

Keep `OPENAI_BASE_URL` as the hostname
`https://www.hfsyapi.cn/v1`; do not replace it with a raw IPv4 address, because
HTTPS certificate validation may then fail. Before generation, check the route:

```powershell
curl.exe -4 -I --connect-timeout 15 https://www.hfsyapi.cn/v1/
```

An HTTP `401`, `404`, or `405` still proves that DNS, TCP, and TLS reached the
relay; authentication and request-shape errors are handled separately. If the
IPv4 check succeeds but `image_gen.py --manifest` still fails with a timeout,
connection reset, or `WinError 10013`, use the direct relay fallback in Section
4 and run each POST/download through `curl.exe -4`. Do not silently switch to
IPv6 or another image provider.

## 2. Manifest contract

Write `<project>/images/image_prompts.json` as UTF-8 without BOM. The top level
contains a non-empty `items` array. Every item contains `filename`, `prompt`,
`aspect_ratio`, and `status`; initialize new items with `status: "Pending"`.
Use `16:9` and `1K` for ordinary full-slide backgrounds unless the layout
requires another ratio. Keep prompts as one coherent paragraph and inject the
selected Wangyan rendering and palette behavior into every item.

Validate before generation:

```powershell
Get-Content -Raw <project>\images\image_prompts.json | ConvertFrom-Json
```

The file must not contain a BOM, duplicate filenames, empty prompts, or secret
values.

## 3. Normal generation path

Resolve `<PPT_MASTER_DIR>` as the sibling `../ppt-master` of the installed
Wangyan skill. Use an absolute script path; a repository clone is not required.
The engine resolves its sibling Python modules from the script location.
On Windows, perform the IPv4 check in Section 1.1 first:

```powershell
python3 <PPT_MASTER_DIR>/scripts/image_gen.py `
  --manifest <project>\images\image_prompts.json
```

The dispatcher loads the configured OpenAI-compatible backend, sends each
pending/failed item to `<OPENAI_BASE_URL>/images/generations`, saves base64 or
URL responses to the manifest's `filename`, and updates each status to
`Generated`, `Failed`, or `Needs-Manual`. Retry only `Pending` and `Failed`.

After the command, inspect the manifest and output directory. Do not proceed to
SVG embedding while a required image is missing or still `Pending`.

## 4. Direct relay fallback

Use this only when `image_gen.py` cannot load the configured backend but the
relay credentials are available, or when its request path fails after the
IPv4 check. On Windows, use `curl.exe -4` for both the POST and any signed-URL
download. For each item, POST JSON to
`<OPENAI_BASE_URL>/images/generations` with:

```json
{
  "model": "gpt-image-2",
  "prompt": "<item.prompt>",
  "size": "1280x720",
  "quality": "medium",
  "background": "auto",
  "output_format": "png"
}
```

Send `Authorization: Bearer <OPENAI_API_KEY>` and
`Content-Type: application/json`. Accept either `data[0].b64_json` or
`data[0].url`; decode or download it to the requested filename, then update
that item status in place. Use retry with backoff for transient HTTP failures,
but stop after two consecutive failures for the same item and mark it
`Needs-Manual` with a concise `last_error`.

Never paste the key into a prompt, log, manifest, code file, or final response.
Never keep signed response URLs after downloading the file.

## 5. Verification

For every `Generated` item, verify that the file exists, is a readable PNG, and
matches the requested aspect ratio closely enough for the target container.
For full-slide backgrounds, verify `1280x720` or the backend's documented
equivalent. Keep the image free of body copy, numbers, logos, watermarks, and
legible labels; regenerate if these appear.
