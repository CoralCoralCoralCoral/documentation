#### File Structure Overview

**app** - contains the different pages, layout doc, global css doc and the fonts used.
**api** - handlers for API routes.
**components\ui** - reuseable UI components.
**store** - contains the different slices of store along with the respecitve reducers. 

#### GameProvider
This is a context provider which wraps the entire application and injects the game context into the app.

The game provider provides the following control functions and state via the `useGameContext` hook, which allows any component rendered within the GameProvider's tree to start, pause and resume simulations, along with a few additional state variable and methods.

```ts
import { useGameContext } from "@/game/GameContext"

const ExampleComponentWithinGameProviderTree = () => {

    const {
        error,
        isLoading,
        isConnected,
        isInitialized,
        isPaused,
        gameId,
        sendCommand,
        startGame,
        pauseGame,
        resumeGame
    } = useGameContext()

    return <div>This is a Demo Component!</div>
}

```

The GameProvider handles all the logic of setting up bidirectional messaging between the client and the simulation engine over websockets.

All of this logic lives inside the root level `game` directory.

This component depends on the availability of a metrics and policy store (already configured), which it will update based on event and metrics messages received from the simulation-engine.

#### GameMap

This is a component that renders a map of the area in focus. The behaviour of the gameMap can be modified via `components/ui/gameMap.tsx`. The default behaviour of the map is such that it focuses in on the currently selected `jurisdiction` as tracked by the `navigation` slice of the applicaton's main redux store.

#### Oracle

The Oracle is a component located at `components/ui/Oracle.tsx`

This component currently implements a basic Oracle, that listens to real-time metrics updates (by hooking into the metrics store), and works by way of a set of triggers.

The current behaviour of the Oracle is the following:
- Interrupts the gameplay, pauses the game and appears as a Dialog warning the user of the event that triggered it.
- The Oracle gets triggered whenever either a new infection is recorded for the first time in any given Local Authority District (LAD), or whenver the first death has occured in any given LAD.

New triggers can be implemented for the Oracle by following the reference implementation.