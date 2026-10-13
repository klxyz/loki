# Loki

A location-based multiplayer AR game: discover persistent power-ups, collect them by moving into their location, and cast virtual abilities at other participating online players.

## First prototype

One persistent lightning pickup, a laptop display simulation, and two connected test players:

1. Both players see the same pickup.
2. Moving into its configured radius grants a lightning ability.
3. An in-range cast produces a synchronized effect for the other online player.
4. Pickup and inventory state survive reconnects and server restarts.

Start with clearly labeled simulated position and heading. A later physical test supplies location from a supported device. Geographic persistence is not proof of precise physical collision or world-locked AR rendering.

## Proposed architecture

Separate display rendering, position/heading input, game rules, and persistent shared state. An authoritative server validates collection and casting; clients render synchronized results. Stable object IDs and coordinates identify world objects. Commands must be idempotent, and simultaneous pickup attempts must not duplicate grants.

The runtime, SDK, hosting and concrete gameplay parameters are not selected yet. One shared collectible with no automatic respawn is a proposal pending confirmation.

## Meta platform decision

The originally supplied [test guide](https://developers.meta.com/vr/essentials/test-your-app/) targets Meta VR Glasses/Horizon OS. The [Wearables toolkit](https://developers.meta.com/wearables/device-access-toolkit/) and [Ray-Ban Display Web Apps](https://developers.meta.com/wearables/faq/) are different integration paths.

Select the target glasses and phone OS before committing to a hardware adapter. Verify display, pose, location, simulation, outdoor anchoring and cross-device alignment against current official documentation. A working laptop demo must not be presented as a working glasses integration.

## Delivery plan

[Linear project](https://linear.app/le-gran-orchestra/project/loki-7bd42d332379)

| Issue | Outcome | Dependency |
| --- | --- | --- |
| [LE-16](https://linear.app/le-gran-orchestra/issue/LE-16) | Validate Meta target and spatial feasibility | Hardware selection |
| [LE-17](https://linear.app/le-gran-orchestra/issue/LE-17) | Persist shared pickup and inventory | LE-16 |
| [LE-18](https://linear.app/le-gran-orchestra/issue/LE-18) | Simulate movement, collection and multiplayer casting | LE-17 |
| [LE-19](https://linear.app/le-gran-orchestra/issue/LE-19) | Verify physical pickup at a selected Brooklyn test point | LE-18 |

## Verification requirements

Test simultaneous collection, duplicate commands, out-of-range collection/casts, casting without an ability, stale position, disconnect/reconnect and server restart. Two-client tests must verify consistent visibility and inventory without replaying old effects.

Physical testing additionally requires location consent, freshness and accuracy checks, denied-permission handling, and observed drift/false-pickup results. Use synthetic coordinates in committed fixtures; never commit an apartment address, live player location or credentials.

## Current status

Planning and repository setup only. No application, SDK integration, dependency tooling or tests exist yet. Full city gameplay, matchmaking, elimination, additional powers and public rollout are deferred.
