---
title: Scripting Support
---

## Scripting Support

GameHook exposes a REST API to interact with it.

GameHook out-of-the-box provides bindings for the following languages:
* Javascript / Node.js

### Classes and Functions
```js
class GameHookMapperClient
    - static decimalToHexdecimal(x: Integer, uppercase: Boolean)
    - static hexdecimalToDecimal(x: String)
    - connect()
    - onConnected() /* Override */
    - onDisconnected() /* Override */
    - onGameHookError() /* Override */
    - onMapperLoaded() /* Override */
    - onMapperLoadError() /* Override */
    - onDriverError() /* Override */
    - onPropertyChanged() /* Override */
    - onPropertyFrozen() /* Override */
    - onPropertyUnfrozen() /* Override */

class GameHookProperty
    - setBytes(bytes: Array<int>, freeze: Boolean)
    - freeze(freeze: Boolean)
    - change(fn: Function)
    - once(fn: Function)
```

### Example Code and Templates
More examples can be found on our Discord server.

```html
    <!-- Include the following scripts in your HTML -->
    <script src="https://unpkg.com/@microsoft/signalr@latest/dist/browser/signalr.min.js"></script>
    <script src="http://localhost:8085/dist/gameHookMapperClient.js"></script>
```

##### Example 1
```js
    // Create a new GameHook client.
    const mapper = new GameHookMapperClient()

    (async function() {
        // Establish a connection to GameHook.
        await mapper.connect()
        
        // You can then access properties you see in GameHook via mapper.properties.
        const prop = mapper.properties.player.name;
        console.info(`Your name is ${mapper.properties.player.name}.`)
    })();
```

##### Example 2
```js
    // Setup the GameHook client.
    const mapper = new GameHookMapperClient()

    const setWildEncounters = async() => {
        const level = 0x01
        const species = 0x14

        await Promise.all([
            await mapper.properties.overworld.encounters.encounterTable.common1.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.common2.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.common3.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.common4.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon1.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon2.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon3.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon4.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.rare1.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.rare2.level.setBytes([level], true),
            await mapper.properties.overworld.encounters.encounterTable.common1.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.common2.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.common3.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.common4.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon1.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon2.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon3.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.uncommon4.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.rare1.pokemon.setBytes([species], true),
            await mapper.properties.overworld.encounters.encounterTable.rare2.pokemon.setBytes([species], true),
        ])
    }

    // Main code starts executing here.
    (async function() {
        // Establish the connection to GameHook.
        await mapper.connect()

        // You can listen for properties to change like this
        // after the connection has been established.
        mapper.properties.overworld.loadedMap.change(async(x) => {
            console.info(`Entered ${x.value || "a new map"} -- setting all encounters.`)
            await setWildEncounters()
        })

        console.info(`Initial load -- setting all encounters.`)
        await setWildEncounters()
    })();
```

---

#### Related Articles
[Quickstart Guide](/quickstart)