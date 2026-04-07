---
description: Preview server start, stop, and status check. Local development server management.
---

# /preview - Preview Management

$ARGUMENTS

---

## Task

Manage preview server: start, stop, status check.

### Commands

```
/preview           - Show current status
/preview start     - Start server
/preview stop      - Stop server
/preview restart   - Restart
/preview check     - Health check
```

---

## Usage Examples

### Start Server
```
/preview start

Response:
🚀 Starting preview...
   Port: <detected-or-requested-port>
   Type: Next.js

✅ Preview ready!
   URL: <local-preview-url>
```

### Status Check
```
/preview

Response:
=== Preview Status ===

🌐 URL: <local-preview-url>
📁 Project: <project-path>
🏷️ Type: nextjs
💚 Health: OK
```

### Port Conflict
```
/preview start

Response:
⚠️ Requested port is in use.

Options:
1. Start on the next available port
2. Close app on the conflicting port
3. Specify different port

Which one? (default: 1)
```

---

## Technical

Auto preview uses `auto_preview.py` script:

```bash
python .agent/scripts/auto_preview.py start [port]
python .agent/scripts/auto_preview.py stop
python .agent/scripts/auto_preview.py status
```
