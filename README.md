# Trivia Showdown

Responsive real-time trivia for 4–12 players. No accounts or installation. Built with Node.js, Express and Socket.IO.

## Implemented
- Create room, join by six-character code, shareable invite URL.
- Host plays as a normal player; host starts the match.
- Ten randomly selected questions, 15 seconds each, reveal/fact between rounds.
- Server-authoritative answers and speed-based scoring (500–1,000 points).
- Live score and answer-status updates.
- Browser local-storage resume token with 60-second reconnect grace period.
- Mobile/desktop responsive interface and visible rules.
- `/health` endpoint for deployment checks.

## Run locally
Requires Node.js 20+.

```sh
npm install
npm start
```
Open http://localhost:3000. Use four browser profiles/devices to test the 4-player minimum.

## Public deployment (Render example)
1. Push this folder to a GitHub repository.
2. Create a Render **Web Service** from that repository.
3. Build command: `npm install`; start command: `npm start`; health path: `/health`.
4. Open the generated HTTPS URL and share it. `render.yaml` is included as a blueprint option.
5. Test on mobile and laptop before sharing widely.

Run one server instance only. Room state is stored in memory; a restart loses active rooms. Multiple instances need a shared Socket.IO adapter and shared game-state storage before scaling.

## Not implemented / requires configuration
- Public HTTPS URL: requires deployment to a hosting provider.
- Durable rooms, database, recovery after server restart: not implemented.
- Multi-instance scaling: not supported by the current in-memory room store.
- Custom domain: optional DNS/host configuration.
- Moderation, reporting, profanity filter, analytics and automated tests: not included.
- Anti-cheat is basic: scoring and answer submission are server validated, but this MVP is not hardened against players inspecting network traffic.

Reconnect is designed for the same browser/device and works for up to 60 seconds while the server process and room still exist. Treat the stored resume token as a temporary room credential. Edit the `questions` array in `server.js` to change the question bank.
