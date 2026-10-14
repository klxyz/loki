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

## Hardware targets and platform strategy

The originally supplied [test guide](https://developers.meta.com/vr/essentials/test-your-app/) targets Meta VR Glasses/Horizon OS. The [Wearables toolkit](https://developers.meta.com/wearables/device-access-toolkit/) and [Ray-Ban Display Web Apps](https://developers.meta.com/wearables/faq/) are different integration paths.

Target families confirmed by the product owner on 2026-10-13: **Ray-Ban Display, VITURE and XREAL**, with **Meta VR glasses (the owner's 2027 target)** as the long-term goal. The year is a planning horizon, not a verified hardware release commitment. Exact VITURE/XREAL models, accessories and host devices remain to be selected.

Keep shared multiplayer state and rules independent of each vendor SDK. Proposed delivery order: laptop simulation, a Ray-Ban Display HUD, then model-specific spatial adapters for VITURE/XREAL and eventually Meta VR. This ordering is a recommendation, not a requirement to implement every platform in the first prototype.

| Target | Documented starting point | Validation still required |
| --- | --- | --- |
| Ray-Ban Display | [Web Apps and browser simulation](https://developers.meta.com/wearables/web-apps/) | Device input/location behavior and whether world-locked rendering is supported; HUD rendering alone does not prove it |
| VITURE | [Glasses SDK and Unity SDK](https://www.viture.com/developer) | Exact glasses/host combination, available pose tracking, world persistence and outdoor alignment |
| XREAL | [SDK releases](https://developer.xreal.com/download/) include model-dependent tracking and anchor features | Supported glasses/accessory/host combination, persistence, multi-user alignment and outdoor reliability |
| Future Meta VR | [Horizon OS test paths](https://developers.meta.com/vr/essentials/test-your-app/) | Shipping hardware, final SDK capabilities, outdoor suitability and device verification |

Treat display-only, orientation tracking and positional tracking as separate capabilities. Unsupported devices can use an explicitly labeled direction/distance HUD; that fallback does not meet the street-anchored 3D acceptance case. Device-local anchors also do not establish a shared city coordinate frame. Verify each adapter independently. Research checked 2026-10-13; no hardware validation has been performed.

## Delivery plan

[Linear project](https://linear.app/le-gran-orchestra/project/loki-7bd42d332379)

| Issue | Outcome | Dependency |
| --- | --- | --- |
| [LE-16](https://linear.app/le-gran-orchestra/issue/LE-16) | Validate Meta target and spatial feasibility | Exact device/host capability validation |
| [LE-17](https://linear.app/le-gran-orchestra/issue/LE-17) | Persist shared pickup and inventory | LE-16 |
| [LE-18](https://linear.app/le-gran-orchestra/issue/LE-18) | Simulate movement, collection and multiplayer casting | LE-17 |
| [LE-19](https://linear.app/le-gran-orchestra/issue/LE-19) | Verify physical pickup at a selected Brooklyn test point | LE-18 |

## Verification requirements

Test simultaneous collection, duplicate commands, out-of-range collection/casts, casting without an ability, stale position, disconnect/reconnect and server restart. Two-client tests must verify consistent visibility and inventory without replaying old effects.

Physical testing additionally requires location consent, freshness and accuracy checks, denied-permission handling, and observed drift/false-pickup results. Use synthetic coordinates in committed fixtures; never commit an apartment address, live player location or credentials.

## Current status

Planning and repository setup only. No application, SDK integration, dependency tooling or tests exist yet. Full city gameplay, matchmaking, elimination, additional powers and public rollout are deferred.
