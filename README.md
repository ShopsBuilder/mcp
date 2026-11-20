<p align="center">
  <img src="https://mcp.shopsbuilder.app/static/icon-512.png" alt="ShopsBuilder" width="96" height="96">
</p>

# ShopsBuilder MCP Server

Launch and manage online stores with AI agents: products, inventory, pricing, orders and promotions.

This repository holds documentation only. The server is hosted by ShopsBuilder, so there is
nothing to install or run.

```text
https://mcp.shopsbuilder.app/mcp
```

- Transport: Streamable HTTP
- Auth: OAuth sign-in with a ShopsBuilder account (you can create one during the first sign-in).
  Don't add API keys or authorization headers.
- Access: the agent signs in as you and works only on stores you own.

## Connect

### Claude

Add ShopsBuilder from the [Claude directory](https://claude.ai/directory/shopsbuilder), then sign in.

For Claude Code:

```bash
claude mcp add --transport http shopsbuilder https://mcp.shopsbuilder.app/mcp
```

Then run `/mcp`, select `shopsbuilder` and sign in.

Or install the ShopsBuilder plugin, which adds the same server plus two skills: `launch-store`
(create a store and publish the first product) and `store-checkup` (sales, orders, restock and
products shoppers can't buy):

```text
/plugin install shopsbuilder --marketplace ShopsBuilder/mcp
```

### VS Code and GitHub Copilot

```bash
code --add-mcp '{"name":"shopsbuilder","type":"http","url":"https://mcp.shopsbuilder.app/mcp"}'
```

Or add it to `mcp.json`, then start the server and sign in when VS Code asks:

```json
{
  "servers": {
    "shopsbuilder": {
      "type": "http",
      "url": "https://mcp.shopsbuilder.app/mcp"
    }
  }
}
```

### Other clients

See [Connect an AI agent](https://shopsbuilder.app/en/docs/connect-ai-agent/) for ChatGPT and the
other supported clients.

## What agents can do

- **Stores:** create a store after you confirm a preview, list and select your stores, update the
  store profile.
- **Catalog:** products, variants and variant options, categories and product types.
- **Pricing and stock:** set variant prices and stock per warehouse.
- **Channels and shipping:** channels, warehouses, shipping zones and rates, channel readiness.
- **Orders and sales:** orders, order counts, sales summaries and customers.
- **Promotions:** create and delete promotions and sales.
- **Media:** add product and category images, delete product media.

Changes go to your live store. Delete tools show a preview and run only after you confirm.

## Data

The agent sends the store and catalogue data it reads or writes (products, prices, stock,
orders, customers, shipping and promotions) to `mcp.shopsbuilder.app`, only after you sign in with
OAuth, and only for stores you own or administer. ShopsBuilder stores it to run your shop as
described in the [Privacy Policy](https://shopsbuilder.app/en/legal/privacy/). The plugin itself
has no code and keeps no data on your machine.

## Links

- Docs: [Connect an AI agent](https://shopsbuilder.app/en/docs/connect-ai-agent/)
- [Privacy Policy](https://shopsbuilder.app/en/legal/privacy/)
- [Terms](https://shopsbuilder.app/en/legal/terms/)
- Support: [partners@shopsbuilder.app](mailto:partners@shopsbuilder.app)
