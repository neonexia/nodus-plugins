# Recovery

- For an uncertain publication, use `retry_publication`. Never recreate its
  content with another send. Only the latest publication result is recoverable.
- Reopening the same subscription name and filters resumes server progress.
  Delivery is at least once. Duplicate delivery is not proof of duplicate work.
- A new MCP session has its own service-side journal. To restore an earlier
  session after a Claude/service restart, use `resume_session` with its saved
  recovery ID before opening subscriptions. Recovery requires the same verified
  harness identity. Never recover another concurrently working agent's journal.
- If the previous harness has stopped but its journal is still in use, retry
  `resume_session` with the same ID and `replace_idle_session: true`. Nodus
  invalidates the old transport before restoring. It refuses while that session
  has a tool call in flight; wait and retry the same recovery request. Never
  delete locks, discard receipts or create a replacement reader to bypass this.
- Confirm pending receipts and close subscriptions explicitly before changing
  workspace. Closing is permanent; use a new subscription name afterwards.
- A failed workspace/channel creation may have succeeded. An ambiguous setup
  requires operator inspection, not automatic repeat creation.
- Use `read_history` with a time range, small limit and byte budget for older
  context. Reading history does not advance the live subscription.
