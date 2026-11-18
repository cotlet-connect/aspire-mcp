# How to connect Aspire to Claude Code, ChatGPT and any AI agent

**Yes, ChatGPT, Claude and other AI agents can work in your Aspire account.** Aspire's External API is included on Enterprise and activated on request for Growth and Corporate, and Aspire has no official MCP server. Cotlet.dev connects your own signed-in Aspire account to any AI agent, so you can ask in plain words and the AI schedules work, prepares proposals and manages invoices for you.

## What you can ask

> Put all unscheduled tickets on the board for tomorrow and show me the crew assignments.

> Price the Maple Court enhancement from the catalog and prepare the proposal for my approval.

> Which invoices are overdue by branch? Draft follow-up messages without sending them.

> Order the materials needed for this week's won jobs and show me the vendor totals.

> Find jobs running over their planned hours and explain where the schedule is slipping.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Aspire tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"aspire":{"command":"uvx","args":["aspire-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t aspire-mcp .
docker run -i --rm -e COTLET_API_KEY aspire-mcp
```

Tools: `aspire_guide`, `aspire_status`, `aspire_open`, `aspire_read`, `aspire_click`, `aspire_type`, `aspire_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install aspire-mcp        # or run it once: uvx aspire-mcp connect
aspire-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 aspire_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 aspire_agent.py status    # is Aspire ready in your Cotlet.dev account
python3 aspire_agent.py guide     # Aspire screens and sign-in link
python3 aspire_agent.py read      # open Aspire, read the page, close the browser
python3 aspire_agent.py tools     # list Cotlet.dev tools
python3 aspire_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Aspire users

**Does Aspire have an API?**

Aspire has an External API on Enterprise and can activate it for Growth and Corporate on request. An Aspire Admin creates the client ID and key, and the documented OData endpoints cover opportunities, contacts, work tickets, invoices, receipts, vendors and equipment.

**How do I connect Aspire to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT, sign in to Aspire once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No Aspire API key is needed for the hosted connection.

**Is there a way to use Claude with Aspire?**

Yes. Add https://cotlet.dev/mcp/v1 as a custom connector in Claude, or use the Claude Code command in this repository. Claude then works in your own signed-in Aspire account.

**Is there an Aspire MCP server?**

Aspire has no official MCP server or official ChatGPT or Claude connector. Cotlet.dev provides a hosted Aspire MCP server with tools for schedules, opportunities, estimates, purchasing, invoices, equipment and related office work.

## Find it on

- [Aspire on Cotlet.dev](https://cotlet.dev/integrations/aspire-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=aspire&utm_content=find)
- [PyPI package aspire-mcp](https://pypi.org/project/aspire-mcp/)
- [Odel](https://odel.app/modules/cotlet/aspire)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/aspire/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-aspire-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [AroFlo MCP](https://github.com/cotlet-connect/aroflo-mcp)
- [Simpro MCP](https://github.com/cotlet-connect/simpro-mcp)
- [Workiz MCP](https://github.com/cotlet-connect/workiz-mcp)
- [Kickserv MCP](https://github.com/cotlet-connect/kickserv-mcp)
- [Service Autopilot MCP](https://github.com/cotlet-connect/service-autopilot-mcp)
- [Boulevard MCP](https://github.com/cotlet-connect/boulevard-mcp)
- [Mindbody MCP](https://github.com/cotlet-connect/mindbody-mcp)
- [Meevo MCP](https://github.com/cotlet-connect/meevo-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [Jane App MCP](https://github.com/cotlet-connect/jane-app-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [Petpooja MCP](https://github.com/cotlet-connect/petpooja-mcp)
- [Teachers Pay Teachers MCP](https://github.com/cotlet-connect/teachers-pay-teachers-mcp)
- [Bloom MCP](https://github.com/cotlet-connect/bloom-mcp)
- [AestheticsPro MCP](https://github.com/cotlet-connect/aestheticspro-mcp)
- [Club OS MCP](https://github.com/cotlet-connect/club-os-mcp)
- [EZ Lawn Biller MCP](https://github.com/cotlet-connect/ez-lawn-biller-mcp)
- [Eversports Studio Manager MCP](https://github.com/cotlet-connect/eversports-studio-manager-mcp)
- [Exercise.com MCP](https://github.com/cotlet-connect/exercise-com-mcp)
- [Gymdesk MCP](https://github.com/cotlet-connect/gymdesk-mcp)
- [Iris Works MCP](https://github.com/cotlet-connect/iris-works-mcp)
- [CoachingPortal MCP](https://github.com/cotlet-connect/coachingportal-mcp)
- [CrewNest MCP](https://github.com/cotlet-connect/crewnest-mcp)
- [Paired Plus MCP](https://github.com/cotlet-connect/paired-plus-mcp)
- [ClubReady MCP](https://github.com/cotlet-connect/clubready-mcp)
- [Joist MCP](https://github.com/cotlet-connect/joist-mcp)
- [Trainerize MCP](https://github.com/cotlet-connect/trainerize-mcp)
- [Substack MCP](https://github.com/cotlet-connect/substack-mcp)
- [AnyList MCP](https://github.com/cotlet-connect/anylist-mcp)
- [Midjourney MCP](https://github.com/cotlet-connect/midjourney-mcp)
- [Systeme.io MCP](https://github.com/cotlet-connect/systeme-io-mcp)
- [VaultRE MCP](https://github.com/cotlet-connect/vaultre-mcp)
- [Hopper.so MCP](https://github.com/cotlet-connect/hopper-so-mcp)
- [oto.photo MCP](https://github.com/cotlet-connect/oto-photo-mcp)
- [Zolmi MCP](https://github.com/cotlet-connect/zolmi-mcp)
- [Estimate Rocket MCP](https://github.com/cotlet-connect/estimate-rocket-mcp)
- [Pikit MCP](https://github.com/cotlet-connect/pikit-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/aspire-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=aspire

Start free: https://cotlet.dev/signup?app=aspire&utm_source=github&utm_medium=readme&utm_campaign=aspire
