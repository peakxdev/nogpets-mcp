<p align="center"><img src="logo.png" width="128" alt="NogPets"></p>

# NogPets MCP server

Run your pet grooming business from your AI assistant. Sign a pet business up from anywhere; book grooming, walks and sitting in Stellenbosch.

The owner, managers and staff of a business on NogPets ask their assistant about the day, clients and money, and change prices, hours, time off and bookings. The assistant shows a summary and waits for a yes before it changes anything that matters. Groomers, dog walkers and pet sitters in any country sign up by asking their assistant: it collects the business, its country, currency and time zone, services and prices, service area, vans, staff and hours, and submits only when they say yes. NogPets reviews every application. Pet owners in Stellenbosch, South Africa can book NogPets' own mobile grooming, walks and sitting; a request from anywhere else is noted so a person from NogPets can follow up.

This repo describes the hosted server. There is nothing to install.

| | |
| --- | --- |
| **URL** | `https://mcp.nogpets.com/mcp` |
| **Transport** | Streamable HTTP |
| **Auth** | OAuth 2.1 + PKCE (client ID metadata documents and dynamic client registration; no client id or secret needed) |
| **Docs** | https://nogpets.com/developers/mcp · for businesses: https://nogpets.com/for-groomers |
| **REST API** | https://nogpets.com/openapi.json |
| **Registry** | `com.nogpets/nogpets` on the official MCP Registry |

## Connect

- **ChatGPT**: Settings → Security and login → Developer mode on → chatgpt.com/plugins → **+** → paste the URL → OAuth.
- **Claude**: Customize → Connectors → Add custom connector → paste the URL.
- **Claude Code**: `claude mcp add --transport http nogpets https://mcp.nogpets.com/mcp`
- **VS Code, Cursor, Windsurf, Gemini CLI, Zed**: add a remote (HTTP) MCP server with the URL.

You sign in to NogPets once and choose what the assistant may do. Disconnect any time in the NogPets app → Profile → Connected assistants.

## Try

Running your business:

- "What's my day look like?"
- "Block Friday afternoon, the van's in for a service."
- "Raise large-dog full grooms to R650 from next month."
- "Tina called, book Max for his usual groom next Tuesday."
- "Who hasn't paid this week?"

Signing up and booking:

- "Register my dog grooming business with NogPets."
- "I run a mobile grooming van in Austin, Texas. Sign my business up with NogPets: prices in US dollars, 25 km around Austin, Monday to Friday 8 to 5."
- "What's still missing from my NogPets business application?"
- "Do you groom dogs in Die Boord? What does a full groom cost for a 9 kg Boston terrier?"
- "Book a full groom for Bokkie next week, any morning."

## Tools

Running a business (shown to a connection with the "Run your pet business" permission; owners and managers make changes, staff see their own day):

- Read only: `business_overview`, `list_business_bookings`, `get_day_plan`, `next_booking`, `list_business_services`, `find_business_times`, `find_client`, `get_client`, `earnings_summary`, `list_payouts`, `list_unpaid_bookings`.
- Changes: `update_prices`, `set_business_hours`, `add_time_off`, `remove_time_off`, `update_service_area`, `pause_resource`, `resume_resource`, `add_client_note`, `create_booking_for_client`, `book_repeat`, `send_payment_link`, `reschedule_business_booking`, `cancel_business_booking`.
- Booking through NogPets works for South African businesses for now; elsewhere those tools say so, and the rest works in the business's own currency and time zone.

Read only: `list_services`, `check_coverage`, `get_quote`, `find_times`, `my_profile`, `list_pets`, `list_addresses`, `list_bookings`, `get_booking`, `find_reschedule_times`, `find_pet_businesses`, `get_signup_status`.

Actions: `add_pet`, `add_address`, `book`, `reschedule_booking`, `cancel_booking`, `pay_booking`.

Business sign-up and management (any country; shown to a connection with the business permission): `start_business_signup`, `add_business_services`, `set_service_area`, `add_resources`, `set_operating_hours`, `invite_staff`, `connect_payfast` (South Africa only), `get_signup_status`, `submit_business_for_review`. Each business keeps its own country, currency, time zone and phone format.

Every tool has a title and read-only / destructive / idempotent / open-world hints.

## Safety

- **The assistant never pays or charges.** A card booking returns a Payfast link the person opens. Cash bookings, cancellations and business submissions need an explicit yes.
- **A business's changes wait for a yes.** New bookings, moves, cancellations, prices, hours and areas answer with a summary first. Time off never cancels a booking. A business only ever sees its own clients and bookings.
- No card data reaches the assistant or our API. `connect_payfast` stores a merchant id only, never a key or passphrase. Outside South Africa a business only says how it would like to be paid; account numbers and keys are refused.
- Every action is logged with the assistant's name. Tokens are scoped, expire and can be revoked.
- New businesses are reviewed by NogPets before anything goes live.
- Asked for a booking somewhere NogPets doesn't serve yet, the assistant says so plainly and promises nothing; the request is noted for a person to follow up.

## Contact

hello@nogpets.com · https://nogpets.com/support · [Privacy](https://nogpets.com/privacy) · [Terms](https://nogpets.com/terms)

NogPets is a trading name of Peak Software (Pty) Ltd, South Africa.
