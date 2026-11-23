# Installing the wapi.kz MCP server (instructions for AI agents)

wapi.kz is a **remote** MCP server — nothing to install or build.

1. Ask the user for a wapi.kz API key. If they don't have one: sign up at https://wapi.kz/register.
   - A free **sandbox key** (`wa_test_…`, virtual number, no analytics) is available right after sign-up and e-mail confirmation — good for testing.
   - A live key works with a real WhatsApp number (330 KZT per number per day).
2. Add the server to the client config:
   - URL: `https://wapi.kz/api/mcp` (Streamable HTTP)
   - Header: `Authorization: Bearer <API_KEY>` — keep the key in an environment variable (e.g. `WAPI_KEY`), never in the repo.
   - Claude Code: `claude mcp add --transport http wapi https://wapi.kz/api/mcp --header "Authorization: Bearer $WAPI_KEY"`
   - Cline / clients without header support: use `npx -y mcp-remote https://wapi.kz/api/mcp --header "Authorization:Bearer ${WAPI_KEY}"`.
3. Verify: call `get_status` — it returns the numbers on the account and the balance.
4. Before sending, call `get_limits`. Write only to people who expect the message: cold bulk messages get WhatsApp numbers banned, and wapi.kz limits first messages to new contacts by the number's trust score.

Main value: `get_analytics`, `list_leads`, `get_link_stats` show which ad, tracking link or website brought each WhatsApp chat and whether it became a sale.
