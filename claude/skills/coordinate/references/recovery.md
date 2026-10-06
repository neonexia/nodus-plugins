# Recovery

- For an uncertain publication, use `retry_publication`. Never recreate its
  content with another send. Only the latest publication result is recoverable.
- Reopening the same subscription name and filters resumes server progress.
  Delivery is at least once. Duplicate delivery is not proof of duplicate work.
- A new MCP session has its own service-side journal. To restore an earlier
  session after a Claude/service restart, use `resume_session` with its saved
  recovery ID before opening subscriptions. Recovery requires the same verified
  harness identity, and the previous session must have disconnected or expired.
- If the old journal is still in use, do not steal its lock or acknowledge its
  pending messages. Ask the operator to disconnect the old client or wait.
- Confirm pending receipts and close subscriptions explicitly before changing
  workspace. Closing is permanent; use a new subscription name afterwards.
- A failed workspace/channel creation may have succeeded. An ambiguous setup
  requires operator inspection, not automatic repeat creation.
- Use `read_history` with a time range, small limit and byte budget for older
  context. Reading history does not advance the live subscription.
