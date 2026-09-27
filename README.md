<p align="center"><img src="logo.png" width="128" alt="NogPets"></p>

# NogPets MCP server

Register and manage your pet business with NogPets from any AI assistant, anywhere; book grooming, walks and sitting in Stellenbosch.

Groomers, dog walkers and pet sitters in any country sign up by asking their assistant: it collects the business, its country, currency and time zone, services and prices, service area, vans, staff and hours, and submits only when they say yes. NogPets reviews every application. Pet owners in Stellenbosch, South Africa can book NogPets' own mobile grooming, walks and sitting; a request from anywhere else is noted so a person from NogPets can follow up.

This repo describes the hosted server. There is nothing to install.

| | |
| --- | --- |
| **URL** | `https://mcp.nogpets.com/mcp` |
| **Transport** | Streamable HTTP |
| **Auth** | OAuth 2.1 + PKCE (client ID metadata documents and dynamic client registration; no client id or secret needed) |
| **Docs** | https://nogpets.com/developers/mcp |
| **REST API** | https://nogpets.com/openapi.json |
| **Registry** | `com.nogpets/nogpets` on the official MCP Registry |

## Connect

- **ChatGPT**: Settings → Security and login → Developer mode on → chatgpt.com/plugins → **+** → paste the URL → OAuth.
- **Claude**: Customize → Connectors → Add custom connector → paste the URL.
- **Claude Code**: `claude mcp add --transport http nogpets https://mcp.nogpets.com/mcp`
- **VS Code, Cursor, Windsurf, Gemini CLI, Zed**: add a remote (HTTP) MCP server with the URL.

You sign in to NogPets once and choose what the assistant may do. Disconnect any time in the NogPets app → Profile → Connected assistants.

## Try

- "Register my dog grooming business with NogPets."
- "I run a mobile grooming van in Austin, Texas. Sign my business up with NogPets: prices in US dollars, 25 km around Austin, Monday to Friday 8 to 5."
- "What's still missing from my NogPets business application?"
- "Do you groom dogs in Die Boord? What does a full groom cost for a 9 kg Boston terrier?"
- "Book a full groom for Bokkie next week, any morning."

## Tools

Read only: `list_services`, `check_coverage`, `get_quote`, `find_times`, `my_profile`, `list_pets`, `list_addresses`, `list_bookings`, `get_booking`, `find_reschedule_times`, `find_pet_businesses`, `get_signup_status`.

Actions: `add_pet`, `add_address`, `book`, `reschedule_booking`, `cancel_booking`, `pay_booking`.

Business sign-up and management (any country; shown to a connection with the business permission): `start_business_signup`, `add_business_services`, `set_service_area`, `add_resources`, `set_operating_hours`, `invite_staff`, `connect_payfast` (South Africa only), `get_signup_status`, `submit_business_for_review`. Each business keeps its own country, currency, time zone and phone format.

Every tool has a title and read-only / destructive / idempotent / open-world hints.

## Safety

- **The assistant never pays.** A card booking returns a Payfast link the person opens. Cash bookings, cancellations and business submissions need an explicit yes.
- No card data reaches the assistant or our API. `connect_payfast` stores a merchant id only, never a key or passphrase. Outside South Africa a business only says how it would like to be paid; account numbers and keys are refused.
- Every action is logged with the assistant's name. Tokens are scoped, expire and can be revoked.
- New businesses are reviewed by NogPets before anything goes live.
- Asked for a booking somewhere NogPets doesn't serve yet, the assistant says so plainly and promises nothing; the request is noted for a person to follow up.

## Contact

hello@nogpets.com · https://nogpets.com/support · [Privacy](https://nogpets.com/privacy) · [Terms](https://nogpets.com/terms)

NogPets is a trading name of Peak Software (Pty) Ltd, South Africa.
