# Cloudflare Realtime Agents

### Getting started
Install dependencies
```bash
pnpm i
```

Create .env from .env.example (do not worry about filling .env out)
```bash
cp .env.example .env
```

Generate types
```bash
pnpm cf-typegen
```

### Deploy you AI Worker
Ensure CLI is logged in
```bash
npx wrangler login
```

Deploy
```bash
npx wrangler deploy
```

Note the terminal log response:
```bash
Deployed cloudflare-realtime-agents...
https://cloudflare-realtime-agents.<YOUR_SUBDOMAIN>.workers.dev
```

### Cloudflare console

#### Create your Realtime API token
Go to your Cloudflare console > Manage Account > Account API tokens:
1. Create Token
2. Select custom, then select Realtime, then select Admin

#### Set environment variables
Go to Compute (Workers) > cloudflare-realtime-agents > Settings > Variables and Secrets:
Now set your worker's environment variables names and values:
- ACCOUNT_ID
  - Get from Cloudflare Account home, select 3 dots next to account home name, select copy account ID
- API_TOKEN
  - What we created previously
- DEEPGRAM_API_KEY
  - Get from deepgram.com
- ELEVENLABS_API_KEY
  - Get from elevenlabs.io

### Setup Realtime Meeting
In Cloudflare console, go to Realtime > Go to RealtimeKit Dashboard > Presets:
1. Create a preset for Voice (WebRTC) with any settings
2. Go to Meetings, create a meeting with any name
3. Select Join under Actions on the right side of the Meetings page, enter your user name, select preset, and select Join Now
4. Go back to your Realtime browser tab, selt Join again but this time enter Agent for user name and select Generate Link instead of Join Now
The link should look similar to this:
```https://demo.realtime.cloudflare.com/v2/meeting?id=bbbb2fac-953c-4239-9ba8-75ba912d76fc&authToken=ey...```
Notice the two variables meeting and authToken in the link. We will use these in the next step.

### Get your AI Worker to join you in the meeting

In terminal, replace the following variables with your own then run:
```bash
curl -X POST 'https://cloudflare-realtime-agents.<YOUR_SUBDOMAIN>.workers.dev/init?meetingId=<REALTIME_KIT_MEETING_ID>' -H "Authorization: Bearer <REALTIME_KIT_AUTH_TOKEN>"
```

Now go back to the browser tab where you joined the meeting. You should see the Agent has joined you and can now speak with it.


## Community
Join my free AI builders community: [Discord](https://discord.gg/v6nj7dShND)



## References

- [CLoudflare Realtime Agents](https://developers.cloudflare.com/realtime/agents/getting-started)
